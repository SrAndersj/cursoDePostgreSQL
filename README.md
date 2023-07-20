# Inserción y consulta de datos
## PgAdmin 

tabla estacion

insertar scripts  INSERT Script

```sql

INSERT INTO public.estacion(
	 nombre, direccion)
	VALUES ( 'centro','calle 80 #12');



ALTER TABLE public.tren
ALTER COLUMN modelo TYPE VARCHAR(50); -- Cambia "VARCHAR(50)" según la longitud máxima que desees para el modelo.

INSERT INTO public.tren(
	 capacidad,modelo)
	VALUES ( 100,'Modelo 1');


  INSERT INTO public.trayecto(
	id_estacion, id_tren, nombre)
	VALUES (1, 1, 'Ruta 1');

  
```

