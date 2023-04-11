# Comando 'find'
```bash
find ./** -type f -name "archivo.txt" -exec echo {} \;
find ./** -type f -name "archivo.txt" -exec rm -v {} \;
```

# Comandos de ejemplo

## Fuck all \_\_pycache\_\_/ and migrations/ related stuff**
```bash
find . | grep -E "(/__pycache__$|\.pyc$|\.pyo$)" | sudo xargs rm -rf
sudo find . -path "*/migrations/*.py" ! -path "./venv/*" -not -name "__init__.py" -delete
```

## Limpiar mapas de Minecraft y solo dejar (level.dat y region/)
```bash
find . \( -name "data" -o -name "DIM-1" -o -name "serverconfig" -o -name "advancements" -o -name "terrain-textures" -o -name "mcedit.log" -o -name "poi" -o -name "playerdata" -o -name "DIM1" -o -name "stats" -o -name "*.dat_old" -o -name "*.dat_mcr" -o -name "*.lock" -o -name "uid.dat" -o -name "WorldDownloader.txt" -o -name "mcedit_waypoints.dat" -o -name "*.swp" -o -name "*.swo" -o -name "*.DS_Store" -o -name "forcedchunks.dat" -o -name "icon.png" -o -name "spc" \) -exec rm -rfv {} \;
```

## Imprimir los mundos de Minecraft que tengan mas de 2 archivos (donde haya un level.dat)
```bash
find . -name "level.dat" -exec sh -c 'test $(find "${1%/*}" -maxdepth 1 | wc -l) -gt 2 && echo "$1"' _ {} \;
```
