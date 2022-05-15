![Banner](./images/webpack.png)

#### Table Of Contents

**[Webpack Cheatsheet](#webpack-cheatsheet)**

- [Installation](#installation)

- [Loaders](#loaders) `[to import stuff]`

- [Plugins](#plugins) `[to perform actions]`

- [Development and Production Builds](#development-and-production-builds) 

- [Multi Page Applications](#multi-page-applications)

- [Extras](#extras) `[adding bootstrap,font awesome]`

- [ES Lint](#es-lint)

---

# Webpack Cheatsheet

> Link to an Awesome Webpack Boilerplate : [Athlon Webpack boilerplate](https://github.com/WeAreAthlon/frontend-webpack-boilerplate)

## Installation

```bash
npm install webpack webpack-cli --save-dev
```

```js
//webpack.config.js
const path = require("path");

module.exports = {
   entry: "./src/index.js",
   output: {
      filename: "bundle.js",
      path: path.resolve(__dirname, "./dist"),
   },
   mode: "none",
};
```

using Webpack , we can now **export** and **import** data and files between each other.

---

## Loaders

Libraries that help to import stuff using webpack

### Adding  Images

```bash
npm install file-loader --save-dev
```

```js
//webpack.config.js
module.exports = {
   entry: "./src/index.js",
   output: {
      filename: "bundle.js",
      path: path.resolve(__dirname, "./dist"),
      publicPath: "", /* to specify image location for html , website URL in production */
   },
   mode: "none",
   module: {
      rules: [
         {
            test: /\.(png|jpg)$/,
            use: ["file-loader"],
         },
      ],
   },
};
```

```js
//index.js
import Kiwi from "./kiwi.jpg";
```

### Adding CSS in JS

```bash
npm install style-loader css-loader --save-dev
```

```js
//webpack.config.js
{
    test: /\.css$/,
    use: ["style-loader", "css-loader"],
},
```

```js
//component.js
import "./hello-world-button.css";
```

### Adding SCSS

```bash
npm install sass-loader sass --save-dev
```

```js
//webpack.config.js
{
    test: /\.scss$/,
    use: ["style-loader", "css-loader", "sass-loader"], //first style-loader at last sass-loader
},
```

```js
//component.js
import "./hello-world-button.scss";
```

### Adding Babel

```bash
npm install @babel/core babel-loader @babel/preset-env babel-plugin-transform-class-properties --save-dev
```

```js
//webpack.config.js
{
    test: /\.js$/,
    exclude: /node_modules/,
    use: {
        loader: "babel-loader",
        options: {
            presets: ["@babel/env"],
            plugins: ["transform-class-properties"],
        },
    },
},
```

---

## Plugins

Plugins Perform Specific Actions on the Imported Stuff

### Minify JS

```bash
npm install terser-webpack-plugin --save-dev
```

```js
//webpack.config.js
const TerserPlugin = require("terser-webpack-plugin");

/* Inside Module.exports */
plugins: [new TerserPlugin()],
```

---

### Extracting CSS into a Specific File

```bash
npm install mini-css-extract-plugin --save-dev
```

```js
//webpack.config.js
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
    rules = [
        {
            test: /\.css$/,
            use: [MiniCssExtractPlugin.loader, "css-loader"],
        },
        {
            test: /\.scss$/,
            use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"],
        },
    ]
}

plugins: [
    new MiniCssExtractPlugin({
        filename: "style.css",
    }),
],
```

----

### Generate New File Name Every Execution (only on content change)

```js
//simple add [contenthash] to the filename you want to have new name
filename: "bundle.[contenthash].js",
```

---

### Deleting Old Files and Rendering new on Every Build

```bash
npm install clean-webpack-plugin --save-dev
```

```js
//webpack.config.js

const { CleanWebpackPlugin } = require("clean-webpack-plugin");

// Running This PLugin without option , will automatically clean dist folder

plugins: [
    new CleanWebpackPlugin({
        cleanOnceBeforeBuildPatterns: [
            "**/*",  //this runs by default in dist folder
            path.join(process.cwd(), "build/**/*"), //adding other folders
        ],
    }),
],
```

---

### Generating HTML using Webpack

```bash
npm install html-webpack-plugin --save-dev 
```

```js
//webpack.config.js

const HtmlWebpackPlugin = require("html-webpack-plugin");

plugins: [
    new HtmlWebpackPlugin(), //generates default html file
]

//publicPath can be empty as html is generated in the same place as other files by default. (the path specified)
```

#### - Specifying Manual HTML options

```js
new HtmlWebpackPlugin({  //extra options for the html file
    title: "Hello World",
    filename: "subfolder/custom_filename.html",
    meta: {
        description: "Some Description",
    },
}),
```

#### -  Using HTML template Engine (HandleBars)

```bash
npm install handlebars-loader --save-dev
npm install handlebars --save
```

```js
// Add a Test in module rules for hbs files to use handlebars loader
{
    test: /\.hbs$/,
    use: ["handlebars-loader"],
}

//Also add the new plugin to access hbs
new HtmlWebpackPlugin({
    title: "Hello World",
    template: "src/index.hbs",
    description: "Some Description",
}),
```

---

## Development and Production Builds

### Changing Mode

```js
//webpack.config.js
module.exports = {
    mode : "production", //for production (here no source or anything is done)
    mode : "development", //source maps are rendered and development is faster
    mode : "none" //to not use any mode
}
```

---

### Creating Different Config for Different Modes

- Save Your Webpack configuration in different files , changing the mode specifically in both
- then create the npm scripts for specific files

```json
//package.json

"scripts": {
    "build": "webpack --config webpack.production.config.js",
    "dev": "webpack --config webpack.dev.config.js"
  },
```

---

### Using Webpack-dev-server in Development mode

```bash
npm install webpack-dev-server --save-dev
```

```js
//webpack.dev.config.js

module.exports = {
    devServer: {
         contentBase : path.resolve(__dirname, "./dist"),
         index: 'index.html',
         port: 9000
   }
}
```

```json
//package.json

scripts = {
    "dev": "webpack-dev-server --config webpack.dev.config.js --hot"
}
```

---

## Multi Page Applications

### Rendering Multiple Pages

```js
//webpack.production.config.js

module.exports = {
    entry: {
        'hello-world': './src/hello-world.js', //file 1
        'kiwi': './src/kiwi.js', // file 2
    },
    output: {
        filename: "[name].[contenthash].js", //will generate different names
        path: path.resolve(__dirname, "./dist"),
        publicPath: "",
    },
    plugins: [
        new MiniCssExtractPlugin({
            filename: "[name].[contenthash].css", //same for css files
        }),
        new HtmlWebpackPlugin({
         filename: 'hello-world.html', //different Html Files
         chunks: ['hello-world'], //is used from entry point
         title: "Hello World",
         description: "Hello World",
         template: "src/page-template.hbs",
      }),
      new HtmlWebpackPlugin({
         filename: 'kiwi.html',
         chunks: ['kiwi'], //specify only the ones u need
         title: "Kiwi",
         description: "Kiwi",
         template: "src/page-template.hbs",
      }),
    ]
}
```

### Creating Common File for Dependencies

```js
//webpack.production.config.js

module.exports = {
    optimization: {
        splitChunks: {
            chunks: "all", //this will integrate all the extra packages into one extra js file 
            minSize : 10000, //this specifies the minimum size of the bundle to split
             automaticNameDelimiter: '_' //this specifies the separation between file names , by default ~
        }
    },  
    plugins : [
        new HtmlWebpackPlugin({
            chunks: ['hello-world'],
        }),
        new HtmlWebpackPlugin({
            chunks: ['kiwi'],
        }),
    ] // integrating the extra modules js file into the HTML 

}
```

---

## Extras

### Adding Custom Fonts

```js
//webpack.config.js
{
    test: /\.{woff2|woff}$/,
    use: [
        {
            loader: 'file-loader',
            options: {
                name: '[name].[ext]',
                outputPath: 'fonts/',
            }
        }
    ],
}

//add font face in scss 
//import scss in js
```

### Adding Bootstrap

```bash
npm install bootstrap jquery popper.js --save
```

- Use Bootstrap , without editing it

```js
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
```

- Use Precompiled Bootstrap

```bash
npm install postcss-loader precss autoprefixer --save-dev
```

```js
//webpack.config.js

test: /\.scss$/,
    use: [
        MiniCssExtractPlugin.loader,
        "css-loader",
        {
            loader: "postcss-loader",
            options: {
                plugins: function () {
                    return [require("precss"), require("autoprefixer")];
                },
            },
        },
        "sass-loader",
    ],
```

```scss
//index.scss
@import "~bootstrap/scss/bootstrap";
```

### Adding Font Awesome

- Installing Core packages to only include needed icons in final bundle

```bash
npm install --save-dev @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/free-regular-svg-icons @fortawesome/free-brands-svg-icons
```

```js
//index.js

import { library, dom } from "@fortawesome/fontawesome-svg-core";
//library is used to import the specific icon , dom replaces i tag in DOM
import { faSpinner } from "@fortawesome/free-solid-svg-icons";
// import only the icons needed 


library.add(faSpinner); //puts the icon in the library
dom.watch(); //watches for changes in the html, and replaces every font awesome <i> tag
```

```html
<!-- index.html -->

<i class="fas fa-spinner fa-spin"></i> 
<!-- simply consume the icon needed -->
```

---

## ES Lint

- This file specifies basic rules to check for errors in js , especially used for linting and providing universal using standard. 

```bash
npm install eslint babel-eslint --save-dev
```

- create `.eslintrc.json` (can be generated too , check out docs)

```json
{
    "extends": "eslint:recommended", //recommended settings
    "parser": "babel-eslint", // babel for classes
    "parserOptions": { //for es6 import and others
        "ecmaVersion": 6,
        "sourceType": "module"
    }, 
    "env": {
        "node": true, //tells we are using node , for "require"
        "browser": true //tells running in browser , for "document"
    },
    "rules": { //specific rules that we want to add
        "no-console": 0
    }
}
```

- manually run eslint using `eslint .`
- or Install specific Linter plugins in your Editor to get the errors while coding itself.

---
