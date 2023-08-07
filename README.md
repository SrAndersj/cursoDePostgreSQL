# Simulando conexion a bases de datos remotos
##datos externos
## dblink 

permite conectarse a servidores remotos dentro de una consulta

### creamos una base de datos para simular que es la remota 

create databases

se llama remota 


```sql

-- Database: remota

-- DROP DATABASE IF EXISTS remota;

CREATE DATABASE remota
    WITH
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Spanish_Spain.1252'
    LC_CTYPE = 'Spanish_Spain.1252'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;


```


creamos una tabla 

```sql

CREATE TABLE public.vip
(
    id integer,
    fecha date
);

ALTER TABLE IF EXISTS public.vip
    OWNER to postgres;

```

hacemos un insert script  para decir que pasajero 50 es vip desde tal fecha



```sql
INSERT INTO public.vip(
	id, fecha)
	VALUES (50, '2010-01-01');

```


## vamos a conectarnos a remota desde la base de datos de transporte

nos desconectamos de remota 


creamos un script en tabla pasajero cual es el vip y que me traiga la informacion 

### instalamos dblink 

```sql
CREATE EXTENSION dblink;
```


consultamos 


```sql
SELECT * FROM 
dblink('dbname=remota
	   port=5432
	   host=127.0.0.1 
	   user=postgres 
	   password=etc123', 
	   'SELECT id,fecha FROM vip')
	   AS datos_remotos(id integer,fecha date);

```


### ahora usamos un join para cruzar con datos locales 

```sql



-- Primero, asegúrate de tener la extensión dblink instalada:
-- CREATE EXTENSION IF NOT EXISTS dblink;

-- Luego, realiza la consulta utilizando dblink en la cláusula FROM:
SELECT * 
FROM pasajero
JOIN
(
    SELECT id, fecha
    FROM dblink('dbname=remota
                 port=5432
                 host=127.0.0.1 
                 user=postgres 
                 password=etc123', 
                'SELECT id, fecha FROM vip'
    ) AS datos_remotos(id integer, fecha date)
) AS datos_remotos
ON (pasajero.id = datos_remotos.id);

```
### es lo mismo con USING id 


```sql



-- Primero, asegúrate de tener la extensión dblink instalada:
-- CREATE EXTENSION IF NOT EXISTS dblink;

-- Luego, realiza la consulta utilizando dblink en la cláusula FROM:
SELECT * 
FROM pasajero
JOIN
(
    SELECT id, fecha
    FROM dblink('dbname=remota
                 port=5432
                 host=127.0.0.1 
                 user=postgres 
                 password=etc123', 
                'SELECT id, fecha FROM vip'
    ) AS datos_remotos(id integer, fecha date)
) AS datos_remotos
USING (id);



```