# Apuntes de NoSql con MongoDB 

## 1. Introducción a NoSql con MongoDB 

Hay dos tipos de bases de datos: bases de datos relacionales y no relacionales. Las **no relacionales** a menudo se denominan bases de datos **NoSQL**. 

Una base de datos NoSQL se utiliza para almacenar grandes cantidades de datos complejos y diversos, como catálogos de productos, registros, interacciones de usuarios, análisis y más. 

**MongoDB** es una de las bases de datos NoSQL más establecidas, con características como agregación de datos, transacciones ACID ( Atomicity, Consistency, Isolation, Durability).

### MongoDB

MongoDB es una popular base de datos **NoSQL** que puede almacenar datos estructurados y no estructurados. Fundada en 2007 por Kevin P. Ryan, Dwight Merriman y Eliot Horowitz en Nueva York, la organización se llamó inicialmente 10gen y luego se renombró como MongoDB, una palabra inspirada en el término **humongous**.

Su diseño basado en **documentos** hace que sea fácil de entender y usar. Su sintaxis intuitiva para consultas y comandos hace que sea fácil de aprender.

## 2. Documentos y tipos de datos

Una de las características de **MongoDB** es su modelo de datos basado en **documentos**, que son aceptados como una forma flexible de transportar información. 

Muchas aplicaciones que intercambian datos en forma de documentos **JavaScript Object Notation ( JSON )**. MongoDB almacena datos en formato **JSON binario (BSON)** y los representa en JSON legible por humanos.


### Sintaxis JSON

Los documentos u objetos **JSON** son un conjunto de texto sin formato de pares **clave-valor**. 

JSON tiene una estructura de un conjunto de llaves ( { } ), corchetes ( [ ] ), dos puntos ( : ), y comas ( , ). 

En un objeto JSON, los pares **clave-valor** están encerrados con llaves { }. La **clave** es siempre una cadena de texto y el **valor** puede ser cualquier **tipo** especificado por JSON.

```
{ key : value }
```
Un **array** es un conjunto de valores encerrados entre corchetes [ ] y separados por comas. JSON no especifica el orden de los elementos del array.

```
[ value1, value2, value3 ]
```
Un ejemplo de un documento JSON que contiene la información básica de una empresa:

```
{
  "company_name" : "Sparter",
  "founded_year" : 2007,
  "twitter_username" : null,
  "address" : "15 East Street",
  "no_of_employees" : 7890,
  "revenue" : 879423000
}
```

### Tipos de datos JSON

- **String**: se refiere a texto sin formato
- **Number**: consta de todos los campos numéricos
- **Boolean**: valores true o false
- **Object**: otros objetos JSON incrustados
- **Array**: colección de campos
- **Null**: valor especial para denotar campos sin ningún valor

JSON es un formato de intercambio de datos. La presencia de tipos de datos básicos proporcionados por JSON reduce la complejidad durante este proceso. Por eso se mantiene simple y mínimo en términos de tipos de datos.

### JSON y números

En los documentos JSON, un número es solo una secuencia de dígitos. No distingue entre números como enteros o flotantes. 

### JSON y fechas

En los documentos JSON no admite un tipo de datos Fecha y estas solo se representan como cadenas simples. Ejemplos:

```
{"title": "A Swedish Love Story", released: "1970-04-24"}
{"title": "A Swedish Love Story", released: "24-04-1970"}
{"title": "A Swedish Love Story", released: "24th April 1970"}
{"title": "A Swedish Love Story", released: "Fri, 24 Apr 1970"}

```

Las partes que intercambian la información deben estandarizar el formato fecha durante las transferencias. La forma de leer los datos depende de los intérpretes de los idiomas y de sus contratos de intercambio de datos.

### Ejercicio: Creación de su propio documento JSON

Abra un validador JSON, por ejemplo: [https://jsonlint.com/](https://jsonlint.com/).

Escriba la información anterior en formato JSON:

```
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

### Documentos de MongoDB

Una base de datos MongoDB se compone de **colecciones** y **documentos**. Una base de datos puede tener una o más colecciones, y cada colección puede almacenar uno o más documentos relacionados.

En comparación con RDBMS, las **colecciones** son análogas a las **tablas** y los **documentos** son análogos a las **filas** dentro de una tabla. Sin embargo, los documentos son mucho más flexibles en comparación con las filas de una tabla.

### Tipos de datos de MongoDB

MongoDB almacena documentos similares a JSON.

**Strings**: en MongoDB, los campos de cadena están codificados en UTF-8. Ademas, admiten capacidades de búsqueda con expresiones regulares.

```
{ "name" : "Tom Walter" }
```

**Numbers**: En MongoDB se admite los varios tipos de números.

double: punto flotante de 64 bits
int: entero de 32 bits con signo
long: entero sin signo de 64 bits
decimal: punto flotante de 128 bits, que cumple con IEE 754

**Booleans**: se utiliza para representar si algo es verdadero o falso.

```
{ "isMongoDBHard": false }
```

**Objects**

Los campos de objeto se utilizan para representar documentos **anidados** o **incrustados,** es decir, un campo cuyo valor es otro documento JSON válido.

```
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
El valor del campo de host es otro documento de JSON válido. 

MongoDB usa una notación de puntos ( . ) para acceder a los objetos incrustados. 

Para acceder a un documento anidado, crearemos una variable del listado en el shell de mongo:

```
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
```bash
listing.host.host_name

David
```

**Array**

Un campo con un tipo de **Array** tiene una colección de cero o más valores. Considere la siguiente matriz de ejemplo que contiene cuatro números:

```
var doc = { first_array: [ 4, 3, 2, 1 ] }
```
Se puede acceder a cada elemento de una matriz utilizando su posición de índice. El número de índice se incluye entre corchetes. Accedamos al tercer elemento de la matriz:

```
doc.first_array[3]
1
```
Usando la posición del índice, también puede agregar nuevos elementos a una matriz existente:

```
doc.first_array[4] = 99
```
Al imprimir la matriz, verá que el quinto elemento se ha agregado correctamente, que contiene la posición del índice, 4:

```
doc.first_array
[4, 3, 2, 1, 99]
```
