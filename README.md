# Otras Extensiones para Postgres

https://www.postgresql.org/docs/11/contrib.html 


abrimos editor y hacemos la consulta que nos permite comparar dos palabras pronunciacion 

```sql

CREATE EXTENSION fuzzystrmatch;

SELECT levenshtein('oswaldo','osvaldo')

1

```
el numero que sale es la cantidad de letras que hay que cambiar para que las palabras sean iguales 



# vamos a usar difference, nos dice de cero a 4 que tan diferentes son 


```sql
SELECT difference('oswaldo','osvaldo');

2


SELECT difference('beard','bird');

4
```

si es 4 es que la pronunciacion es practicamente lo mismo 

