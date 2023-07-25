# Cruzar tablas: SQL JOIN

supongamos que queremos saber que pasajeros han tomado
almenos un viaje 


```sql

SELECT *FROM pasajero

JOIN viaje ON (viaje.id_pasajero =pasajero.id );

```

Consultar pasajeros que no han hecho ningun viaje 


```sql

SELECT *FROM pasajero


LEFT JOIN viaje ON(viaje.id_pasajero =pasajero.id)
WHERE viaje.id IS NULL;


```