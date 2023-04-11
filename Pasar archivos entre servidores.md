# archivo SSH a carpeta actual local
```bash
rsync -rv --progress -e ssh claudio@ejemplo.com:/home/claudio/deploys/backup-media.tar.gz .
```

# archivo local a SSH
```bash
rsync -rv --progress -e ssh backup.tar.gz claudio@ejemplo.com:/home/claudio/
```
