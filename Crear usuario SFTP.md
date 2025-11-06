# 🧩 Guía completa: Crear un usuario SFTP aislado en Ubuntu

## 1. Crear el usuario

```bash
sudo adduser usuario-sftp
```

(Sigue las indicaciones y asigna una contraseña segura.)

---

## 2. Deshabilitar acceso por shell (solo SFTP)

```bash
sudo usermod -s /usr/sbin/nologin usuario-sftp
```

---

## 3. Crear la estructura de directorios para SFTP

Creamos una carpeta **fuera del home de otros usuarios**, para evitar errores de permisos del chroot.

```bash
sudo mkdir -p /sftp/usuario-sftp/home
```

Asignamos los permisos requeridos:

```bash
sudo chown root:root /sftp/usuario-sftp
sudo chmod 755 /sftp/usuario-sftp

sudo chown usuario-sftp:usuario-sftp /sftp/usuario-sftp/home
```

---

## 4. Configurar SSHD para el usuario

Crea un archivo de configuración en `/etc/ssh/sshd_config.d/`
(puedes llamarlo por ejemplo `/etc/ssh/sshd_config.d/usuario-sftp.conf`)

```bash
sudo nano /etc/ssh/sshd_config.d/usuario-sftp.conf
```

Y agrega el siguiente contenido:

```bash
Match User usuario-sftp
    PasswordAuthentication yes
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no
    ChrootDirectory /sftp/usuario-sftp
```

Guarda y cierra el archivo.

---

## 5. Reiniciar el servicio SSH

Para aplicar los cambios:

```bash
sudo systemctl restart sshd
```

---

## 6. Probar la conexión

Desde el mismo servidor o remoto:

```bash
sftp usuario-sftp@localhost
```

Si todo está correcto deberías ver:

```
Connected to localhost.
sftp> pwd
Remote working directory: /
sftp> ls
home
```
