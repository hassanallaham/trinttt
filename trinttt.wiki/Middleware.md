**[Back to Home](https://github.com/biggora/trinte/wiki)**

**[Middleware for route](https://github.com/biggora/trinte/wiki/Routes#wiki-middleware)**

* [Created Application](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Application configuration](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Directory structure](https://github.com/biggora/trinte/wiki/Directory-Structure)
  * [Routing and params](https://github.com/biggora/trinte/wiki/Routes)
  * [Middleware](https://github.com/biggora/trinte/wiki/Middleware)

Global middleware setup in project `/config/middleware.js`

```js

var useragent = require('express-useragent');

module.exports = function(app, express) {
        // Cross-site request forgery middleware
        app.use(express.csrf());
        // Exposing user-agent middleware
        app.use(useragent.express());
        // Add custom middleware here ...
        // ...
        // ...
};
```

**[Middleware for route](https://github.com/biggora/trinte/wiki/Routes#wiki-middleware)**

**[Back to Home](https://github.com/biggora/trinte/wiki)**