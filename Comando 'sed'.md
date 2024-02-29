# Comando 'sed'
textotexto
```bash
sed -i 's/VIEJO/NUEVO/g' ./ruta/del/*/archivo.txt
```

remplazar toda la linea blabla si contiene palabra clave
```bash
sed -i '/SQL_HOST/c SQL_HOST=db_ext' .env
```

remplazar toda la linea blabla si EMPIEZA con palabra clave
```bash
sed -i '/^SQL_HOST=/c SQL_HOST=db_ext' .env
```

reemplazar todas estas lineas usando find
```bash
find . -type f -name ".env" -print -exec \
sed -i -e '/SQL_HOST/c SQL_HOST=ip' \
       -e '/SQL_PORT/c SQL_PORT=5432' \
       -e '/SQL_USER/c SQL_USER=user' \
       -e '/SQL_PASSWORD/c SQL_PASSWORD=password' \
       -e '/SQL_DBNAME/c SQL_DBNAME=database' \
       -e '/DB_HOST/c DB_HOST=ip' \
       -e '/DB_PORT/c DB_PORT=5432' \
       -e '/DB_USER/c DB_USER=user' \
       -e '/DB_PASS/c DB_PASS=password' \
       -e '/DB_NAME/c DB_NAME=database' {} \;
```
