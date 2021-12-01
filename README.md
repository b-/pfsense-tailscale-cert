# pfsense-import-certificate
Script to import an SSL certificate into a running pfsense system

## usage


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

```

```
