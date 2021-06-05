# 🦄 Apuntes de NoSql con MongoDB 

## 🐥 1. Introducción a NoSql con MongoDB 

Hay dos tipos de bases de datos: bases de datos relacionales y no relacionales. Las **no relacionales** a menudo se denominan bases de datos **NoSQL**. 

Una base de datos NoSQL se utiliza para almacenar grandes cantidades de datos complejos y diversos, como catálogos de productos, registros, interacciones de usuarios, análisis y más. 

**MongoDB** es una de las bases de datos NoSQL más establecidas, con características como agregación de datos, transacciones ACID ( Atomicity, Consistency, Isolation, Durability).

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/Sql%20y%20NoSql.jpg)

### 🔥 MongoDB

MongoDB es una popular base de datos **NoSQL** que puede almacenar datos estructurados y no estructurados. Fundada en 2007 por Kevin P. Ryan, Dwight Merriman y Eliot Horowitz en Nueva York, la organización se llamó inicialmente 10gen y luego se renombró como MongoDB, una palabra inspirada en el término **humongous**.

Su diseño basado en **documentos** hace que sea fácil de entender y usar. Su sintaxis intuitiva para consultas y comandos hace que sea fácil de aprender.

### 🔥 Descarga e instalación de MongoDB

**👉Paso 1: Descargar e instalar la versión Community Server**

Ir al página oficial de MongoDB https://www.mongodb.com/try/download/community

En este video de youtube te indica paso a paso como descargar e instalar y algunas consideraciones a tomar en cuenta: [https://www.youtube.com/watch?v=Y3RUzKNiiIA&ab_channel=programadornovato](https://www.youtube.com/watch?v=Y3RUzKNiiIA)

**👉Paso 2. Encender el servidor de MongoDB**

La opción fácil de encender el servidor de mongo es ir a la carpeta de tu PC donde se instaló Mongo y abrir el archivo ejecutable **mongod**. 
Debes seguir esta ruta para buscar el archivo ejecutable: 
```
C:\Program Files\MongoDB\Server\4.4\bin
```
Dentro de la carpeta **bin** se encuentra los archivos ejecutables: **mongod** y **mongo**

Antes de abrir ejecutar el archivo **mongod** hay que hace un paso previo. Deberás crear en el **disco C** una carpeta llamada **data** y dentro de esta otra capeta llamada **db**.
```
C:\data\db
```
Ahora si, abrir el archivo ejecutable **mongod** y te saldrá la clásica pantalla negra.

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/consola%20mongo.PNG)

En esta pantalla te mostrará que el servidor de mongo esta encendido y está esperando que alguien se conecte. (No debes cerrar esta pantalla)

**👉Paso 3. Abrir la consola y conectarse al servidor**

Ahora deberás abrir el otro ejecutable de la carpeta bin llamada: **mongo**. Este ejecutable es una **consola o terminal** para poder trabajar (la clásica pantalla negra).

Escribimos en la consola **2+2** para probar que funciona.

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/consola%20mongod.png)

Para interactuar con servidor de MongoDB además de la consola clásica (ventana negra) hay aplicaciones con entorno visual para comodidad del usuario como **MongoDB Compass**

**👉MongoDB Compass**

El MongoDB Compass es un entorno visual e intuitivo para interactuar con el servidor. Generalmente se instala junto cuando se instala MongoDB.

Para usar MongoDB Compass debes abrir el programa y conectarte a tu servidor de mongo. Para esto hay que copiar el string que te apareció previamente en la consola de mongo: 
```
mongodb://127.0.0.1:27017 
```
Luego clic en Connect y listo. Ahora podrás crear tu propia base de datos o subir un archivo de base de datos.

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/mongo%20compass.PNG)

En la seccion 3 veremos como crear una base de datos mediante la consola y con la interfaz de MongoDB Compass.


## 🐥 2. Documentos y tipos de datos

Una de las características de **MongoDB** es su modelo de datos basado en **documentos**, que son aceptados como una forma flexible de transportar información. 

Muchas aplicaciones que intercambian datos en forma de documentos **JavaScript Object Notation ( JSON )**. MongoDB almacena datos en formato **JSON binario (BSON)** y los representa en JSON legible por humanos.

### 😻 Sintaxis JSON

Los documentos u objetos **JSON** son un conjunto de texto sin formato de pares **clave-valor**. 

JSON tiene una estructura de un conjunto de llaves ( { } ), corchetes ( [ ] ), dos puntos ( : ), y comas ( , ). 

En un objeto JSON, los pares **clave-valor** están encerrados con llaves { }. La **clave** es siempre una cadena de texto y el **valor** puede ser cualquier **tipo** especificado por JSON.

```javascript
{ key : value }
```
Un **array** es un conjunto de valores encerrados entre corchetes [ ] y separados por comas. JSON no especifica el orden de los elementos del array.

```
[ value1, value2, value3 ]
```
Un ejemplo de un documento JSON que contiene la información básica de una empresa:

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

- **👉String**: se refiere a texto sin formato
- **👉Number**: consta de todos los campos numéricos
- **👉Boolean**: valores true o false
- **👉Object**: otros objetos JSON incrustados
- **👉Array**: colección de campos
- **👉Null**: valor especial para denotar campos sin ningún valor

JSON es un formato de intercambio de datos. La presencia de tipos de datos básicos proporcionados por JSON reduce la complejidad durante este proceso. Por eso se mantiene simple y mínimo en términos de tipos de datos.

### 😻 JSON y números

En los documentos JSON, un número es solo una secuencia de dígitos. No distingue entre números como enteros o flotantes. 

### 😻 JSON y fechas

En los documentos JSON no admite un tipo de datos Fecha y estas solo se representan como cadenas simples. Ejemplos:

```javascript
{"title": "A Swedish Love Story", released: "1970-04-24"}
{"title": "A Swedish Love Story", released: "24-04-1970"}
{"title": "A Swedish Love Story", released: "24th April 1970"}
{"title": "A Swedish Love Story", released: "Fri, 24 Apr 1970"}

```
Las partes que intercambian la información deben estandarizar el formato fecha durante las transferencias. La forma de leer los datos depende de los intérpretes de los idiomas y de sus contratos de intercambio de datos.

### 💪 Ejercicio: Creación de tu propio documento JSON

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
Recuerde, un documento JSON siempre comienza con { y termina con }. Cada elemento está separado por dos puntos ( : ) y los pares de valores clave están separados por una coma ( , ).

Haga clic en **Validar JSON** para validar el código.

### 😻 Documentos de MongoDB

Una base de datos MongoDB se compone de **colecciones** y **documentos**. Una base de datos puede tener una o más colecciones, y cada colección puede almacenar uno o más documentos relacionados.

En comparación con RDBMS, las **colecciones** son análogas a las **tablas** y los **documentos** son análogos a las **filas** dentro de una tabla. Sin embargo, los documentos son mucho más flexibles en comparación con las filas de una tabla.

### 😻 Tipos de datos de MongoDB

MongoDB almacena documentos similares a JSON.

**👉Strings**: en MongoDB, los campos de cadena están codificados en UTF-8. Ademas, admiten capacidades de búsqueda con expresiones regulares. Ejemplo:

```javascript
{ "name" : "Tom Walter" }
```

**👉Numbers**: En MongoDB se admite los varios tipos de números.

double: punto flotante de 64 bits
int: entero de 32 bits con signo
long: entero sin signo de 64 bits
decimal: punto flotante de 128 bits, que cumple con IEE 754

**👉Booleans**: se utiliza para representar si algo es verdadero o falso. Ejemplo:

```javascript
{ "isMongoDBHard": false }
```

**👉Objects**: Los campos de objeto se utilizan para representar documentos **ANIDADOS** o **INCRUSTADOS,** es decir, un campo cuyo valor es otro documento JSON válido. 
Ejemplo: El siguiente documento tiene otro documento anidado llamado **"host"**

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
El valor del campo de host es otro documento de JSON. MongoDB usa una notación de puntos ( . ) para acceder a los objetos incrustados. 

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

**👉Array**: es una colección de cero o más valores que deben estar encerrado con corchetes \[ ]. En MongoDB, no hay límite para la cantidad de elementos que puede contener un array o la cantidad de arrays que puede tener un documento. Sin embargo, el tamaño total del documento no debe exceder los 16 MB.

Considere la siguiente array que contiene cuatro números:

```javascript
var doc = { first_array: [ 4, 3, 2, 1 ] }
```
Se puede acceder a cada elemento de un array utilizando su posición de índice. El número de índice se incluye entre corchetes. (Los índices empiezan desde 0). Accedamos al tercer elemento del array:

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

Al igual que los objetos que tienen objetos incrustados, los arrays también pueden tener arrays incrustadas. La siguiente sintaxis agrega un array incrustado en el sexto elemento:

```javascript
doc.first_array[5] = [11, 12]
```
Si imprime el array, verá la array incrustada de la siguiente manera:

```javascript
doc.first_array
```
`[4, 3, 2, 1, 99, [11, 12]]`

Ahora, puede usar la notación de corchetes, \[ ] , para acceder a los elementos de un índice específico. En este ejemplo queremos acceder al primer elemento del quinto elemento del array anidado.
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

## 🐥 3. Creando tu propia base datos en MongoDB

### ⚡ Conociendo comandos básicos

Primero debe tener abierto la consola de mongo para comenzar a escribir los comandos.

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

- El comando **`bd`** muestra en que base datos estamos actualmente. Al incio indicará que estamos en un entorno de **test**.
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
```
use Sample1
```

- El comando **`show collections`** muestra las **COLECCIONES** (TABLAS) de la base datos **Sample1**. En este caso tenemos 2 colecciones: comments y movies.
```
show collections
```
![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/show%20collections.PNG)

### ⚡ Creando una base datos sencilla

- Para crear una base datos tambien se usa el comando **`use`** junto al nombre de la nueva base datos.
```
use mibase
```
- Si ejecuta el comando **`show dbs`** aún no aparecerá en el listado debido que se debe crear una colección (o tabla).

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

### ⚡ Subir una coleccion (documento JSON) a la base datos

**👉Pimero**, deberás descargar las colecciones (archivo JSON) **movies.json** y **comments.json** para subirla a la base datos **Sample** que deberás crear.

- **movies**: [link de descarga](https://raw.githubusercontent.com/zpio/mongodb-sample-dataset/main/sample_mflix/movies.json)

- **comments**: [link de descarga](https://raw.githubusercontent.com/zpio/mongodb-sample-dataset/main/sample_mflix/comments.json)

**👉Segundo** cree una base datos en la consola llamada **Sample**.

Una forma muy intuitiva de subir colecciones a partir de un documento JSON a nuestra base datos es con el programa **Mongo Compass**.

**👉Tercero**, deberás abrir Mongo Compass y conectarte con servidor de Mongo. Una vez ahi, deberas crear las colecciones en la base datos **Sample** y subir los archivos JSON respectivamente.

Listo, ya tienes una base datos con 2 colecciones para comenzar a hacer las respectivas consultas, filtros, actualización, etc.


## 🐥 4. Consulta de documentos (Querying Documents)

### 🧡 Estructura de consulta MongoDB

Las consultas de MongoDB se basan en documentos JSON. El siguiente diagrama es un ejemplo de una consulta simple de MongoDB que encuentra todos los documentos donde el campo de **name** contiene el valor **David**:

![](https://github.com/zpio/Apuntes_NoSql_con_MongoDB/blob/main/imagenes/formato%20find.jpg)

En sintaxis SQL seria:

`SELECT * FROM USERS WHERE name = 'David';`

MongoDB no tienen palabras clave como **SELECT**, **FROM** y **WHERE**.

### 🧡 Consultas básicas de MongoDB

Todas las consultas de esta sección son consultas de nivel superior; es decir, se basan en los campos de nivel superior (también conocidos como nivel raíz) de los documentos.

**👉 Mostrar documentos - función find()**

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
        "text" : "Sit ullam tenetur atque delectus. Pariatur eos sequi enim. Quasi eligendi labore saepe rerum modi incidunt accusamus ex. Expedita temporibus consequatur dolore modi.",
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
**👉 Elegir los campos para la salida - projection**

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
db.movies.distinct("rated", {"year" : 1994})
```
```
[ "G", "NOT RATED", "PG", "PG-13", "R", "TV-14", "TV-PG", "UNRATED" ]
```
**👉Contando los documentos - count**

La función **count** se utiliza para devolver el recuento de documentos dentro de una colección o un recuento de los documentos que coinciden con la consulta dada. Cuando se ejecuta sin ningún argumento de consulta, devuelve el recuento total de documentos en la colección.

```javascript
db.movies.count()
```
` 23539 `

Devolver el recuento de películas que tienen exactamente 6 comentarios:
```javascript
db.movies.count({"num_mflix_comments" : 6})
```
` 17 `

En MongoDB v4.0 countDocuments( ) devuelve el recuento de documentos que coinciden con la condición dada. Un argumento de consulta es obligatorio db.movies.countDocuments( ) no es valido y fallara.
```javascript
db.movies.countDocuments ({"year": 1999})
```
` 542 ` 

**👉Operadores condicionales**

👉 **Equals ($eq)** (Operador de Igualdad)

Devolver películas cuyo recuento de comentarios sea igual a 5. Ambas consultas tienen el mismo efecto:
```javascript
db.movies.find({"num_mflix_comments" : 5})

db.movies.find({"num_mflix_comments" : {$eq : 5 }})
```

👉 **Not Equal To ($ne)**

Devolver películas cuyo recuento de comentarios no sea igual a 5:
```javascript
db.movies.find(
    { "num_mflix_comments" :
        {$ne : 5 }
    }
)
```

👉 **Greater Than ($gt) and Greater Than or Equal To ($gte)**
```javascript
db.movies.find(
    {year : {$gt : 2015}}
).count()
```
`1`
```javascript
db.movies.find(
    {year : {$gte : 2015}}
).count()
```
`485`

Contar las películas que se estrenaron en el siglo XXI (desde el 1 de enero de 2000):
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

Todas las películas que han sido clasificadas como G, PG o PG-13:
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
La consulta anterior devuelve películas que no están clasificadas como G , PG o PG-13, incluidas las que no tienen el campo rated

Para ver qué sucede cuando usa `$nin` con un campo inexistente, primero, busque el total de documentos que tiene, de la siguiente manera:
```javascript
db.movies.countDocuments ({})
23539
```
Ahora, use `$nin` con algunos valores, excepto null, en un objeto inexistente. Esto significa que todos los documentos coinciden.
```javascript
db.movies.countDocuments(
    {"nef" :
        {$nin : ["a value", "another value"]}
    }
)
```
`23539`

Ahora, agregue un valor null a la matriz `$nin`:
```javascript
db.movies.countDocuments(
    {"nef" :
        {$nin : ["a value", "another value", null ]}
    }
)
```
`0`

Esta vez, no coincidió con ningún documento. Esto se debe a que, en MongoDB, un campo inexistente siempre tiene un valor de nulo, por lo que la condición `$nin` no se cumplió para ninguno de los documentos.

💪 **Ejercicio: Consulta de películas de un actor**

Encuentre el numero de películas en las que aparece Leonardo DiCaprio usando el campo de cast.
```javascript
db.movies.countDocuments ({"cast": "Leonardo DiCaprio"})
```
`25`

Encuentre los género de estas películas, devuelva un array.
```javascript
db.movies.distinct("genres", {"cast" : "Leonardo DiCaprio"})
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



















