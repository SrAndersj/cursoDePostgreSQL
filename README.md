# Archivos de configuración

archivos que suelen ser la causa de problemas si no
los sabemos configurar,y si los configuramos bien sera el 95%
de las soluciones que necesitamos

* postgresql.conff

* pg_hba.conf

* pg_ident.conf

## vamos al pgdmin
vamos a Query Tool y le preguntamos donde estan los
archivos de configuracion 
```
SHOW config_file;
# vamos a la ruta de los archivos
```
## postgresql.conf
dentro de  postgresql.conf vemos 

* listen_addresses  que nos indica que direcciones escucha

* port = 5432   , aqui para cambiar el puerto
*  max_connections = 100	 maximo de conexiones

* en # - Settings - todo lo que aparece abajo es lo que esta predeterminado ,
si queremos cambiarlo pues lo descomentamos y hacemos cambio


## cuando se hacen cambios la base de datos solo los toma cuando se reinicia la base de datos 

## en este archivo tambien se encuetran las replicas 

las replicas son un servicio que permite tener un respaldo de la informacion
en tiempo real 

## pg_hba.conf

este archivo muestra los roles y los tipos de acceso que tienen a la base de datos

### tiene 5 columnas basicamente ,
una que dice la fuente de la conexion , otra dice que acciones puede hacer , otra dice que usuarios pueden conectarse , otra dice la direccion desde la que se estan conectando 
y otra que dice el metodo de autenticacion 
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     trust
host    replication     all             127.0.0.1/32            trust
host    replication     all             ::1/128                 trust

## explicacion 
dice que cualquier host , usando cualquier base de datos usando cualquier usuario
desde la direccion local 127.0.0.1/32 su metodo de acceso es md5(clave encriptada en md5)
```
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5


```

podemos cambiar el metodo ,(trust es para que no pida clave)
```
# METHOD can be "trust", "reject", "md5", "password", "scram-sha-256",
# "gss", "sspi", "ident", "peer", "pam", "ldap", "radius" or "cert".
# Note that "password" sends passwords in clear text; "md5" or
# "scram-sha-256" are preferred since they send encrypted passwords.
```

para bloquera ips que pueden ser malignas 


```
# IPv4 local connections:
host    all             all             121.0.0.1/32            deny
```


## pg_ident.conf

nos permite mapear usuarios , muchas veces teemos servicios que corren en linux que tienen usuario root y super usuario, este archivo tiene que ver con ellos ya que le permite a postgres saber que usuario local corresponde 


por ejemplo puedo decir que sudo  o admin , corresponden a un usuario adminsi

 Put your actual configuration here
# ----------------------------------

# MAPNAME       SYSTEM-USERNAME         PG-USERNAME
mapeo-admin     sudo                  administrador
                oswald


                cuando sudo acceda  que de una vez le de rol de administrador 
