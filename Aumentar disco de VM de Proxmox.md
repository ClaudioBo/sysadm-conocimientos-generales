# Aumentar disco de VM de Proxmox
Despues de aumentar el tamaño del disco de la VM en Proxmox, para que la VM tome en cuenta el espacio nuevo se hara lo siguiente:
1. Ubicar el numero de partición de nuestros datos
```sh
sudo parted /dev/sda print
# En mi caso fue 1:  
# 1      116MB   209GB   208GB   ext4
```
2. Expandir al 100% el espacio
```sh
sudo parted /dev/sda resizepart 1 100%
```
3. Checar en fdisk el espacio
```sh
sudo fdisk -l /dev/sda
```
4. Resizear filesystem si es necesario
```sh
sudo resize2fs /dev/sda1
```
5. Comprobar espacio nuevo
```sh
df -h
```