
# Creación de Tablas

CREATE 

ALTER 

DROP 


## CREAR pg ADMIN


click derecho  en database

create , database

damos nombre y dejamos todo 

podemos ver en sql la sentencia


vamos a schemas luego a public y a  tables

creamos la tabla pasajeros 
y en columns  agregamos las columnas definidas 

### columns


id serial   y activamos el primary key 


nombre  character varying 

direccion_residencia character varying  

fecha_nacimiento  date 


### constraints

aqui creamos la llave primaria 

vamos a primary key 

Name           columns

pasajero_pkey    id 


el sql de todo esto es

``` sql

CREATE TABLE public."pasajeros "
(
    id serial,
    nombre character varying,
    "direccion _residencia" character varying,
    fecha_nacimiento date,
    PRIMARY KEY (id)
);

ALTER TABLE IF EXISTS public."pasajeros "
    OWNER to postgres;

```


ahora vamos a hacer el script de insercion 


encima de la  tabla pasajeros click derecho , scripts  , INSERT script 

salio el codigo 

```sql
INSERT INTO public."pasajeros "(
	id, nombre, "direccion _residencia", fecha_nacimiento)
	VALUES (?, ?, ?, ?);

```

como id es un campo que se va ir actualizando con cada insert lo borramos

```sql
INSERT INTO public."pasajeros "(
	 nombre, "direccion _residencia", fecha_nacimiento)
	VALUES (?, ?, ?, ?);

```

en VALUES  reemplazamos los ? por los valores 


```sql
INSERT INTO public."pasajeros "(
	 nombre, "direccion _residencia", fecha_nacimiento)
	VALUES ('Primer Pasajero', 'Direccion x', '"2023-07-04"');

```

consulta sencilla para consultar fecha

```sql
SELECT current_date;

```