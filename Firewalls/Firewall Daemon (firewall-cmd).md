# Firewall Daemon (firewall-cmd)
<sub><sub><sub> Tengo que usar esta pendejada por Oracle Cloud 💤💤💤 </sub></sub></sub>
Se instala con el comando:
```bash
sudo apt install firewalld -y
```

# Agregar puerto
textotexto
```bash
sudo firewall-cmd --permanent --zone=public --add-port=3000/tcp
sudo firewall-cmd --reload
```

# Cerrar puerto
textotexto
```bash
¯\_(ツ)_/¯
```

# Troubleshoot
## Service not running
En caso de que no se pueda agregar un puerto o algo, podria salir alguno de estos dos errores:
```diff
- Error: DBUS_ERROR: Failed to connect to socket /run/dbus/system_bus_socket: No such file or directory
- FirewallD is not running
```
Para arreglarlo, hay que correrlo, posiblemente el servicio este "masked" entonces habra que "unmaskearlo":
```bash
sudo systemctl unmask firewalld
```
y despues inicializar el servicio:
```bash
sudo systemctl enable firewalld
sudo systemctl start firewalld
```

<!--
```bash
sudo iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT
sudo netfilter-persistent save
sudo netfilter-persistent reload
```
-->
