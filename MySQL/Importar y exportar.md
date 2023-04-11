# Exportar base de datos
textotexto exportar
```bash
sudo mysqldump test_db > dump-test_db.sql
# Este comando no esta chido este pq tmb copia las tablas internas de mysql:
# sudo mysqldump --all-databases > todo.sql 
```

# Importar base de datos
textotexto test_db debe estar creada antes de importar
```bash
sudo mysql test_db < dump-test_db.sql
```