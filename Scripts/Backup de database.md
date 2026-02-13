# Backup de database
```bash
#!/bin/bash
DATE_STR=$(date +"%d%m%Y_%H%M%S")
BACKUPS_DIRECTORY=~/db_backups
NEW_FILE_NAME=database_$DATE_STR

# Crear carpetas
mkdir $BACKUPS_DIRECTORY

# En caso de que sea PostgreSQL o MySQL, descomentar
# PGPASSWORD=xxxxxx pg_dump -h localhost -U username database_db > $BACKUPS_DIRECTORY/$NEW_FILE_NAME.db
# sudo mysqldump -u root database_db > $NEW_FILE_NAME

# Lo mejor es comprimir el dump, ahorra demasiado espacio
tar czvf $BACKUPS_DIRECTORY/$NEW_FILE_NAME.tar.gz $BACKUPS_DIRECTORY/$NEW_FILE_NAME.db
rm $BACKUPS_DIRECTORY/$NEW_FILE_NAME.db

# Backupeo de volumen de Docker
# NOMBRE_VOLUMEN=proyecto-data && sudo docker run --rm -v "${NOMBRE_VOLUMEN}:/volume-data:ro" alpine sh -c "cd /volume-data && tar --numeric-owner -cvf - ." | zstd -v -19 -T0 -o "${NOMBRE_VOLUMEN}.tar.zst"

# Restaurar jaja
# NOMBRE_VOLUMEN=proyecto-data && zstd -d -c "${NOMBRE_VOLUMEN}.tar.zst" | sudo docker run --rm -i -v "${NOMBRE_VOLUMEN}:/volume-data" alpine sh -c "cd /volume-data && tar --numeric-owner -xvf -" && unset NOMBRE_VOLUMEN

# Limpiar backups mayor a 7 dias, manteniendo minimo 7 archivos
MIN_FILES=7
FILE_COUNT=$(find "$BACKUPS_DIRECTORY" -type f | wc -l)
if [ "$file_count" -gt "$MIN_FILES" ]; then
    find "$BACKUPS_DIRECTORY" -type f -ctime +7 -exec rm -rf {} \;
fi


```
