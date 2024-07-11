# Copiar las migraciones encontradas
textotexto
## Script
textotexto
```bash
#!/bin/bash
DEPLOYS_DIR="/home/ubuntu/deploys"
find "$DEPLOYS_DIR" -type d -name "migrations" ! -path "*venv*" ! -path "*migrador*" | while read -r MIGRATIONS_FOLDER; do
    REL_PATH="${MIGRATIONS_FOLDER#$DEPLOYS_DIR/}"
    ENV_DIR=$(dirname "$REL_PATH")
    mkdir -p "$/home/ubuntu/backups/general/$ENV_DIR"
    cp -r "$MIGRATIONS_FOLDER" "$/home/ubuntu/backups/general/$ENV_DIR/"
done
```
