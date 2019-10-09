# Build NodeJS App with ES6 features and Dev/Prod env

## Create nodejs project

## Install dependencies

```
npm i --save-dev @babel/cli @babel/core @babel/node @babel/preset-env nodemon
npm i --save rimraf npm-run-all
```

## Create thoses scripts into package.json

```
"script": {
    "start": "npm run prod",
    "server": "babel-node ./src/bin/www",
    "server:prod": "node ./dist/bin/www",
    "dev": "NODE_ENV=development npm-run-all server",
    "clean": "rimraf dist",
    "build": "babel ./src --out-dir dist",
    "prod": "NODE_ENV=production npm-run-all clean build server:prod",
    "watch": "nodemon"  
}
```

## Create nodemon.json and .babelrc file at app's root folder

```
// nodemon.json
{
  "exec": "num run dev",
  "watch": ["src/*", "public/*"],
  "ext": "js, html, css, json"
}

// .babelrc
{
  "presets": ["@babel/preset-env"]
}

```

## Additionnals elements

```
npm install --save core-js
npm install --save regenerator-runtime
```

in index.js (app's entry point)

```
import "core-js/stable";
import "regenerator-runtime/runtime";
```


# RUN

npm run dev             // Run dev env
npm run watch           // Run dev env with nodemon (hot-reload)

npm start
npm run prod            // Run prod, create dist folder and exec
