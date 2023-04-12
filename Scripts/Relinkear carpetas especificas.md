# Re-linkear carpetas especificas
textotexto
## Script
```bash
#!/bin/bash
for file in $(find . -maxdepth 1 -type d ! -path "." ! -name "*fastapi" ! -name "modelos"); do
    if [[ (! -L $file"/comun") && (-d $file"/comun") ]]; then
        sudo rm -rf $file/comun
        sudo ln -sn $(pwd)/modelos/ $file/comun
        echo "$file fue re-linkeado de vuelta."
    fi
done
```