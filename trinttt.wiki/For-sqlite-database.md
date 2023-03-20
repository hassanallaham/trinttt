**[Back to Home](https://github.com/biggora/trinte/wiki)**

#### Database configuration
* [For MongoDB database](https://github.com/biggora/trinte/wiki/For-MongoDB-database)
* [For MySQL database](https://github.com/biggora/trinte/wiki/For-MySQL-database)
* [For Redis database](https://github.com/biggora/trinte/wiki/For-Redis-database)
* [For SQLite database](https://github.com/biggora/trinte/wiki/For-SQLite-database)
* [For PostgeSQL database](https://github.com/biggora/trinte/wiki/For-PostgeSQL-database)

### Steps
- Add dependency to `sqlite3` database driver module in app `package.json`, and install it.
- Rewrite database configuration file 

To configure trinte app for SQLite database use adapter name `sqlite3`.

### Database Configuration file
```
|-- config
    |-- ...
    `-- database.js
```
### Example
you must first create a directory.
```js
module.exports.production = {
    driver     : 'sqlite3',
    database   : './db/trinte-dev.db'
};
module.exports.development = {
...
};
module.exports.test = {
...
};
```
Full database params list [here](https://github.com/biggora/caminte/wiki/Connecting-to-DB#connecting)

**[Back to Home](https://github.com/biggora/trinte/wiki)**