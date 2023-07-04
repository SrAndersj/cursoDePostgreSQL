# Creación de Tablas

Basandonos en la estructura Diagrama:

[Diagrama en OneNote](https://udlaedu-my.sharepoint.com/:o:/g/personal/jho_castano_udla_edu_co/EhSghH-c5QNDp3tqirH82kYBXWhthm6-zOFinONDGSHuxA?e=xLf9x9)




hay que crear 

## ESTACION

```sql

CREATE TABLE public.estacion
(
    id serial,
    nombre character varying,
    direccion character varying,
    PRIMARY KEY (id)
);

ALTER TABLE IF EXISTS public.estacion
    OWNER to postgres;

```


## TREN


```sql
CREATE TABLE public.tren
(
    id serial,
    modelo character varying[],
    capacidad integer,
    PRIMARY KEY (id)
);

ALTER TABLE IF EXISTS public.tren
    OWNER to postgres;

```


## TRAYECTO

no estoy seguro como es el asunto de las llaves foraneas id_...


```sql
CREATE TABLE public.trayecto
(
    id_estacion serial,
    id_tren serial,
    nombre character varying
);

ALTER TABLE IF EXISTS public.trayecto
    OWNER to postgres;
```



## VIAJE


```sql 

CREATE TABLE public.viaje
(
    id serial,
    id_pasajero serial,
    id_trayecto serial,
    inicio time with time zone,
    fin time with time zone,
    PRIMARY KEY (id_pasajero)
);

ALTER TABLE IF EXISTS public.viaje
    OWNER to postgres;

```
