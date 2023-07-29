# PL/SQL

## procedimientos almacenados

vamos a crear una PL 

pg admin


para que texto aparezca 


```sql

DO $$
BEGIN
	RAISE NOTICE 'algo esta pasando ';

END

$$

```


llamar a los nombres de pasajeros


```sql

DO $$
DECLARE 
	rec record;
	
	contador integer :=0;
BEGIN
	FOR rec IN SELECT * FROM pasajero LOOP
		RAISE NOTICE 'un pasajero se llama %', rec.nombre;
		contador :=contador+1;
	END LOOP;
	
	RAISE NOTICE 'conteo es %',contador;
END


$$;


```



creamos una funcion en base al codigo anterior
 * void es para quee no retorne nada

```sql
CREATE FUNCTION importantePL()
RETURNS void 
AS $$
DECLARE 
	rec record;
	
	contador integer :=0;
BEGIN
	FOR rec IN SELECT * FROM pasajero LOOP
		RAISE NOTICE 'un pasajero se llama %', rec.nombre;
		contador :=contador+1;
	END LOOP;
	
	RAISE NOTICE 'conteo es %',contador;
END


$$
LANGUAGE PLPGSQL;


```

llamar la funcion

```sql
SELECT importantePL();

```

para que retorne valores del contador

```sql

-- Primero, elimina la función existente (¡cuidado, esto borrará la función y sus definiciones!)
DROP FUNCTION IF EXISTS importantePL();

-- Luego, crea la función con el nuevo tipo de retorno
CREATE OR REPLACE FUNCTION importantePL()
RETURNS integer 
AS $$
DECLARE 
    rec record;
    contador integer := 0;
BEGIN
    FOR rec IN SELECT * FROM pasajero LOOP
        RAISE NOTICE 'un pasajero se llama %', rec.nombre;
        contador := contador + 1;
    END LOOP;
    
    RAISE NOTICE 'conteo es %', contador;
    RETURN contador;
END
$$
LANGUAGE PLPGSQL;


```

## VAMOS A USAR FUINCIONES CON LA  HERRAMIENTA DE PGADMIN 


vamos a FUNCTIONS , create

en definition colocamos el tipo de retorno 

integer

y language PLSQL


en code pegamos


```sql



DECLARE 
    rec record;
    contador integer := 0;
BEGIN
    FOR rec IN SELECT * FROM pasajero LOOP
        RAISE NOTICE 'un pasajero se llama %', rec.nombre;
        contador := contador + 1;
    END LOOP;
    
    RAISE NOTICE 'conteo es %', contador;
    RETURN contador;
END


```


lo que sale es


```sql
CREATE FUNCTION public."importantePL2"()
    RETURNS integer
    LANGUAGE 'plpgsql'
    
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
    RETURN contador;
END
$BODY$;

ALTER FUNCTION public."importantePL2"()
    OWNER TO postgres;



```


```sql

SELECT public."importantePL2"()

```