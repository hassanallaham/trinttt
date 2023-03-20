**[Back to Home](https://github.com/biggora/trinte/wiki)**

* [Created Application](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Application configuration file](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Database configuration file](https://github.com/biggora/trinte/wiki/Application-configuration#database-configuration)
  * [Directory structure](https://github.com/biggora/trinte/wiki/Directory-Structure)
  * [Routing and params](https://github.com/biggora/trinte/wiki/Routes)
  * [Middleware](https://github.com/biggora/trinte/wiki/Middleware)

### Application configuration

`/config/configuration.js`

```js
module.exports = {
    port : 3000,
    session: {
        maxAge : 8640000,
        key : "trinte",
        secret : "Web-based Application"
    },
    parser : {
        encoding : "utf-8",
        keepExtensions : true
    } ...
```

### Database configuration

`/config/database.js`

```js
module.exports = {
    db: {
        driver     : "mongoose",
        host       : "localhost",
        port       : "27017",
        username   : "",
        password   : "",
        database   : "trinte-dev"
    } ...
```

  * [For MongoDB database](https://github.com/biggora/trinte/wiki/For-MongoDB-database)
  * [For MySQL database](https://github.com/biggora/trinte/wiki/For-MySQL-database)
  * [For Redis database](https://github.com/biggora/trinte/wiki/For-Redis-database)
  * [For SQLite database](https://github.com/biggora/trinte/wiki/For-SQLite-database)
  * [For PostgeSQL database](https://github.com/biggora/trinte/wiki/For-PostgeSQL-database)

**[Back to Home](https://github.com/biggora/trinte/wiki)**