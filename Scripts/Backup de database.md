# Backup de database
```bash
#!/bin/bash
DATE_STR=$(date +"%d-%m-%Y_%H-%M-%S")
FILE_DIRECTORY=~/db_backups
FILE_NAME=database_$DATE_STR

# Crear carpetas
mkdir $FILE_DIRECTORY

# En caso de que sea PostgreSQL o MySQL, descomentar
# PGPASSWORD=xxxxxx pg_dump -h localhost -U username database_db > $FILE_DIRECTORY/$FILE_NAME.db
# sudo mysqldump -u root database_db > $FILE_NAME

# Lo mejor es comprimir el dump, ahorra demasiado espacio
tar czvf $FILE_DIRECTORY/$FILE_NAME.tar.gz $FILE_DIRECTORY/$FILE_NAME.db
rm $FILE_DIRECTORY/$FILE_NAME.db

# Limpiar backups mayor a 7 dias
find $FILE_DIRECTORY/ -type f -ctime +7 -exec rm -rf {} \;
```