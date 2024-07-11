# Enlistar repositorios en una ruta
textotexto
## Script
textotexto
```bash
#!/bin/bash
DATE_STR=$(date +"%d%m%Y_%H%M%S")

# Enlistar repositorios en deploys
DEPLOYS_DIR="/home/ubuntu/deploys"
LIST_DEPLOYS_FILE="/home/ubuntu/backups/list_deploys-$DATE_STR.txt"
for item in "$DEPLOYS_DIR"/*; do
  if [ -d "$item" ]; then
    if [ -d "$item/.git" ]; then
      cd "$item" || continue
      COMMIT_HASH=$(git rev-parse HEAD)
      REMOTE_URL=$(git remote get-url origin)
      echo "$(basename "$item"): $COMMIT_HASH - $REMOTE_URL" >> "$LIST_DEPLOYS_FILE"
      cd - > /dev/null || continue
    else
      echo "$(basename "$item"): Not a git repository." >> "$LIST_DEPLOYS_FILE"
    fi
  fi
done
```
