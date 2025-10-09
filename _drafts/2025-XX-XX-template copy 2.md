---
title: "Splunk: Configure Splunk Edge Processor"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

# Enable JWT to send Data vom Edge Proessor to Data Manager 

1. Open a shell prompt or PowerShell window.
2. Change to the $SPLUNK_HOME/etc/system/local directory.
3. Use a text editor to open the authorize.conf file.
4. In the authorize.conf file, edit the following lines of 
    *  ```[tokens_auth]
    disabled = true```
5. Save the authorize.conf file and close it.
6. Restart Splunk Enterprise.

* [Disable token authentication using configuration files][def]

## source

* [Disable token authentication using configuration files][def]

[def]: https://help.splunk.com/en/splunk-enterprise/administer/manage-users-and-security/10.0/authenticate-into-the-splunk-platform-with-tokens/enable-or-disable-token-authentication#id_24702475_d8c1_494c_9bec_829fb2ecb2ae__Enable_or_disable_token_authentication
