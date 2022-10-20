# Comando 'find'
```bash
find ./** -type f -name "archivo.txt" -exec echo {} \;
find ./** -type f -name "archivo.txt" -exec rm -v {} \;
```

## Fuck all \_\_pycache\_\_/ and migrations/ related stuff**
```bash
find . | grep -E "(/__pycache__$|\.pyc$|\.pyo$)" | sudo xargs rm -rf
sudo find . -path "*/migrations/*.py" ! -path "./venv/*" -not -name "__init__.py" -delete
```