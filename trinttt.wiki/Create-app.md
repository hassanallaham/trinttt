**[Back to Documentation](https://github.com/biggora/trinte/wiki)**

### Table of contents
* [Create Default Application](https://github.com/biggora/trinte/wiki/Create-app#create-default-application)
* [Create Application with Database](https://github.com/biggora/trinte/wiki/Create-App#create-application-with-database)
* [Create Application with Theme](https://github.com/biggora/trinte/wiki/Create-app#create-application-with-theme)
* [Create Application with session](https://github.com/biggora/trinte/wiki/Create-app#create-application-with-session)
* [Create Application with authorization](https://github.com/biggora/trinte/wiki/Create-app#create-application-with-authorization)
* [Create Application with file Uploader](https://github.com/biggora/trinte/wiki/Create-App#create-application-with-uploader)
* [Create Application with Recaptcha](https://github.com/biggora/trinte/wiki/Create-App#create-application-with-recaptcha)
* [Create Application with Mailer](https://github.com/biggora/trinte/wiki/Create-App#create-application-with-mailer)
* [Create Application with Shopping Cart](https://github.com/biggora/trinte/wiki/Create-App#create-application-with-shopping-cart)
* [Create Application with Socket.io](https://github.com/biggora/trinte/wiki/Create-app#create-application-with-socket-support)

#### Create Default Application
```
      # Create application
      $ trinte -i HelloWorld     
      # intall dependencies              
      $ cd HelloWorld && npm -l install        

      # generate scaffold
      $ trinte -g crud User active:bool name email password
      # running server
      $ trinte -s                              
```
- Browse your application to [http://localhost:3000](http://localhost:3000)

On initialization directories tree generated, [like that](https://github.com/biggora/trinte/wiki/Directory-Structure)


#### Create Application with database

      $ trinte -i HelloWorld  --db sqlite3:./db/main.sqlite

- Add deps to database driver module
- Rewrite file `/config/database.js` 

```js
module.exports = {
    db: {
        driver     : "sqlite3",
        database   : "./db/main.sqlite"
    }
};
```
For more information about the configuration of access to the database server, [see here](https://github.com/biggora/trinte/wiki/Application-configuration#database-configuration).

#### Create Application with Theme
Available 9 themes `default`, `cerulean`, `cosmo`, `cyborg`, `flatly`, `united`, `yeti`, `simplex`, `sandstone`. Default theme `default`.
```      
      # add `--theme` argument
      $ trinte -i HelloWorld --theme cosmo
```
See themes [here](https://bootswatch.com/default/).

#### Create Application with Session
```      
      # add `--sess` argument
      $ trinte -i HelloWorld --sess
```
Will be the following changes:
- Add deps to `connect-caminte` module
- Rewrite file `/config/session.js` [code here](https://gist.github.com/biggora/8508814)

access to session data from the controller:
```js
module.exports = {
    ...
    'index': function(req, res, next) {
         var sess = req.session;
         ...
    }
}
```

#### Create Application with Authorization

      $ trinte -i HelloWorld  --auth

- Add deps to `trinte-auth`, `passport` and `passport-local` modules
- Add file `/config/authorization/local.js` [code here](https://gist.github.com/biggora/8509314)
- Rewrite file `/config/routes.js` 

```js
var Auth = require('./authorization/local'); 

module.exports = function routes(map, app) { 

    // default login page
    map.all( "/login", "apps#login" );
    // default logout route
    map.all( "/logout", Auth.logOut( '/' ) );

    // adding Auth middleware examples:

    // for Named routes
    map.get('/post/:id', 'posts#show', [Auth.isLoggedIn( '/login')]);

    // for Singleton resources
    map.resources( "posts", {
        middleware: [Auth.isLoggedIn( '/login')]
    });

    // for Namespaces
    map.namespace('api', {
        middleware: [Auth.isLoggedIn( '/login')]
    }, function (api) {
        api.resources("fligths");
        api.resources("airports");
        ...
    });
});
```
For more information about of routing, [see here](https://github.com/biggora/trinte/wiki/Routes)

#### Create Application with Uploader

      $ trinte -i HelloWorld  --uploader

- Add deps to `express-uploader`, `gm` and `node-uuid` modules
- Add file `/config/addons/uploader.js` [code here](https://gist.github.com/biggora/e1078c00c87e54de6bac)
- Rewrite file `/config/routes.js` 

```js
var Uploader = require('./addons/uploader');

module.exports = function routes(map, app) { 

    map.post('/uploading', Uploader.middleware());

});
```
For more information about the configuration of uploader, [see here](https://github.com/biggora/express-uploader)

#### Create Application with Recaptcha

      $ trinte -i HelloWorld  --recaptcha

- Add deps to `recaptcha` module
- Add file `/config/addons/recaptcha.js` [code here](https://gist.github.com/biggora/f1cdc260e4ca6ce524fb)
- Rewrite file `/config/routes.js` 

```js
var Recaptcha = require('./addons/recaptcha');

module.exports = function routes(map, app) { 
    /**
     * recapcha middleware usage Recaptcha.middleware()
     **/
});
```
access to recaptcha from the controller:
```js
module.exports = {
    ...
    'index': function(req, res, next) {
         var recaptcha = req.locals.recaptcha;
         ...
    }
}
```

For more information about the configuration of `recaptcha`, [see here](https://www.npmjs.com/package/recaptcha)

#### Create Application with Mailer

      $ trinte -i HelloWorld  --mailer

- Add deps to `nodemailer` module
- Add file `/config/addons/mailer.js` [code here](https://gist.github.com/biggora/d0cea7278e73c0470373)
- Rewrite file `/config/routes.js` 

```js
var Mail = require('./addons/mailer');

module.exports = function routes(map, app) { 

    map.post('/sendmail', Mail.mailSender());

});
```
For more information about the configuration of `nodemailer`, [see here](https://github.com/andris9/Nodemailer)


#### Create Application with Shopping Cart
Session required.

      $ trinte -i HelloWorld  --cart

- Add file `/config/addons/cart.js` [code here](https://gist.github.com/biggora/3d84528842cabed68d60)
- Rewrite file `/config/routes.js` 

```js
var Cart = require('./addons/cart');

module.exports = function routes(map, app) { 

    map.get('/cart', Cart.getProductFromCart());
    map.post('/cart', Cart.addProductToCart());

});
```
access to cart data from the controller:
```js
module.exports = {
    ...
    'index': function(req, res, next) {
         var cart = req.session.cart;
         ...
    }
}
```
access to cart data from the view use `cart` variable.

#### Create Application with Socket support


      $ trinte -i HelloWorld  --socket

- Rewrite file `/config/routes.js` 
- Add `<script src="/socket.io/socket.io.js"></script>` in to `views/_layout.ejs`

```js

module.exports = function routes(map, app) { 

       app.io.on('connection', function (socket) {
          if (config.debug) console.log('a client connected');
          socket.on('disconnect', function () {
             if (config.debug) console.log('client disconnected');
          });
       });

});
```
access to socket from the controller:
```js
module.exports = {
    ...
    'index': function(req, res, next) {
         var socket = req.app.io;
         ...
    }
}
```

**[Back to Documentation](https://github.com/biggora/trinte/wiki)**