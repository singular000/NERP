# Server
## Node, Express, Postgres

Examples:
"Books App API" 📚

* [Single model](https://github.com/singular000/node-express-pgp-single-model)
* [One-to-many](https://github.com/singular000/node-express-pgp-one-to-many)
* [Many-to-many](https://github.com/singular000/node-express-pgp-many-to-many)


## Application Structure



## QueryFiles



<br>



<br>

<br>

## DEV NOTES

**Restart server after changes to QueryFile**

Changing a `.sql` file doesn't restart the server and reload the changes: `new QueryFile` will not re-instantiate. Restart server to instantiate new QueryFile after changing a `.sql` file.

**Errors and exceptions**

In the `catch` clause of a db query, the base err object will appear in console as a stack trace but sometimes not in thre response. For response text, pg-promise errors from queryFile show in `err.message`.

Errors within queryfiles themselves are also possible.

```javascript
if (err instanceof db.$config.pgp.errors.QueryFileError) {             
	console.log('query file error', err);                                
}                                                                      
```

**Delete route**

For DELETE I arbitrarily decided to send the deleted resource in the response: using `RETURNING *` in the sql statement. using `db.one` query in the controller, and status code of 200 (instead of 204).

![](https://i.imgur.com/t2c5RCG.png)

**JSON notes**

Postgres JSON datatype: Postgres validates json, but there is no native schema validation support for nested json fields and datatypes. Relating JSON data is also problematic. Lesson-wise, this could lead into the topic of relations -- "if you think you need a JSON column, or an array, make a second table instead" -- and maybe some talk about "anti-patterns" using json in a relational db.

#### Misc

Validation: only way to protect against empty strings is with CHECK

```sql
title VARCHAR NOT NULL CHECK (title <> '')
```

Run create db file in bash

```
$ psql -f db/create_db.sql
```

Run schema file in bash

```
$ psql books_app_api -f models/books/schema.sql
```

NOTEWORTHY ERRORS:

```
error: syntax error at or near "$"
```

If you forgot to supply an object to a 'create' or 'update' query, the QueryFile will kick up this error. It's as if it's trying to read SQL as opposed to pg-promise's named parameters syntax.

Don't do this on a create route:

![](https://i.imgur.com/H8bNGUU.png)

Do do this instead  (include the `req.body` object as data ):

![](https://i.imgur.com/vleQVbc.png)


## Resources

#### PG-Promise Resources

* [API Basics](http://mherman.org/blog/2016/03/13/designing-a-restful-api-with-node-and-postgres/)
* [pg-promise examples from creator](https://github.com/vitaly-t/pg-promise/wiki/Learn-by-Example)
* [queryfiles usage from pg-promise creator](http://vitaly-t.github.io/pg-promise/QueryFile.html)
* [data layer example from pg-promise creator](https://github.com/vitaly-t/pg-promise-demo)

#### Postgres / SQL Resources

* [formatting](http://www.sqlstyle.guide/)
* [json](http://www.postgresqltutorial.com/postgresql-json/)
* [postgres reference](http://www.postgresqltutorial.com/)
* [vim highlighting](https://github.com/exu/pgsql.vim)
* [validate json schema](https://github.com/gavinwahl/postgres-json-schema)


