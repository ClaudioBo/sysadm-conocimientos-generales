# SSH a Local
```bash
rsync -rv --progress -e ssh claudio@ejemplo.com:/home/claudio/deploys/backup-media.tar.gz .
```

# Local a SSH
```bash
rsync -rv --progress -e ssh backup.tar.gz claudio@ejemplo.com:/home/claudio/
```