# Generacion de llaves SSH
```bash
ssh-keygen -t rsa -b 4096

# se puede agregar un comentario
ssh-keygen -t rsa -b 4096 -C "hola jaja"
# otro ejemplo
ssh-keygen -t rsa -b 4096 -C "micorreo@gmail.com"
```
> Opcional: poner contraseña para que al momento de acceder la pida.

Rolar la publica (id_rsa.pub) y quedate con la privada (id_rsa)

id_rsa es la cerradura y id_rsa.pub es la llave (explicacion qlera)