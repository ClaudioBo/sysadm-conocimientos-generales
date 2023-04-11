# Comando 'certbot'
Se debera instalar ``certbot`` con el siguiente comando:
```bash
sudo apt install certbot python3-certbot-apache -y
```

Dependiendo de que si tienes `Apache2` o `NGINX` puedes instalar su complementos para el proceso de verificación que mencionare mas adelante:
```bash
sudo apt install python3-certbot-apache -y
sudo apt install python3-certbot-nginx -y
```

---
## Crear certificado con wildcard
Un certificado con wildcard permite que se comparta el mismo certificado de un dominio a todos sus subdominios, evitando generar un certificado para cada subdominio.
Si el dominio ya tiene su certificado, [se tiene que borrar](#borrar-certificados) o se generara en una ruta nueva (ej. ``ejemplo.com-0001``, ejemplo.com-002``).
Para generarlo, es con el siguiente comando:
```bash
sudo certbot certonly \
--manual \
--preferred-challenges=dns \
--server https://acme-v02.api.letsencrypt.org/directory \
--agree-tos -d *.ejemplo.com -d ejemplo.com \
--email tucorreo@gmail.com
```
El comando te dara dos codigos (no le des ``ENTER`` al segundo codigo aún) los cuales deberas meter en un ``Record TXT`` nuevo en la administracion de DNS de tu dominio bajo el nombre de:
- ``_acme-challenge.ejemplo.com``

Finalmente terminas la comprobación dando ``ENTER`` y listo, se tendra que renovar manualmente cada 90 días.

## Crear certificado y implementarlo automaticamente con el servidor web
Para hacerlo es con el siguiente comando, elegir el dominio y seguir sus pasos:
```bash
sudo certonly
```

## Crear certificado normal
Para crear un certificado normal es con el siguiente comando y seguir sus pasos:
```bash
sudo certbot certonly
```

## Ver certificados
Para ver los certificados y sus estados que tienen registrados ``certbot`` es con el siguiente comando:
```bash
sudo certbot certificates
```

## Borrar certificados
Para borrar los certificados que tiene registrado ``certbot`` es con el siguiente comando:
```bash
sudo certbot delete --cert-name ejemplo.com
```



