# Comando 'certbot'
Para instalar `certbot` habra que instalar estas dependencias:
```bash
sudo apt install python3-pip python3-venv libaugeas0
```
Si se tenia instalado `certbot` por medio de apt-get, se tendra que desinstalar:
```bash
sudo apt remove certbot
sudo apt autoremove
```
Se tendra que crear un `venv` en cualquier ruta, para que no estorbe la crearemos en `/opt/certbot/`
```bash
sudo python3 -m venv /opt/certbot/
```
En ese `venv` se actualizara pip y se instalara `certbot` y sus plugins para `apache2` y `certbot-dns-google-domains` porque en mi caso uso **Google Domains**
```bash
sudo /opt/certbot/bin/pip install --upgrade pip
sudo /opt/certbot/bin/pip install certbot certbot-apache certbot-dns-google-domains
```

Por ultimo, se creara el comando `certbot` para no tener que meterse a la carpeta donde se instalo el `venv` y todo ese rollo
```bash
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```

---

## Generar certificado con wildcard automaticamente con Google Domains
Un certificado con wildcard permite que se comparta el mismo certificado de un dominio a todos sus subdominios, evitando generar un certificado para cada subdominio.  
Si el dominio ya tiene su certificado, [se tiene que borrar](#borrar-certificados) o se generara en una ruta nueva (ej. `tu-dominio.com-0001`, tu-dominio.com-002`).  

Primero obtendremos el token de Google Domains en
> `Seleccionas tu dominio` **>** `Seguridad` **>** `API de DNS de ACME` **>** `Crear token` **>** `Copiar token`

Despues, se creara el archivo que contendra la credencial que obtuvimos de Google Domains
```bash
sudo tee /etc/letsencrypt/ejemplo_credentials.ini << END
dns_google_domains_access_token = INSERTAR_TOKEN_DE_GOOGLE_DOMAINS_AQUI
dns_google_domains_zone = tu-dominio.com
END
```

Para generar el certificado, es con el siguiente comando:
```bash
sudo certbot certonly \
 --agree-tos \
 --authenticator 'dns-google-domains' \
 --dns-google-domains-credentials '/etc/letsencrypt/ejemplo_credentials.ini' \
 --server 'https://acme-v02.api.letsencrypt.org/directory' \
 -d '*.tu-dominio.com'
```

## Generar certificado normal y implementarlo automaticamente con el servidor web
Cualquiera de los comandos de generacion de certificado se renovaran automaticamente (el cront se encuentra en `/etc/cron.d/certbot`)  
Para hacerlo es con el siguiente comando, elegir el dominio y seguir sus pasos:  
```bash
sudo certbot
```

## Generar certificado normal
Para crear un certificado normal es con el siguiente comando y seguir sus pasos:
```bash
sudo certbot certonly
```

## Ver certificados
Para ver los certificados y sus estados que tienen registrados `certbot` es con el siguiente comando:
```bash
sudo certbot certificates
```

## Borrar certificados
Para borrar los certificados que tiene registrado `certbot` es con el siguiente comando:
```bash
sudo certbot delete --cert-name tu-dominio.com
```

---

# Instrucciones deprecadas
Se automatizo con Google Domains, pero si tu dominio no esta alli, tendras que hacer la investigacion tú  
En dado caso, aqui dejo las instrucciones para tener un certificao wildcard manual  

## Crear certificado con wildcard
Un certificado con wildcard permite que se comparta el mismo certificado de un dominio a todos sus subdominios, evitando generar un certificado para cada subdominio.
Si el dominio ya tiene su certificado, [se tiene que borrar](#borrar-certificados) o se generara en una ruta nueva (ej. `tu-dominio.com-0001`, tu-dominio.com-002`).
Para generarlo, es con el siguiente comando:
```bash
sudo certbot certonly \
--manual \
--preferred-challenges=dns \
--server https://acme-v02.api.letsencrypt.org/directory \
--agree-tos -d *.tu-dominio.com -d tu-dominio.com \
--email tucorreo@gmail.com
```
El comando te dara dos codigos (no le des `ENTER` al segundo codigo aún) los cuales deberas meter en un `Record TXT` nuevo en la administracion de DNS de tu dominio bajo el nombre de:
- `_acme-challenge.tu-dominio.com`

Finalmente terminas la comprobación dando `ENTER` y listo, se tendra que renovar manualmente cada 90 días.

