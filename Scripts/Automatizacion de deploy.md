# Automatizacion de deploy
textotexto
## Script
```bash
#!/bin/bash

# Dirigirse a la carpeta donde esta ubicado el script
cd $( dirname -- "$BASH_SOURCE"; )

# Guardar ultimo hash del commit
PREV_COMMIT=$(git rev-list HEAD -n 1)
git pull
NEW_COMMIT=$(git rev-list HEAD -n 1)

# Comprobar si no cambio de commit
if [[ $PREV_COMMIT == $NEW_COMMIT ]]; then
    if [[ -z "$1" || "$1" != "--force" ]]; then
        exit 0
    fi
fi

# Logica de redeploy
sudo docker compose -f docker-compose.staging.yml up -d --build --remove-orphans
```