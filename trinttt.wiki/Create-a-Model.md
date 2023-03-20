**[Back to Home](https://github.com/biggora/trinte/wiki)**

How to create Model via [CLI](http://en.wikipedia.org/wiki/Command-line_interface) [TrinteJS MVC](http://www.trintejs.com/)

## Table of contents
* [Command format](#command-format)
* [Create a Model](#empty-model)
* [Create a Model with fields](#fields-model)
* [Created a Model example](#model-example)
* [Model Tuning](#model-extend)
* [Setup Model Validations](#field-validation)
* [Setup Models Relationships](#field-relationships)
* [Field types](#field-types)

<a name="command-format"></a>
### Command format
      format: trinte -g model [model name] [field(s)]

<a name="empty-model"></a>
### Create a Model

      // Create Post Model
      $ trinte -g model Post

<a name="fields-model"></a>
### Create a Model with fields

      // create User Model with fields name, email, password, active: Boolean
      $ trinte -g model User name email password active:boolean

Generated files, path like that:
```
    .
    |
    `-- app
        `-- models
            |-- User.js
            `-- ...
```

<a name="model-example"></a>
### Created Model example

```js
/**
 *  Define User Model
 *  @param {Object} schema
 *  @return {Object}
 **/
module.exports = function(schema){
    var User = schema.define('user', {
	      active : { type: Boolean },
	      name : { type: String },
	      email : { type: String },
	      password : { type: String }
    });
    return User;
};
```
<a name="field-types"></a>
### Field types
Following are all valid field types.

      String
      Number
      Date
      Boolean
      Text

Learn more on [CaminteJS](http://camintejs.com).

<a name="field-extend"></a>
### Model Tuning
```js
module.exports = function(schema){
    var Post = schema.define('Post', {
            active : { type : Boolean, 'default' : 1, index : true },
            title : { type: String,  limit: 255, require : true },
	    content : { type: schema.Text },
	    tags : { type: schema.JSON },
            created: { type: Date, default: Date.now, index: true }
    });
    return Post;
};
```
Learn more on [CaminteJS](http://camintejs.com).

<a name="field-validation"></a>
### Setup Model Validations

set validation in ModelsHelper file, location in project `/app/helpers/ModelsHelper.js`
```js
User.validatesPresenceOf('name', 'email')
User.validatesLengthOf('password', {min: 5, message: {min: 'Password is too short'}});
User.validatesInclusionOf('gender', {in: ['male', 'female']});
User.validatesExclusionOf('domain', {in: ['www', 'billing', 'admin']});
User.validatesNumericalityOf('age', {int: true});
User.validatesUniquenessOf('email', {message: 'email is not unique'});
```
usage in controller.
```js
user.isValid(function (valid) {
    if (!valid) {
        user.errors // hash of errors {attr: [errmessage, errmessage, ...], attr: ...}
    }
});
```
Learn more on [CaminteJS](http://camintejs.com).

<a name="field-relationships"></a>
### Setup Models Relationships

set relationships in ModelsHelper file, location in project `/app/helpers/ModelsHelper.js`

```js
User.hasMany(Post,   {as: 'posts',  foreignKey: 'userId'});
// creates instance methods:
// user.posts(conds)
// user.posts.build(data) // like new Post({userId: user.id});
// user.posts.create(data) // build and save

Post.belongsTo(User, {as: 'author', foreignKey: 'userId'});
// creates instance methods:
// post.author(callback) -- getter when called with function
// post.author() -- sync getter when called without params
// post.author(user) -- setter when called with object
```
usage in controller.
```js
// work with models:
var user = new User;
user.save(function (err) {
    var post = user.posts.build({title: 'Hello world'});
    post.save(console.log);
});
```
Learn more on [CaminteJS](http://camintejs.com).

**[Back to Home](https://github.com/biggora/trinte/wiki)**