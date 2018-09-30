# tutorial-drf-vue
Django Rest Framework with VUE 

## Step 1. Install vue-cli
```bash
npm install -g vue-cli
``` 

## Step 2. Setup view project
```bash
vue init webpack-simple nodejs
``` 
Answer questions as follows
```text
? Project name nodejs
? Project description NodeJS Project for Django project
? Author Cuauhtemoc <temoc@amdg-tech.com>
? License MIT
? Use sass? Yes
```
Install base vue project (this may take a while)
```bash
npm install
```

## Step 3. Install webpack tools and other libraries
In order to export the javascript files over to the django static 
directories you will need additional node packages to assist
the building and exporting of the scripts and assets.  To accomplish 
this the following packages are installed into the node environment:  

* [webpack-bundle-tracker](https://github.com/owais/webpack-bundle-tracker)
* [write-file-webpack-plugin](https://github.com/gajus/write-file-webpack-plugin)
* [vue-cookies](https://www.npmjs.com/package/vue-cookies)
* [cookies](https://github.com/js-cookie/js-cookie/)


```bash
npm install webpack-bundle-tracker --save-dev
npm install write-file-webpack-plugin --save-dev
npm install vue-cookies --save
npm install js-cookies --save
```

## Step 4. Update webpack configuration

Open webpack.config.js and perform these changes:

### Add bundle and write-file plugins
Add the following lines at the top of the file:

```vue
var BundleTracker = require('webpack-bundle-tracker')
var WriteFilePlugin = require('write-file-webpack-plugin')

```


### Update Output setting

**From**
```vue
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: 'build.js'
  },
```
**To**
```vue
  output: {
    path: path.resolve(__dirname, './static_assets'),
    publicPath: '/static/',
    filename: 'vue_webpack.js'
  },
  plugins: [
    new BundleTracker({filename: '../webpack-django.json'}),
    new WriteFilePlugin()
    ],  
```
#### Update devServer
Update devServer setting as shown below to help with debugging issues:

```vue
  devServer: {
    historyApiFallback: true,
    noInfo: false,
    overlay: true
  },
```

#### Update index.html
Update index.html as follows

**From**
```html
    <script src="/dist/build.js"></script>
```
**To**
```html
    <script src="/static/vue_webpack.js"></script>
```
Build and export the webpack files using the "run build" as shown below:
```bash
npm run build
```
Run the server
```bash
npm run dev
```

