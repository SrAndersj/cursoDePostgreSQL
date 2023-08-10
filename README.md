# Mantenimiento

postgres hace mantenimiento o limpieza 

hace dos niveles de limpieza 

quita todas las filas columnas etc que no se usan 

el modo liviano esta todo el tiempo

full es capas de bloquear las tablas para hacer la limpieza 

## vamos a hacer y revisar el mantenimiento en pgadmin 


click derecho opcion maintenance
4 opciones
## vacuum
se refiere a vaciar

full significa que la tabla estara limpia en su totalidad 
freeze durante ese proceso se va a congelar la tabla o base de datos

analyze es la mas suave , ejecuta una revision pero no hace cambios 

## ANALYZE

no hace ningun cambio , solo hace la revicion 

## REINDEX 

aplica para tablas que tienen indices como llaves primarias

es importante cuando hay indices que son mas grandes que las tablas 

## cluster 
es decirle al motor que reorganice  el disco duro 