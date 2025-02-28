# Crear usuario
adduser usuario-sftp

# Deshabilitar login
usermod -s /usr/sbin/nologin usuario-sftp

# Configurar sshd con acceso al usuario
Crear archivo .conf (nombrar como sea) en `/etc/ssh/sshd_config.d/` con este contenido:
```py
Match User usuario-sftp
    PasswordAuthentication yes
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no
    ChrootDirectory /mnt/wd-red/usuario-sftp
```

# Crear carpeta del usuario (los permisos deben ser root)
sudo mkdir /mnt/wd-red/usuario-sftp

# Crear carpeta accesible para el usuario
sudo mkdir /mnt/wd-red/usuario-sftp/home
sudo chown -R usuario-sftp:usuario-sftp /mnt/wd-red/usuario-sftp/home
