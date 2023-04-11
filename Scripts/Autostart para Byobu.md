# Autostart para Byobu
## Cronjob
```bash
@reboot sudo su - claudio -c "bash -l inicio.sh"
```

## Script
```bash
#!/bin/bash -l
export TERM=screen-256color
export BYOBU_TERM=screen-256color

# A la berga todo byobu
tmux kill-server

# Sesión 1 - Correr comandos directamente - Es necesario llamar `bash -i` para que la pestaña no se cierre
byobu new-session -d -s platano -n "servicio1" -c "/home/claudio/algo/platano/" "mc ; bash -i"
byobu new-window -n "servicio2" -c "/home/claudio/algo/platano/" "htop ; bash -i"

# Sesión 2 - Correr comandos escritos """manualmente""" - Es compatible con las aliases del usuario
byobu new-session -d -s melon -n "servicio1" -c "/home/claudio/algo/melon/" ; byobu send-keys "mc" Enter
byobu new-window -n "servicio2" -c "/home/claudio/algo/melon/" ; byobu send-keys "htop" Enter
```