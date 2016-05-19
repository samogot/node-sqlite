## SQLite client library for Node.js applications

[![NPM version](http://img.shields.io/npm/v/sqlite.svg?style=flat-square)](https://www.npmjs.com/package/sqlite)
[![NPM downloads](http://img.shields.io/npm/dm/sqlite.svg?style=flat-square)](https://www.npmjs.com/package/sqlite)
[![Build Status](http://img.shields.io/travis/kriasoft/node-sqlite/master.svg?style=flat-square)](https://travis-ci.org/kriasoft/node-sqlite)
[![Dependency Status](http://img.shields.io/david/kriasoft/node-sqlite.svg?style=flat-square)](https://david-dm.org/kriasoft/node-sqlite)
[![IRC Chat](http://img.shields.io/badge/IRC_Chat-%23sqlite_%40%20Freenode-blue.svg?style=flat-square)](https://webchat.freenode.net/?channels=sql,sqlite)

> This is just a wrapper library that adds ES6 promises to [sqlite3](https://github.com/mapbox/node-sqlite3/) ([docs](https://github.com/mapbox/node-sqlite3/wiki)).

### How to Install

```sh
$ npm install sqlite --save
```

### How to Use

This module has the same API as the original [SQLite3](https://github.com/mapbox/node-sqlite3/wiki/API)
library except that all its API methods return promises and do not accept callback arguments.

Below is an example of how to use it with Node.js/Express and [Babel](http://babeljs.io/):

```js
import express from 'express';
import Promise from 'bluebird';
import db from 'sqlite';

const app = express();
const port = process.env.PORT || 3000;

app.get('/', async (req, res, next) => {
  try {
    const row = await db.get(`SELECT * FROM tableName WHERE id = ?`, 123);
    res.send(`Hello, ${row.columnName}!`);
  } catch (err) {
    next(err);
  }
});

// Connect to the database before launching Node.js app
db.open('./database.sqlite', { verbose: true, Promise })
  .catch(err => console.error(err))
  .finally(() => {
    app.listen(port, () => {
      console.log(`Node.js app is running at http://localhost:${port}/`);
    });
  });
```

**NOTE**: For Node.js v5 and below use `var db = require('sqlite/legacy');` instead.

### Related Projects

* [React Starter Kit](https://github.com/kriasoft/react-starter-kit) — Isomorphic web app boilerplate (Node.js/Express, React.js, GraphQL)
* [Babel Starter Kit](https://github.com/kriasoft/babel-starter-kit) — JavaScript library boilerplate (ES2015, Babel, Rollup)
* [Membership Database](https://github.com/membership/membership.db) — SQL database boilerplate for web app users, roles and auth tokens

### License

The MIT License © 2015-2016 Kriasoft, LLC. All rights reserved.

---
Made with ♥ by Konstantin Tarkus ([@koistya](https://twitter.com/koistya)) and [contributors](https://github.com/kriasoft/node-sqlite/graphs/contributors)
