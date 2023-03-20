**[Back to Documentation](https://github.com/biggora/trinte/wiki)**

How to create Scaffold via [CLI](http://en.wikipedia.org/wiki/Command-line_interface) [TrinteJS MVC](http://www.trintejs.com/)

### Table of contents
* [Command format](#command-format)
* [Create a Scaffold](#empty-scaffold)
* [Create a Scaffold with fields](#fields-scaffold)
* [Create a Scaffold with namespace](#namespace-scaffold)

<a name="command-format"></a>
### Command format
      format: trinte -g crud [scaffold name] [field(s)]

<a name="empty-scaffold"></a>
### Create a Scaffold

      // Creates all (model, views, controller, tests)
      $ trinte -g crud User

<a name="fields-scaffold"></a>
### Create a Scaffold with fields

      // create Post model and etc. with fields: title, content, created, active
      $ trinte -g crud Post title content created:date active:boolean

 - See all valid field types [here](#field-types).

Generated files, path like that:
```
    .
    |
    `-- app
        |-- models
        |   `-- Post.js
        `-- controllers
        |   `-- PostsController.js
        `-- views
            `-- posts
                |-- form.ejs
                |-- edit.ejs
                |-- new.ejs
                |-- index.ejs
                `-- show.js
```

Add routes in `/config/routes.js`
```js
    map.resources('posts');
```

will provide the following routes:

    method    route                          controller#action   helper method
    --------------------------------------------------------------------------
    GET       /posts                         posts#index         pathTo.posts()
    GET       /posts/:id                     posts#show          pathTo.show_post(post)
    POST      /posts                         posts#create        pathTo.create_posts()
    GET       /posts/new                     posts#new           pathTo.new_post()
    GET       /posts/edit/:id                posts#edit          pathTo.edit_post(post)
    DELETE    /posts/:id                     posts#destroy       pathTo.destroy_post(post)
    PUT       /posts/:id                     posts#update        pathTo.update_post(post)
    DELETE    /posts                         posts#destroyall    pathTo.destroy_posts()

<a name="namespace-scaffold"></a>
### Create a Scaffold with namespace

      // create Post model and etc. with fields: title, message, active
      $ trinte g crud admin#Post title message active:boolean

Generated files, path like that:
```
    .
    |
    `-- app
        |-- models
        |   `-- Post.js
        |-- controllers
        |   `-- admin
        |       `-- PostsController.js
        `-- views
            `-- admin
                `-- posts
                    |-- form.ejs
                    |-- edit.ejs
                    |-- new.ejs
                    |-- index.ejs
                    `-- show.js
```

Add routes in `/config/routes.js`
```js
    map.namespace('admin', function(admin){
        admin.resources("posts");
    });
```

will provide the following routes:

    method    route                          controller#action         helper method
    ---------------------------------------------------------------------------------
    GET       /admin/posts                   admin/posts#index         pathTo.admin_posts()
    GET       /admin/posts/:id               admin/posts#show          pathTo.show_admin_post(post)
    POST      /admin/posts                   admin/posts#create        pathTo.create_admin_posts()
    GET       /admin/posts/new               admin/posts#new           pathTo.new_admin_post()
    GET       /admin/posts/edit/:id          admin/posts#edit          pathTo.edit_admin_post(post)
    DELETE    /admin/posts/:id               admin/posts#destroy       pathTo.destroy_admin_post(post)
    PUT       /admin/posts/:id               admin/posts#update        pathTo.update_admin_post(post)
    DELETE    /admin/posts                   admin/posts#destroyall    pathTo.destroy_admin_posts()


**[Back to Documentation](https://github.com/biggora/trinte/wiki)**