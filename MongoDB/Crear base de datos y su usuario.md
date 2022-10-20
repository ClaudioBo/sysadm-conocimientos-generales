# Crear base de datos y su respectivo usuario
No he tenido tanta oportunidad o tenido mucho tiempo para ver, manejar y hacer buena practica en Mongodb pero equis:

## Crear admin
textotexto
```bash
mongo
```

comandoscomandos
```json
use admin;
db.dummy.insertOne({"dummy":1})
db.createUser({
	user:'admin',
	pwd:'contraseña-nueva',
	roles: [{role:"userAdminAnyDatabase",db:"admin"}]
})
```

---

## Crear database con su user
textotexto
```bash
mongo -u admin -p --authenticationDatabase admin
```
USAR bd_nueva
```json
use bd_nueva;
```
CREAR UNA TABLA DE ADORNO PARA QUE SE CREE LA BASE DE DATOS
```json
db.dummy.insertOne({"dummy":1})
```
CREAR USUARIO EXCLUSIVO PARA ESTA BASE DE DATOS (le puse el mismo nombre 'bd_nueva')
```json
db.createUser({
	user:'bd_nueva',
	pwd:'FZry9StJ7nmuxEUj',
	roles : [{role:'readWrite',db:'bd_nueva'}]
})
```