# ROLES 

## que puede hacer un ROL


* crear y eliminar 

* asignar atributos 

* agrupar con otros roles

* Roles predeterminados   


## desde la shell  

consultamos que podemos hacer 
```sql
postgres=# \h CREATE ROL


```

creamos rol 


```sql

postgres=# CREATE ROLE  usuario_consulta ;
CREATE ROLE


```


para ver el listado de usuarios

```sql
postgres=# \dg


  Nombre de rol   |                         Atributos
               | Miembro de
------------------+------------------------------------------------------------+------------
 postgres         | Superusuario, Crear rol, Crear BD, Replicaci¾n, Ignora RLS | {}
 usuario_consulta | No puede conectarse

```


## vamos a darle capacidad de acceder a la base de datos 

```sql
postgres=# ALTER ROLE  usuario_consulta WITH LOGIN;
ALTER ROLE



postgres=# \dg
                                       Lista de roles
  Nombre de rol   |                         Atributos
               | Miembro de
------------------+------------------------------------------------------------+------------
 postgres         | Superusuario, Crear rol, Crear BD, Replicaci¾n, Ignora RLS | {}
 usuario_consulta |
               | {}

```

## vamos a darle estatus super usuario 

```sql
postgres=# ALTER ROLE  usuario_consulta WITH SUPERUSER;

```

## asignamos contraseña 




```sql
postgres=# ALTER ROLE  usuario_consulta WITH PASSWORD 'toor'; 

```



vamos a borrarlo 


```sql

postgres=# DROP ROLE  usuario_consulta ;

```




```sql


```