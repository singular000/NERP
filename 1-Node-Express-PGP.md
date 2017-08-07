# Server
## Node, Express, Postgres

Examples:
"Books App API" 📚

* [Single model](https://github.com/singular000/node-express-pgp-single-model)
* [One-to-many](https://github.com/singular000/node-express-pgp-one-to-many)
* [Many-to-many](https://github.com/singular000/node-express-pgp-many-to-many)


## Application Structure

```
|
|_controllers/
|_models/
|_db/
|_server.js
```

This follows on from Unit 2 and 3 Express MVC and MC* structure as taught in Remote.

I'm considering removing the 'models' folder and putting all the sql files in the 'db' folder within a 'sql' subfolder, as advocated [here](http://vitaly-t.github.io/pg-promise/QueryFile.html)

As a next step, beyond this unit, the creator of pg-promise advocates [this](https://github.com/vitaly-t/pg-promise-demo/tree/master/JavaScript), which would be a good exercise in abstracting away repetition.

## QueryFiles



<br>

## async / await

* Using **async** with the **req, res** callback apparently is fine as long as errors are accounted for: [async / await in express routes](https://medium.com/@yamalight/danger-of-using-async-await-in-es7-8006e3eb7efb)

* In production multiple queries should done with a pg-promise **task**, but it is overkill for students first learning the ropes of pg-promise:

```javascript
router.get('/:id'. (req, res) => {
  db.task(async t => {
    const book = await t.one(Book.find, req.params.id);
    book.notes = await t.any(Note.all, req.params.id);
    return book;
  })
  .then(data => {
    res.status(200).json({ status: 'success', data, message: 'found a book' });
  })
  .catch(err => {
    res.status(400).json({ status: 'failure', data: err.message, message: 'could not find book' });
  });
});
```

Therefore, students can stick with basic awaits within a try/catch for now :

```javascript
router.get('/:id', async (req, res) => {
  try {
    const book = await db.one(Book.find, req.params.id);
    book.notes = await db.any(Note.all, req.params.id);
    res.status(200).json({ success: true, data: book, message: 'found a book' });
  } catch (err) {
    res.status(400).json({ success: false, err: err.message, message: 'could not find book' })
  }
});
```

## Endpoints -- status codes


**Delete Book**

For DELETE I arbitrarily decided to send the deleted resource in the response: using `RETURNING *` in the sql statement. using `db.one` query in the controller, and status code of 200 (instead of 204).

<br>
<hr>

## DEV NOTES

**Restart server after changes to QueryFile**

By default, changing a `.sql` file doesn't restart the server and reload the changes. `new QueryFile` doesn't re-instantiate. To change this, use the `debug: true` option or set `NODE_ENV` to development. [Docs](http://vitaly-t.github.io/pg-promise/QueryFile.html#.Options)


**Errors and exceptions**

In the `catch` clause of a db query, the base err object will appear in console as a stack trace and sometimes not in the response. For response text, pg-promise errors from queryFile show in `err.message`.

Errors within queryfiles themselves are also possible.

```javascript
if (err instanceof db.$config.pgp.errors.QueryFileError) {             
	console.log('query file error', err);                                
}                                                                      
```

![](https://i.imgur.com/t2c5RCG.png)

**Forgot to send data**

```
error: syntax error at or near "$"
```

If you forgot to supply an object to a 'create' or 'update' query, the QueryFile will kick up this error. It's as if it's trying to read SQL as opposed to pg-promise's named parameters syntax.

Don't do this on a create route:

![](https://i.imgur.com/H8bNGUU.png)

Do do this instead  (include the `req.body` object as data ):

![](https://i.imgur.com/vleQVbc.png)

**JSON notes**

Postgres JSON datatype: Postgres validates json, but there is no native schema validation support for nested json fields and datatypes. Relating JSON data is also problematic. Lesson-wise, this could lead into the topic of relations -- "if you think you need a JSON column, or an array, make a second table instead" -- and maybe some talk about "anti-patterns" using json in a relational db.

**Misc**

Validation: only way to protect against empty strings is with CHECK

```sql
title VARCHAR NOT NULL CHECK (title <> '')
```

**Postman**

Must use **x-www-form-urlencoded** option in Postman to send data

![](https://i.imgur.com/Mksv6jQ.png)

Otherwise will receive 'column' does not exist:

![](https://i.imgur.com/tv7owCJ.png)

**trailing whitespace matters** in key names within postman. 

<br>
<hr>

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


