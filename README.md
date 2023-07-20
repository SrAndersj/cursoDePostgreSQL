# Llaves foraneas

##  estructura

Tabla origen

Tabla destino 

Acciones

## pgadmin

nos posicionamos en tabla trayecto damos click derecho

propiedades 

constraints

foreign key 

Name :  TablaOrigen_tablaDestinofkey

trayecto_estacion_fkey


damos editar
columns 

Local column  : id_estacion

References  : public.stacion 

referencing : id 

### vamos a action 

es importante porque dice que tiene que hacer
la base de datos cuando ocurra un cambio

## On update 

si se actualiza el id de la estacion ....

cascade . dice que si el id tabla principal se actualiza 

## On delate 

si se borra en la principal  el id  aqui le decimos si puede o no borrarlo aca 

Cascade 


para hacer el otro constraint 


```sql


ALTER TABLE IF EXISTS public.trayecto
    ADD CONSTRAINT trayecto_tren_fkey FOREIGN KEY (id_tren)
    REFERENCES public.tren (id) MATCH SIMPLE
    ON UPDATE NO ACTION
    ON DELETE NO ACTION
    NOT VALID;

```


```sql

ALTER TABLE IF EXISTS public.viaje
    ADD CONSTRAINT viaje_trayecto_fkey FOREIGN KEY (id_trayecto)
    REFERENCES public.trayecto (id) MATCH SIMPLE
    ON UPDATE CASCADE
    ON DELETE CASCADE
    NOT VALID;


ALTER TABLE IF EXISTS public.viaje
    ADD CONSTRAINT viaje_pasajero_fkey FOREIGN KEY (id_pasajero)
    REFERENCES public.pasajero (id) MATCH SIMPLE
    ON UPDATE CASCADE
    ON DELETE CASCADE
    NOT VALID;

```