# No preguntar por contraseña de sudo
textotexto
```bash
whoami # claudio
```
textotexto
```bash
sudo visudo
```
textotexto al final del archivo (con tu nombre de usuario, el que dijo el comando whoami)
```
claudio		ALL=(ALL) NOPASSWD:ALL
```
