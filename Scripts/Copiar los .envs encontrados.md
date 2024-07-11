# Copiar los .envs encontrados
textotexto
## Script
textotexto
```bash
#!/bin/bash
DATE_STR=$(date +"%d%m%Y_%H%M%S")

# Copiar los .envs encontrados
DEPLOYS_DIR="/home/ubuntu/deploys"
LIST_DEPLOYS_FILE="/home/ubuntu/backups/list_deploys-$DATE_STR.txt"
find "$DEPLOYS_DIR" -type f -name ".env" | while read -r ENV_FILE; do
    REL_PATH="${ENV_FILE#$DEPLOYS_DIR/}"
    ENV_DIR=$(dirname "$REL_PATH")
    mkdir -p "/home/ubuntu/backups/$ENV_DIR"
    cp "$ENV_FILE" "/home/ubuntu/backups/$ENV_DIR/"
done
```
