# [svgo](https://github.com/svg/svgo) loader for [webpack](https://github.com/webpack/webpack)

## Install

```
$ npm install svgo svgo-loader --save-dev
```

... or with Yarn

```
$ yarn add svgo svgo-loader -D
```

DON'T FORGET TO INSTALL / UPDATE THE `svgo` PACKAGE after you update `svg-loader` (see [#20](https://github.com/rpominov/svgo-loader/issues/20))

## Usage

[Documentation: Using loaders](http://webpack.github.io/docs/using-loaders.html)

Svgo-loader just passes config
to the [svgo](https://github.com/svg/svgo) library.

### Webpack 2

``` javascript
{
  test: /\.svg$/,
  use: [
    {
      loader: 'file-loader'
    },
    {
      loader: 'svgo-loader',
      options: {
        plugins: [
          {removeTitle: true},
          {convertColors: {shorthex: false}},
          {convertPathData: false}
        ]
      }
    }
  ]
}
```

### Webpack 1

There is two ways of loading svgo configuration.
You can pass it as a JSON string after loader name, like this:

``` javascript
// webpack.config.js

var svgoConfig = JSON.stringify({
  plugins: [
    {removeTitle: true},
    {convertColors: {shorthex: false}},
    {convertPathData: false}
  ]
});

module.exports = {
  ...
  module: {
    loaders: [
      {
        test: /.*\.svg$/,
        loaders: [
          'file-loader',
          'svgo-loader?' + svgoConfig
        ]
      }
    ]
  }
}
```

Or you can save svgo config in your main webpack config object,
and then specify name of the property in the loader query string.

However, this option will not work in Webpack 2.<br>This is only shown here in the documentation for backwards compatibility.

``` javascript
// webpack.config.js

module.exports = {
  ...
  module: {
    loaders: [
      {
        test: /.*\.svg$/,
        loaders: [
          'file-loader',
          'svgo-loader?useConfig=svgoConfig1'
        ]
      }
    ]
  },
  svgoConfig1: {
    plugins: [
      {removeTitle: true},
      {convertColors: {shorthex: false}},
      {convertPathData: false}
    ]
  }
}
```
