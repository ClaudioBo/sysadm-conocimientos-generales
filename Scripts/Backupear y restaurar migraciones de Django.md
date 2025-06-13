# Backupear y restaurar migraciones de Django
## Backupear
```sh
sudo tar -czf migrations.tar.gz $(find . -path "*/migrations/*.py" ! -path "./venv/*" -not -name "__init__.py")
```
## Restaurar
```sh
tar -xvzf migrations.tar.gz
```
