**[Back to Home](https://github.com/biggora/trinte/wiki)**

* [Created Application](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Application configuration](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Directory structure](https://github.com/biggora/trinte/wiki/Directory-Structure)
  * [Routing and params](https://github.com/biggora/trinte/wiki/Routes)
  * [Param pre-condition functions](https://github.com/biggora/trinte/wiki/Routes#wiki-param-pre-condition-functions)
  * [Middleware](https://github.com/biggora/trinte/wiki/Middleware)

### Routes
Local middleware setup in `/config/routes.js`

#### Features

- [resourceful routes](#singleton)
- generic routes
- url helpers
- [namespaces](#namespaces)
- [custom helper names / paths for resources](#custom-helper)
- [named parameters in url helpers](#named-routing)
- [route with middleware](#middleware)
- [filter methods](#filter)

<a name="named-routing"></a>
#### Named route params

Example:
```js
    map.get('/test/:param1/:param2', 'controller#action');
    map.pathTo.test({param1: 'foo', param2: 'bar'}); // '/test/foo/bar'
```
<a name="singleton"></a>
#### Singleton resources

Example:
```js
    map.resource('post');
```
Will generate the following routes:

    method    route                          controller#action   helper method
    --------------------------------------------------------------------------
    GET       /posts                         posts#index         pathTo.posts()
    GET       /posts/:skip-:limit            posts#index         pathTo.paging_posts()
    GET       /posts/:id                     posts#show          pathTo.show_post(post)
    POST      /posts                         posts#create        pathTo.create_posts()
    GET       /posts/new                     posts#new           pathTo.new_post()
    GET       /posts/edit/:id                posts#edit          pathTo.edit_post(post)
    DELETE    /posts/:id                     posts#destroy       pathTo.destroy_post(post)
    PUT       /posts/:id                     posts#update        pathTo.update_post(post)
    DELETE    /posts                         posts#destroyall    pathTo.destroy_posts()

Singleton resources can also have nested resources. For example:
```js
    map.resource('users', function(users) {
      users.resources('posts');
    });
```
Will generate the following routes:

    method   route                           controller#action   helper method
    --------------------------------------------------------------------------
    GET     /users/:user_id/posts            posts#index         pathTo.users_posts(user)
    GET     /users/:user_id/posts/:id        posts#show          pathTo.show_users_post(user, post)
    POST    /users/:user_id/posts            posts#create        pathTo.create_users_posts(user)
    GET     /users/:user_id/posts/new        posts#new           pathTo.new_users_post(user)
    GET     /users/:user_id/posts/edit/:id   posts#edit          pathTo.edit_users_post(user, post)
    DELETE  /users/:user_id/posts/:id        posts#destroy       pathTo.destroy_users_post(user, post)
    PUT     /users/:user_id/posts/:id        posts#update        pathTo.update_users_post(user, post)
    DELETE  /users/:user_id/posts            posts#destroyall    pathTo.destroy_users_posts(user)

<a name="namespaces"></a>
#### Namespaces
Example:
```js
    map.namespace('admin', function(admin) {
      admin.resources('users');
    });
```
Will generate the following routes:

    method    route                          controller#action         helper method
    ---------------------------------------------------------------------------------
    GET       /admin/posts                   admin/posts#index         pathTo.admin_posts()
    GET       /admin/posts/:skip-:limit      admin/posts#index         pathTo.paging_admin_posts(skip, limit)
    GET       /admin/posts/:id               admin/posts#show          pathTo.show_admin_post(post)
    POST      /admin/posts                   admin/posts#create        pathTo.create_admin_posts()
    GET       /admin/posts/new               admin/posts#new           pathTo.new_admin_post()
    GET       /admin/posts/edit/:id          admin/posts#edit          pathTo.edit_admin_post(post)
    DELETE    /admin/posts/:id               admin/posts#destroy       pathTo.destroy_admin_post(post)
    PUT       /admin/posts/:id               admin/posts#update        pathTo.update_admin_post(post)
    DELETE    /admin/posts                   admin/posts#destroyall    pathTo.destroy_admin_posts()

<a name="custom-helper"></a>
#### Custom helper names / paths for resources
If you want to override default routes behaviour, you can use two options: as and path to specify a helper name and a path you want to have in the result.
```js
    map.resources('posts',{as: 'articles'});
```
This will create the following routes:

    method    route                          controller#action         helper method
    ---------------------------------------------------------------------------------
    GET       /posts                         posts#index               pathTo.articles()
    GET       /posts/:skip-:limit            posts#index               pathTo.paging_articles(skip, limit)
    GET       /posts/:id                     posts#show                pathTo.show_article(post)
    POST      /posts                         posts#create              pathTo.create_articles()
    GET       /posts/new                     posts#new                 pathTo.new_article()
    GET       /posts/edit/:id                posts#edit                pathTo.edit_article(post)
    DELETE    /posts/:id                     posts#destroy             pathTo.destroy_article(post)
    PUT       /posts/:id                     posts#update              pathTo.update_article(post)
    DELETE    /posts                         posts#destroyall          pathTo.destroy_articles()

If you want to change the base path:
```js
    map.resources('posts', { path: 'articles' });
```
This will create the following routes:

    method    route                          controller#action         helper method
    ---------------------------------------------------------------------------------
    GET       /articles                      posts#index               pathTo.posts()
    GET       /articles/:skip-:limit         posts#index               pathTo.paging_posts(skip, limit)
    GET       /articles/:id                  posts#show                pathTo.show_post(post)
    POST      /articles                      posts#create              pathTo.create_posts()
    GET       /articles/new                  posts#new                 pathTo.new_post()
    GET       /articles/edit/:id             posts#edit                pathTo.edit_post(post)
    DELETE    /articles/:id                  posts#destroy             pathTo.destroy_post(post)
    PUT       /articles/:id                  posts#update              pathTo.update_post(post)
    DELETE    /articles                      posts#destroyall          pathTo.destroy_posts()


<a name="middleware"></a>
#### Route with Middleware

Example:
```js
    // named route
    map.get('/test/:param1/:param2', 'controller#action', [middleware1, middleware2, ...]);

    // singleton resources
    map.resource('post', {
        middleware: [middleware1, middleware2, ...]
    });

    // nested resources
    map.resource('users', {
        middleware: [middleware1, middleware2, ...]
    }, function(users) {
       users.resources('posts', {
          middleware: [middleware3, middleware4, ...]
       });
    });

    // namespaces
    map.resource('users', {
        middleware: [middleware1, middleware2, ...]
    }, function(users) {
      users.resources('posts');
    });
```
<a name="filter"></a>
#### Routes with Filter Methods
Example `except` param:
```js
    map.resources('posts',{except: ['edit','destroy','destroyAll']});
```
instead of:
```js
    map.get('/posts.:format?', 'posts#index');
    map.get('/posts/new.:format?', 'posts#new');
    map.post('/posts.:format?', 'posts#create');
    map.get('/posts/:id.:format?', 'posts#show');
```
Example `only` param:
```js
    map.resources('posts',{only: ['index','show']});
```
instead of:
```js
    map.get('/posts.:format?','posts#index');
    map.get('/posts/:id.:format?','posts#show');
```
<a name="params"></a>
#### Param pre-condition functions

`/config/params.js`
```js
    app.param('id', /^[A-Za-z0-9]+$/);
    app.param('controller', /^[a-zA-Z]+$/);
    app.param('action', /^[a-zA-Z]+$/);
    app.param('format', /^[a-zA-Z]+$/);
    app.param('from', /^\d+$/);
    app.param('to', /^\d+$/);
```

**[Back to Home](https://github.com/biggora/trinte/wiki)**
