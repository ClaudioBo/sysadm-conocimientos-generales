# Copiar los scripts de crons
textotexto
## Script
textotexto
```bash
#!/bin/bash

# Copiar los scripts de crons
find "/root/crons" -maxdepth 1 -type f -name "*.sh" | while read -r CRON_SCRIPT; do
    cp "$CRON_SCRIPT" "/home/ubuntu/backups/"
done
```
