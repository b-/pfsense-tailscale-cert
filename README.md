# pfsense-import-certificate
Script to import an SSL certificate into a running pfsense system, set the webui to use the new certificate and restart the webui.

Use this to automate deploying letsencrypt certificates to your pfsense firewalls from your central letsencrypt managment system.

Using opnsense, see repo at https://github.com/pluspol-interactive/opnsense-import-certificate

## usage
1. Copy script to your firewall.
2. Copy your certificate files to your firewall.
3. Run the script on your firewall.


```
Usage: php pfsense-import-certificate.php /path/to/cert.pem /path/to/private/privkey.pem
```

## automation example with dehydrated acme

```
./dehydrated -c -f config-lan
# push cert to pfsense
scp pfsense-import-certificate.php certs/yourhost.domain.tld/privkey.pem certs/yourhost.domain.tld/fullchain.pem root@yourpfsensehost: \
&& ssh root@yourpfsensehost 'php pfsense-import-certificate.php /root/fullchain.pem /root/privkey.pem'
```

## Using dehyrdated.default.sh

In the "function deploy_cert" section, use something like this to deploy certificates to your firewall when they are created or renewed.

```
    if [[ "${DOMAIN}" =~ ..-firewall\.example\.org ]]; then  #assumes hostname like xx-firewall.example.org
      #copy the pfsense cert import script
      scp ~/pfsense-import-certificate/pfsense-import-certificate.php root@${DOMAIN}:./

      #copy the certs
      scp ~/letsencrypt/dehydrated/certs/${DOMAIN}/cert.pem ~/letsencrypt/dehydrated/certs/${DOMAIN}/privkey.pem root@${DOMAIN}:./

      #install the certs
      ssh root@${DOMAIN} "php ./pfsense-import-certificate.php ./cert.pem ./privkey.pem"
    fi

```
