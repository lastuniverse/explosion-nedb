# explosion-nedb
This in middleware for use explosion with nedb.

## Download this repository
```
git clone https://github.com/lastuniverse/explosion-nedb.git
```
## Install  via npm
```
npm install explosion-nedb
```

for latest unstable version use:
```
npm install https://github.com/lastuniverse/explosion-nedb/tarball/master
```

## Usage

### on server side

index.js
```
var explosion = require( 'explosion' );
var nedb = require('explosion-nedb');
var path = require('path');

var app = explosion( server );

app.use(
  nedb({
    app: app,
    path: path.join(__dirname,'data/nedb'),
    ext: 'json'
  })
);

// open 'users' db
app.nedb.open('users'); 

// set index for 'users' db
app.nedb.index('users','_id');

// set compactification timeout for 'users' db
app.nedb.compact('users',1000*60*10);

// insert data to 'users' db
app.nedb.db.users.insert(
  { _id: 1, expires: 2, data: {test: "test"} }, 
  function (err, newDoc) {
    if (err)
      return console.log("nedb", err);
    return console.log("nedb OK");
  }
);

// update data to 'users' db
app.nedb.db.users.update(
  { "_id": 1 },
  { data: data, expires: expires }, 
  {}, 
  function (err, numReplaced) {
    if (err)
      return console.log("nedb", err);
    return console.log("nedb OK");
  }
);

// Get all messages send from all clients to "/system/..." distributions
wsapp.use( "/system/users", function( req, res, next ) {
  if( req.data.method == 'get' && req.data.user_id ){
    // get data from 'users' db
    req.app.nedb.db.users.findOne(
      { "_id": user_id },
      function (err, json) {
        if( err ){
        }else{
          console.log("get data",json);
          // Define confirmation of receipt message.
          // It will be sent automatically when the client is waiting for confirmation
          res.confirm = json;
          // deny processing of the next middleware handler
          res.end();
        }
      }
    );
  }else{
    // allow processing of the next middleware handler
    next();
  }
});

// start explosion server
var port = 3000;
server.on( 'request', app );
server.listen( port, function() {
  console.log( 'Listening on ' + server.address().port )
} );
```


[NeDB](https://github.com/louischatriot/nedb) - The detailed documentation for NeDB


## Participation in development
```
https://github.com/lastuniverse/explosion/issues
```
## License

MIT

## Important

library development is not yet complete


[![NPM](https://nodei.co/npm/explosion.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/explosion/)
