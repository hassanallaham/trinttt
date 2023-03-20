**[Back to Home](https://github.com/biggora/trinte/wiki)**

How to create View(s) via [CLI](http://en.wikipedia.org/wiki/Command-line_interface) [TrinteJS MVC](http://www.trintejs.com/)

### Table of contents
* [Command format](#command-format)
* [Create a View](#empty-view)
* [Create a View with namespace](#namespace-view)

<a name="command-format"></a>
### Command format

      format: trinte -g view [view name]

<a name="empty-view"></a>
### Create a View

    $ trinte -g view Post

Generated files, path like that:
```
    .
    |
    `-- app
        `-- views
            `-- posts
                |-- edit.ejs
                |-- form.ejs
                |-- index.ejs
                |-- new.ejs
                `-- show.ejs
```
<a name="namespace-view"></a>
### Create a View(s) with namespace

    $ trinte -g view admin#User

Generated files with namespace, path like that:
```
    .
    |
    `-- app
        `-- views
            `-- admin
                `-- posts
                    |-- edit.ejs
                    |-- form.ejs
                    |-- index.ejs
                    |-- new.ejs
                    `-- show.ejs
```


**[Back to Home](https://github.com/biggora/trinte/wiki)**
