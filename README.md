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
