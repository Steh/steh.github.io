---
title: "Splunk: Upgraid failed to 9.4 because of KV-Store"
categories: 
  - informationsecurity
tags:
  - splunk
classes: 
  - wide
excerpt: "KV-Store won´t upgrade to 7.0"
toc: true
date: 2025-07-17
---

# Problems with KV-Store upgrade

* after Upgrading to Splunk 9.4 the KV-Store needs an upgrade to the Version 7.0
* this failed in our environment
* look for errors in mongodb log:
   * ```index=_internal error sourcetype=mongod SSLHandshakeFailed```

# How did we resolve this?

At first validate your kv-store status:
* ```bin/splunk show kvstore-status --verbose```

1. Check you SSL config, by now KV-Store 7.0 does not support custom certificates ([Splunk Help][def])
   * ```/bin/splunk cmd btool server list sslConfig```
   * so splunk recons you to use the default one
2. validate your certs: ([About self-renewing default splunk certificates][def1])
   * ```bin/splunk cmd openssl verify -verbose -x509_strict -CAfile etc/auth/cacert.pem server.pem```
   * in my case the default cert are expired and i need to create new ones
      * At first copy the old ones to *.old (as a backup if something goes wrong)
         * ```mv ca.pem ca.pem.bak, mv cacert.pem cacert.pem.bak, mv server.pem server.pem.bak```
      * ```bin/genRootCA.sh -d etc/auth``

# References

1. [Preparing custom certificates for use with KV store][def]
2. [About self-renewing default splunk certificates][def1]

[def]: https://help.splunk.com/en/splunk-enterprise/administer/admin-manual/9.4/administer-the-app-key-value-store/preparing-custom-certificates-for-use-with-kv-store
[def1]:  https://splunk.my.site.com/customer/s/article/About-renewing-default-splunk-certificates