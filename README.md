# Triggers

permiten ejecutar funciones dependiendo de acciones que se
ejecuten en una tabla 

cuando se hace Insert , Update , Delete



Vamos a guardar el contador "importantePL2"()  en una tabla adicional 


creamos tabla conteo_pasajeros

```sql
CREATE TABLE public.conteo_pasajeros
(
    total integer,
    tiempo time with time zone,
    id serial,
    PRIMARY KEY (id)
);

ALTER TABLE IF EXISTS public.conteo_pasajeros
    OWNER to postgres;

```

ahora modificamos la pl "importantePL2"() , en la funcion damos create script

agregamos las lineas 

```sql
INSERT INTO conteo_pasajeros(total,tiempo)
	VALUES(contador,now())

```

y queda asi 


```sql
CREATE OR REPLACE FUNCTION public."importantePL2"()
    RETURNS integer
    LANGUAGE 'plpgsql'
    COST 100
    VOLATILE PARALLEL UNSAFE
AS $BODY$
DECLARE 
    rec record;
    contador integer := 0;
BEGIN
    FOR rec IN SELECT * FROM pasajero LOOP
        RAISE NOTICE 'un pasajero se llama %', rec.nombre;
        contador := contador + 1;
    END LOOP;
    
    RAISE NOTICE 'conteo es %', contador;
	INSERT INTO conteo_pasajeros (total, tiempo)
	VALUES (contador, now());
    
    RETURN contador;
END
$BODY$;

ALTER FUNCTION public."importantePL2"()
    OWNER TO postgres;


```


la ejecutamos 


```sql
SELECT "importantePL2"()
```

vamos a hacer que la funcion sea de tipo trigger con

```sql

 RETURNS integer 
 lo cambiamos a

 RETURNS TRIGGER

```


```sql

CREATE OR REPLACE FUNCTION public."importantePL2"(
	)
    RETURNS TRIGGER
    LANGUAGE 'plpgsql'
    COST 100
    VOLATILE PARALLEL UNSAFE
AS $BODY$
DECLARE 
    rec record;
    contador integer := 0;
BEGIN
    FOR rec IN SELECT * FROM pasajero LOOP
        RAISE NOTICE 'un pasajero se llama %', rec.nombre;
        contador := contador + 1;
    END LOOP;
    
    RAISE NOTICE 'conteo es %', contador;
	INSERT INTO conteo_pasajeros (total, tiempo)
	VALUES (contador, now());
    
    RETURN contador;
END
$BODY$;

ALTER FUNCTION public."importantePL2"()
    OWNER TO postgres;

```


conexion entre la trigger la pl y la tabla



```sql
CREATE TRIGGER mi_trigger

AFTER INSERT
ON pasajero

FOR EACH ROW
EXECUTE PROCEDURE "importantePL2"();

```



actualizamos pl


```sql
-- FUNCTION: public.importantePL2()

-- DROP FUNCTION IF EXISTS public."importantePL2"();

CREATE OR REPLACE FUNCTION public."importantePL2"()
    RETURNS trigger
    LANGUAGE 'plpgsql'
    COST 100
    VOLATILE NOT LEAKPROOF
AS $BODY$
DECLARE 
    rec record;
    contador integer := 0;
BEGIN
    FOR rec IN SELECT * FROM pasajero LOOP
        
        contador := contador + 1;
    END LOOP;
    
    RAISE NOTICE 'conteo es %', contador;
	INSERT INTO conteo_pasajeros (total, tiempo)
	VALUES (contador, now());
    
    RETURN NEW;
END
$BODY$;

ALTER FUNCTION public."importantePL2"()
    OWNER TO postgres;


```


insertamos datos en la tabla

```sql



```