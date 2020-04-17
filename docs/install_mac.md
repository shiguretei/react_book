# Instllation process for macOS

## 2-4 Install Node.js

### If Homebrew installed

```shell
brew -v
brew update
brew install nodejs
node -v
```


### If Homebrew is't installed

Download and install latest version from https://nodejs.org/ja/

```shell
node -v
```


## 2-6 Create a project for installation

* Create a project.

```shell
mkdir hello_react
cd hello_react
npm init -y
```


* Change a package.json file.

```json
{
  "name": "hello_react",
  "version": "1.0.0",
  "description": "Hello React",
  "private": true,
  "main": "index.js",
  "scripts": {
    "start": "webpack-dev-server",
    "webpack": "webpack -d"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

## 2-7 Install node packages

```shell
npm install react react-dom
npm install webpack webpack-cli webpack-dev-server --save-dev
npm install @babel/core @babel/preset-env @babel/preset-react @babel/cli --save-dev
npm install eslint babel-eslint eslint-loader eslint-plugin-react --save-dev
npm install css-loader style-loader babel-loader --save-dev
```


## 2-8 Create sample code

* Make directories.

```shell
mkdir src
mkdir public
```


* Create a .babelrc file.

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```
* Create a .eslintrc.json file.

```json
{
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "es6": true
  },
  "parserOptions": {
    "sourceType": "module",
    "ecmaFeatures": {
      "experimentalObjectRestSpread": true,
      "jsx": true
    }
  },
  "extends": ["eslint:recommended", "plugin:react/recommended"],
  "plugins": ["react"],
  "rules": {
    "no-console": "off"
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  }
}
```
* Create a webpack.config.js file.

```js
module.exports = {
  entry: {
    app: "./src/index.js"
  },
  output: {
    path: __dirname + '/public/js',
    filename: "[name].js"
  },
    devServer: {
    contentBase: __dirname + '/public',
    port: 8080,
    publicPath: '/js/'
  },
  devtool: "eval-source-map",
  mode: 'development',
  module: {
    rules: [{
      test: /\.js$/,
      enforce: "pre",
      exclude: /node_modules/,
      loader: "eslint-loader"
    }, {
      test: /\.css$/,
      loader: ["style-loader","css-loader"]
    }, {
      test: /\.js$/,
      exclude: /node_modules/,
      loader: 'babel-loader'
     }]
  }
};
```

* Create a public/index.html file.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta http-equiv="X-UA-Compatible" content="IE=Edge, chrome=1" />
  <title>React App</title>
</head>
<body>
  <div id="root"></div>
  <script type="text/javascript" src="js/app.js" charset="utf-8"></script>
</body>
</html>
```

* Create a src/index.js file.

```js
import React from 'react'
import ReactDOM from 'react-dom'

ReactDOM.render(
  <h1>Hello, react!!</h1>,
  document.getElementById('root')
)
```

*  Check

```shell
npm start
```

If you see this message `webpack: Compiled successfully.` in the terminal, try access `http://localhost:8080` .