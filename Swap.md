# Crear swap
Primero se debera crear el archivo contenedora del swap con el siguiente comando:
```bash
# count=16M significa 16GB
sudo dd if=/dev/zero of=/swap_new.swap bs=1K count=16M
sudo mkswap /swap_new.swap
```

Despues se inicializa con el comando:
```bash
sudo swapon /swap_new.swap
```

Para comprobar si funciono, se puede usar el comando `htop` o el siguiente:
```bash
sudo swapon --show
```

Se tendra que configurar para que Ubuntu inicialize automaticamente el swap nuevo al iniciar el sistema editando `/etc/fstab` agregando la siguiente linea al final:
```c
/swap_new.swap	none	swap	sw	0	0 
```

# Reiniciar swap
Para reiniciar/liberar el swap en caso de que este este lleno, es con el comando:
```bash
sudo swapoff -a && sudo swapon -a
```