# NodeJS

## INSTALLATION

### Linux
```
sudo apt-get install curl software-properties-common
curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -

sudo apt-get install nodejs
```

## Initialisation

$ npm init

## BASE Packages

$ npm install -s assert boom dotenv hapi mongodb nodemon

$ npm install --save-dev @babel/core @babel/node @babel/plugin-syntax-dynamic-import @babel/preset-env

  => Create .babelrc file and add :
```
  " {
    "presets": [
      "@babel/preset-env"
    ],
    "plugins": [
      "@babel/plugin-syntax-dynamic-import"
    ]
  } "

  => Modify your script to add babel-node like this :
  " {
    'scripts': {
      'start': node babel-node index.js',
    }
  }"
```

## Create a basic server
  ```
  var http = require('http');

  var server = http.createServer(function(req, res) {
    res.writeHead(200);
    res.end('Salut tout le monde !');
  });
  server.listen(8080);
  ```
  _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

## Base pour générer du Json et accepter les demandes externes pour l'API

```
  app.use(function (req, res, next) {
      res.header('Content-Type', 'application/json');
      next();
  })
  app.use(function (req, res, next) {
      res.header('Access-Control-Allow-Origin', '*')
      res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept, Authorization");
      res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE,PATCH,OPTIONS')
      res.header('Access-Control-Allow-Credentials', true)
      next();
  })
```  

## Outils ESLINT & BABEL

  	/!\ Ne pas oublier de rajouter les fichier babelrc.json et eslintrc

      "babel-cli": "6.26.0",
      "babel-plugin-transform-flow-strip-types": "6.22.0",
      "babel-plugin-transform-object-rest-spread": "6.26.0",
      "babel-polyfill": "6.26.0",
      "babel-preset-env": "1.7.0",
      "babel-register": "6.26.0",
      "eslint": "5.1.0",
      "eslint-config-airbnb": "17.0.0",
      "eslint-plugin-flowtype": "2.50.0",
      "eslint-plugin-import": "2.13.0",
      "eslint-plugin-jest": "21.17.0",
      "eslint-plugin-jsx-a11y": "6.0.3",
      "eslint-plugin-react": "7.10.0",


## Base pour server Node.js qui communique

  const app = require('express')()
  /*const server = require('http').Server(app)*/
  const server = app.listen(8080)
  const io = require('socket.io').listen(server)


## package.json / Launch for Windows or Linux

  	-> Linux
  "start": "set NODE_ENV=development NODE_PATH=src/ yarn && ./node_modules/.bin/nodemon -I -w ./ ./App.js"
  	-> Windows
  "start": "set NODE_ENV=development NODE_PATH=src\\ yarn && .\\node_modules\\.bin\\nodemon -I -w .\\ .\\App.js"


## Passer un array type Map en paramètre de SockeT.io

  let m = new Map([['one', 1], ['ten', 10], ['hundred', 100]]);
  console.log(JSON.stringify(m));
  // "{}"		<== the result...

  	It’s very inelegant but I convert to an array-of-arrays on the server-side,
  	transmit that, and recreate the map on the client:

  let transitString = JSON.stringify(Array.from(m));
  console.log(transitString)
  // "[["one",1],["ten",10],["hundred",100]]"

  var newMap = new Map(JSON.parse(transitString));
  console.log(newMap)
  // Map {"one" => 1, "ten" => 10, "hundred" => 100}

  	So in your case, I’d do io.emit('user_change', Array.from(users));
  	on the server, and on the client, change the for loop to consume a
  	map: for (let user of (new Map(users))).
