# Debugeo de scripts
textotexto
## Cronjob
textotexto
```bash
0 */1 * * * bash ~/crons/script-malo.sh >> ~/crontest.log 2>&1
```
## Script
textotexto
```bash
# Debugear
set -x # Imprimir comandos
set -e # Detener si hay error
```
