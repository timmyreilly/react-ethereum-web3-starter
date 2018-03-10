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
    <div class="root"></div>
</body>

</html>
```




















Some Relevant Links:

[Ethereum/Web3 GitHub](https://github.com/ethereum/web3.js/)
