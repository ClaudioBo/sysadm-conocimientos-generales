# Azure y los certificados de Certbot
textotextotexto **azure is bruh**
convertir a pfx
```bash
sudo openssl pkcs12 \
-export \
-out certificado.pfx \
-inkey /etc/letsencrypt/live/ejemplo.com/privkey.pem \
-in /etc/letsencrypt/live/ejemplo.com/cert.pem
```

## Convertir los tres archivos de certificados **(privkey.pem, cert.pem y fullchain.pem)** a .crt:
1. Juntar los .pems en un solo .pfx
```bash
sudo openssl pkcs12 \
-export \
-out juntos.pfx \
-inkey privkey1.pem \
-in cert1.pem \
-certfile fullchain1.pem
```
2. Convertir .pfx a un solo .pem
```bash
sudo openssl pkcs12 \
-in input.pfx \
-out output.pem \
-nodes
```
3. Convertir .pem a .crt
```bash
sudo openssl x509 \
-outform der \
-in input.pem \
-out output.crt
```

## .crt to .pfx

con la key, cert y CA
```bash
sudo openssl pkcs12 \
-export \
-out certificate.pfx \
-inkey input-key.key \
-in input-crt.crt \
-certfile input-CA.crt
```

sin llave pem
```bash
sudo openssl pkcs12 \
-export \
-nokeys \
-out certificate.pfx \
-inkey input-key.key \
-in input-crt.crt \
-certfile input-CA.crt
```
