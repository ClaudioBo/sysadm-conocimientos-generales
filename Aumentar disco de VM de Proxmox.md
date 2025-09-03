# Aumentar disco de VM de Proxmox
Despues de aumentar el tamaño del disco de la VM en Proxmox, para que la VM tome en cuenta el espacio nuevo se hara lo siguiente:

1. Desmontar el disco que será afectado, en este caso /dev/sda que esta montado en /mnt/disk1
```rb
sudo umount /mnt/disk1
```
2. Ubicar el numero de partición de nuestros datos
```rb
sudo parted /dev/sda print
# Te preguntara si quieres arreglarlo, escribe 'Fix' y Enter
```
3. Expandir al 100% el espacio
```rb
sudo parted /dev/sda resizepart 1 100%
```
4. Verificar integridad (necesario)
```rb
sudo e2fsck -f /dev/sda1
```
5. Checar en fdisk el espacio
```rb
sudo fdisk -l /dev/sda
```
6. Resizear filesystem si es necesario
```rb
sudo resize2fs /dev/sda1
```
7. Re-montar disco
```rb
sudo mount -a # Montar todos los discos en /etc/fstab
```
9. Comprobar espacio nuevo
```sh
df -h
```
