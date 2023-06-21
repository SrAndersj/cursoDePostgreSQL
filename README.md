# Windows
## listar
```
\l
```

## acceder a una base de datos 

```
\c transporte_masivo
```


##cear tabla con query

```
CREATE TABLE usuarios (
    id serial PRIMARY KEY,
    nombre text
);

```

## ver las tablas dentro de esta 
```
\dt
```

## ver todas las funciones que pdemos ejecutar
```
\h
```

## consultar una de las funciones del listado
```
\h ALTER
# salir contrl c
```


## consultar version postgres
```
SELECT version();
```

## volver a ejecutar el ultimo comando , si otro usuario uso funcion desde otra parte sirve para ver lo que ejecuto
```
\g
```

## que nos diga en cuanto tiempo demora en ejecuta

```
\timing
``

