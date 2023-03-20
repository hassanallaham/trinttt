**[Back to Home](https://github.com/biggora/trinte/wiki)**

How to create Controller via [CLI](http://en.wikipedia.org/wiki/Command-line_interface) [TrinteJS MVC](http://www.trintejs.com/)

## Table of contents
* [Command format](#command-format)
* [Create a REST](#empty-rest)
* [REST routes](#routes-rest)
* [REST requests](#response-rest)


<a name="command-format"></a>
### Command format
      format: trinte -g rest [rest name] [field(s)]

<a name="empty-rest"></a>
### Create a default REST with namespace 

    $ trinte -g rest v1#Post active:bool title content:text created:date author

Generated files, path like that:
```
    .
    |
    `-- app
        |-- models 
        |   `-- Post.js
        `-- controllers
            `-- v1
                `-- PostsController.js
            
```

Add routes in `/config/routes.js`
```js
       map.namespace("v1",function(v1){
           v1.resources("posts");
       });
```
<a name="routes-rest"></a>
will provide the following routes:

    method    route                           controller#action         helper method
    ---------------------------------------------------------------------------------
    GET       /v1/posts.:format?              v1/posts#index            pathTo.v1_posts()
    GET       /v1/posts/skip-limit.:format?   v1/posts#index            pathTo.paging_v1_posts(skip, limit)
    GET       /v1/posts/:id.:format?          v1/posts#show             pathTo.show_v1_post(post)
    POST      /v1/posts.:format?              v1/posts#create           pathTo.create_v1_posts()
    DELETE    /v1/posts/:id.:format?          v1/posts#destroy          pathTo.destroy_v1_post(post)
    PUT       /v1/posts/:id.:format?          v1/posts#update           pathTo.update_v1_post(post)
    DELETE    /v1/posts.:format?              v1/posts#destroyall       pathTo.destroy_v1_posts()

Default response format `JSON`.

<a name="response-rest"></a>
### REST requests

Example REST requests:
```
# Get all posts ordered bi id DESC
GET /v1/posts
# Get all posts ordered bi id DESC in XML format
GET /v1/posts.xml
# Get last 10 posts ordered bi id DESC
GET /v1/posts/1-10
# Get last 10 active posts ordered bi id ASC
GET /v1/posts/1-10?active=1&sort=id
# Get all active posts where title 'MyFirst' ordered bi id ASC
GET /v1/posts?active=1&title=MyFirst&sort=id
```

Example JSON response:
```
{
  "title": "Posts",
  "first_page": 1,
  "curent_page": 1,
  "total_pages": 1,
  "items_per_page": 20,
  "items_total": 0,
  "items_start": 0,
  "items_end": 20,
  "items": [{
       "id" : 1,
       "active" : 1, 
       "title" : "My first Post",
       "content" : "Lorem ipsum"
       "created" : "2014-01-01T19:00:00" 
       "author" : "Aleksej Gordejev"
  },{
       "id" : 2,
       "active" : 1, 
       "title" : "My second Post",
       "content" : "Lorem ipsum"
       "created" : "2014-01-01T19:10:00" 
       "author" : "Aleksej Gordejev"
  }]
}
```

Example XML response:
```
<root>
  <title>Posts</title>
  <first_page>1</first_page>
  <curent_page>1</curent_page>
  <total_pages>1</total_pages>
  <items_per_page>20</items_per_page>
  <items_total>0</items_total>
  <items_start>0</items_start>
  <items_end>20</items_end>
  <items>
    <item>
       <id>1</id>
       <active>1</active> 
       <title>My first Post</title>
       <content>Lorem ipsum</content>
       <created>2014-01-01T19:00:00</created>
       <author>Aleksej Gordejev</author>
    </item>
    <item>
       <id>2</id>
       <active>1</active> 
       <title>My second Post</title>
       <content>Lorem ipsum</content>
       <created>2014-01-01T19:10:00</created>
       <author>Aleksej Gordejev</author>
    </item>
  </items>
</root>
```
**[Back to Home](https://github.com/biggora/trinte/wiki)**