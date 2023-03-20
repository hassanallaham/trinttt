**[Back to Home](https://github.com/biggora/trinte/wiki)**

* [Command format](https://github.com/biggora/trinte/wiki/Command-format)
* [Create and initialize app](https://github.com/biggora/trinte/wiki/Create-App)
* [Creates a Scaffold](https://github.com/biggora/trinte/wiki/Create-a-Scaffold)
* [Creates a Model](https://github.com/biggora/trinte/wiki/Create-a-Model)
* [Creates a Controller](https://github.com/biggora/trinte/wiki/Create-a-controller)
* [Creates a View](https://github.com/biggora/trinte/wiki/Create-a-View)
* [Creates a Rest](https://github.com/biggora/trinte/wiki/Create-a-Rest)
* [Field types](https://github.com/biggora/trinte/wiki/Create-a-Model#field-types)
* [Runs server](https://github.com/biggora/trinte/wiki/Runs-Server)

#### Usage: 

    trinte command [argument(s)] [option(s)]
 
#### Commands:

    -h, --help [name]            output usage information
    -V, --version                output the version number
    -i, --init <name> [opts]     create new mvc project with <name>
    -f, --force                  force on non-empty directory
    -s, --server [port]          run the application as a server.
    -c, --cluster [port]         run the application using the cluster module.
    -g, --generate <generator>   run a generator
    
#### Options:     
 
    --sess                       session store
    --auth                       authorization support
    --theme <name>               theme (default|black|blue|green|orange|pink|violet) 
    --db                         database [driver]:[database]:[port]:[username]:[password]
                                 drivers - redis|mongodb|mysql|sqlite3|postgres
                                 defaults to memory
            
#### Generators:

    controller <name>  [args]    Creates a controller
    model      <name>  [args]    Creates a model
    view       <name>  [args]    Creates a view
    crud       <name>  [args]    Creates a scaffold
    rest       <name>  [args]    Creates a rest
    test       <name>  [args]    Creates a test
    help       [name]            Show help 

#### Examples:
  
    # create new mvc project
    $ trinte -i Test -sess -auth
  
    # create new mvc project with db
    $ trinte -i Test -sess -auth -db mysql:test:3306:root 
    
    # create scaffold
    $ trinte -g crud Post active:bool name:string desc:text created:date



**[Back to Home](https://github.com/biggora/trinte/wiki)**
