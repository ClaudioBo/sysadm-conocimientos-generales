# Matar proceso corriendo en X puerto
textotexto matar proceso corriendo en puerto
```bash
sudo fuser -k 3000/tcp
```

# Checar si esta corriendo algo en X puerto
```bash
sudo netstat -anpe | grep LISTEN | grep 3000
```