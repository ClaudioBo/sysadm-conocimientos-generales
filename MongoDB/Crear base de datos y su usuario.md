# Crear base de datos y su respectivo usuario
No he tenido tanta oportunidad o tenido mucho tiempo para ver, manejar y hacer buena practica en MongoDB pero equis:

## Crear admin
textotexto
```bash
mongosh
```

comandoscomandos
```json
use admin;
db.dummy.insertOne({"dummy":1})
db.createUser({
	user:'admin',
	pwd:'contraseña-nueva',
	roles: ["userAdminAnyDatabase", "dbAdminAnyDatabase", "readWriteAnyDatabase"]
})
```

---

## Crear database con su user
textotexto
```bash
mongosh -u admin -p
```
USAR bd_nueva
```json
use bd_nueva;
```
CREAR UN DOCUMENTO DE ADORNO PARA QUE SE CREE LA BASE DE DATOS
```json
db.dummy.insertOne({"dummy":1})
```
CREAR USUARIO EXCLUSIVO PARA ESTA BASE DE DATOS (le puse el mismo nombre 'bd_nueva')
```json
db.createUser({
	user:'bd_nueva',
	pwd:'contraseña-nueva',
	roles : [{role:'readWrite',db:'bd_nueva'}]
})
```