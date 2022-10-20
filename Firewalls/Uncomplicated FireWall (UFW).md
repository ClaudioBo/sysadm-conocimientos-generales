# Uncomplicated FireWall (UFW)

Para instalarlo es con el comando (aunque ya deberia estar incluido predeterminadamente en el SO):
```bash
sudo apt install ufw -y
```

textotexto
```bash
sudo ufw allow 22/tcp
```

textotexto
```bash
sudo ufw enable
```

---

# Abrir puerto
textotexto
```bash
sudo ufw allow 3000/tcp
```

# Cerrar puerto
textotexto borra la regla anteriormente agregada textotexto
```bash
sudo ufw delete allow 3000/tcp
```

# Permitir direcciones IP
textotexto
```bash
sudo ufw allow from DIRECCION.IP # Permite completamente la ip
sudo ufw allow from DIRECCION.IP to any port 3000/tcp # Permite una ip a cierto puerto
```