**[Back to Documentation](https://github.com/biggora/trinte/wiki)**

How to create Controller via [CLI](http://en.wikipedia.org/wiki/Command-line_interface) [TrinteJS MVC](http://www.trintejs.com/)

## Table of contents
* [Command format](#command-format)
* [Create a Controller](#empty-controller)
* [Create a Controller with actions](#actions-controller)
* [Create a Controller with namespace](#namespace-controller)

<a name="command-format"></a>
### Command format
      format: trinte -g controller [controller name] [action(s)]

<a name="empty-controller"></a>
### Create a empty Controller

    $ trinte -g controller Post

<a name="actions-controller"></a>
### Create a Controller with actions

    $ trinte -g controller User index create edit delete

Generated files, path like that:
```
    .
    |
    `-- app
        `-- controllers
            |-- PostsController.js
            `-- ...
```
<a name="namespace-controller"></a>
### Create a Controller with namespace and actions

    $ trinte -g controller admin#Post index create edit delete

Generated files with namespace, path like that:
```
    .
    |
    `-- app
        `-- controllers
            `-- admin
                |-- PostsController.js
                `-- ...
```

**[Back to Documentation](https://github.com/biggora/trinte/wiki)**