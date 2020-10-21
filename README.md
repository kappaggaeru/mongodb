**Crear una nueva base de datos de un sistema de streaming de video**
```js
use flix
```
**Crear una colección de "movies"**
```js
db.createCollection("movies")
```
**Para cada movie, se debería guardar la siguiente información**
_Título, Año, Puntaje, Género, Descripción, Actores [ ], País, Ganancias y Duración_

**Agregar películas usando insert( )**
```js
db.movies.insert({
	title:"Batman begins",
	year:2005,
	rating:4.5,
	gender:"Action",
	description:"Batmen",
	actors:[{name:"Chris",age:12},{name:"Chris",age:12}],
	country:"US",
	income:1000,
	duration:120
})
//output: WriteResult({ "nInserted" : 1 })
```
**Agregar películas usando insertOne( )**
```js
db.movies.insertOne({
	title:"Pulp Fiction",
	year:1986,
	rating:4.9,
	gender:"Action",
	description:"Tarantino's Film",
	actors:[{name:"Samuel",age:36},{name:"Travolta",age:42}],
	country:"US",
	income:2890,
	duration:180
})
//output: 
//{
//	"acknowledged" : true,
//	"insertedId" : ObjectId("...")
//}
```
**Agregar películas usando insertMany( )**
```js
db.movies.insertMany([
{
	title:"Lord of The Rings",
	year:1999,
	rating:4.7,
	gender:"Action",
	description:"Tolkien",
	actors:[{name:"Bloom",age:26},{name:"Frodo",age:22}],
	country:"UK",
	income:3500,
	duration:160
},
{
	title:"Star Wars IV",
	year:1991,
	rating:4.4,
	gender:"SCIFI",
	description:"A New Hope",
	actors:[{name:"Hamil",age:36},{name:"Fisher",age:42}],
	country:"US",
	income:2890,
	duration:180
}
])
//output: 
//{
//	"acknowledged" : true,
//	"insertedIds" : [
//		ObjectId("..."),
//		ObjectId("...")
//	]
//}
```
**Actualizar películas agregando el field highlighted=true a aquellas con rating > 4.5**
```js
db.movies.updateMany(
{rating: {$gt: 4.5}},
{
	$set: {
		highlighted: true	
	}
})
//output: { "acknowledged" : true, "matchedCount" : 2, "modifiedCount" : 2 }
```
**Actualizar películas cambiando el género “drama” por “bored”**
```js
db.movies.updateMany(
{gender: "Action"},
{
	$set: {
		gender: "Drama"
	}
})
//output: { "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
```
**Borrar todas las películas que tengan más de 30 años.**
```js
db.movies.find({year:{$gt: 1990}})
//output: []
```
**Buscar todas las películas argentinas.**
```js
db.movies.find({country: "US"})
//output: []
```
**Buscar todas las películas de acción con un buen rating (ej. > 4.0) que hayan salido los últimos 2 años.**
```js
db.movies.find({$and:[{gender:"Drama"},{rating:{$gt: 4.4}},{year:{$gt: 2018}}]})
//output: []
```
