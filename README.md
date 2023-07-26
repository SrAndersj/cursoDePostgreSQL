# Funciones Especiales Principales

## ON CONFLICT DO

tabla estacion


vamos a reemplazar


```sql

INSERT INTO public.estacion(
	id, nombre, direccion)
	VALUES (1, 'nombre test', 'direccion test');


ERROR:  Ya existe la llave (id)=(1).llave duplicada viola restricción de unicidad «estacion_pkey» 

ERROR:  llave duplicada viola restricción de unicidad «estacion_pkey»
SQL state: 23505
Detail: Ya existe la llave (id)=(1).

    ```
sale error porque el id 1 ya existe 




```sql
INSERT INTO public.estacion(
	id, nombre, direccion)
	VALUES (1, 'nombre test', 'direccion test')
	ON CONFLICT(id)DO UPDATE SET nombre='nombre test',direccion='direccion test'	;



```

## RETURNING

```sql


INSERT INTO public.estacion(
	 nombre, direccion)
	VALUES ( 'RET', 'RETDRI')

RETURNING * ;

```



## LIKE / ILIKE

buscaremos un nombre donde sea parecido al siguiente formato

LIKE diferencia mayusculas y minusculas ILIKE  no 

```
SELECT id, nombre
	FROM public.pasajero
	WHERE nombre ILIKE 'a%';
	
-- % es uno o cualquier valor
-- _ es solo uno



```


## IS/IS NOT


que modelo es nulo

```sql 
SELECT *
	FROM public.tren
	WHERE modelo IS NULL;

```

