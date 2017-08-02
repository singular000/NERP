# NERP Stack Unit

**Node**, **Express**, **React**, **Postgres**

[Technical arguments for the NERP Stack](https://blog.scottnonnenberg.com/n-for-node-js-nerp-stack-part-1/)

* above blog post published Feb 2016. Compares NERP to the MEAN Stack.

Unit will be broken into four parts: **Server**, **Client**, **Auth**, and **More**. The four parts are not necessarily sequential, but can be woven.


## Server

[Full technical overview](

**Goal:** Students build a RESTFul Node/Express API using Postgres as DBMS. Serves JSON. The API is standalone and excludes any opinions on clientside tech. The student can interact using any separate client -- Angular, React, React Native, Postman, cURL, etc.

**Documentation of the endpoints:** and how the user can consume the API. 

**Raw SQL:** a day of basic raw SQL and db theory, and more SQL every day, along with app integration, that introduces a new relationship. In-app, use just `pg-promise` for most of the unit to reinforce **raw SQL commands** (No ORM). Use QueryFiles for `.sql`: write clear multi-line SQL queries within `.sql` files instead of yucky string arguments.

**Status codes and exceptions**: Send the proper status codes, messages, data. Handle errors and  exceptions properly in all cases so that disparate clients operate in a standard way.

**CORS**: Server will accept incoming requests via CORS (The client-side app will be separate).

For simplicity, keep syntax to what is available in Node 8+ without babel config (we get async/await, but no import/export).

**More section**: Stateless authentication with JSON Web Tokens ("More").

**Maybe**: For ORM, introduce Sequelize or Bookshelf at the end of the unit as an option ("More").

Dependencies:

* `pg-promise`
* `cors`
* `jwt`
* `bcrypt`
* `body-parser`

Dev-dependencies:

* `morgan`
* `pretty-error`

Possible

* `sequelize` or `bookshelf`- ORM
* `request` - server-side AJAX
* `socket.io` - cross-domain sockets
* `helmet` - security
* `lusca` - security
* Yeoman - scaffolding


## Client
Goal: Build a client server, separate from the Node-SQL API server. The client server will run React and interact with the API using **fetch**. 

Use Facebook's `create-react-app` to learn React. 

Introduce Redux (not as far as thunk or react-redux)

**More section**: Introduce build systems with webpack / babel config at the end of the unit ("More" section).

**Maybe**: Introduce modern styling methods with `styled-components` at the end of the unit ("More").

Tools:

* `create-react-app`
* fetch
* Redux
* `webpack` and `babel`

## More

* Authentication - **json web tokens**
* Styling - **styled-components**
* Build tools - **webpack and babel**
* ORM - **sequelize**








