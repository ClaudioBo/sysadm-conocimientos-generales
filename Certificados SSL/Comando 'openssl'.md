# Comando 'openssl'
## Crear string random de 32 caracteres
```bash
openssl rand -hex 32
```

## Azure y los certificados de Certbot
textotextotexto **azure is bruh**
convertir .pems a .pfx
```bash
openssl pkcs12 \
-export \
-out certificado.pfx \
-inkey /etc/letsencrypt/live/claudiobo.com/privkey.pem \
-in /etc/letsencrypt/live/claudiobo.com/cert.pem
```

# Debugear los certificados de una pagina web HTTPS
```bash
openssl s_client -connect claudiobo.com:443
```

# Mostrar los certificados que tiene un sitio
```bash
openssl s_client -showcerts -servername claudiobo.com -connect claudiobo.com:443
```

# Comprobar si los certificados llaves privadas son compatibles
Para certificado usar:
```bash
openssl x509 -noout -modulus -in certificado.pem | openssl md5
```
Para llave privada usar:
```bash
openssl rsa -noout -modulus -in llave-privada.pem | openssl md5
```
Si ambos MD5 coinciden, son compatibles y se pueden usar en conjunto