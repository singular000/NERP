# NERP Stack Unit

**Node**, **Express**, **React**, **Postgres**

We could also call it **NERD**, which would be better, but this refers to any database and not postgres specifically.

[Technical arguments for the NERP Stack](https://blog.scottnonnenberg.com/n-for-node-js-nerp-stack-part-1/)

* above blog post published Feb 2016. Compares NERP to the MEAN Stack.

NERP / NERD Unit will be broken into four parts: **Server**, **Client**, **Auth**, and **More**. The four parts depend on each other in this sequence and are being developed in this sequence. But for lesson planning they could be woven together in any number of ways for the old brain wire-up.

<br>

## Server

[Technical details, explanations, and walkthroughs of my approach and conclusions here](https://github.com/singular000/NERP/blob/master/1-Node-Express-PGP.md)

My demos:

* [Single model repo](https://github.com/singular000/node-express-pgp-single-model)
* [One-to-many repo](https://github.com/singular000/node-express-pgp-one-to-many)
* [Many-to-many repo](https://github.com/singular000/node-express-pgp-many-to-many)



**Goal:** Students build a RESTFul Express API using Postgres. Serves JSON. The API is standalone and unopinionated on the client -- The student can interact from a separate domain and using any of Angular, React, React Native, Postman, cURL, etc.

**SQL emphasis:** Emphasis on raw SQL and db theory. In-app, use `pg-promise`'s QueryFile module to reinforce **raw SQL commands**. Write clear multi-line SQL queries within `.sql` files using the QueryFile module (no yucky string queries or ORM). _Intention for lesson planning:_ Teach SQL in tandem every day with app integration--introduce a new SQL relationship or concept and then integrate it into the app. 

**Status codes and exceptions**: Send the proper status codes, messages, and data from the API. Handle errors and  exceptions properly in all cases so that disparate clients operate in a standard way. Along with documentation, make the API clear and easy to use.

**async / await:** `pg-promise` is `pg` with Promises instead of callbacks. However, Promises themselves take callbacks! On top of a Promise we can use ES7's **async / await** syntax. With async / await we can remove callbacks from our handling of db queries. We can write sequential db calls with only one level of nesting (within a **try / catch** construct), and assign data intuitively to variables and pass the data around like we would for regular "synchronous" code.

**Documentation of the endpoints:** Students properly document the endpoints and how a user can consume the API.

Node packages:

* `pg-promise`
* `body-parser`

Node packages, dev-dependencies:

* `morgan`
* `pretty-error`

<br>

## Client

Technical details, explanations, and walkthroughs of my approach and conclusions are in progress

My demos are in progress

**Goal:** Build a client server, separate from the Node-SQL API server. The client server will run **React** and interact with the API using **fetch**. 

Use Facebook's `create-react-app` to teach React without worrying about the build tools up-front. 

Tools:

* `create-react-app`
* fetch

(Note: most of the "More" section is focused on _more React_ stuff, like Redux, Webpack, and styling). 

<br>

## Auth

**CORS**: Server will accept incoming requests via CORS (The client-side app will be on a separate domain).

**JWT**: Stateless authentication with JSON Web Tokens.

Dependencies:

* `cors`
* `jwt`
* local storage
* `bcrypt`

All server-side stuff can be done with just the `jwt` package for tokens, and `bcrypt` for passwords.

<br>

## More

Introduce Redux (not as far as thunk or react-redux).

Introduce build systems with webpack / babel config.

Introduce modern styling methods with `styled-components`.

Introduce an ORM like Sequelize or Bookshelf for db queries.

* Redux
* Styling - **styled-components**
* Build tools - **webpack and babel**
* ORM - **sequelize** or **bookshelf**








