# MusicList
A website for tracking music and albums

This is a change to an existing file

# Installing React Necessities - Video 23
yarn add react react-dom webpack babel-loader babel-core babel-jest babel-preset-react sass-loader node-sass

yarn add babel-preset-es2017

# Installing Webpack Hot-Reloading - Video 27
yarn add --dev webpack-dev-server react-hot-loader
yarn add --dev react-hot-loader@next
yarn add --dev react-hot-loader

# Installing Webpack Hot-Reloading - Video 28
yarn add react-hot-loader@next

# Troubleshooting "public" folder and will remove subfolders
images
javascripts
stylesheets

=========================================================================
### New

const { resolve } = require('path');
const webpack = require('webpack');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

const cssOutputLocation = process.env.NODE_ENV === 'production' ?
  'public/stylesheets/style-prod.css' :
  'stylesheets/style.css';

const jsProdOutput = {
  filename: 'public/javascripts/build-prod.js',
  path: resolve(__dirname),
  publicPath: '/',
};

const jsDevOutput = {
  filename: 'javascripts/build.js',
  path: '/',
  publicPath: '/',
};

const jsOutputLocation = process.env.NODE_ENV === 'production' ? jsProdOutput : jsDevOutput;

module.exports = {
  context: resolve(__dirname, 'src'),
  entry: [
    './index.jsx',
  ],
  output: jsOutputLocation,
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /(node_modules|bower_components|public\/)/,
        loader: 'babel-loader',
      },
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: 'css-loader',
        }),
      },
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          use: [
            {
              loader: 'css-loader',
            },
            {
              loader: 'sass-loader',
            },
          ],
          fallback: 'style-loader',
        }),
      },
    ],
  },
  plugins: [
    new webpack.NamedModulesPlugin(),
    new webpack.NoEmitOnErrorsPlugin(),
    new ExtractTextPlugin(cssOutputLocation),
  ],
};

if (process.env.NODE_ENV === 'production') {
  module.exports.plugins.push(new webpack.optimize.UglifyJsPlugin());
}

if (process.env.NODE_ENV !== 'production') {
  module.exports.entry.unshift(
    'react-hot-loader/patch',
    'react-hot-loader/babel',
    'webpack-hot-middleware/client',
  );
  module.exports.plugins.unshift(new webpack.HotModuleReplacementPlugin());
}

=============================================================================
### Old

const { resolve } = require('path');
const webpack = require('webpack');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

const cssOutputLocation = process.env.NODE_ENV === 'production' ?
  'public/stylesheets/style-prod.css' :
  'stylesheets/style.css';

const jsProdOutput = {
  filename: 'public/javascripts/build-prod.js',
  path: resolve(__dirname),
  publicPath: '/',
};

const jsDevOutput = {
  filename: 'javascripts/build.js',
  path: '/',
  publicPath: '/',
};

const jsOutputLocation = process.env.NODE_ENV === 'production' ? jsProdOutput : jsDevOutput;

module.exports = {
  context: resolve(__dirname, 'src'),
  entry: [
    './index.jsx',
  ],
  output: jsOutputLocation,
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /(node_modules|bower_components|public\/)/,
        loader: 'babel-loader',
      },
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: 'css-loader',
        }),
      },
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          use: [
            {
              loader: 'css-loader',
            },
            {
              loader: 'sass-loader',
            },
          ],
          fallback: 'style-loader',
        }),
      },
    ],
  },
  plugins: [
    new webpack.NamedModulesPlugin(),
    new webpack.NoEmitOnErrorsPlugin(),
    new ExtractTextPlugin(cssOutputLocation),
  ],
};

if (process.env.NODE_ENV === 'production') {
  module.exports.plugins.push(new webpack.optimize.UglifyJsPlugin());
}

if (process.env.NODE_ENV !== 'production') {
  module.exports.entry.unshift(
    'react-hot-loader/patch',
    'react-hot-loader/babel',
    'webpack-hot-middleware/client',
  );
  module.exports.plugins.unshift(new webpack.HotModuleReplacementPlugin());
}
