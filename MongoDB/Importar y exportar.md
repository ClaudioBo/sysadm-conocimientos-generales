# Importar y exportar
## Exportar
comando que exportara su cagadero en una carpeta (no recuerdo si era en la misma carpeta o en una nueva)
```bash
sudo mongodump -u admin --authenticationDatabase admin -d exportar_esto
```

## Importar
textotexto
```bash
sudo mongorestore -u admin --authenticationDatabase admin -d importar_aca /ruta/del/dump/
```
