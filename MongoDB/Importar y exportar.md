# Importar y exportar
## Exportar colección
comando que exportara su cagadero en una carpeta llamada dump/
```bash
sudo mongodump -u admin -d exportar_esto
```

## Importar colección
textotexto se crea automaticamente la database
```bash
sudo mongorestore -u admin /ruta/del/dump/
```
