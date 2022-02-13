# Mongo---Aggregation-pipelines-
Aggregation pipelines
create a mock movies table in sequel and mongodb which has 500 documents which has following columns/fields

- id
- movie_name
- movie_genre
- production_year ( between 1990 to 2020)
- budget ( 9000 to 20000)
- rating ( 0 - 10 )
- rated ( PG or G )
- language
- genres

#### create an aggregation query for the following
- rating is atleast 8
```js
  db.movies.aggregate([{$match : {rating : {$gte : 8  }  }} ])
```

- genres do not contain "Thriller" or "Romance"
```js
  db.movies.aggregate([{$match : {genre : {$ne : {$in : [ "Thriller", "Romance" ]}  }  }} ])
```

- rated "PG"
```js
  db.movies.aggregate([{$match : {rated : {$eq : "PG"  }  }} ])
```

- languages contain English or French
```js
  db.movies.aggregate([{$match : {language : {$eq : {$in : [ "French", "English" ]}  }  }} ])
```

- production_year after 2012
```js
  db.movies.aggregate([{$match : { production_year : {$gt : 2012 } } }])
```

### 2. you have been given a task by your manager

- you have a huge collection of data
- you need to find the total number of duplicates that are found on against a key
- here the duplicates are formed from the name

```js 
  { name: "aman", id: 1 } , { name: "albert", id : 2 } { name: "aman", id: 3 } , { name: "albert", id : 4 }  { name :"nrupul", id: 5 } 
 ```

- in this case required output is

```js 
  { name: "aman", duplicates: 1 }, { name: "albert", duplicates: 1 } ,{ name: "nrupul", duplicates: 0 } 
```
- use aggregations and try to solve this
- Answer query.1

```js
  db.task.aggregate([ {$group : { _id : "$name", count : {$sum :1}}},{$match : { _id : { $ne : null},"count" : { $gt : 1}  }},{$project : { name : "$_id", "_id" : 0, duplicates : "$count" } }  ])
```

- OR 

```js
  db.task.aggregate( [{$match : {}}, {$group : { _id : "$name", duplicatesFound : {$sum :1}}} ])
```

