# Funciones Especiales Avanzadas

## COALESCE 


```sql
SELECT id, nombre, direccion_residencia, fecha_nacimiento
	FROM public.pasajero WHERE id= 1;

```

```sql

SELECT id,COALESCE (nombre,'NO APLICA '), direccion_residencia, fecha_nacimiento
	FROM public.pasajero WHERE id= 1;

```

## NULLIF

compara
```sql
SELECT NULLIF (0,0)

```
## GREATEST

nos retorna el numero mayor 

```sql

SELECT GREATEST (1,3,5,7,9,4,3,2)

```

## LEAST

retorna el menor 

```sql

SELECT LEAST (1,3,5,7,9,4,3,2)
```

## BLOQUES ANONIMOS 


CONSULTAR SI ES NIÑO 


```sql

SELECT id, nombre, direccion_residencia, fecha_nacimiento,

CASE

WHEN fecha_nacimiento >'2015-01-01' THEN
'Niño'
ELSE
'Mayor '
END
	FROM public.pasajero;
    
```


