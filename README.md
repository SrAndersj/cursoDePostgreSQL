# Particiones

* Separación fisica de datos

* Estructura lógica

## vamos a crear una tabla , agregarle particiones 



creamos tabla bitacora_vaije         


[Mis clases Platzi OneNote]( https://udlaedu-my.sharepoint.com/:o:/g/personal/jho_castano_udla_edu_co/EhSghH-c5QNDp3tqirH82kYB2h-zv3H2ySw2iAr3fB465A?e=9muHky)

### en la pestaña general

activamos que es una tabla particionable 
### en pesttaña partition

agregamos fila 

el key type le decimos por Column

Colmn seleccionamos fecha


esto quiere decir que vamos a crear varias tablas pequeñas que contienen diferentes rangos de fecha para guardar la informacion 


```sql



CREATE TABLE public.bitacora_viaje
(
    id serial,
    id_viaje integer,
    fecha date
) PARTITION BY RANGE (fecha);

ALTER TABLE IF EXISTS public.bitacora_viaje
    OWNER to postgres;


```  


ahora creada si queremos hacer una insercion no se puede porque no existe una particion donde guardar

vamos a hacer la consulta de insertar con script insert 

```sql

INSERT INTO public.bitacora_viaje(
	id_viaje, fecha)
	VALUES (1, '2010-01-01');


ERROR:  La llave de particionamiento de la fila que falla contiene (fecha) = (2010-01-01).no se encontró una partición de «bitacora_viaje» para el registro 

ERROR:  no se encontró una partición de «bitacora_viaje» para el registro
SQL state: 23514
Detail: La llave de particionamiento de la fila que falla contiene (fecha) = (2010-01-01).

```


## vamos a crear la particion de la tabla bitacora 


```sql


CREATE TABLE bitacora_viaje_2010_01 PARTITION OF bitacora_viaje
FOR VALUES FROM ('2010-01-01') TO ('2010-01-31');


```

intentamos hacer la insercion 


```sql

INSERT INTO public.bitacora_viaje(
	id_viaje, fecha)
	VALUES (1, '2010-01-10');


INSERT 0 1

Query returned successfully in 36 msec.


```
## consultamos 

```sql

SELECT *FROM bitacora_viaje;


```

vamos a borrar esta tabla particionada bitacora_viaje

