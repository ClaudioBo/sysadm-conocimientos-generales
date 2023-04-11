# Backup de carpeta incremental
```bash
#!/bin/bash
SAVETO_DIR="/mnt/archivitos/backup_temporal/"
BACKUP_SOURCE="/mnt/archivitos/media/"

DATE=$(date +"%d-%m-%YT%H%M%S")
INCREMENTAL_FILE="backup_filelist.list"
INCREMENTAL_DATED_FILE="backup_filelist_$DATE.list"
ZIP_DATED_FILE="backup_$DATE.tar.gz"

# Ir a la carpeta de lo que se backupeara
cd $BACKUP_SOURCE

# Crear el backup y generar el archivo incremental
tar czvf $SAVETO_DIR/$ZIP_DATED_FILE --listed-incremental=$SAVETO_DIR/$INCREMENTAL_FILE *

# Ir a la carpeta de donde se guardo los backups
cd $SAVETO_DIR

# Backupear el archivo incremental
cp $INCREMENTAL_FILE $INCREMENTAL_DATED_FILE

# Subir el backup a servidor de backup
scp $ZIP_DATED_FILE claudio@backups.claudiobo.com:/mnt/backups
scp $INCREMENTAL_DATED_FILE claudio@backups.claudiobo.com:/mnt/backups

# Checar si el tamaño de los archivos transferidos es igual al original para eliminarlos
SIZE_REMOTE_INCREMENTAL_CMD="wc -c /mnt/backups/"$INCREMENTAL_DATED_FILE
SIZE_REMOTE_ZIP_CMD="wc -c /mnt/backups/"$ZIP_DATED_FILE

SIZE_REMOTE_INCREMENTAL=$(ssh claudio@backups.claudiobo.com $SIZE_REMOTE_INCREMENTAL_CMD | awk '{print $1}')
SIZE_REMOTE_ZIP=$(ssh claudio@backups.claudiobo.com $SIZE_REMOTE_ZIP_CMD | awk '{print $1}')

SIZE_ORIGINAL_INCREMENTAL=$(wc -c /mnt/archivitos/backup_temporal/$INCREMENTAL_DATED_FILE | awk '{print $1}')
SIZE_ORIGINAL_ZIP=$(wc -c /mnt/archivitos/backup_temporal/$ZIP_DATED_FILE | awk '{print $1}')

SIZE_REMOTE_INCREMENTAL=$(expr $SIZE_REMOTE_INCREMENTAL + 0)
SIZE_ORIGINAL_INCREMENTAL=$(expr $SIZE_ORIGINAL_INCREMENTAL + 0)
SIZE_REMOTE_ZIP=$(expr $SIZE_REMOTE_ZIP + 0)
SIZE_ORIGINAL_ZIP=$(expr $SIZE_ORIGINAL_ZIP + 0)

# Comprobar si el tamaño de los archivos transferidos es igual al original para eliminarlos
if [[ $SIZE_ORIGINAL_INCREMENTAL -eq $SIZE_REMOTE_INCREMENTAL ]]; then
    rm $INCREMENTAL_DATED_FILE
fi

if [[ $SIZE_ORIGINAL_ZIP -eq $SIZE_REMOTE_ZIP ]]; then
    rm $ZIP_DATED_FILE
fi
```