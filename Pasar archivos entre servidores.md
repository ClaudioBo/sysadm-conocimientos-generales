# archivo SSH a carpeta actual local
```bash
rsync -rv --progress -e ssh claudio@ejemplo.com:/home/claudio/deploys/backup-media.tar.gz .
```

# archivo local a SSH
```bash
rsync -rv --progress -e ssh backup.tar.gz claudio@ejemplo.com:/home/claudio/
```

# alternativa
```bash
scp $ZIP_DATED_FILE claudio@backups.claudiobo.com:/mnt/backups
```

# Alternativa: Subir el backup a servidor de backup por contraseña (inseguro)
```bash
sshpass -p "$SSH_PASSWORD" scp -r "$ZIP_DATED_FILE.tar.gz" "claudio@backups.claudiobo.com:/mnt/backups"
```