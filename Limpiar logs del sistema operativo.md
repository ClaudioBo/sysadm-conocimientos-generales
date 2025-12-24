# Truncar logs existentes
```sh
sudo find /var/log -type f -exec truncate -s 0 {} \;
```
# Borrar logs rotados (.log.1, etc.)
```sh
sudo find /var/log -type f \
  \( -name "*.log.[0-9]*" -o -name "*.gz" -o -name "*.xz" -o -name "*.zst" \) \
  -delete
```
