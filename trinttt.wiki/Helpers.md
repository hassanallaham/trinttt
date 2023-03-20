**[Back to Home](https://github.com/biggora/trinte/wiki)**

### Application Helper

file location in project `/app/helpers/ApplicationHelper.js`

#### Define variables or any Custom Methods

```javascript
module.exports = {
    getClientIp: function(req) {
        var ipAddress;
        // The request may be forwarded from local web server.
        var forwardedIpsStr = req.header( 'x-forwarded-for' );
        if( forwardedIpsStr ) {
            // 'x-forwarded-for' header may return multiple IP addresses in
            // the format: "client IP, proxy 1 IP, proxy 2 IP" so take the
            // the first one
            var forwardedIps = forwardedIpsStr.split( ',' );
            ipAddress = forwardedIps[0];
        }
        if( !ipAddress ) {
            // If request was not forwarded
            ipAddress = req.connection.remoteAddress;
        }
        return ipAddress;
    }
...
};
```
### Views Helper

file location in project `/app/helpers/ViewsHelper.js`

#### Define variables or any Custom Methods

```javascript
module.exports = {
    normalizeDate: function(date) {
        if( typeof date === 'number' ) {
            return new Date( date ).toISOString();
        } else if( date.getTime ) {
            return date.toISOString();
        } else {
            return new Date().toISOString();
        }
    }
...
};
```
Available Views Helper Methods [here](https://github.com/biggora/trinte/wiki/Available-Views-Helper-Methods)

### Models Helper

file location in project `/app/helpers/ModelsHelper.js`

#### Setup Validations
```javascript
User.validatesPresenceOf('name', 'email')
User.validatesLengthOf('password', {min: 5, message: {min: 'Password is too short'}});
User.validatesInclusionOf('gender', {in: ['male', 'female']});
User.validatesExclusionOf('domain', {in: ['www', 'billing', 'admin']});
User.validatesNumericalityOf('age', {int: true});
User.validatesUniquenessOf('email', {message: 'email is not unique'});

user.isValid(function (valid) {
    if (!valid) {
        user.errors // hash of errors {attr: [errmessage, errmessage, ...], attr: ...}
    }
})
```

#### Setup Relationships

```javascript
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

// work with models:
var user = new User;
user.save(function (err) {
    var post = user.posts.build({title: 'Hello world'});
    post.save(console.log);
});
```

#### Define any Custom Method

```javascript
User.prototype.getNameAndAge = function () {
    return this.name + ', ' + this.age;
};
```

#### Define scope

```javascript
Post.scope('active', { published : true });

Post.active(function(err, posts){
    // your code here
});

```

#### Middleware (Hooks)

Models The following callbacks supported:

    - afterInitialize
    - beforeCreate
    - afterCreate
    - beforeSave
    - afterSave
    - beforeUpdate
    - afterUpdate
    - beforeDestroy
    - afterDestroy
    - beforeValidation
    - afterValidation


```javascript
User.afterUpdate = function (next) {
    this.updated_ts = new Date();
    this.save();
    // Pass control to the next
    next();
};
```

**[Back to Home](https://github.com/biggora/trinte/wiki)**