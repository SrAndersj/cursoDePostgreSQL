# Comandos más utilizados en PostgreSQL


```sql
\? 
```
  Con el cual podemos ver la lista de todos los comandos disponibles en consola, comandos que empiezan con backslash ( \ )

```sql
\h
```

con este comando veremos la información de todas las consultas SQL disponibles en consola. Sirve también para buscar ayuda sobre una consulta específica, para buscar información sobre una consulta específica basta con escribir \h seguido del inicio de la consulta de la que se requiera ayuda, así: \h ALTER



# Comandos de navegación y consulta de información

### <span style="color:red">\c</span> Saltar entre bases de datos

### <span style="color:red">\l</span> Listar base de datos disponibles

### <span style="color:red">\dt</span> Listar las tablas de la base de datos

### <span style="color:red">\d &lt;nombre_tabla&gt;</span> Describir una tabla

### <span style="color:red">\dn</span> Listar los esquemas de la base de datos actual

### <span style="color:red">\df</span> Listar las funciones disponibles de la base de datos actual

### <span style="color:red">\dv</span> Listar las vistas de la base de datos actual

### <span style="color:red">\du</span> Listar los usuarios y sus roles de la base de datos actual


.....

# Comandos de inspección y ejecución

### <span style="color:red">\g</span> Volver a ejecutar el comando ejecutando justo antes

### <span style="color:red">\s</span> Ver el historial de comandos ejecutados

### <span style="color:red">\s &lt;nombre_archivo&gt;</span> Si se quiere guardar la lista de comandos ejecutados en un archivo de texto plano

### <span style="color:red">\i &lt;nombre_archivo&gt;</span> Ejecutar los comandos desde un archivo

### <span style="color:red">\e</span> Permite abrir un editor de texto plano, escribir comandos y ejecutar en lote. \e abre el editor de texto, escribir allí todos los comandos, luego guardar los cambios y cerrar, al cerrar se ejecutarán todos los comandos guardados.

### <span style="color:red">\ef</span> Equivalente al comando anterior pero permite editar también funciones en PostgreSQL

# Comandos para debug y optimización

### <span style="color:red">\timing</span> Activar / Desactivar el contador de tiempo por consulta

# Comandos para cerrar la consola

### <span style="color:red">\q</span> Cerrar la consola




# Ejecutando consultas en la base de datos usando la consola

De manera predeterminada PostgreSQL no crea bases de datos para usar, debemos crear nuestra base de datos para empezar a trabajar, verás que existe ya una base de datos llamada postgres pero no debe ser usada ya que hace parte del CORE de PostgreSQL y sirve para gestionar las demás bases de datos.

Para crear una base de datos debes ejecutar la consulta de creación de base de datos, es importante entender que existe una costumbre no oficial al momento de escribir consultas; consiste en poner en mayúsculas todas las palabras propias del lenguaje SQL cómo CREATE, SELECT, ALTE, etc y el resto de palabras como los nombres de las tablas, columnas, nombres de usuarios, etc en minúscula. No está claro el porqué de esta especie de “estándar” al escribir consultas SQL pero todo apunta a que en el momento que SQL nace, no existían editores de consultas que resaltaran las palabras propias del lenguaje para diferenciar fácilmente de las palabras que no son parte del lenguaje, por eso el uso de mayúsculas y minúsculas.

Las palabras reservadas de consultas SQL usualmente se escriben en mayúscula, ésto para distinguir entre nombres de objetos y lenguaje SQL propio, no es obligatorio, pero podría serte útil en la creación de Scripts SQL largos.

Vamos ahora por un ligero ejemplo desde la creación de una base de datos, la creación de una tabla, la inserción, borrado, consulta y alteración de datos de la tabla.

Primero crea la base de datos, “CREATE DATABASE transporte;” sería el primer paso



```sql

postgres=# CREATE DATABASE transporte;
CREATE DATABASE
postgres=#

```

Ahora saltar de la base de datos postgres que ha sido seleccionada de manera predeterminada a la base de datos transporte recién creada utilizando el comando \c transporte.



```sql
postgres=# \c transporte
Ahora está conectado a la base de datos «transporte» con el usuario «postgres».
transporte=#

```


Ahora vamos a crear la tabla tren, el SQL correspondiente sería:


```sql


transporte=# CREATE TABLE tren ( id serial NOT NULL, modelo character varying, capacidad integer, CONSTRAINT tren_pkey PRIMARY KEY (id) );
CREATE TABLE

```


La columna id será un número autoincremental (cada vez que se inserta un registro se aumenta en uno), modelo se refiere a una referencia al tren, capacidad sería la cantidad de pasajeros que puede transportar y al final agregamos la llave primaria que será id.


Ahora que la tabla ha sido creada, podemos ver su definición utilizando el comando \d tren



```sql 


\d tren
                                    Tabla ½public.tren╗
  Columna  |       Tipo        | Ordenamiento | Nulable  |           Por omisi¾n
-----------+-------------------+--------------+----------+----------------------------------
 id        | integer           |              | not null | nextval('tren_id_seq'::regclass)
 modelo    | character varying |              |          |
 capacidad | integer           |              |          |
═ndices:
    "tren_pkey" PRIMARY KEY, btree (id)


```


PostgreSQL ha creado el campo id automáticamente cómo integer con una asociación predeterminada a una secuencia llamada ‘tren_id_seq’. De manera que cada vez que se inserte un valor, id tomará el siguiente valor de la secuencia, vamos a ver la definición de la secuencia. Para ello, \d tren_id_seq es suficiente:


```sql
transporte=# \d tren_id_seq
                    Secuencia ½public.tren_id_seq╗
  Tipo   | Inicio | MÝnimo |   Mßximo   | Incremento | ┐Cicla? | Cache
---------+--------+--------+------------+------------+---------+-------
 integer |      1 |      1 | 2147483647 |          1 | no      |     1
```


Vemos que la secuencia inicia en uno, así que nuestra primera inserción de datos dejará a la columna id con valor uno.

INSERT INTO tren( modelo, capacidad ) VALUES (‘Volvo 1’, 100);

```sql

transporte=# INSERT INTO tren( modelo, capacidad ) VALUES (‘Volvo 1’, 100);
INSERT 0 1

```

Consultamos ahora los datos en la tabla:

SELECT * FROM tren;


```sql 

transporte=#  SELECT * FROM tren;
 id | modelo  | capacidad
----+---------+-----------
  1 | Volvo 1 |       100
(1 fila)

```

Vamos a modificar el valor, establecer el tren con id uno que sea modelo Honda 0726. Para ello ejecutamos la consulta tipo UPDATE tren SET modelo = 'Honda 0726' Where id = 1;


```sql



UPDATE tren SET modelo = 'Honda 0726' Where id = 1;

```


Verificamos la modificación SELECT * FROM tren;



```sql

transporte=# SELECT * FROM tren;
 id |   modelo   | capacidad
----+------------+-----------
  1 | Honda 0726 |       100
(1 fila)


```


Ahora borramos la fila: DELETE FROM tren WHERE id = 1;


```
transporte=# DELETE FROM tren WHERE id = 1;
DELETE 1

```

Verificamos el borrado SELECT * FROM tren;


```sql

transporte=# SELECT * FROM tren;
 id | modelo | capacidad
----+--------+-----------
(0 filas)

```


El borrado ha funcionado tenemos 0 rows, es decir, no hay filas. Ahora activemos la herramienta que nos permite medir el tiempo que tarda una consulta \timing


```sql
transporte=# \timing
El despliegue de duración está activado.
transporte=#

```


Probemos cómo funciona al medición realizando la encriptación de un texto cualquiera usando el algoritmo md5:


```sql

transporte=# SELECT MD5('vamos a encriptar un texto como el que lees');
               md5
----------------------------------
 f688a864a75734c953faf35588a8e942
(1 fila)


Duración: 1,169 ms

```

