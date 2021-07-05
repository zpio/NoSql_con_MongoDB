# 🦄 Apuntes de NoSql con MongoDB 

## Tabla de Contenido
- [1. Introducción a NoSql con MongoDB](#introduction_nosql_mongodb)
- [2. Documentos y tipos de datos](#documentos_tipos_datos)
- [3. Creando una base datos en MongoDB](#creando_bd_mongodb)
- [4. Consulta de documentos (Querying Documents)](#querying_documents)
- [5. Insertar, actualizar y eliminar documentos](#insertar_actualizar_eliminar)
- [6. Insertar, actualizar y eliminar campos Array](#actualizar_campos_array)
- [7. Data Aggregation](#data_aggregation)
- [8. Joins entre colecciones](#joins_colecciones)
- [9. Bibliografía](#bibliografia)

## 🐥 1. Introducción a NoSql con MongoDB <a name="introduction_nosql_mongodb"></a>

Hay dos tipos de bases de datos: bases de datos relacionales y no relacionales. 

Las bases datos **no relacionales** a menudo se denominan bases de datos **NoSQL**. 

Una base de datos NoSQL se utiliza para almacenar grandes cantidades de datos complejos y diversos, como catálogos de productos, registros, interacciones de usuarios, análisis y más. 

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/Sql%20y%20NoSql.jpg)

### 🔥 MongoDB

MongoDB es una popular base de datos **NoSQL** que puede almacenar datos estructurados y no estructurados. Fundada en 2007 por Kevin P. Ryan, Dwight Merriman y Eliot Horowitz en Nueva York, la organización se llamó inicialmente 10gen y luego se renombró como MongoDB, una palabra inspirada en el término **humongous**.

Su diseño basado en **documentos** y su sintaxis intuitiva para consultas y comandos hace que sea fácil de aprender.

### 🔥 Descarga e instalación de MongoDB

**👉Paso 1: Descargar e instalar la versión Community Server**

Ir al página oficial de MongoDB https://www.mongodb.com/try/download/community

El siguiente video de youtube indica paso a paso como descargar e instalar: [Link](https://www.youtube.com/watch?v=Y3RUzKNiiIA)

**👉Paso 2. Encender el servidor MongoDB**

Una opción fácil para encender el servidor es ir a la carpeta del ordenador donde se instaló Mongo y abrir el archivo **mongod**. 

Dentro de la carpeta **bin** se encuentra los archivos ejecutables: **mongod** y **mongo**
```
C:\Program Files\MongoDB\Server\4.4\bin
```
Antes de abrir el archivo **mongod** hay que hacer un paso previo: Crear en el **disco C** una carpeta llamada **data** y dentro de esta otra capeta llamada **db**.
```
C:\data\db
```
Ahora si, al abrir el archivo **mongod** y saldrá la clásica pantalla negra.

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/consola%20mongo.PNG)

En esta pantalla mostrará que el servidor esta encendido y está esperando que alguien se conecte. (No debes cerrar esta pantalla)

**👉Paso 3. Abrir la consola y conectarse al servidor**

Ahora se deberá abrir el otro ejecutable: **mongo**. Este ejecutable es una **consola o terminal**.

Escribimos en la consola **2+2** para probar que funciona.

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/consola%20mongod.png)

Además de la consola clásica hay aplicaciones de entorno visual para comodidad del usuario como **MongoDB Compass**.

**👉MongoDB Compass**

MongoDB Compass es un entorno visual e intuitivo para interactuar con el servidor. Generalmente se instala junto cuando se instala MongoDB.

Para usar MongoDB Compass se debe abrir el programa y conectase al servidor de mongo. Para esto hay que copiar el string que apareció previamente en la consola: 
```
mongodb://127.0.0.1:27017 
```
Luego clic en Connect y listo. Ahora podrás crear su propia base de datos o subir un archivo de base de datos.

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/mongo%20compass.PNG)

En la seccion 3 se verá como crear una base de datos mediante la consola y con la interfaz MongoDB Compass.


## 🐥 2. Documentos y tipos de datos <a name="documentos_tipos_datos"></a>

Una de las características de **MongoDB** es su modelo de datos basado en **documentos**, que son aceptados como una forma flexible de transportar información. 

Muchas aplicaciones que intercambian datos en forma de documentos **JavaScript Object Notation (JSON)**. MongoDB almacena datos en formato **JSON binario (BSON)** y los representa en JSON legible por humanos.

### 😻 Sintaxis JSON

Los documentos u objetos **JSON** son un conjunto de texto sin formato de pares **clave-valor**. 

JSON tiene una estructura de un conjunto de llaves `{ }`, corchetes `[ ]`, dos puntos `:` y comas `,`. 

**Clave : Valor**

En un objeto JSON, los pares **clave-valor** están encerrados con llaves `{ }`. La **clave** es siempre una cadena de texto y el **valor** puede ser cualquier **tipo** especificado por JSON.

```javascript
{ key : value }
```
**Array**

Un **array** es un conjunto de valores encerrados entre corchetes `[ ]` y separados por comas `,`.

```javascript
[ value1, value2, value3 ]
```
Ejemplo de un documento JSON que contiene la información básica de una empresa:

```javascript
{
  "company_name" : "Sparter",
  "founded_year" : 2007,
  "twitter_username" : null,
  "address" : "15 East Street",
  "no_of_employees" : 7890,
  "revenue" : 879423000
}
```

### 😻 Tipos de datos JSON

- **👉 String**
- **👉 Number**
- **👉 Boolean**
- **👉 Object**
- **👉 Array**
- **👉 Null**

JSON es un formato de intercambio de datos. La presencia de tipos de datos básicos proporcionados por JSON reduce la complejidad durante este proceso. Por eso se mantiene simple y mínimo en términos de tipos de datos.

### 😻 JSON y números

En los documentos JSON, un número es solo una secuencia de dígitos. No distingue entre números como enteros o flotantes. 

### 😻 JSON y fechas

En los documentos JSON no admite un tipo de datos Fecha y estas solo se representan como cadenas simples. Ejemplos:

```javascript
{
  "title": "A Swedish Love Story", 
  "released": "1970-04-24"
}
```
Las partes que intercambian la información deben estandarizar el formato fecha durante las transferencias. La forma de leer los datos depende de los intérpretes de los lenguajes y de sus contratos de intercambio de datos.

### 💪 Ejercicio: Creación de un documento JSON

Abra un validador JSON, por ejemplo: [https://jsonlint.com/](https://jsonlint.com/).

Escriba la información anterior en formato JSON:

```javascript
{
  "id" : 14253,
  "title" : "Beauty and the Beast",
  "year" : 2016,
  "language" : "English",
  "imdb_rating" : 6.4,
  "genre" : "Romance",
  "director" : "Christophe Gans",
  "runtime" : 112
}
``` 
Recuerde, un documento JSON siempre comienza con `{` y termina con `}`. Cada elemento está separado por dos puntos `:` y los pares `clave:valor` están separados por una coma.

Haga clic en **Validar JSON** para validar el código.

### 😻 Documentos de MongoDB

Una base de datos MongoDB se compone de **colecciones** y **documentos**. Una base de datos puede tener una o más colecciones, y cada colección puede almacenar uno o más documentos relacionados.

En comparación con RDBMS, las **colecciones** son análogas a las **tablas** y los **documentos** son análogos a las **filas** dentro de una tabla. Sin embargo, los documentos son mucho más flexibles en comparación con las filas de una tabla.

### 😻 Tipos de datos de MongoDB

MongoDB almacena documentos similares a JSON.

**👉Strings**: en MongoDB, los campos de cadena están codificados en UTF-8. Ademas, admiten capacidades de búsqueda con expresiones regulares.

```javascript
{ "name" : "Tom Walter" }
```

**👉Numbers**: En MongoDB se admite los varios tipos de números.

- **double**: punto flotante de 64 bits
- **int**: entero de 32 bits con signo
- **long**: entero sin signo de 64 bits
- **decimal**: punto flotante de 128 bits, que cumple con IEE 754

```javascript
{ "edad" : 25 }
```

**👉Booleans**: se utiliza para representar si algo es verdadero o falso.

```javascript
{ "isMongoDBHard": false }
```

**👉Objects**: Se utilizan para representar documentos **ANIDADOS** o **INCRUSTADOS,** es decir, un campo cuyo valor es otro documento JSON válido. 

El siguiente documento tiene otro documento anidado llamado **"host"**

```javascript
{
  "listing_url": "https://www.airbnb.com/rooms/1001265",
  "name": "Ocean View Waikiki Marina w/prkg",
  "summary": "A great location that work perfectly for business.",
  "host":{
    "host_id": "5448114",
    "host_name": "David",
    "host_location": "Honolulu, Hawaii, United States"
  }
}
```
El valor del campo de host es otro documento de JSON. MongoDB usa una notación de puntos `.` para acceder a los objetos anidados. 

Para acceder a un documento anidado, podemos crear una variable y a partir de ahi usar la notacion de punto para acceder al documento anidado. 

Ejemplo: Acceder la informacion del **host_name** del documento **listing**.

**"host_name"** es un campo que está dentro del documento **"host"** que a su vez es un documento anidado del documento principal **listing** almacenado en una variable.

```javascript
var listing = { 
  "listing_url": "https://www.airbnb.com/rooms/1001265",
  "name": "Ocean View Waikiki Marina w/prkg",
  "summary": "A great location that work perfectly for business.",
  "host": {
    "host_id": "5448114",
    "host_name": "David",
    "host_location": "Honolulu, Hawaii, United States"
  }
}
```
Usamos la notacion punto de la siguente manera:
```javascript
listing.host.host_name
```
`David`

**👉Array**: es una colección de cero o más valores que deben estar encerrado con corchetes `\[ ]`. En MongoDB, no hay límite para la cantidad de elementos que puede contener un array o la cantidad de arrays que puede tener un documento. Sin embargo, el tamaño total del documento no debe exceder los 16 MB.

Considere la siguiente array que contiene cuatro números:

```javascript
var doc = { first_array: [ 4, 3, 2, 1 ] }
```
Se puede acceder a cada elemento de un array utilizando su posición de **índice**. El número de índice se incluye entre corchetes. (Los índices empiezan desde 0). 

Accedamos al tercer elemento del array:
```javascript
doc.first_array[3]
```
` 1 `

Usando la posición del índice, también puede agregar nuevos elementos al array existente:

```javascript
doc.first_array[4] = 99
```
Al imprimir el array, verá el elemento que se ha agregado correctamente, en el índice 4:

```javascript
doc.first_array
```
`[4, 3, 2, 1, 99]`

Los arrays también pueden tener arrays anidados. La siguiente sintaxis agrega un array incrustado en el sexto elemento:

```javascript
doc.first_array[5] = [11, 12]
```
Si imprime el array, verá la array incrustada de la siguiente manera:

```javascript
doc.first_array
```
`[4, 3, 2, 1, 99, [11, 12]]`

Ahora, puede usar la notación de corchetes, `\[ ]` , para acceder a los elementos de un índice específico. Ejemplo: acceder al primer elemento del quinto elemento del array anidado.
```javascript
doc.first_array[5][1]
```
`12`

Un array puede contener cualquier campo de tipo de datos válido de MongoDB. Esto se puede ver en el siguiente ejemplo:

```javascript
[ "this", "is", "a", "text" ] // array of strings

[ 1.1, 3.2, 553.54 ] // array of doubles

[ { "a" : 1 }, { "a" : 2, "b" : 3 }, { "c" : 1 } ] // array of Json objects

[ 12, "text", 4.35, [ 3, 2 ], { "type" : "object" } ] // array of mixed elements
```

**👉Null**: Nulo es un tipo de datos especial en un documento y denota un campo que no contiene un valor. El campo nulo solo puede tener nulo como valor. 

```javascript
var obj = null
obj
```
`Null`

```javascript
var nullField = null
doc.first_array[6] = nullField
doc.first_array
```
`[ 4, 3, 2, 1, 99, [11, 12], null]`

**👉ObjectId**: Cada documento de una colección debe tener un **\_id** que contenga un valor único. Este campo actúa como clave principal para estos documentos. Las claves primarias se utilizan para identificar de forma única los documentos y siempre están indexadas. El valor del campo **\_id** debe ser único en una colección.

Si inserta un documento sin un campo **\_id**, el controlador MongoDB generará automáticamente una ID única y la agregará al documento. Cuando el controlador agrega automáticamente el campo **\_id**, el valor se genera mediante **ObjectId**.

El valor **ObjectId** está diseñado para generar código ligero que es único en diferentes máquinas. Genera un valor único de 12 bytes, donde los primeros 4 bytes representan la marca de tiempo, los bytes 5 a 9 representan un valor aleatorio y los últimos 3 bytes son un contador incremental.

```javascript
var uniqueID = new ObjectId ()
uniqueID
```
`ObjectId("5dv.8ff48dd98e621357bd50")`

**👉Fechas**: MongoDB si admite tipos de fecha explícitamente. Puesto que en JSON no admiten tipos de fecha porque se representan como cadenas sin formato.

Las fechas de MongoDB se almacenan en forma de milisegundos desde el 1 de enero de 1970. Para almacenar la representación de milisegundos de una fecha, MongoDB usa un entero de 64 bits ( long ). Todas las fechas se almacenan en UTC y no hay una zona horaria asociada a ellas.

Puede crear instancias de fecha usando **Date () , new Date () o new ISODate ()**

Las fechas creadas con un **new Date () o new ISODate ()** siempre estarán en UTC, y las creadas con **Date ()** estarán en la zona horaria local. 

**Date()** usa la representación de fecha de JavaScript, que está en forma de cadenas simples. No son útiles para la comparación o manipulación.

```javascript
var date = Date()
```
`Sat Sept 03 1989 07:28:46 GMT-0500 (CDT)`

Con new Date(), obtiene la fecha envuelta en ISODate (). Estas fechas se pueden manipular, comparar y buscar.

```javascript
var date = new Date()
```
`ISODate("1989-09-03T10:11:23.357Z")`

También puede usar el new ISODate () directamente para crear objetos de fecha. Estas fechas se pueden manipular, comparar y buscar.

```javascript
var isoDate = new ISODate()
```
`ISODate("1989-09-03T11:13:26.442Z")`

**Timestamps**: Timestamps es una representación de 64 bits de la fecha y la hora. De los 64 bits, los primeros 32 bits almacenan el número de segundos desde la época de Unix, que es el 1 de enero de 1970. Los otros 32 bits indican un contador en aumento. MongoDB utiliza exclusivamente el Timestamps para operaciones internas.

### 💪 Practica 1: Modelar un tweet en un documento JSON

Tweet: (https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/twitter_practica1.jpg)

Abra un validador JSON para verificar que tiene el formato correcto: [https://jsonlint.com/](https://jsonlint.com/).

**Solución**:

```javascript
{
    "id": 1,
    "created_at": "Sun Apr 17 16:29:24 +0000 2011",
    "user": {
        "id": "Lord_Of_Winterfell",
	"name": "Office of Ned Stark",
	"profile_pic": "https://user.profile.pic",
	"isVerified": true
    },
    "text": "Tweeps in the #north. The long nights are upon us. Do stock enough warm clothes, meat and mead…",
    "hashtags": [
        "north",
	"WinterfellCares",
	"flueshots"
    ],
    "mentions": [
	"MaesterLuwin",
	"TheNedStark",
	"CatelynTheCat"
    ],
    "likes_count": 14925,
    "retweet_count": 12165,
    "comments_count": 0
}
```

## 🐥 3. Creando una base datos en MongoDB <a name="creando_bd_mongodb"></a>

### ⚡ Conociendo comandos básicos

Abier la consola de mongo y comenzar a escribir los siguientes comandos:

- El comando **`cls`** limpia la consola.
```
cls
```
![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/cls_limpiar_consola.PNG)

- El comando **`show dbs`** muestra todas las bases datos almacenadas en MongoDB.
```
show dbs
```
![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/show_dbs.PNG)

- El comando **`bd`** muestra en que base datos estamos actualmente. Al incio indicará que estamos en **test**.
```
db
```
![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/db.PNG)

- El comando **`use`** es para movernos a la base datos que vamos a trabajar.
```
use Sample1
```
![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/use%20db.PNG)

- Si ejecuta nuevamente el comando **`db`** mostrará que ahora ya estamos en la base datos **Sample1**.

- El comando **`show collections`** muestra las **COLECCIONES** (TABLAS) de la base datos **Sample1**. En este caso tenemos 2 colecciones: comments y movies.
```
show collections
```
![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/show%20collections.PNG)

### ⚡ Creando una base datos sencilla

- Para crear una base datos tambien se utiliza el comando **`use`** junto al nombre de la nueva base datos.
```
use mibase
```
- Si ejecuta el comando **`show dbs`** aún no aparecerá en el listado debido que se debe crear una colección (tabla).

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/show_dbs.PNG)

- El comando **`db.createCollection()`** crea un colección en la base datos que estemos. Hay que proporcionar un nombre a la collección.
```javascript
db.createCollection('miColeccion')
```
- Si ejecuta nuevamente el comando **`show dbs`** ahora si aparecerá en el listado.

- El comando **`db.miColeccion.drop()`** borra una coleccion de la base datos.
```javascript
db.miColeccion.drop()
```
- El comando **`db.dropDatabase()`** borra la base datos que estemos usando.
```javascript
db.dropDatabase()
```

### ⚡ Subir una coleccion (documento JSON) a la base datos

**👉 Pimero**: descargar las colecciones (archivo JSON) **movies.json** y **comments.json** para subirla a la base datos **Sample** que deberás crear.

- **movies**: [link de descarga](https://raw.githubusercontent.com/zpio/mongodb-sample-dataset/main/sample_mflix/movies.json)

- **comments**: [link de descarga](https://raw.githubusercontent.com/zpio/mongodb-sample-dataset/main/sample_mflix/comments.json)

**👉Segundo**: creear una base datos en la consola llamada **Sample**.

Una forma muy intuitiva de subir colecciones a partir de un documento JSON a nuestra base datos es con el programa **Mongo Compass**.

**👉Tercero**: abrir Mongo Compass y conectarse al servidor de Mongo. Una vez ahi, deberas crear las colecciones en la base datos **Sample** y subir los archivos JSON respectivamente.

Listo, ya tienes una base datos con 2 colecciones para comenzar a hacer las respectivas consultas, filtros, actualización, etc.


## 🐥 4. Consulta de documentos (Querying Documents) <a name="querying_documents"></a>

### 🧡 Estructura de consulta MongoDB

Las consultas de MongoDB se basan en documentos JSON. El siguiente diagrama es un ejemplo de una consulta simple de MongoDB que encuentra todos los documentos donde el campo de **name** contiene el valor **David**:

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/formato%20find.jpg)

En sintaxis SQL seria:

`SELECT * FROM USERS WHERE name = 'David';`

MongoDB no tienen palabras clave como **SELECT**, **FROM** y **WHERE**.

### 🧡 Consultas básicas de MongoDB

Todas las consultas de esta sección son consultas de nivel superior; es decir, se basan en los campos de nivel superior (también conocidos como nivel raíz) de los documentos.

**👉 Mostrar documentos - función find**

- La función **find** mostrará todos los documentos de la colección. 
```javascript
db.comments.find()
```
- Para devolver solo documentos específicos, se puede proporcionar una **condición**.
```javascript
db.comments.find ({"name": "Lauren Carr"})
```
- Con la función **pretty** muesta un resultado bien formateado.
```javascript
db.comments.find({"name" : "Lauren Carr"}).pretty()
```
```javascript
{
  "_id" : ObjectId("5a9427648b0beebeb6962d2d"),
  "name" : "Lauren Carr",
  "email" : "lauren_carr@fakegmail.com",
  "movie_id" : ObjectId("573a139af29313caabcf0d74"),
  "text" : "Sit ullam tenetur atque delectus. Pariatur eos sequi enim...",
  "date" : ISODate("1978-03-25T06:29:47Z")
}
{
  "_id" : ObjectId("5a9427648b0beebeb6962d2e"),
  "name" : "Lauren Carr",
  "email" : "lauren_carr@fakegmail.com",
  "movie_id" : ObjectId("573a139af29313caabcf0d74"),
  "text" : "Temporibus iste error id molestias. Et quia quas voluptate asperiores. Consectetur quisquam rerum est suscipit ullam.",
  "date" : ISODate("1986-10-26T11:31:17Z")
}
.....
.....
```
- La función **findOne** muestra solo un registro coincidente, devolviendo solo el primero:
```javascript
db.comments.findOne ()
```
```javascript
{
  "_id" : ObjectId("5a9427648b0beebeb6962d2d"),
  "name" : "Lauren Carr",
   "email" : "lauren_carr@fakegmail.com",
   "movie_id" : ObjectId("573a139af29313caabcf0d74"),
   "text" : "Sit ullam tenetur atque delectus. Pariatur eos sequi enim. Quasi eligendi labore saepe rerum modi incidunt accusamus ex. Expedita temporibus consequatur dolore modi.",
   "date" : ISODate("1978-03-25T06:29:47Z")
}
```
Las siguientes consultas tienen el mismo comportamiento. Muestran todos los documentos de la coleccion.
```javascript
db.comments.find ()

db.comments.find ({})
```
**👉 Elegir los campos para la salida con projection**

En las consultas de MongoDB, puede incluir o excluir campos específicos del resultado. Esta técnica se llama **projection**.

La proyección se expresa como un segundo argumento para las funciones **find** o **findOne**. Se puede excluir explícitamente un campo configurándolo en 0 o incluir con 1.
```javascript
db.comments.find(
    {"name" : "Lauren Carr"},
    {"name" : 1, "date": 1}
).pretty()
```
```javascript
{
  "_id" : ObjectId("5a9427648b0beebeb6962d2d"),
  "name" : "Lauren Carr",
  "date" : ISODate("1978-03-25T06:29:47Z")
}
{
  "_id" : ObjectId("5a9427648b0beebeb6962d2e"),
  "name" : "Lauren Carr",
  "date" : ISODate("1986-10-26T11:31:17Z")
}
{
  "_id" : ObjectId("5a9427648b0beebeb6962d2f"),
  "name" : "Lauren Carr",
  "date" : ISODate("1972-03-23T02:37:03Z")
}
```
El campo **\_id** siempre se incluirá, a menos que se excluya explícitamente.
```javascript
db.comments.find(
  {"name" : "Lauren Carr"},
  {"name" : 1, "date": 1, "_id" : 0}
).pretty()
```
```javascript
{ "name" : "Lauren Carr", "date" : ISODate("1978-03-25T06:29:47Z") }
{ "name" : "Lauren Carr", "date" : ISODate("1986-10-26T11:31:17Z") }
{ "name" : "Lauren Carr", "date" : ISODate("1972-03-23T02:37:03Z") }
```
**👉Encontrar los campos distintos - distinct**

Usaremos la colección de **movies**. A cada película se le asigna una calificación de idoneidad de audiencia que se basa en el contenido y la edad de los espectadores. Busquemos las ratings únicas que existen en la colección con **distinct**. **Distinct** siempre se devuelve como un array.
```javascript
db.movies.distinct("rated")
```
```javascript
[
  "AO",
  "APPROVED",
  "Approved",
  "G",
  "GP",
  "M",
  "NC-17",
  "NOT RATED",
  "Not Rated",
  "OPEN",
  "PASSED",
  "PG",
  "PG-13",
  "R",
  "TV-14",
  "TV-G",
  "TV-MA",
  "TV-PG",
  "TV-Y7",
  "UNRATED",
  "X"
]
```
Encuentre todas las ratings únicas que han recibido las películas que se estrenaron en 1994:
```javascript
db.movies.distinct(
  "rated", {"year" : 1994}
)
```
```
[ "G", "NOT RATED", "PG", "PG-13", "R", "TV-14", "TV-PG", "UNRATED" ]
```
**👉Contando los documentos con count**

La función **count** se utiliza para devolver el recuento de documentos dentro de una colección o un recuento de los documentos que coinciden con la consulta dada. Cuando se ejecuta sin ningún argumento de consulta, devuelve el recuento total de documentos en la colección.

```javascript
db.movies.count()
```
` 23539 `

Devolver el recuento de películas que tienen exactamente 6 comentarios:
```javascript
db.movies.count(
  {"num_mflix_comments" : 6}
)
```
` 17 `

En MongoDB v4.0 **countDocuments** devuelve el recuento de documentos que coinciden con la condición dada. Un argumento de consulta es obligatorio.
```javascript
db.movies.countDocuments (
  {"year": 1999}
)
```
` 542 ` 

### 🧡 Operadores condicionales

👉 **Equals ($eq) (Operador de Igualdad)**

Devolver películas cuyo recuento de comentarios sea igual a 5. Ambas consultas tienen el mismo efecto:
```javascript
db.movies.find(
  {"num_mflix_comments" : 5}
)

db.movies.find(
  {"num_mflix_comments": {$eq : 5}}
)
```

👉 **Not Equal To ($ne)**

Devolver películas cuyo recuento de comentarios no sea igual a 5:
```javascript
db.movies.find(
  {"num_mflix_comments" : {$ne : 5} }
)
```

👉 **Greater Than ($gt) and Greater Than or Equal To ($gte)**

Devolver la cantidad de películas cuya fecha sea mayor a 2015:
```javascript
db.movies.find(
    {year : {$gt : 2015}}
).count()
```
`1`

Devolver la cantidad de películas cuya fecha sea mayor igual a 2015:
```javascript
db.movies.find(
    {year : {$gte : 2015}}
).count()
```
`485`

Devolver la cantidad de películas que se estrenaron en el siglo XXI (desde el 1 de enero de 2000):
```javascript
db.movies.find(
    {"released" :
        {$gte: new Date('2000-01-01')}
    }
).count()
```
`13767`

👉 **Less Than ($lt) and Less Than or Equal To ($lte)**

Contar películas que tienen menos de dos comentarios:
```javascript
db.movies.find(
    {"num_mflix_comments" :
        {$lt : 2}
    }
).count()
```
`8514`

Cantidad de películas que tienen un máximo de dos comentarios:
```javascript
db.movies.find(
    {"num_mflix_comments" :
        {$lte : 2}
    }
).count()
```
`13185` 

Contar las películas que se lanzaron en el siglo anterior:
```javascript
db.movies.find(
    {"released" :
        {$lt : new Date('2000-01-01')}
    }
).count()
```
`9268`

👉 **In ($in) and Not In ($nin)**

Encontrar todas las películas que han sido clasificadas como G, PG o PG-13:
```javascript
db.movies.find(
  {"rated" :
    {$in : ["G", "PG", "PG-13"]}
  }
)
```
Todas las películas que no han sido clasificadas como G, PG o PG-13:
```javascript
db.movies.find(
  {"rated" :
    {$nin : ["G", "PG", "PG-13"]}
  }
)
```
La consulta anterior devuelve películas que no están clasificadas como G , PG o PG-13, incluidas las que no tienen el campo rated.

Para ver qué sucede cuando usa **$nin** con un campo inexistente, primero, busque el total de documentos que tiene:
```javascript
db.movies.countDocuments ({})
23539
```
Ahora, use **$nin** con algunos valores, excepto null, en un campo inexistente:
```javascript
db.movies.countDocuments(
  {"nef" :
    {$nin : ["a value", "another value"]}
  }
)
```
`23539`
Esto significa que todos los documentos coinciden.

Ahora, agregue un valor **null** a la matriz `$nin`:
```javascript
db.movies.countDocuments(
  {"nef" :
     {$nin: ["a value", "another value", null ]}
  }
)
```
`0`

Esta vez, no coincidió con ningún documento. Esto se debe a que, en MongoDB, un campo inexistente siempre tiene un valor de nulo, por lo que la condición `$nin` no se cumplió para ninguno de los documentos.

💪 **Ejercicio: Consulta de películas de un actor**

Encuentre el numero de películas en las que aparece `Leonardo DiCaprio` usando el campo de cast.
```javascript
db.movies.countDocuments(
  {"cast": "Leonardo DiCaprio"}
)
```
`25`

Encuentre los géneros de estas películas, devuelva un array.
```javascript
db.movies.distinct(
  "genres", {"cast" : "Leonardo DiCaprio"}
)
```
```javascript
[
  "Action",
  "Adventure",
  "Biography",
  "Comedy",
  "Crime",
  "Documentary",
  "Drama",
  "History",
  "Mystery",
  "Romance",
  "Sci-Fi",
  "Short",
  "Thriller",
  "Western"
]
```
Encuentre sus Títulos de películas y sus respectivos años de estreno.
```javascript
db.movies.find(
    {"cast" : "Leonardo DiCaprio"},
    {"title":1, "year":1, "_id":0}
)
```
```javascript
{ "year" : 1993, "title" : "This Boy's Life" }
{ "title" : "What's Eating Gilbert Grape", "year" : 1993 }
{ "title" : "The Quick and the Dead", "year" : 1995 }
{ "title" : "Total Eclipse", "year" : 1995 }
{ "title" : "Marvin's Room", "year" : 1996 }
{ "year" : 1996, "title" : "Romeo + Juliet" }
{ "year" : 1997, "title" : "Titanic" }
{ "year" : 1998, "title" : "The Man in the Iron Mask" }
{ "year" : 2000, "title" : "The Beach" }
{ "title" : "Gangs of New York", "year" : 2002 }
{ "year" : 2002, "title" : "Catch Me If You Can" }
{ "title" : "The Aviator", "year" : 2004 }
{ "year" : 2006, "title" : "The Departed" }
{ "title" : "Blood Diamond", "year" : 2006 }
{ "year" : 2007, "title" : "The 11th Hour" }
{ "year" : 2008, "title" : "Body of Lies" }
{ "year" : 2008, "title" : "Revolutionary Road" }
{ "year" : 2013, "title" : "The Wolf of Wall Street" }
{ "year" : 2008, "title" : "Body of Lies" }
{ "year" : 2010, "title" : "Shutter Island" }
Type "it" for more
```
Encuentre la cantidad de películas que ha dirigido.
```javascript
db.movies.countDocuments({"directors" : "Leonardo DiCaprio"})
```
`0`

### 🧡 Operadores logicos

👉 **$and Operator**

Con el operador **$and**, puede tener cualquier número de condiciones envueltas en un array y el operador devolverá solo los documentos que satisfacen todas las condiciones. Cuando un documento falla en una verificación de condición, se omiten las siguientes condiciones. Es por eso que al operador se le llama operador de cortocircuito. 

Películas sin clasificación que se lanzaron en 2008:
```javascript
db.movies.countDocuments(
  {$and :
    [{"rated" : "UNRATED"}, {"year" : 2008}]
  }
)
```
`37`

En las consultas de MongoDB, el operador **$and** está implícito y se incluye de forma predeterminada si un documento de consulta tiene más de una condición. 
```javascript
db.movies.countDocuments (
  {"rated": "UNRATED", "year" : 2008}
)
```
`37`

👉 **$or Operator**

En el ejemplo que usamos en la sección de In ($ in) y Not In ($ nin), escribió una consulta para contar las películas clasificadas como G, PG o PG-13. Con el operador $or, reescriba la misma consulta:
```javascript
db.movies.find(
  {$or : [
     {"rated" : "G"},
     {"rated" : "PG"},
     {"rated" : "PG-13"}
  ]}
)
```
El operador **$in** se usa para determinar si un campo dado tiene al menos uno de los valores proporcionados en una matriz, mientras que el operador **$or** no está vinculado a ningún campo específico y acepta múltiples expresiones de diferentes campos.

```javascript
db.movies.find(
  {$or:[
    {"rated" : "G"},
    {"year" : 2005},
    {"num_mflix_comments" : {$gte : 5}}
  ]}
)
```

👉 **$not Operator**

El operador **$not** representa la operación lógica NOT que niega la condición dada. 

Ejemplo: Devuelva todas las películas que no tienen 5 o más comentarios:
```javascript
db.movies.find(
  {"num_mflix_comments" :
    {$not: {$gte : 5}}
  }
)
```

💪 **Ejercicio: Combinación de varias consultas**

Encontrar los títulos y años de estreno de películas de drama o crimen en cuya producción han colaborado Leonardo DiCaprio y Martin Scorsese.
```javascript
db.movies.find(
    {
      "cast": "Leonardo DiCaprio",
      "directors" : "Martin Scorsese",
      "$or" : [{"genres" : "Drama"}, {"genres": "Crime"}]
    },
    {
      "title" : 1, "year" : 1, "_id" : 0
    }
)
```
```javascript
{ "title" : "Gangs of New York", "year" : 2002 }
{ "title" : "The Aviator", "year" : 2004 }
{ "year" : 2006, "title" : "The Departed" }
{ "year" : 2013, "title" : "The Wolf of Wall Street" }
```

### 🧡 Expresiones regulares

👉 **Usando $regex**

En las consultas de MongoDB, las expresiones regulares se pueden usar con el operador **$regex**.

Ejemplo: Encontrar todas las películas cuyos títulos contienen la palabra **Opera** en cualquier posicion:
```javascript
db.movies.find(
    {"title" : {$regex :"Opera"}},
    {"title" : 1}
)
```

👉 **Usando El Operador caret (^)**

Para buscar solo las cadenas que comienzan con la expresión regular dada se utiliza el operador ( ^ ).

Ejemplo: Buscar solo aquellas películas cuyos títulos comienzan con la palabra Opera:
```javascript
db.movies.find (
    {"title": {$ regex: "^Opera"}},
    {"title" : 1}
)
```

👉 **Usando El Operador Dólar ($)**

Para hacer coincidir las cadenas que terminan con la expresión regular dada.

Ejemplo: Encontrar títulos de películas que terminen con la palabra "Opera".
```javascript
db.movies.find (
    {"title": {$regex: "Opera$"}}
)
```
👉 **Búsqueda Que No Distingue Entre Mayúsculas Y Minúsculas (Case-Insensitive)**

La búsqueda con expresiones regulares distingue entre mayúsculas y minúsculas de forma predeterminada. Las mayúsculas y minúsculas de los caracteres en el patrón de búsqueda proporcionado coincide exactamente.

El operador **$options** es para hacer búsquedas de expresiones regulares que no distinguen entre mayúsculas y minúsculas.  El argumento $options con un valor de i, donde i significa que no distingue entre mayúsculas y minúsculas.
```javascript
db.movies.find(
    {"title" :
        {"$regex" : "the", $options: "i"}
    }
)
```

### 🧡 Consultas de Arrays y Documentos Anidados

👉 **Encontrar un Array por elemento**

Consultar un array es similar a consultar cualquier otro campo. En la colección de **movies**, hay varios arrays y el campo de **cast** es una de ellas. 

Ejemplo: Encontrar películas protagonizadas por el actor Charles Chaplin.
```javascript
db.movies.find ({"cast": "Charles Chaplin"}, {"cast": 1, "_id": 0})
```
 ```
{ "cast" : [ "Charles Chaplin", "Edna Purviance", "Eric Campbell", "Albert Austin" ] }
{ "cast" : [ "Carl Miller", "Edna Purviance", "Jackie Coogan", "Charles Chaplin" ] }
{ "cast" : [ "Charles Chaplin", "Mack Swain", "Tom Murray", "Henry Bergman" ] }
{ "cast" : [ "Charles Chaplin", "Paulette Goddard", "Henry Bergman", "Tiny Sandford" ] }
{ "cast" : [ "Charles Chaplin", "Jack Oakie", "Reginald Gardiner", "Henry Daniell" ] }
{ "cast" : [ "Charles Chaplin", "Mady Correll", "Allison Roddan", "Robert Lewis" ] }
{ "cast" : [ "Charles Chaplin", "Claire Bloom", "Nigel Bruce", "Buster Keaton" ] }
{ "cast" : [ "Charles Chaplin", "Maxine Audley", "Jerry Desmonde", "Oliver Johnston" ] }
```
Ejemplo: Buscar películas con los actores Charles Chaplin y Edna Purviance juntos:
```javascript
db.movies.find(
    {$and :[
        {"cast" : "Charles Chaplin"},
        {"cast": "Edna Purviance"}
    ]},
    {"cast": 1, "_id": 0}
)
```
👉 **Buscar un campo Array usando un Array**

Cuando busca un campo de array utilizando un array, los elementos y su orden deben coincidir.

Ejemplo: Encontrar películas que estén disponibles tanto en English como en German. Prepare un array de ambos valores y consulte el campo de languages:
```javascript
db.movies.find(
    {"languages" : ["English", "German"]}, {"languages" : 1}
)
```
```
{ "_id" : ObjectId("573a1392f29313caabcd9fc4"), "languages" : [ "English", "German" ] }
{ "_id" : ObjectId("573a1392f29313caabcda64c"), "languages" : [ "English", "German" ] }
{ "_id" : ObjectId("573a1392f29313caabcdbabd"), "languages" : [ "English", "German" ] }
{ "_id" : ObjectId("573a1393f29313caabcdc13b"), "languages" : [ "English", "German" ] }
.....
.....
```
Ahora, cambiemos el orden de los elementos de la matriz y busquemos nuevamente:
```javascript
db.movies.find(
    {"languages" : ["German", "English"]}, {"languages" : 1}
)
```
Tenga en cuenta que la consulta es la misma que la anterior, excepto por el orden de los elementos de la matriz, que se invierte. Debería ver el siguiente resultado:
```
{ "_id" : ObjectId("573a1394f29313caabce0e55"), "languages" : [ "German", "English" ] }
{ "_id" : ObjectId("573a1395f29313caabce1082"), "languages" : [ "German", "English" ] }
{ "_id" : ObjectId("573a1395f29313caabce1bb0"), "languages" : [ "German", "English" ] }
....
....
```
Al cambiar el orden de los elementos en la matriz, se han hecho coincidir diferentes registros.

Cuando se buscan campos de array utilizando un array, el valor se compara mediante una verificación de igualdad. Dos array cualesquiera solo pasan la verificación de igualdad si tienen los mismos elementos en el mismo orden. Por lo tanto, las dos consultas siguientes no son iguales y devolverán resultados diferentes:
```javascript
// Find movies languages by [ "English", "French", "Cantonese", "German"]
db.movies.find(
    {"languages": [ "English", "French", "Cantonese", "German"]},
    {"languages" : 1, "_id": 0}
)
```
```javascript
// Find movies languages by ["English", "French", "Cantonese"]
db.movies.find(
    {"languages": ["English", "French", "Cantonese"]},
    {"languages" : 1, "_id": 0}
)
```
La única diferencia entre estas dos consultas es que la segunda consulta no contiene el último elemento "German".

👉 **Buscando en un Array con el Operador $all**

El operador **$all** busca todos aquellos documentos donde el valor del campo contiene todos los elementos, independientemente de su orden o tamaño.

Ejemplo: Buscar todas las películas disponibles en English, French y Cantonese.
```javascript
db.movies.find(
    {"languages":{
        "$all" :[ "English", "French", "Cantonese"]
    }},
    {"languages" : 1, "_id": 0}
)
```
```javascript
{ "languages" : [ "English", "French", "Cantonese", "German" ] }
{ "languages" : [ "Cantonese", "English", "Vietnamese", "French" ] }
{ "languages" : [ "French", "Cantonese", "English", "Hakka" ] }
{ "languages" : [ "Cantonese", "English", "French" ] }
{ "languages" : [ "French", "English", "Cantonese", "Italian" ] }
{ "languages" : [ "English", "Cantonese", "Italian", "Japanese", "Mandarin", "French" ] }
{ "languages" : [ "English", "German", "Arabic", "French", "Cantonese" ] }
{ "languages" : [ "Cantonese", "Mandarin", "English", "Korean", "French", "Turkish" ] }
{ "languages" : [ "English", "Cantonese", "French", "German", "Hindi", "Turkish" ] }
{ "languages" : [ "French", "English", "Cantonese" ] }
{ "languages" : [ "French", "English", "Cantonese" ] }
{ "languages" : [ "English", "French", "Cantonese" ] }
{ "languages" : [ "English", "French", "Cantonese", "Gujarati", "Yiddish" ] }
{ "languages" : [ "French", "English", "Cantonese" ] }
{ "languages" : [ "English", "French", "Cantonese" ] }
{ "languages" : [ "Cantonese", "English", "French" ] }
{ "languages" : [ "English", "French", "Cantonese" ] }
{ "languages" : [ "Cantonese", "Mandarin", "English", "Shanghainese", "French" ] }
{ "languages" : [ "Cantonese", "Mandarin", "English", "Shanghainese", "French" ] }
```
**Proyectar elementos de Array**

Hasta ahora, siempre que buscamos un campo de array, la salida siempre contiene el array completo. Hay algunas formas de limitar la cantidad de elementos de un array que se devuelven en la salida de la consulta.

👉 **Proyectar Elementos Coincidentes Usando ($)**

Puede buscar una array por un valor de elemento y usar la proyección para excluir todos excepto el elemento coincidente del array usando el operador **$**.
```javascript
db.movies.find(
    {"languages" : "Syriac"},
    {"languages.$" :1}
)
```
```javascript
{ "_id" : ObjectId("573a1397f29313caabce6443"), "languages" : [ "Syriac" ] }
{ "_id" : ObjectId("573a139af29313caabcf08fe"), "languages" : [ "Syriac" ] }
{ "_id" : ObjectId("573a13b0f29313caabd33446"), "languages" : [ "Syriac" ] }
 ```
El campo array de la salida solo contiene el elemento coincidente, el resto de los elementos se omiten.

👉 **Proyectar Elementos Coincidentes Por Su Posición De Índice ($slice)**

El operador **$slice** se utiliza para limitar los elementos del array en función de su posición de índice. Este operador se puede utilizar con cualquier campo de array, independientemente del campo que se esté consultando o no. Esto significa que puede consultar un campo diferente y todavía utilizan este operador para limitar los elementos de los campos array.

Ejemplo: La película Youth Without Youth tiene 11 elementos en campo array languages. Use **$slice** para imprimir solo los primeros tres elementos:
```javascript
db.movies.find(
    {"title" : "Youth Without Youth"},
    {"languages" : {$slice : 3}}
).pretty()
```
```javascript
"languages" : [
            "English",
            "Sanskrit",
            "German"
    ]
"released" : ISODate("2007-10-26T00:00:00Z"),
"directors" : [
```
La siguiente expresión de proyección devolverá los dos últimos elementos de la matriz:
```javascript
db.movies.find(
    {"title" : "Youth Without Youth"},
    {"languages" : {$slice : -2}}
```
```javascript
"languages" : [
            "Armenian",
            "Egyptian (Ancient)",
    ]
"released" : ISODate("2007-10-26T00:00:00Z"),
```
Se puede indicar omitir y mostrar. Por ejemplo se omitirá los 2 primeros elementos de la matriz y devolverá los siguientes 4 elementos siguientes:
```javascript
db.movies.find(
    {"title" : "Youth Without Youth"},
    {"languages" : {$slice : [2, 4]}}
```
```javascript
"languages" : [
            "German",
            "French",
            "Italian"
            "Russian"
    ]
 "released" : ISODate("2007-10-26T00:00:00Z"),
 "directors" : [
```
También se puede utilizar con un valor negativo para omitir. Por ejemplo, el primer número es negativo. Si el valor de salto es negativo, el conteo comienza desde el final. La expresión, se omitirán cinco elementos contados desde el último índice y se devolverán cuatro elementos a partir de ese índice:
```javascript
db.movies.find(
    {"title" : "Youth Without Youth"},
    {"languages": {$ slice: [-5, 4]}}
```
```javascript
"languages" : [
            "Romanian",
            "Mandarin",
            "Latin"
            "Armenian"
    ]
"released" : ISODate("2007-10-26T00:00:00Z"),
```

👉 **Consultar objetos anidados completos**

De manera similar a las matrices, los objetos anidados también se pueden representar como valores de un campo. Por lo tanto, los campos que tienen otros objetos como valores se pueden buscar utilizando el **objeto completo como valor**. 

En la colección de movies, hay un campo llamado **awards** cuyo valor es un objeto anidado. El siguiente fragmento muestra el objeto de awards para una película aleatoria de la colección:
```javascript
"rated" : "TV-G",
    "awards" : {
             "wins" : 1,
             "nominations" : 0,
             "text" : "1 win."
    }
```
La siguiente consulta busca el objeto de **awards** proporcionando el objeto completo como su valor:
```javascript
db.movies.find(
    {"awards":
        {"wins": 1, "nominations": 0, "text": "1 win."}
    },
    {"awards":1}
)
```
El siguiente resultado muestra que hay varias películas cuyo campo de premios tiene un valor exacto de `{"wins": 1, "nominations": 0, "text": "1 win."}`:
```javascript
{
        "_id" : ObjectId("573a1390f29313caabcd4135"),
        "awards" : {
                "wins" : 1,
                "nominations" : 0,
                "text" : "1 win."
        }
}
{
        "_id" : ObjectId("573a1390f29313caabcd42e8"),
        "awards" : {
                "wins" : 1,
                "nominations" : 0,
                "text" : "1 win."
        }
}
....
....
```
Cuando se buscan campos de objeto anidados con valores de objeto, debe haber una coincidencia exacta. Los pares clave-valor, junto con el orden de los campos, deben coincidir exactamente. 

La siguiente consulta tiene un cambio de orden con respecto al objeto de consulta; por lo tanto, devolverá un resultado **vacío**:
```javascript
db.movies.find(
    {"awards":
        {"nominations": 0, "wins": 1, "text": "1 win."}
    }
)
```
👉 **Consultar campos de objetos anidados**

Con la notación de puntos (.) se puede utilizar para buscar objetos anidados proporcionando los valores de sus campos. 

Ejemplo: Buscar películas que hayan ganado cuatro premios.
```javascript
db.movies.find (
    {"awards.wins": 4}, {"awards": 1, "_id": 0}
)
```
La consulta anterior utiliza la notación de puntos (.) en el campo de **awards** y refiere al campo anidado **wins**. 

Cuando ejecuta la consulta y proyecta solo el campo de awards, muestra todas las películas que tienen exactamente cuatro premios:
```javascript
{
        "awards" : {
                "wins" : 4,
                "nominations" : 0,
                "text" : "Nominated for 1 Oscar. Another 3 wins."
        }
}
{
        "awards" : {
                "wins" : 4,
                "nominations" : 1,
                "text" : "Won 3 Oscars. Another 1 win & 1 nomination."
        }
}
...
...
```
La búsqueda de campos anidados se realiza independientemente del orden de los elementos. La siguiente consulta realiza una búsqueda en dos campos utilizando operadores condicionales y devuelve películas que tienen seis nominaciones y han ganado al menos cinco premios. Los campos de objetos anidados también se pueden proyectar como queramos.
```javascript
db.movies.find(
    {
        "awards.wins" : {$gte : 5},
        "awards.nominations" : 6
    },
    {"awards": 1, "_id": 0}
)
```
Al ejecutar la consulta excluyendo el resto de los campos, debería ver el siguiente resultado:
```javascript
{
        "awards" : {
                "wins" : 6,
                "nominations" : 6,
                "text" : "Won 1 Oscar. Another 5 wins & 6 nominations."
        }
}
{
        "awards" : {
                "wins" : 19,
                "nominations" : 6,
                "text" : "Won 8 Oscars. Another 11 wins & 6 nominations."
        }
}
...
...
```

💪 **Ejercicio: Proyección de campos de objetos anidados**

Mostrar todos los registros y proyectar solo el campo de awards, que es un objeto incrustado:
```javascript
db.movies.find(
    {},
    {
       "awards" :1,
       "_id":0
    }
)
```
Proyectar solo campos específicos de objetos incrustados, puede hacer referencia a un campo de un objeto incrustado utilizando notación de puntos:
```javascript
db.movies.find(
    {},
    {
        "awards.wins" :1,
        "awards.nominations" : 1,
        "_id":0
    }
)
```
Solo dos de los campos anidados se incluyen en la respuesta. El objeto de awards en la salida sigue siendo un objeto anidado, pero el campo de texto se ha excluido.

### 🧡 Limitando el resultado con limit

Con la función **limit** se puede restringir el tamaño del resultado. Ejemplo: Limitar el resultado a 3 registros.
```javascript
db.movies.find(
    {"cast" : "Charles Chaplin"},
    {"title": 1, "_id" :0}
).limit(3)
```
```javascript
{ "title" : "The Immigrant" }
{ "title" : "The Kid" }
{ "title" : "The Gold Rush" }
```
Establecer el límite en cero equivale a no establecer ningún límite, devolverá todos los registros de la consulta.

Un límite de tamaño negativo se considera equivalente al límite de un número positivo.

### 🧡 Excluir documentos con Skip

La funcion **Skip*** se utiliza para excluir algunos documentos del conjunto de resultados y devolver el resto. El cursor MongoDB proporciona la función skip (), que acepta un número entero y omite el número especificado de documentos del cursor, devolviendo el resto.
```javascript
db.movies.find(
    {"cast" : "Charles Chaplin"},
    {"title": 1, "_id" :0}
).skip(2)
```
Dado que la función skip se ha proporcionado con el valor 2, los dos primeros documentos se excluirán de la salida:
```javascript
{ "title" : "The Gold Rush" }
{ "title" : "Modern Times" }
{ "title" : "The Great Dictator" }
{ "title" : "Monsieur Verdoux" }
{ "title" : "Limelight" }
{ "title" : "A King in New York" }
 ```
Similar a limit(), pasar un valor cero a skip() es equivalente a no llamar a la función en absoluto, y se devuelve el conjunto de resultados completo. Sin embargo, skip() tiene un comportamiento diferente para números negativos; no permite el uso de números negativos. 
```javascript
db.movies.find(
    {"cast" : "Charles Chaplin"},
    {"title": 1, "_id" :0}
).skip(-3)
```
```javascript
Error: error: {
        "ok" : 0,
        "errmsg" : "Skip value must be non-negative, but received: -3",
        "code" : 2,
        "codeName" : "BadValue"
}
 ```
### 🧡 Ordenando documentos con sort

La ordenación de documentos se puede realizar en varios campos y cada campo puede tener un ordenamiento diferente.

En esta siguiente consulta, está llamando a la función **sort()** en el cursor resultante. El argumento **title: 1** se especifica que el campo dado debe ordenarse en orden **ascendente**. 
```javascript
db.movies.find(
    {"cast" : "Charles Chaplin"},
    {"title" : 1, "_id" :0}
).sort({"title" : 1})
```
```
{ "title" : "A King in New York" }
{ "title" : "Limelight" }
{ "title" : "Modern Times" }
{ "title" : "Monsieur Verdoux" }
{ "title" : "The Gold Rush" }
{ "title" : "The Great Dictator" }
{ "title" : "The Immigrant" }
{ "title" : "The Kid" }
```
Para ordenar en forma **descendente** se especifica con el valor -1.
```javascript
db.movies.find(
    {"cast" : "Charles Chaplin"},
    {"title" : 1, "_id" :0}
).sort({"title" : -1})
```
```javascript
{ "title" : "The Kid" }
{ "title" : "The Immigrant" }
{ "title" : "The Great Dictator" }
{ "title" : "The Gold Rush" }
{ "title" : "Monsieur Verdoux" }
{ "title" : "Modern Times" }
{ "title" : "Limelight" }
{ "title" : "A King in New York" }
```
Ordenar las calificaciones de IMDb de las películas en orden descendente y el año en orden ascendente:
```javascript
db.movies.find()
    .limit(50)
    .sort({"imdb.rating": -1, "year" : 1})
```
💪 **Actividad: Búsqueda de películas por género y paginación de resultados**

Se planea proporcionar una nueva función a sus usuarios donde podrán encontrar películas en su género favorito. Dado que la base de datos de películas es enorme, hay muchas películas de cada género y devolver todos los títulos de películas coincidentes no es muy útil. El requisito es servir los resultados en pequeños trozos.

Su tarea para esta actividad es crear una función de JavaScript. La función debe aceptar un género a elección del usuario e imprimir todos los títulos coincidentes, donde los títulos con las calificaciones de IMDb más altas deben aparecer en la parte superior. Junto con el género, la función aceptará dos parámetros más para el tamaño de página y el número de página. El **pageSize** define cuántos registros deben mostrarse en una página, mientras que el **pageNumber** indica en qué página se encuentra el usuario.

```javascript
var findMoviesByGenre = function(genre, pageNumber, pageSize){
    var toSkip = 0;
    if(pageNumber < 2){
        toSkip = 0;
    } else{
        toSkip = (pageNumber -1) * pageSize;
    }
    var movies = db.movies.find(
        {"genres" : genre},
        {"_id" : 0, "title" :1})
	.sort({"imdb.rating" : -1})
	.skip(toSkip)
	.limit(pageSize)
	.toArray()
    print("************* Page : " + pageNumber)
    for(var i =0; i < movies.length; i++){
        print(movies[i].title)
    }
}
```
Ejecutamos la funcion:
```javascript
findMoviesByGenre("Action", 3, 5)
```
Obtenemos lo siguiente:
```javascript
/*
************* Page : 3
Harakiri
Battlestar Galactica
Star Wars: Episode IV - A New Hope
The Matrix
Sholay
*/
```

 ## 🐥 5. Insertar, actualizar y eliminar documentos <a name="insertar_actualizar_eliminar"></a>

### 🧡 Insertar documentos con insert

La funcion **insert()** se utiliza para crear un nuevo documento en una colección. Cuando se ejecuta un comando de inserción de documento, MongoDB también creará la colección dada, si aún no existe.

Cree una nueva base de datos **`use newbase`**. Luego inserte una película en la coleccion **new_movies** con la funcion **insert** asi:
```javascript
db.new_movies.insert({"_id" : 1, "title" : "Dunkirk"})
```
`WriteResult({ "nInserted" : 1 })`

Realice una consulta con **find** y confirme si el registro se creó:
```javascript
db.new_movies.find({"_id" : 1})
```
`{ "_id" : 1, "title" : "Dunkirk" }`
```
``javascript
show collections
```
`new_movies`

### 🧡 Insertar varios documentos con insertMany

Se puede usar tanto la funcion **insert** o la funcion **insertMany**, que toma un array de documentos.
```javascript
db.new_movies.insert({"_id": 2, "title": "Baby Driver"})
db.new_movies.insert({"_id": 3, "title" : "Logan"})
db.new_movies.insert({"_id": 4, "title": "John Wick: Chapter 2"})
db.new_movies.insert({"_id": 5, "title": "A Ghost Story"})
```
```javascript
db.new_movies.insertMany([
    {"_id" : 2, "title": "Baby Driver"},
    {"_id" : 3, "title": "Logan"},
    {"_id" : 4, "title": "John Wick: Chapter 2"},
    {"_id" : 5, "title": "A Ghost Story"}
])
```
Para insertar varios documentos, es preferible usar la función **insertMany()**, porque la inserción ocurre como una sola operación. La inserción de cada documento por separado se ejecutará como una serie de comandos de base de datos diferentes y hará que el proceso sea más lento.

### 🧡 Insertar claves duplicadas

El valor expresado por el campo **\_id** es una clave principal, por lo que debe ser único. Si intenta insertar un documento cuya clave ya está presente en la colección, obtendrá un error de clave duplicada. Esto aplica también cuando se usa **insertMany**.
```javascript
db.new_movies.insert({"_id" : 2, "title" : "Some other movie"})
```
```
WriteResult({
        "nInserted" : 0,
        "writeError" : {
                "code" : 11000,
                "errmsg" : "E11000 duplicate key error collection: CH05.new_movies index: _id_ dup key: { _id: 1.0 }"
        }
})
```
Pruebe la siguiente consulta:
```javascript
db.new_movies.insertMany([
    {"_id" : 6, "title" : "some movie 1"},
    {"_id" : 7, "title" : "some movie 2"},
    {"_id" : 2, "title" : "Movie with duplicate _id"},
    {"_id" : 8, "title" : "some movie 3"},
])
``` 
El resultado muestra que dos documentos se han insertado correctamente el 6 y el 7. 
```javascript
db.new_movies.find({"_id" : {$in : [6, 7, 2, 8]}})
```
```javascript
{ "_id" : 2, "title" : "Baby Driver" }
{ "_id" : 6, "title" : "some movie 1" }
{ "_id" : 7, "title" : "some movie 2" }
```
Podemos concluir que el comando falló al insertar el tercer documento. Sin embargo, los documentos insertados antes del tercero permanecerán en la base de datos.

### 🧡 Insertar sin \_id

MongoDB verifica la presencia y unicidad de una clave primaria dada y, si la clave primaria aún no está presente, la base de datos la genera automáticamente y la agrega a el documento.
```javascript
db.new_movies.insert ({"título": "Thelma"})
```
`WriteResult ({"nInserted": 1})`

```javascript
db.new_movies.find ({"título": "Thelma"})
```
`{"_id": ObjectId ("5df6a0e1b32aea114de21834"), "title": "Thelma"}`

```javascript
db.new_movies.insertMany([
    {"_id" : 9, "title" : "movie_1"},
    {"_id" : 10, "title" : "movie_2"},
    {"title" : "movie_3"},
    {"_id" : 8, "title" : "movie_4"}
])
```
 
### 🧡 Eliminar Documentos usando deleteOne

La función **deleteOne** se usa para eliminar un solo documento de una colección. Como el método elimina solo un documento, el valor de respuesta **deletedCount** es 1. Si la condición de consulta dada coincide con más de un documento en la colección, solo se eliminará el primer documento.
```javascript
db.new_movies.deleteOne({"_id": 2})
```
`{ "acknowledged" : true, "deletedCount" : 1 }`


💪 **Ejercicio 5.01: eliminar uno de los muchos documentos coincidentes**

En este ejercicio, usará una consulta que coincida con más de un documento y verificará que solo se elimine el primer documento cuando lo haga.
```javascript
db.new_movies.find({"title" : {"$regex": "^movie"}})
```
```
{ "_id" : 9, "title" : "movie_1" }
{ "_id" : 10, "title" : "movie_2" }
{ "_id" : ObjectId("5ef2666a6c3f28e14fddc816"), "title" : "movie_3" }
{ "_id" : 8, "title" : "movie_4" }
```
```javascript
db.new_movies.deleteOne({"title" : {"$regex": "^movie"}})
```
`{ "acknowledged" : true, "deletedCount" : 1 }`

```javascript
db.new_movies.find({"title" : {"$regex": "^movie"}})
```
```
{ "_id" : 10, "title" : "movie_2" }
{ "_id" : ObjectId("5ef2666a6c3f28e14fddc816"), "title" : "movie_3" }
{ "_id" : 8, "title" : "movie_4" }
```

### 🧡 Eliminación de varios documentos con deleteMany

La función **deleteMany** sirve para eliminar varios documentos en un solo comando. Debe proporcionarse con una condición de consulta, y se eliminarán todos los documentos que coincidan con la consulta dada.
```javascript
db.new_movies.deleteMany({"title" : {"$regex": "^movie"}})
```
`{ "acknowledged" : true, "deletedCount" : 3 }`

Pasar un documento de consulta vacío equivale a no pasar ningún filtro y, por lo tanto, todos los documentos coinciden. La función **deleteOne** eliminará el documento que se encuentre primero. La función **deleteMany** eliminará todos los documentos de la colección. 
```javascript
db.new_movies.deleteOne ({})
db.new_movies.deleteMany ({})
```
Un campo inexistente se considera nulo y, por tanto, la condición dada coincidirá con todos los documentos de la colección:
```javascript
db.new_movies.deleteOne({"non_existent_field" : null})
db.new_movies.deleteMany({"non_existent_field" : null})
```
Siempre debe asegurarse de que no haya errores tipográficos en el nombre del campo. Un nombre de campo incorrecto puede dar lugar a la eliminación de todos los documentos de la colección.

### 🧡 Eliminar usando findOneAndDelete

Busca y elimina un documento de la colección. Si se encuentra más de un documento, solo se eliminará el primero. Una vez eliminado, **muestra el documento eliminado** como respuesta. En el caso de coincidencias de varios documentos, la opción de **sort** se puede utilizar para influir en qué documento se elimina. La proyección se puede utilizar para incluir o excluir campos del documento en respuesta.

```javascript
db.new_movies.findOneAndDelete({"_id": 3})
```
`{ "_id" : 3, "title" : "Logan" }`

```javascript
db.new_movies.insertMany([
  { "_id" : 11, "title" : "movie_11" },
  { "_id" : 12, "title" : "movie_12" },
  { "_id" : 13, "title" : "movie_13" },
  { "_id" : 14, "title" : "movie_14" },
  { "_id" : 15, "title" : "series_15" }
])
```
```javascript
db.new_movies.findOneAndDelete(
      {"title" : {"$regex" : "^movie"}},
      {sort : {"_id" : -1}}
  )
```
`{ "_id" : 14, "title" : "movie_14" }`

```javascript
db.new_movies.findOneAndDelete(
     {"title" : {"$regex" : "^movie"}},
     {sort : {"_id" : -1}, projection : {"_id" : 0, "title" : 1}}
)
```
`{ "title" : "movie_13" }`

💪 **Ejercicio 5.02: Eliminación de una película de baja calificación**

Usando la coleccion de **movies** ejecutar un comando de eliminación para que se elimine una película con menos premios, una calificación de IMDb de menos de 2 y más de 50000 votos. Luego, solo muestre el título y el \_id de la película eliminada.

La clasificación de IMDb es un campo anidado; por lo tanto, usará la notación de puntos para acceder al campo:
```javascript
db.movies.findOneAndDelete(
  { 
    "imdb.rating" : {$lt : 2}, 
    "imdb.votes" : {$gt : 50000}
  },
  {
    "sort" : {"awards.won": 1},
    "projection" : {"title" : 1}
  }
)
```

### 🧡 Reemplazo de documentos con replaceOne

Reemplazar completamente los documentos de una colección. 

Usando la base de datos **newbase** cree una colección denominada **users** e inserte algunos usuarios en ella:
```javascript
db.users.insertMany([
  {"_id": 2, "name": "Jon Snow", "email": "Jon.Snow@got.es"},
  {"_id": 3, "name": "Joffrey Baratheon", "email": "Joffrey.Baratheon@got.es"},
  {"_id": 5, "name": "Margaery Tyrell", "email": "Margaery.Tyrell@got.es"},
  {"_id": 6, "name": "Khal Drogo", "email": "Khal.Drogo@got.es"}
])
```
`{ "acknowledged" : true, "insertedIds" : [ 2, 3, 5, 6 ] }`

```javascript
db.users.find()
```
```javascript
{ "_id" : 2, "name" : "Jon Snow", "email" : "Jon.Snow@got.es" }
{ "_id" : 3, "name" : "Joffrey Baratheon", "email" : "Joffrey.Baratheon@got.es" }
{ "_id" : 5, "name" : "Margaery Tyrell", "email" : "Margaery.Tyrell@got.es" }
{ "_id" : 6, "name" : "Khal Drogo", "email" : "Khal.Drogo@got.es" }
```
MongoDB proporciona el método **replaceOne()**, que acepta un filtro de consulta y un documento de reemplazo. El primer argumento es el filtro de consulta para identificar el documento que se reemplazará y el segundo argumento es el nuevo documento. 
```javascript
db.users.replaceOne(
  {"_id" : 5},
  {"name": "Margaery Baratheon", "email": "Margaery.Baratheon@got.es"}
)
```
`{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }`

No es necesario que el filtro de consulta sea siempre el campo \_id . Puede ser cualquier consulta que filtre usando cualquier campo o combinación de múltiples campos y operadores.
```javascript
db.users.replaceOne(
  {"name": "Margaery Tyrell },
  {"name": "Margaery Baratheon", "email": "Margaery.Baratheon@got.es"}
)
```

### 🧡 Los Campos \_Id Son Inmutables

El \_id del documento original se conserva en el nuevo documento. El campo \_id sirve como identificador único de un documento y, por lo tanto, no debe cambiarse mientras exista el documento.
```javascript
db.users.find({"name" : "Margaery Baratheon"})
{"_id": 5, "name": "Margaery Baratheon", "email": "Margaery.Baratheon@got.es" }
```
El siguiente reemplazo no se ejcutará:
```javascript
db.users.replaceOne(
  {"name" : "Margaery Baratheon"},
  {"_id": 9, "name": "Margaery Baratheon", "email": "Margaery.Baratheon@got.es"}
)
```

### 🧡 Reemplazar y/o actualizar con replaceOne y upsert

Habrá ocasiones en las que desee reemplazar un documento existente por uno nuevo y, si el documento aún no existe, inserte el nuevo documento. 

Actualización o **update** (si se encuentra) o inserción **insert** (si no se encuentra), que se abrevia con **upsert**. 

Se debe pasar un argumento adicional **{upsert: true}**.

Considere los siguientes registros en la colección de users:
```javascript
db.users.find()
{"_id": 2, "name": "Jon Snow", "email": "Jon.Snow@got.es"}
{"_id": 3, "name": "Joffrey Baratheon", "email": "Joffrey.Baratheon@got.es"}
{"_id": 5, "name": "Margaery Baratheon", "email": "Margaery.Baratheon@got.es"}
{"_id": 6, "name": "Khal Drogo", "email": "Khal.Drogo@got.es"}
```
La actualización que recibe del servidor de usuarios contiene el registro actualizado para Margaery y el nuevo registro para Tommen, de la siguiente manera:
```
{"name": "Margaery Tyrell", "email": "Margaery.Tyrell@got.es"}
{"name": "Tommen Baratheon", "email": "Tommen.Baratheon@got.es"}
```
```javascript
db.users.replaceOne(
  {"name" : "Margaery Baratheon"},
  {"name": "Margaery Tyrell", "email": "Margaery.Tyrell@got.es"},
  { upsert: true }
)
```
```javascript
db.users.replaceOne(
  {"name" : "Tommen Baratheon"},
  {"name": "Tommen Baratheon", "email": "Tommen.Baratheon@got.es"},
  { upsert: true }
)
```
El resultado del primer upsert indica que se encontró una coincidencia y que el documento se actualizó. Sin embargo, el segundo denota que no se encontró la coincidencia y se insertó un nuevo documento con una clave primaria generada automáticamente.

### 🧡 Reemplazo con findOneAndReplace

Las principales características de findOneAndReplace son las siguientes:

- Busca un documento y lo reemplaza.
- Si se encuentra más de un documento que coincide con la consulta, se reemplazará el primero.
- Se puede utilizar una opción de **sort** para influir en qué documento se reemplaza si se hace coincidir más de un documento.
- De forma predeterminada, devuelve el **documento original**.
- Si se establece la opción de **{returnNewDocument: true}**, se devolverá el documento recién agregado.
- La **proyección** de campo se puede utilizar para incluir solo campos específicos en el documento devuelto como respuesta.

Para ver findOneAndReplace() en acción, agregue cinco documentos a una colección de movies:
```javascript
db.movies.insertMany([
    { "_id": 1011, "title" : "Macbeth" },
    { "_id": 1513, "title" : "Macbeth" },
    { "_id": 1651, "title" : "Macbeth" },
    { "_id": 1819, "title" : "Macbeth" },
    { "_id": 2117, "title" : "Macbeth" }
])
```
Debe utilizar el campo \_id incremental, donde la película con el valor \_id más grande es la última. Para simplificar las consultas de búsqueda en el futuro, se le ha indicado que busque el documento de la última película con este título y agregue una marca de **latest: true** a ese documento.
```javascript
db.movies.findOneAndReplace(
    {"title" : "Macbeth"},
    {"title" : "Macbeth", "latest" : true},
    {
        sort : {"_id" : -1},
        projection : {"_id" : 0}
    }
)
```
El codigo anterior, encontró el documento de una película por su título y lo reemplazó con otro documento que contiene un campo adicional **"latest" : true**. Aparte de eso, el comando utilizó la opción de **sort** para que el registro con el valor más grande \_id aparezca en la parte superior. El comando también usa una opción de **proyección** para incluir solo el campo de título en la respuesta.

Alternativamente, si se le solicita que obtenga el documento actualizado en la respuesta, puede hacer uso del indicador **returnNewDocument**.
```javascript
db.movies.findOneAndReplace(
    {"title" : "Macbeth"},
    {"title" : "Macbeth", "latest" : true},
    {
        sort : {"_id" : -1},
        projection : {"_id" : 0},
        returnNewDocument : true
    }
)
```
```javascript
db.movies.find({"title" : "Macbeth"})
```
```javascript
{ "_id" : 1011, "title" : "Macbeth" }
{ "_id" : 1513, "title" : "Macbeth" }
{ "_id" : 1651, "title" : "Macbeth" }
{ "_id" : 1819, "title" : "Macbeth" }
{ "_id" : 2117, "title" : "Macbeth", "latest" : true }
```

### 🧡 Replace versus Delete and Re-Insert

Es posible reemplazar un documento usando una combinación de eliminar e insertar, donde elimina un documento existente e inserta uno nuevo. 

Primero, elimine todos los documentos previamente insertados o modificados de la colección:
```javascript
db.movies.deleteMany({})
```
`{ "acknowledged" : true, "deletedCount" : 5 }`

Ahora, inserte los cinco documentos nuevamente:
```javascript
db.movies.insertMany([
    { "_id": 1011, "title" : "Macbeth" },
    { "_id": 1513, "title" : "Macbeth" },
    { "_id": 1651, "title" : "Macbeth" },
    { "_id": 1819, "title" : "Macbeth" },
    { "_id": 2117, "title" : "Macbeth" }
])
```
Ahora, busque el documento de la última película titulada Macbeth y agregue la marca **latest: true** a ella:
```javascript
var deletedDocument = db.movies.findOneAndDelete(
                          {"title" : "Macbeth"},
                          {sort : {"_id" : -1}}
    )
    
db.movies.insert(
  {
    "_id" : deletedDocument._id, 
    "title" : "Macbeth", "latest" : true
   }
)
```
Este fragmento muestra dos comandos diferentes. El primero es un comando findOneAndDelete() que busca una película por su título y también usa la opción de sort para que solo se elimine la película con el \_id más grande . El resultado de la operación es el documento eliminado, se almacena en una variable de deletedDocument.

El siguiente comando en el fragmento anterior es una operación de inserción que vuelve a insertar la misma película junto con la marca **latest: true**. Mientras lo hace, utiliza el valor \_id del documento eliminado, de modo que el nuevo registro se inserta con la misma clave principal:
```javascript
db.movies.find()
{ "_id" : 1011, "title" : "Macbeth" }
{ "_id" : 1513, "title" : "Macbeth" }
{ "_id" : 1651, "title" : "Macbeth" }
{ "_id" : 1819, "title" : "Macbeth" }
{ "_id" : 2117, "title" : "Macbeth", "latest" : true }
```
Aunque los resultados son exactamente los mismos, la operación de dos pasos es más propensa a errores. Por lo tanto, siempre es preferible utilizar las funciones especiales proporcionadas por MongoDB.

### 🧡 Actualizar un documento con updateOne y $set

Para modificar uno o solo algunos campos de un documento, MongoDB proporciona el comando de updateOne. Devolve las estadísticas de la consulta, como cuántos registros coincidieron y cuántos registros se modificaron.

Antes de usar esta función, primero elimine todos los registros previamente insertados y modificados de la colección:
```javascript
db.movies.deleteMany({})
{ "acknowledged" : true, "deletedCount" : 5 }
```
Luego:
```javascript
db.movies.insertMany([
  {"_id": 1, "title": "Macbeth", "year": 2014, "type": "series"},
  {"_id": 2, "title": "Inside Out", "year": 2015, "type": "movie", "num_mflix_comments": 1},
  {"_id": 3, "title": "The Martian", "year": 2015, "type": "movie", "num_mflix_comments": 1},
  {"_id": 4, "title": "Everest", "year": 2015, "type": "movie", "num_mflix_comments": 1}
])
```
`{ "acknowledged" : true, "insertedIds" : [ 1, 2, 3, 4 ] }`

Actualize un documento con updateOne() y $set:
```javascript
db.movies.updateOne(
    {"title" : "Macbeth"},
    {$set : {"year" : 2015}}
)
```
`{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }`

EL primer argumento es la condición de consulta. El segundo argumento es un documento que especifica un nuevo campo de año y su valor. Se usa $set, para asignar valores a los campos proporcionados en un documento. 
```javascript
db.movies.find({"title" : "Macbeth"})
```
`{ "_id" : 1, "title" : "Macbeth", "year" : 2015, "type" : "series" }`
```javascript
db.movies.updateOne(
    {"title" : "Macbeth"},
    {$set : {"year" : 2015}}
)
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 0 }
```
No se realizará ninguna actualización ya que el valor ya es 2015.

### 🧡 Modificar Más De Un Campo con updateOne y $set

```javascript
db.movies.updateOne(
  {"title" : "Macbeth"},
  {$set : {"type" : "movie", "num_mflix_comments" : 1}}
)
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```
El campo num_mflix_comment no existe en la película respectiva, un registro se modificó como se esperaba.
```javascript
db.movies.find({"title" : "Macbeth"}).pretty()
```
```javascript
{
  "_id" : 1,
  "title" : "Macbeth",
  "year" : 2015,
  "type" : "movie",
  "num_mflix_comments" : 1
}
```
Se ha agregado un nuevo campo llamado num_mflix_comments con el valor dado. Con $set se puede usar para actualizar varios campos en el mismo comando, y si un campo es nuevo, se agregará al documento con el valor especificado.

Actualizar el mismo campo varias veces es válido, independientemente del valor del campo.
```javascript
db.movies.updateOne(
  {"title" : "Macbeth"},
  {$set : {"year" : 2015, "year" : 2015, "year" : 2016, "year" : 2017}}
)
```
`{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }`

```javascript
db.movies.find({"title" : "Macbeth"}).pretty()
{
  "_id" : 1,
  "title" : "Macbeth",
  "year" : 2017,
  "type" : "movie",
  "num_mflix_comments" : 1
}
```

### 🧡 Varios Documentos Que Coinciden Con Una Condición con UpdateOne

La función updateOne, siempre actualiza solo un documento en la colección. Si la condición de consulta dada coincide con más de un documento, solo se modificará el primer documento:
```javascript
db.movies.updateOne(
  {"type" : "movie"},
  {$set : {"flag" : "modified"}}
)
```
`{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }`

Recuerde que tenemos un total de tres documentos de tipo película en nuestra colección de películas. Si hay más de un documento que coincide con la condición de consulta dada, solo se elige y actualiza un documento.

### 🧡 Upsert Con UpdateOne

Cuando se ejecutan actualizaciones con upsert, el documento se actualizará si se encuentra; si no se encuentra el documento, se crea un nuevo documento dentro de la colección. updateOne también admite actualizaciones con un indicador adicional en el comando. 
```javascript
db.movies.updateOne(
  {"title" : "Sicario"},
  {$set : {"year" : 2015}}
)
```
`{ "acknowledged" : true, "matchedCount" : 0, "modifiedCount" : 0 }`

El resultado indica que no se comparó ningún documento y no se actualizó ningún documento.

```javascript
db.movies.updateOne(
  {"title" : "Sicario"},
  {$set : {"year" : 2015}},
  {"upsert" : true}
)
```
La operación anterior utiliza un tercer argumento, que contiene un documento con **upsert: true**, que es falso de forma predeterminada.
En este caso no se comparó ningún documento y no se actualizó ningún documento. Sin embargo, "upsertedId": ObjectId ("5e ...") indica que se insertó un documento con una clave primaria generada automáticamente .
```javascript
db.movies.find({"_id" : ObjectId("5ef5484b76db1f20a60917d2")}).pretty()
```
```
{
  "_id" : ObjectId("5ef5484b76db1f20a60917d2"),
  "title" : "Sicario",
  "year" : 2015
}
```
Una cosa a tener en cuenta aquí es que el nuevo documento tiene dos campos, de los cuales el año del campo era parte de la expresión de actualización; sin embargo, el título formaba parte de la condición de la consulta. Cuando MongoDB crea un nuevo documento como parte de una operación upsert, combina campos de las expresiones de actualización y condiciones de consulta.

### 🧡 Actualizar un documento con findOneAndUpdate

Cuando se usa findOneAndUpdate no devolve las estadísticas de la consulta, como cuántos registros coincidieron y cuántos registros se modificaron. En cambio, devuelve el documento en su estado anterior.

```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$set : {"num_mflix_comments" : 10}}
)
```

```javascript
db.movies.find({"title" : "Macbeth"}).pretty()
```
```
{
  "_id" : 1,
  "title" : "Macbeth",
  "year" : 2017,
  "type" : "movie",
  "num_mflix_comments" : 10,
  "flag" : "modified"
}
```

### 🧡 Mostrar el documento nuevo como respuesta en findOneAndUpdate

Para conocer el nuevo documento actualizado debe usar **"returnNewDocument": true**
```javascript
db.movies.findOneAndUpdate (
  {"title": "Macbeth"},
  {$ set: {"num_mflix_comments": 15}},
  {"returnNewDocument": true}
)
```
```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$set : {"num_mflix_comments" : 20}},
  {
    "projection" : {"_id" : 0, "num_mflix_comments" : 1},
    "returnNewDocument" : true
  }
)
```
 
### 🧡 Ordenar Para Encontrar Un Documento findOneAndUpdate y sort

La función **findOneAndUpdate** proporciona una opción adicional para ordenar los documentos coincidentes en un orden específico. Con la opción de **sort**, puede influir en qué documento se selecciona para la modificación.
```javascript
db.movies.findOneAndUpdate(
  {"type" : "movie"},
  {$set : {"latest" : true}},
  {
    "returnNewDocument" : true,
    "sort" : {"_id" : -1}
  }
)
```

### 🧡 Actualización de varios documentos con updateMany

Considere que nuestra colección **movies** tiene 4 películas que se lanzaron en 2015. Agregue un campo llamado **languages** a estas películas:
```javascript
db.movies.updateMany(
  {"year" : 2015},
  {$set : {"languages" : ["English"]}}
)
```
`{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }`

Algunos puntos importantes sobre las **operaciones de actualización** y son aplicables a las tres funciones:

- Ninguna de las funciones de actualización le permite cambiar el campo \_id.
- El orden de los campos en un documento siempre se mantiene, excepto cuando la actualización incluye cambiar el nombre de un campo. Sin embargo, el campo \_id siempre aparecerá primero.
- Las operaciones de actualización son atómicas en un solo documento. Un documento no se puede modificar hasta que otro proceso haya terminado de actualizarlo.
- Todas las funciones de actualización admiten **upsert**. Para ejecutar un comando upsert, `upsert: true` debe pasarse como una opción.

### 🧡 Operadores de actualización

1. El operador **$set** ya visto anteriormente, que es uno de los operadores de actualización proporcionados por MongoDB. Que se usa para establecer los valores de los campos en un documento o agregar nuevos campos.

2. El operador de incremento **$inc** se utiliza para **incrementar** o **decrementar** el valor de un campo numérico en un número específico. 

Ejemplo: Incrementar en 3 unidades el campo num_mflix_comments. 

```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$inc : {"num_mflix_comments" : 3, "rating" : 1.5}},
  {returnNewDocument : true}
)
```
En el ejemolo se utilizó el operador $ inc en dos campos, de los cuales "num_mflix_comments existe en el documento y rating, findOneAndUpdate agregara este nuevo campo.

3. El operador de Multiplicar **$mul** se utiliza para multiplicar el valor de un campo numérico en un número específico.

Ejemplo: Multiplicar por 2 el campo rating.
```javascript
db.movies.findOneAndUpdate (
  {"title": "Macbeth"},
  {$mul: {"rating": 2}},
  {returnNewDocument: true}
)
```
Cuando use un campo inexistente con $mul, no importa qué multiplicador proporcionemos, el campo se creará y siempre se establecerá en cero. 
```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$mul : {"box_office_collection" : 16.3}},
  {returnNewDocument : true}
)
```
4. El operador Rename **$rename** se usa para cambiar el nombre de los campos. Si el campo aún no está presente en el documento, el operador lo ignora y no hace nada. El campo proporcionado y su nuevo nombre deben ser diferentes. Si son iguales, la operación falla con un error. Si un documento ya contiene un campo con el nuevo nombre proporcionado, se eliminará el campo existente.
```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$rename : {"num_mflix_comments" : "comments", "imdb_rating" : "rating"}},
  {returnNewDocument : true}
)
```
Con este operador rename, un campo también se puede mover hacia y desde documentos anidados. Para hacerlo, debe usar una notación de puntos:
```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$rename : {"rating" : "imdb.rating"}},
  {returnNewDocument : true}
)
```
5. El operador currentDate **$currentDate** se usa para establecer el valor de un campo dado como Date o timestamp. Si el campo aún no está presente, se creará. Proporcionar un nombre de campo con un valor de true insertará la fecha actual como una Date. Se puede usar un operador **$type** para especificar el valor como una Date o timestamp. La notación de puntos anida documentos.
```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$currentDate : {
       "created_date" : true,
       "last_updated.date" : {$type : "date"},
       "last_updated.timestamp" : {$type : "timestamp"},
  }},
  {returnNewDocument : true}
)
```
6. El operador de eliminacion **$unset** elimina todos los campos dados del documento coincidente. A medida que se eliminan los campos proporcionados, sus valores especificados no tienen ningún impacto.
```javascript
db.movies.findOneAndUpdate(
  {"title" : "Macbeth"},
  {$unset : {
    "created_date" : "",
    "last_updated" : "dummy_value",
    "box_office_collection": 142.2,
    "imdb" : null,
    "flag" : ""
  }},
  {returnNewDocument : true}
)
```

7. El otro operador de inserción **$setOnInsert** es similar a **$set**; sin embargo, solo establece los campos dados cuando ocurre una inserción durante una operación upsert. No tiene ningún impacto cuando la operación upsert da como resultado la actualización de documentos existentes. 
```javascript
db.movies.findOneAndUpdate(
  {"title":"Macbeth"},
  {
    $rename:{"comments":"num_mflix_comments"},
    $setOnInsert:{"created_time":new Date()}
  },
  {
    upsert : true,
    returnNewDocument:true
  }
)
```
El campo created_time no se agrega porque la operación upsert se usó para actualizar un documento existente.

Ahora vea este ejemplo:
```javascript
db.movies.findOneAndUpdate(
  {"title":"Spy"},
  {
    $rename:{"comments":"num_mflix_comments"},
    $setOnInsert:{"created_time":new Date()}
  },
  {
    upsert : true,
    returnNewDocument:true
  }
)
```
La única diferencia entre este fragmento y el anterior es que esta operación encuentra una película llamada Spy, que no está presente en nuestra colección. Debido a la actualización, la operación dará como resultado la adición de un documento a la colección. Y se ha creado un nuevo registro de película junto con el campo created_time.


## 🐥 6. Insertar, actualizar y eliminar campos Array <a name="actualizar_campos_array"></a>

### 🧡 Actualización de campos Array (Agregando un elemento a la vez con $push)

Insertemos el siguiente documento en la colección de movies:
```javascript
db.movies.insert({"_id" : 111, "title" : "Macbeth"})
```
Luego, con $set insertemos un nuevo campo array:
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$set : {"genre" : ["Unknown"]}},
    {"returnNewDocument" : true}
)
```
Con $unset podemos eliminar el campo ingresado previamente:
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$unset : {"genre" : ""}},
    {"returnNewDocument" : true}
)
 ```
Es útil cuando queremos reemplazar completamente un valor de matriz. Sin embargo, para agregar más elementos a una matriz, se puede usar un operador **$push**.

Para insertar un solo documento, agregue el siguiente comando:
```javascript
db.movies.findOneAndUpdate (
    {_id: 111},
    {$push: {"genre": "unknown"}},
    {"returnNewDocument": true}
)
```
Ahora agregue un género más, como sigue:
```javascript
db.movies.findOneAndUpdate (
    {_id: 111},
    {$push: {"genre": "Drama"}},
    {"returnNewDocument": true}
)
```

### 🧡 Actualización de campos Array (Agregando varios elementos a la vez con $push y $each)

Para agregar varios elementos a una matriz en un solo comando de actualización, tenemos que usar $push junto con $each.
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$push : {
        "genre" : {
            $each : ["History", "Action"]
        }}
    },
    {"returnNewDocument" : true}
)
```

### 🧡 Ordenar un Array con $sort

Las Arrays en MongoDB, y en general, son una colección que permanecerán en el orden en que fueron insertados. Con $push, también podemos ordenar un array. Hay que usar el operador $sort con $each.   
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$push : {
        "genre" : {
            $each : [],
            $sort : 1
        }}
    },
    {"returnNewDocument" : true}
)
```
Podemos agregar un elemento mas y luego ordenarlos:
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$push : {
        "genre" : {
            $each : ["Crime"],
            $sort : -1
        }}
    },
    {"returnNewDocument" : true}
)
```
Sin embargo, si tenemos una array de objetos que contiene varios campos, la clasificación se puede realizar en función de los campos de los objetos anidados. Considere el siguiente registro en una colección de items:
```javascript
db.items.insert({_id : 11, items: [
    {"name" : "backpack", "price" : 127.59, "quantity" : 3},
    {"name" : "notepad", "price" : 17.6, "quantity" : 4},
    {"name" : "binder", "price" : 18.17, "quantity" : 2},
    {"name" : "pens", "price" : 60.56, "quantity" : 3},
    
]})
```
`WriteResult({ "nInserted" : 1 })`

Vamos a ordenar el objeto items en funcion del precio:
```javascript
db.items.findOneAndUpdate(
    {_id : 11},
    {$push : {
        "items" : {
            $each : [],
            $sort : {"price" : -1}
        }}
    },
    {"returnNewDocument" : true}
)
```

### 🧡 Una Array como conjunto (set)

Un Array es una colección sobre los que se puede iterar o acceder a ellos utilizando su posición de índice específica. Un set es una colección de elementos únicos cuyo orden no está garantizado. MongoDB solo admite array simples y ningún otro tipo de colecciones. Sin embargo, es posible que desee que su matriz contenga solo elementos únicos. MongoDB proporciona una forma de hacerlo mediante el operador **$addToSet**.

El operador **$addToSet** es como $push, con la única diferencia de que un elemento se enviará solo si aún no está presente.
```javascript
db.movies.find({"_id" : 111}).pretty()
```
```
{
    "_id" : 111,
    "title" : "Macbeth",
    "genre" : [
        "unknown",
        "History",
        "Drama",
        "Crime",
        "Action"
    ]
}
```
Se va agregar el genero "Action" con $addToSet. En este caso no se actualizará lel array dado que $addToSet solo ingresará el elemento si no esta presente.
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$addToSet : {"genre" : "Action"}},
    {"returnNewDocument" : true }
)
```
El mismo comportamiento es evidente incluso cuando usamos $each para insertar varios elementos.
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$addToSet : {
        "genre" : {
            $each : ["History", "Thriller", "Drama"]
        }}
    },
    {"returnNewDocument" : true}
)
```
### 🧡 Eliminación de elementos de Arrays

## Eliminar El Primer o Último Elemento con $Pop

El operador $pop, cuando se usa en un comando de actualización, le permite eliminar el primer o último elemento de un array. Elimina un elemento a la vez y solo se puede usar con los valores 1 (para el último elemento) o -1 (para el primer elemento):
```javascript
db.movies.find({"_id" : 111}).pretty()
```
```
{
    "_id" : 111,
    "title" : "Macbeth",
    "genre" : [
        "unknown",
        "History",
        "Drama",
        "Crime",
        "Action",
        "Thriller"
    ]
}
```
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$pop : {"genre" : 1}},
    {"returnNewDocument" : true    }
)
```
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$pop : {"genre" : -1}},
    {"returnNewDocument" : true    }
)
```

## Eliminación De Todos Los Elementos con $pullAll

Cuando solo necesita eliminar ciertos elementos de un Array, puede usar el operador $pullAll. Para hacerlo, proporcione uno o más elementos al operador, que luego elimina todas las apariciones de esos elementos de la matriz. 
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$pullAll : {"genre" : ["Action", "Crime"]}},
    {"returnNewDocument" : true    }
)
```

## Eliminar Elementos Coincidentes con $pull

Usaremos $pull, para escribir una condición de consulta, usando varios operadores lógicos y condicionales, y luego se eliminarán los elementos del array que coinciden con la consulta. 
```javascript
db.items.find({"_id" : 11}).pretty()
```
```
{
    "_id" : 11,
    "items" : [
        {
            "name" : "backpack",
            "price" : 127.59,
            "quantity" : 3
        },
        {
            "name" : "pens",
            "price" : 60.56,
            "quantity" : 3
        },
        {
            "name" : "binder",
            "price" : 18.17,
            "quantity" : 2
        },
        {
            "name" : "notepad",
            "price" : 17.6,
            "quantity" : 4
        }
    ]
}
```
```javascript
db.items.findOneAndUpdate(
    {_id : 11},
    {$pull : {
        "items" : {
            "quantity" : 3,
            "name" : {$regex: "ck$"}
        }
    }},
    {"returnNewDocument" : true    }
)
```

### 🧡 Actualización de elementos Array segun su indice

En un Array, cada elemento tiene una posición de índice específica que comienzan en cero, y podemos usar un par de corchetes ( \[ ] ) con la posición de índice respectiva para referirnos a un elemento de la matriz. El uso de este par de corchetes con $set permite actualizar elementos de un array. 

Considere el siguiente fragmento:
```javascript
db.movies.find({"_id" : 111})
```
```
{ "_id" : 111, "title" : "Macbeth", "genre" : [ "History", "Drama" ] }
```
El operador $\[] se refiere a todos los elementos contenidos en un array y la expresión de actualización se aplicará a todos ellos. El array género sigue siendo una matriz de dos elementos.
```javascript
db.movies.findOneAndUpdate(
    {_id : 111},
    {$set : {"genre.$[]" : "Action"}},
    {"returnNewDocument" : true}
)
```
```
{ "_id" : 111, "title" : "Macbeth", "genre" : [ "Action", "Action" ] }
```
Para ctualizar elementos específicos de una matriz primero debemos encontrar dichos elementos e identificarlos. Para derivar un **identificador** de elemento, podemos usar la opción de actualización de **arrayFilters** para proporcionar una condición de consulta y asignarle una variable (conocida como **identificador**) a los elementos coincidentes. Luego usamos el identificador junto con $\[] para actualizar los valores de esos elementos específicos.

Considere el siguiente el siguiente fragmento:
```javascript
db.items.findOneAndUpdate(
    {"_id" : 11},
    {$push : {"items" : {"name" : "it"}}},
    {"returnNewDocument": true}
)
```
```
{
    "_id" : 11,
    "items" : [
        {
            "name" : "pens",
            "price" : 60.56,
            "quantity" : 3
        },
        {
            "name" : "binder",
            "price" : 18.17,
            "quantity" : 2
        },
        {
            "name" : "notepad",
            "price" : 17.6,
            "quantity" : 4
        },
        {
            "name" : "it"
        }
    ]
}
```
El elemento del array que se actualizará se denomina mediante una expresión de **$\[myElements]** y se le asigna un nuevo valor, que es un objeto anidado. El **identificador** de **myElements** se define mediante un **arrayFilters** en función de una condición de consulta. Todos los elementos que coinciden con la condición dada son identificados por myElements, que luego se actualizan usando $set:
```javascript
db.items.findOneAndUpdate(
    {_id : 11},
    {$set : {
        "items.$[myElements]" : {
            "quantity" : 7,
            "price" : 4.5,
            "name" : "marker"
        }
    }},
    {
        "returnNewDocument" : true,
        "arrayFilters" : [{"myElements.quantity" : null}]
    }
)
```
La condición de consulta de **{quantity: null}** coincide con el último elemento de la matriz y se ha actualizado con el nuevo documento.


## 🐥 7. Data Aggregation <a name="data_aggregation"></a>

La **aggregation pipeline** le permite definir una serie de etapas que filtran, fusionan y organizan datos con mucho más control que el comando de find estándar.

El comando **aggregate** en MongoDB es similar al comando de find.

El elemento clave de la agregación se llama **pipeline**. Un **pipeline** es una serie de instrucciones, donde la entrada a cada instrucción es la salida de la anterior. La agregación es un método para tomar una colección y, de manera procedimental, filtrar, transformar y unir datos de otras colecciones para crear conjuntos de datos nuevos y significativos.

### 🧡 Aggregate Syntax

El comando aggregate opera en una colección como los otros comandos Create, Read, Update, Delete (CRUD):
```javascript
var pipeline = [] // Pipeline es una matriz de etapas.
var options = {} 
```
```javascript
db.movies.aggregate(pipeline, options)
```

Hay dos **parámetros** que se utilizan para la agregación:

El parámetro de **Pipeline** contiene toda la lógica para encontrar, ordenar, proyectar, limitar, transformar y agregar nuestros datos. El propio parámetro de Pipeline se pasa como una matriz de documentos JSON. Puede pensar en esto como una serie de instrucciones que se enviarán a la base de datos, y luego los datos resultantes después de la etapa final se almacenan en un cursor que se le devuelve. Cada etapa de la tubería se completa de forma independiente, una tras otra, hasta que no quede ninguna. La entrada a la primera etapa es la colección (por ejemplo movies) y la entrada a cada etapa posterior es la salida de la etapa anterior.

El segundo parámetro es el parámetro de **opciones**. Esto es opcional y le permite especificar los detalles de la configuración, como cómo se debe ejecutar la agregación o algunos indicadores que se requieren durante la depuración y la construcción de sus canalizaciones.

Los parámetros de un comando agregado son menores que los del comando de búsqueda. Por ahora podemos simplificar nuestro comando excluyendo las opciones por completo:
```javascript
db.movies.aggregate(pipeline)
```
En lugar de escribir la canalización directamente en el comando aggregate, primero guardamos la canalización como una variable. Las canalizaciones de agregación pueden volverse muy grandes y difíciles de analizar durante el desarrollo. A veces puede ser útil separar la canalización (o incluso grandes secciones de la canalización) en variables independientes para la claridad del código. 

### 🧡 Pipeline Syntax

La canalización (Pipeline) es un array, y cada elemento del array es un objeto:
```javascript
var pipeline = [
        { . . . },
        { . . . },
        { . . . },
];
```
Cada uno de los objetos del array representa una única etapa en la canalización general, y las etapas se ejecutan en su orden de matriz (de arriba a abajo). Cada objeto de escenario tiene la forma siguiente:
```
{$etapa : parametros}
```
La $etapa representa la acción que queremos realizar sobre los datos (como limitar u ordenar) y los parámetros pueden ser un valor único u otro objeto, dependiendo de la etapa.

La canalización se puede pasar de dos formas, ya sea como una variable guardada o directamente como un comando.
```javascript
var pipeline = [
        { $match: { "location.address.state": "MN"} },
        { $project: { "location.address.city": 1 } },
        { $sort: { "location.address.city": 1 } },
        { $limit: 3 }
     ];
```
Luego, escribir el comando db.theaters.aggregate(pipeline) en el shell de MongoDB proporcionará el siguiente resultado:
```javascript
db.theaters.aggregate(pipeline)
```
```javascript
{ "_id" : ObjectId("59a47287cfa9a3a73e51e94f"), "location" : { "address" : { "city" : "Apple Valley" } } }
{ "_id" : ObjectId("59a47287cfa9a3a73e51eb8f"), "location" : { "address" : { "city" : "Baxter" } } }
{ "_id" : ObjectId("59a47286cfa9a3a73e51e833"), "location" : { "address" : { "city" : "Blaine" } } }
```
Pasándolo directamente al comando aggregate, la salida se verá de la siguiente manera: 
```javascript
db.theaters.aggregate([
  { $match: { "location.address.state": "MN"} },
  { $project: { "location.address.city": 1 } },
  { $sort: { "location.address.city": 1 } },
  { $limit: 3 }
]);
```
```javascript
{ "_id" : ObjectId("59a47287cfa9a3a73e51e94f"), "location" : { "address" : { "city" : "Apple Valley" } } }
{ "_id" : ObjectId("59a47287cfa9a3a73e51eb8f"), "location" : { "address" : { "city" : "Baxter" } } }
{ "_id" : ObjectId("59a47286cfa9a3a73e51e833"), "location" : { "address" : { "city" : "Blaine" } } }
```
Como puede ver, obtiene el mismo resultado con cualquiera de los métodos.

### 🧡 Creando agregaciones

El siguiente código nos ayudará a obtener una lista de todos los cines del estado de Minnesota (MN) usando la coleccion de **theaters**
```javascript
var simpleFind = function() {
    print("Find Result:")
    db.theaters.find(
          {"location.address.state" : "MN"},
          {"location.address.city" : 1} )
    .sort({"location.address.city": 1})
    .limit(3)
    .forEach(printjson);
}
simpleFind();
```
Ejecutando la funcion:
```javascript
simpleFind();

Find Result:
{
        "_id" : ObjectId("59a47287cfa9a3a73e51e94f"),
        "location" : {
                "address" : {
                        "city" : "Apple Valley"
                }
        }
}
{
        "_id" : ObjectId("59a47287cfa9a3a73e51eb8f"),
        "location" : {
                "address" : {
                        "city" : "Baxter"
                }
        }
}
{
        "_id" : ObjectId("59a47286cfa9a3a73e51e7e2"),
        "location" : {
                "address" : {
                        "city" : "Blaine"
                }
        }
}
```
Reconstruyamos este comando como una agregación. 
```javascript
var simpleFindAsAggregate = function() {
    print ("Aggregation Result:")
    var pipeline = [
        { $match: { "location.address.state": "MN"} },
        { $project: { "location.address.city": 1 } },
        { $sort: { "location.address.city": 1 } },
        { $limit: 3 }
    ];
    db.theaters.aggregate(pipeline).forEach(printjson);
}; 

simpleFindAsAggregate();
```
Los comandos **find** y **aggregate** devuelven un **cursor**, pero estamos usando **.forEach (printjson)**; al final para imprimirlos en la consola para facilitar su comprensión.

La etapa $match al comienzo de la canalización es el equivalente a nuestro documento de filtro.

### 🧡 Agrupaciones - La etapa Group

Si desea responder preguntas complejas o extraer el mayor valor posible de sus datos, necesitará saber cómo lograr la parte de agregación de sus canales de agregación.

La etapa **$group** le permite agrupar (o agregar) documentos en función de una condición específica. 

La implementación básica de la etapa $group acepta solo una clave \_id , siendo el valor una expresión. 

Esta expresión define los criterios por los cuales la canalización agrupa los documentos. 

Este valor se convierte en el \_id del documento recién generado con un documento generado para cada \_id único que crea la etapa $group.

En términos de agregación, una expresión puede ser un literal, un objeto de expresión, un operador o una ruta de campo ($rated). Una ruta de campo es a qué campo acceder en los documentos de entrada.

Al agregar, necesitamos decirle a la canalización que queremos acceder al campo del documento que está agregando actualmente. 

En el siguiente código agrupará todas las películas por su clasificación, generando un solo registro para cada categoría de clasificación:
```javascript
var pipeline = [
     {$group: {
         _id: "$rated"
     }}
    ];
    
db.movies.aggregate(pipeline).forEach(printjson);
```
\_id: "$Rated" como equivalente a \_id: "$$CURRENT.rated". Para cada documento, encajará en el grupo que empareja ese mismo documento (actual) con la clave "rated" 

### 🧡 Expresiones de acumulador

El comando $group puede aceptar más de un argumento. También puede aceptar cualquier número de argumentos adicionales en el siguiente formato:
```
field: { $accumulator: expression}
```
Dividamos esto en sus tres componentes:

• field definirá la clave de nuestro campo recién calculado para cada grupo.

• El acumulador debe ser un operador de acumulador compatible. Se trata de un grupo de operadores, como otros operadores con los que ya puede haber trabajado, como $lte , excepto que, como sugiere el nombre, acumularán su valor en varios documentos que pertenecen al mismo grupo.

• La expresión en este contexto se pasará al operador del acumulador como la entrada de qué campo en cada documento debería estar acumulando.
```javascript
var pipeline = [
     {$group: {
         _id: "$rated",
         "numTitles": {$sum: 1},
     }}
    ];
db.movies.aggregate(pipeline).forEach(printjson);
```
**numTitles** es el valor de este campo para cada grupo la suma de los documentos.  Estos campos recién creados a menudo se denominan campos calculados. Para cada documento de un grupo, podemos sumar el valor literal 1 con el resultado acumulado hasta el momento.

Del mismo modo, en lugar de acumular 1 en cada documento, puede acumular el valor de un campo determinado.
```javascript
var pipeline = [
     {$group: {
         _id: "$rated",
         "sumRuntime": { $sum: "$runtime"},
     }}
    ];
    
db.movies.aggregate(pipeline).forEach(printjson);
```
Queremos obtener el average runtime de los títulos para cada uno de nuestros grupos. Podemos cambiar nuestro acumulador de $sum a $avg, que devolverá el tiempo de ejecución promedio en cada grupo, por lo que nuestra canalización se convierte en el siguiente:
```javascript
 var pipeline = [
  {$group: {
     _id: "$rated",
     "avgRuntime": { $avg: "$runtime"},
  }}
 ];

db.movies.aggregate(pipeline).forEach(printjson);
``` 

Agreguemos otra etapa para proyectar el tiempo de ejecución, usando la etapa $trunc, para darnos un valor entero:
```javascript
 var pipeline = [
     {$group: {
         _id: "$rated",
         "avgRuntime": { $avg: "$runtime"},
     }},
     {$project: {
         "roundedAvgRuntime": { $trunc: "$avgRuntime"}
     }}
    ];

db.movies.aggregate(pipeline).forEach(printjson);
```
Esto nos dará un resultado mucho mejor formateado, como este:
```
{"_id": "PG-13", "avgRuntime": 108}
```

## 🐥 8. Joins entre colecciones con $lookup <a name="joins_colecciones"></a>

### 🧡 Usando $lookup para hacer joins

En MongoDB, los joins de colecciones se realizan mediante el paso de agregación **$lookup**.
```javascript
var lookupExample = function() {
    var pipeline = [
        { $match: { $or: [{"name": "Catelyn Stark"}, {"name": "Ned Stark"}]}},
        { $lookup: {
            from: "comments",
            localField: "name",
            foreignField: "name",
            as: "comments"
        }},
  { $limit: 2},
    ];
db.users.aggregate(pipeline).forEach(printjson);
}

lookupExample();
```

Primero, estamos ejecutando un $match en la colección de **users** para obtener solo dos usuarios llamados Ned Stark y Catelyn Stark. Una vez que tenemos estos dos registros, realizamos nuestra búsqueda en la otra colección **comments**. Los cuatro parámetros de $lookup son los siguientes:

• **from**: La colección que estamos joining a nuestra agregación actual. En este caso, estamos trayendo los comentarios a los usuarios.

• **localField**: el nombre del campo que vamos a utilizar para unir nuestros documentos en la colección local (la colección en la que estamos ejecutando la agregación: users). En este caso, el **name** de nuestro usuario.

• **ForeignField**: el campo que enlaza con localField en la colección from (comments). Estos pueden tener diferentes nombres, pero en este escenario, es el mismo campo: name.

• **as**: así es como se etiquetarán nuestros nuevos datos combinados.

En este ejemplo, la búsqueda toma el nombre de nuestro usuario, busca en la colección de comentarios y agrega cualquier comentario con el mismo nombre en un nuevo campo array para el documento de usuario original. Esta nueva array se llama **comments**. De esta manera, podemos buscar un array de todos los documentos relacionados en otra colección e incrustarlos en nuestros documentos originales para usarlos en el resto de nuestra agregación.

### 🧡 Usando $unwind para deconstruir un campo array anidado

En este ejemplo, los usuarios han hecho muchos comentarios, por lo que la matriz incrustada se vuelve bastante sustancial y difícil de ver. 

Estas uniones a menudo pueden dar como resultado grandes conjuntos de documentos relacionados. 

El operador **$unwind**  es una etapa relativamente simple. Deconstruye un campo de matriz de un documento de entrada para generar un nuevo documento para cada elemento de la matriz. 

Un ejemplo de $unwind seria:

```
{a: 1, b: 2, c: [1, 2, 3, 4]}

La salida serán los siguientes documentos:
{"a" : 1, "b" : 2, "c" : 1 }
{"a" : 1, "b" : 2, "c" : 2 }
{"a" : 1, "b" : 2, "c" : 3 }
{"a" : 1, "b" : 2, "c" : 4 }
```
```javascript
var lookupExample = function() {
    var pipeline = [
        { $match: { $or: [{"name": "Catelyn Stark"}, {"name": "Ned Stark"}]}},
        { $lookup: {
            from: "comments",
            localField: "name",
            foreignField: "name",
            as: "comments"
        }},
        { $unwind: "$comments"},
        { $limit: 3},
    ];
    db.users.aggregate(pipeline).forEach(printjson);
}

lookupExample();
```

### 🧡 Generación de resultados con $out

Con $out nos permiten tomar la salida de nuestra canalización y escribirla en una colección para su uso posterior. 

La sintaxis de $out es muy simple. El único parámetro es la colección a la que queremos enviar nuestro resultado. 

A continuación, se muestra un ejemplo de una canalización con $out:
```javascript
var findTopRomanceMovies = function() {
    var pipeline = [
        { $sort: {"imdb.rating": -1}},
        { $match: {
            genres: {$in: ["Romance"]},
            released: {$lte: new ISODate("2001-01-01T00:00: 00Z") }}},
        { $limit: 5 },
        { $project: { title: 1, genres: 1, released: 1, "imdb.rating": 1}},
        { $out: "movies_top_romance"}
    ];
    db.movies.aggregate(pipeline).forEach(printjson);
}
findTopRomanceMovies();
```
Al ejecutar esta canalización, no recibirá ningún resultado. Esto se debe a que la salida se ha redirigido a nuestra colección deseada:
```
findTopRomanceMovies();

```
Podemos ver que se creó una nueva colección con nuestro resultado:
```
show collections
```
```
comments
movies
movies_top_romance
sessions
theaters
users
```
Y si ejecutamos una búsqueda en nuestra nueva colección, podemos ver que los resultados de nuestra agregación ahora se almacenan dentro de ella:
```javascript
db.movies_top_romance.findOne({})
{
        "_id" : ObjectId("573a1399f29313caabceeead"),
        "genres" : [
                "Drama",
                "Romance"
        ],
        "title" : "Pride and Prejudice",
        "released" : ISODate("1996-01-14T00:00:00Z"),
        "imdb" : {
                "rating" : 9.1
        }
}
```
Al colocar nuestros resultados en una colección, podemos almacenar, compartir y actualizar nuevos resultados de agregación complejos. Incluso podemos ejecutar más consultas y agregaciones contra esta nueva colección, $out es una etapa de agregación simple pero poderosa.

Ejercicio: Enlistar las películas más comentadas por los usuarios

La empresa de cine desea saber más sobre qué películas generan más comentarios por parte de sus usuarios. Sin embargo, dados los muchos comentarios en la base de datos, ha decidido que mientras desarrolla esta canalización, usará solo una muestra de los comentarios. A partir de esta muestra, averiguará las películas más comentadas y unirá estos documentos con el documento de la colección de películas para obtener más información sobre la película. La empresa también ha solicitado que la entrega final de su trabajo sea una nueva colección con los documentos de salida. 

```javascript
var findMostCommentedMovies = function() {
    print("Finding the most commented on movies.");
    var pipeline = [
             { $sample: {size: 5000}},
             { $group: {
                 _id: "$movie_id",
                 "sumComments": { $sum: 1}
             }},
             { $sort: { "sumComments": -1}},
             { $limit: 5},
             { $lookup: {
                 from: "movies",
                 localField: "_id",
                 foreignField: "_id",
                 as: "movie"
             }},
             { $unwind: "$movie" },
             { $project: {
                 "movie.title": 1,
                 "movie.imdb.rating": 1,
                 "sumComments": 1,
             }},
             { $out: "most_commented_movies" }
    ];
    db.comments.aggregate(pipeline).forEach(printjson);
}
findMostCommentedMovies();

db.most_commented_movies.find()
```

## 🐥 9. Bibliografía <a name="bibliografia"></a>

MongoDB Fundamentals: A hands-on guide to using MongoDB and Atlas in the real world. Packt Publishing (22 Diciembre 2020). 

https://docs.mongodb.com/manual/tutorial/getting-started/

