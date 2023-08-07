# Transacciones 

## procesos complejos seguros 

si la base de datos falla debe poder devolver todos
los cambios automaticamente 

## BEGIN inicia el motor de base de datos
## ROLBACK es que si algo fallo devuelva todos lso cambios 

```sql
BEGIN

<consult>
COMMIT|ROLLBACK 

```

al lado de ejecutar esta la opcion desplegable de rollback y autocommit

desactivamos el auto commit 



```sql

BEGIN;
SELECT true;



```

como lo hicimos con commit descativado se habilataron dos botones al lado de ejecutar 
uno de commit y otro de rollback 

es decir que todo lo que se hace esta en memoria pero no se guarda en base de datos 

## supongamos que necesitamos hacer insercion en tren y estacion y que si uno falla se haga rollback 


```sql

BEGIN;
INSERT INTO public.estacion(
	 nombre, direccion)
	VALUES ('estacion transaccion' ,'direccion transacion');
	
INSERT INTO public.tren(
	 modelo, capacidad)
	VALUES ('modelo transaccion', 123);
```

se ejecuto correctamente pero si vamos a la tabla no esta la informacion porque no hemos hecho el commit 

 
## vamos a ver un caso en el que una falla  haciendo que una insercion de estacion tenga una id que ya existe 




```sql

BEGIN;
INSERT INTO public.estacion(id,
	 nombre, direccion)
	VALUES (105,'estacion transaccion' ,'direccion transacion');
	
INSERT INTO public.tren(
	 modelo, capacidad)
	VALUES ('modelo transaccion asdf', 123);
	
COMMIT;




ERROR:  Ya existe la llave (id)=(105).llave duplicada viola restricción de unicidad «estacion_pkey» 

ERROR:  llave duplicada viola restricción de unicidad «estacion_pkey»
SQL state: 23505
Detail: Ya existe la llave (id)=(105).

```