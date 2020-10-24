# Serminario de Mongodb
## Actividad #1
**1. Crear una nueva base de datos llamada futbolfifa**
```
use store
```
**2. Crear una nueva _collection_ llamada players**
```js
db.createCollection("games")
```
**3. Insertar 5 documentos en la collection players con datos básicos**
```js
db.games.insert([
	{title:"Life is Strange",price:5},
	{title:"Batman",price:3},
	{title:"The Witcher",price:25}
])
```
**4. Listar todos los documentos de la collection players**
```js
db.games.find()
```
## Actividad #2
**1. Crear una nueva base de datos de un sistema de streaming de video**
```
use flix
```
**2. Crear una colección de "movies"**
```js
db.createCollection("movies")
```
**3. Para cada movie, se debería guardar la siguiente información**
_Título, Año, Puntaje, Género, Descripción, Actores [ ], País, Ganancias y Duración_

**4. Agregar películas usando insert( )**
```js
db.movies.insert({
	title:"Batman begins",
	year:2005,
	rating:4.5,
	gender:"Action",
	description:"Batmen",
	actors:
	[
		{name:"Chris",age:12},
		{name:"Chris",age:12}
	],
	country:"US",
	income:1000,
	duration:120
})
//output: WriteResult({ "nInserted" : 1 })
```
**5. Agregar películas usando insertOne( )**
```js
db.movies.insertOne({
	title:"Pulp Fiction",
	year:1986,
	rating:4.9,
	gender:"Action",
	description:"Tarantino's Film",
	actors:
	[
		{name:"Samuel",age:36},
		{name:"Travolta",age:42}
	],
	country:"US",
	income:2890,
	duration:180
})
```
**6. Agregar películas usando insertMany( )**
```js
db.movies.insertMany([
{
	title:"Lord of The Rings",
	year:1999,
	rating:4.7,
	gender:"Action",
	description:"Tolkien",
	actors:
	[
		{name:"Bloom",age:26},
		{name:"Frodo",age:22}
	],
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
	actors:
	[
		{name:"Hamil",age:36},
		{name:"Fisher",age:42}
	],
	country:"US",
	income:2890,
	duration:180
}
])
```
**7. Actualizar películas agregando el field highlighted=true a aquellas con rating > 4.5**
```js
db.movies.updateMany(
{rating: {$gt: 4.5}},
{
	$set: {
		highlighted: true	
	}
})
```
**8. Actualizar películas cambiando el género “drama” por “bored”**
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
**9. Borrar todas las películas que tengan más de 30 años.**
```js
db.movies.find({year:{$gt: 1990}})
```
**10. Buscar todas las películas argentinas.**
```js
db.movies.find({country: "US"})
```
**11. Buscar todas las películas de acción con un buen rating (ej. > 4.0) que hayan salido los últimos 2 años.**
```js
db.movies.find({$and:[{gender:"Drama"},{rating:{$gt: 4.4}},{year:{$gt: 2018}}]})
```
## Actividad #3
**1. Utilizar la misma base de datos de películas e insertar varias películas con distinto contenido.**
```js
db.movies.insertMany([
	{
		name:"Oscar",
		lastname:"Diaz",
		age:33
	},
	{
		engine:"V8",
		horsepower:400
	}
]);
```
**2. Listar todas las películas del año 2018.**
```js
db.movies.find({year: 2018})
```
**3. Listar las 10 primeras películas de Hollywood.**
```js
db.movies.find({country: "Hollywood"}).limit(10);
```
**4. Listar las 5 películas más taquilleras.**
```js
db.movies.find().sort({income: 1}).limit(5);
```
**5. Listar el 2do conjunto de 5 películas más taquilleras.**
```js
db.movies.find().sort({income: 1}).limit(5).skip(5);
```
**6. Repetir query 3 y 4 pero retornando sólo el título y genre.**
```js
db.movies.find(
	{country: "Hollywood"},
	{title: 1, gender: 1, _id: 0}
	).limit(10);
```
**7. Mostrar los distintos países que existen en la base de datos.**
```js
db.movies.distinct({"country"});
```
