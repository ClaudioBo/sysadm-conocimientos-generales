# Consideracion al usar Docker con UFW

Resulta que todos los servicios expuestos bajo Docker quedan expuestos fuera del firewall de UFW posibilitando su acceso remoto, se deberá configurar tanto Docker como UFW para que no ocurra esto

## Deshabilitar interaccion directa de Docker a iptables
```sh
sudo tee /etc/docker/daemon.json << EOF
{
    "iptables": false
}
EOF
```

## Permitir que los contenedores de Docker pueda tener internet
Editarás el archivo `/etc/ufw/before.rules`
Despues de todas las lineas de la sección \***filter**, agregar:
```sh
# reglas de docker para permitir acceso de internet desde el contenedor
# enrutar trafico a traves del bridge
-A ufw-before-forward -i docker0 -j ACCEPT
-A ufw-before-forward -i testbr0 -j ACCEPT
-A ufw-before-forward -m state --state RELATED,ESTABLISHED -j ACCEPT
```
Al final del archivo, **despues** de la linea que dice `COMMIT`, agregar la siguiente sección:
```sh
# docker
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 172.16.42.0/8 -o eth0 -j MASQUERADE
# no borrar la linea de `COMMIT` o estas reglas no serán procesadas
COMMIT
```

Despues de guardar el archivo, reiniciar ufw con `sudo ufw disable && sudo ufw enable`
De paso, tambien reiniciar Docker Engine con `sudo service docker restart`
