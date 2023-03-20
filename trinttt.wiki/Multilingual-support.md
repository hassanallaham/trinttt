* [Default language](https://github.com/biggora/trinte/wiki/Multilingual-support#default-language)
* [Dictionaries](https://github.com/biggora/trinte/wiki/Multilingual-support#dictionaries)
* [Translation](https://github.com/biggora/trinte/wiki/Multilingual-support#tkey-val)
* [Translate in Controller](https://github.com/biggora/trinte/wiki/Multilingual-support#translation-in-controller)
* [Translate in View](https://github.com/biggora/trinte/wiki/Multilingual-support#translation-in-view)
* [Switch language](https://github.com/biggora/trinte/wiki/Multilingual-support#switch-language)

#### Default language
Set your default language in `config/configuration.js`
```js
module.exports = {
    debug: false,
    language: "en",
    ...
}
```

#### Dictionaries
Dictionaries located `config/locales/*`, writed in the YAML Format.
```
    .
    `-- config
        `-- locales
            |-- en.yml
            |-- ...
            `-- ru.yml
```

#### #t(key, [val])
   Parameters:
   - key  String - translation key (reqired)
   - val  String - default value (optional)

#### Translation in the Controller

```js
module.exports = {
    ...
    'index': function(req, res, next) {
         var title = res.locals.t('main.title');

    ...
    }
}
```
#### Translation in the View

```html
   <h1><%- t('main.title') %></h1>

```

#### Switch language

```html
 <a href="/?language=ru">RU</a>
 <a href="/?language=en">EN</a>
```