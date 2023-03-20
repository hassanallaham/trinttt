**[Back to Home](https://github.com/biggora/trinte/wiki)**

### Database configuration 
* [For MongoDB database](https://github.com/biggora/trinte/wiki/For-MongoDB-database)
* [For MySQL / MariaDB database](https://github.com/biggora/trinte/wiki/For-MySQL-database)
* [For Redis database](https://github.com/biggora/trinte/wiki/For-Redis-database)
* [For SQLite database](https://github.com/biggora/trinte/wiki/For-SQLite-database)
* [For PostgeSQL database](https://github.com/biggora/trinte/wiki/For-PostgeSQL-database)

### Steps
- Add dependency to `pg` database driver module in app `package.json`, and install it.
- Rewrite database configuration file 

To configure trinte app for PostgeSQL database use adapter name `postgres`.

### Example
```js
module.exports.production = {
    driver     : 'postgres',
    host       : 'localhost',
    port       : '5432',
    username   : 'test',
    password   : 'test',
    database   : 'trinte-dev'
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