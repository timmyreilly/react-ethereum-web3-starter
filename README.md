# React Ethereum Web3 Starter

Confused? Same. 

Hopefully the branches of this repository will help you and I come to grips with developing DAPPS!

They're the future after all! 

Here's what we've done so far: 
```
> npm init 
// defaults are fine for now
> npm install -g webpack 
> npm install webpack-cli -g 
// -D saves to dev dependancies 
``` 

This gives us a basic JavaScript setup... 
Let's next add Webpack: 

```
> npm install webpack-cli -D
> webpack-cli init 
// Accept the defaults except multiple bundles - set to No 
```
Next you'll need to update the webpack.config.js with some tests: 
For JavaScript: 
`test: /\.js$/,`
For css: 
`test: /\.css$/,`

Now run webpack: 
`webpack` 

You'll probably get a `WARNING in configuration The 'mode' option has not been set...`

Add mode to your exports
Like this: 
```json
module.exports = {

	entry: "./src/js/index.js",

	mode: 'development', 
...
```
Now you'll not get that warning! Lolz! 

Okay, no you'll have a new /dist folder in your root. 
This has your bundled code.

Next I added a index.html to my /dist folder. 

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <!-- <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" > -->
    <title>How to set up React, Webpack, and Web3</title>
</head>

<body>
    <h1>PUT YO APP HERE</h1> 
    <div class="root"></div>
</body>

</html>
```

Now let's setup our webpack-dev-server for hosting our site for development and testing. 

First I added this line to my package.json 'scripts':
`start: webpack-dev-server --hot --content-base dist/` 

And installed webpack-dev-server: 
`> npm install -D webpack-dev-server` 

Now start your server: 
`> npm run start` 

And visit: `http://localhost:8080/` in your browser and see your incredible site! 

Not much yet... Let's add react on the next branch. 

## Welcome to Branch B!

Let's do some cool, react stuff. 

First install react and react-dom: 

`> npm install -D react react-dom`

Also, we'll need babel-preset-react to get all the goodness out of our non-vanilla JavaScript. 

`> npm install --save-dev babel-cli babel-preset-react`

And update your webpack.config.js to handle babel. 
Now our new rules for javascript: 
```json
{
    test: /\.js$/,
    exclude: /node_modules/,
    loader: 'babel-loader',

    options: {
        presets: ['env', 'react']
    }
}
```

Add a re-write of index.js: 
```JavaScript
import React from 'react'; 
import ReactDOM from 'react-dom'; 

ReactDOM.render(
    <h1>Hello world</h1>,
    document.getElementById('root')
)
```

We'll also need to add our script tag in our index.html. 
Here's a snippet of our HTML: 
```html
<body>
    <h1>Put yo app here</h1>
    <div id="root"></div>
    <script src="./main.bundle.js"></script> 
</body>
```

Alright let's run it again: `npm run start` 

Cool! Now we've got some react on the DOM! 

Let's move to phase 3! 

## Phase 3

### Talking to the blockchain with Drizzle! 
Drizzle is a new thing from the Truffle crew. 

First a prerequsite - (node-gyp)[https://github.com/nodejs/node-gyp]

I'm on windows so I did this in an elevated PowerShell: 
```
> npm install --global --production windows-build-tools 
```

We're going to get Ganache-cli
And drizzle talking to each other... Hopefully. 

First we'll install truffle globall: 
`> npm install -g truffle` 




















Some Relevant Links:

[Ethereum/Web3 GitHub](https://github.com/ethereum/web3.js/)
