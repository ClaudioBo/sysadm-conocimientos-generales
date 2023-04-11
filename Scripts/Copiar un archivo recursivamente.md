# Copiar un archivo recursivamente
Buscar los directorios que contengan `.copiar.aca`
```bash
#!/bin/bash
COPIAR_A=$(find /home/claudio/deploys -type f -name ".copiar.aca" | xargs dirname)

for dir in $COPIAR_A; do
    cp -v ~/texto.txt $dir
done
```