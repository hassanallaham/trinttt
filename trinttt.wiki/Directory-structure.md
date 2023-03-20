**[Back to Home](https://github.com/biggora/trinte/wiki)**

* [Created Application](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Application configuration](https://github.com/biggora/trinte/wiki/Application-configuration)
  * [Directory structure](https://github.com/biggora/trinte/wiki/Directory-Structure)
  * [Routing and params](https://github.com/biggora/trinte/wiki/Routes)
  * [Middleware](https://github.com/biggora/trinte/wiki/Middleware)

On initialization directories tree generated, like that:

    .
    |-- app
    |   |-- models
    |   |   |-- Category.js
    |   |   |-- ...
    |   |   `-- User.js
    |   |-- controllers
    |   |   |-- AppController.js
    |   |   |-- ...
    |   |   `-- UsersController.js
    |   |-- heplers
    |   |   |-- ApplicationHelper.js
    |   |   |-- ModelsHelper.js
    |   |   `-- ViewsHelper.js
    |   |-- lib
    |   |   |-- inflection.js
    |   |   |-- pager.js
    |   |   `-- tools.js
    |   `-- views
    |       |-- app
    |       |   `-- index.ejs
    |       `-- posts
    |       |   |-- edit.ejs
    |       |   |-- index.ejs
    |       |   `-- new.ejs
    |       |-- errors
    |       |   |-- 404.ejs
    |       |   |-- ...
    |       |   `-- 500.ejs
    |       |-- default_layout.ejs
    |       |-- error_layout.ejs
    |       `-- messages.ejs
    |-- bin
    |   |-- flash.js
    |   |-- ...
    |   `-- trinte.js
    |-- config
    |   |-- env
    |   |   |-- development.js
    |   |   |-- production.js
    |   |   `-- test.js
    |   |-- locales
    |   |   |-- en.yml
    |   |   |-- ...
    |   |   `-- ru.yml
    |   |-- configuration.js
    |   |-- database.js
    |   |-- environment.js
    |   |-- middleware.js
    |   |-- params.js
    |   |-- routes.js
    |   `-- session.js
    |-- public
    |   |-- css
    |   |   `-- ...
    |   |-- js
    |   |   `-- ...
    |   `-- img
    |       `-- ...
    |-- .trinte-status
    |-- app.js
    |-- app-cluster.js
    `-- package.json


**[Back to Home](https://github.com/biggora/trinte/wiki)**