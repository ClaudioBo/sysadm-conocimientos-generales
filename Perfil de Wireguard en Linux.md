# Cargar .conf de Wireguard en Linux PC
## Instalar
Toca instalar `wireguard-tools`
## Cargar archivo
```
nmcli connection import type wireguard file claudio.conf
```
## Evitar que la VPN sea la ruta por defecto
```
nmcli connection modify "claudio" \
    ipv4.never-default yes \
    ipv6.never-default yes
```
## Evitar que la VPN sobreescriba los DNS
```
nmcli connection modify "claudio" \
    ipv4.ignore-auto-dns yes \
    ipv6.ignore-auto-dns yes \
    ipv4.dns "" \
    ipv6.dns ""
```
## Levantar la VPN
```
nmcli connection up "claudio"
```
