---
title: "Splunk: Create self-signed certificate"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

For using Splunk-Edge Processor i need a certificate for the Splunk API communication. 
Splunk-Edge is realy strict on this matter, so i need to create a self signed certificate with the servername in sans format.

## create CA

```bash
cd $SPLUNK_HOME/etc/auth/mycerts

# generate ca private key
/opt/splunk/bin/splunk cmd openssl genpkey -aes-256-cbc -algorithm RSA -out myCertAuthPrivateKey.key -pkeyopt rsa_keygen_bits:2048

# create ca.conf
vim ca.conf

# generate csr
/opt/splunk/bin/splunk cmd openssl req -new -key myCertAuthPrivateKey.key -out myCertAuthCertificate.csr -config ca.conf

# create cert
/opt/splunk/bin/splunk cmd openssl x509 -req -in myCertAuthCertificate.csr -sha512 -signkey myCertAuthPrivateKey.key -CAcreateserial -out myCertAuthCertificate.pem -days 1095 -extfile ca.conf
```

```bash
# ca.conf
[req]
distinguished_name = req_distinguished_name
x509_extensions = v3_ca
prompt = no

[req_distinguished_name]
C = country
O = myOrganisation
CN = Internal CA

[v3_ca]
basicConstraints = critical,CA:TRUE
keyUsage = critical, keyCertSign, cRLSign
subjectKeyIdentifier = hash
authorityKeyIdentifier = keyid:always,issuer
```

## create Server Certificate

```bash
# create config
vim etc/auth/myCert/myServer.conf

# generate csr with config
bin/splunk cmd openssl req -new -key myServerPrivateKey.key -out myServerCertificate.csr -config myServer.conf 
 
# sign request
bin/splunk cmd openssl x509 -req -in myServerCertificate.csr -CA myCertAuthCertificate.pem -CAkey myCertAuthPrivateKey.key -CAcreateserial -out myServer.pem -days 1095 -extensions v3_req -extfile myServer.conf

# verifiy
bin/splunk cmd openssl x509 -in myServer.pem -text -noout
bin/splunk cmd openssl verify -CAfile myCertAuthCertificate.pem myServer.pem
```

```bash
# myServer.conf
[req]
distinguished_name = req_distinguished_name
req_extensions = v3_req
prompt = no

[req_distinguished_name]
C = Country
O = My Organisation
CN = server.name

[v3_req]
basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
extendedKeyUsage = serverAuth, clientAuth
subjectAltName = @alt_names

[alt_names]
DNS.1 = server.name
```

## combine to certificate bundle

```bash
# combine
cat myServer.pem myServerPrivateKey.key myCertAuthCertificate.pem > myCertComb.pem

```

## add to system and splunk cert store

```bash
# add cert to server and splunk
sudo cat myCertAuthCertificate.pem >> /cdc/splunk/etc/auth/cacert.pem

cp myCertAuthCertificate.pem /usr/local/share/ca-certificates/myCertAuthCertificate.crt
sudo update-ca-certificates
```

## use for splunk sslconfig

```bash
# /opt/splunk/etc/system/local/server.conf
[sslConfig]
enableSplunkdSSL = true
sslRootCAPath = /opt/splunk/etc/auth/cacert.pem
serverCert = /opt/splunk/etc/auth/mycerts/myCertComb.pem
sslPassword = <my-password>
```

## source

* [How to create and sign your own TLS certificates][def]
* [How to prepare TLS certificates for use with the Splunk platform][def1]
* [Configure TLS certificates for inter-Splunk communication][def2]

[def]: https://docs.splunk.com/Documentation/Splunk/9.4.2/Security/Howtoself-signcertificates
[def1]: https://docs.splunk.com/Documentation/Splunk/9.4.2/Security/HowtoprepareyoursignedcertificatesforSplunk
[def2]: https://docs.splunk.com/Documentation/Splunk/9.4.2/Security/ConfigTLSCertsS2S
