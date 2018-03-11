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
```js
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

First a prerequsite - [node-gyp](https://github.com/nodejs/node-gyp)

I'm on windows so I did this in an elevated PowerShell: 
```
> npm install --global --production windows-build-tools 
```
It will probably take a while. 

Next we need to add python to our node path: 
```
> npm config set python C:\Users\USERNAME\.windows-build-tools\python27\python.exe
```
Or add it to your path... You know the drill. 


We're going to get Ganache-cli
And drizzle talking to each other... Hopefully. 

First we'll install truffle globally: 
`> npm install -g truffle` 

And our ganache-cli: 
`> npm install -g ganache-cli`

Now you'll probably need to re-open your terminal and possibly restart your computer. 

Let's test our new ganache abilities:

`> ganache-cli -b 3 -d `
This will open a test rpc instance in dev mode with a block time of three units. I believe it's seconds. 

#### COOL Now we're ready for contracts! 

I'm going to start by creating a new folder, in this case truff-n-stuff. 
```
mkdir truff-n-stuff
cd truff-n-stuff
```

Then I'm going to cd into that folder and run: 

`> truffle init` 

That will create our first contracts and allow us to manage contract deployment with migrations. 
At this point it's a good idea to have one terminal instance to run ganache-cli and another one to do migrations and all other dev stuff. 

We'll finish setting up truffle by changing our `truff-n-stuff\truffle.js` to this: 
```
module.exports = {
  migrations_directory: "./migrations",
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    }
  },
  solc: {
    optimizer: {
      enabled: true,
      runs: 500
    }
  } 
};
```

Now in one terminal start the ganache-cli: 
`> ganache-cli -b 3` 

And in your other compile and migrate your contracts in the truff-n-stuff directory: 
`\truff-n-stuff> truffle compile`
`\truff-n-stuff> truffle migrate`
`\truff-n-stuff> truffle migrate --reset` <- this one might come in handy. It will reset your contracts. 

Awesome! We're speaking blockchain. 
Let's build a simple storage contract: 

```
pragma solidity ^0.4.18;

contract SimpleStorage {
  event StorageSet(
    string _message
  );

  uint public storedData;

  function set(uint x) public {
    storedData = x;

    StorageSet("Data stored successfully!");
  }
}
```

This is solc a new programming language for Ethereum Contract Dev -> It get compiled to bytecode and deployed when you run truffle migrate. 

We'll also need to add a file to our migrations directory with instructions for truffle on how to put our contract on the chain. 

Our new file will be: `\truff-n-stuff\migrations\2_deploy_contracts.js

And this is what it's contents are: (<- is this proper grammer?)

```
var SimpleStorage = artifacts.require("./SimpleStorage.sol");

module.exports = function(deployer) {
  deployer.deploy(SimpleStorage);
};
```

Cool, now let's re-run our compile and migrate commands: 

`\truff-n-stuff> truffle compile`
`\truff-n-stuff> truffle migrate --reset`

Now inside of `truff-n-stuff\build\contracts\SimpleStorage.json` you can see the details of our deployed contract like the bytecode and the abi! 














Some Relevant Links:

[Ethereum/Web3 GitHub](https://github.com/ethereum/web3.js/)
