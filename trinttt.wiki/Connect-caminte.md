**[Back to Home](https://github.com/biggora/trinte/wiki)**

### To Configure Session
TrinteJS session setup in:
```
|-- config
    |-- ...
    `-- session.js
```

### Example

```js
var config = require('./configuration');
var expressSession = require('express-session');
var caminteStore = require('connect-caminte');
var database = require('./database' )[process.env.NODE_ENV || 'dev'];

module.exports = function (app, express) {
    var SessionStore = caminteStore(expressSession);
    app.use(expressSession({
         cookie: {
             maxAge: config.session.maxAge
         },
         key: config.session.key,
         secret: config.session.secret,
         saveUninitialized: true,
         resave: true,
         store: new SessionStore({
             driver: database.driver,
             collection: 'session',
             db: database,
             secret: config.session.secret,
             maxAge: config.session.maxAge,
             clear_interval: config.session.clear_interval
         })
     }));
};
```

**[Back to Home](https://github.com/biggora/trinte/wiki)**
