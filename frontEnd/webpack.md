# Webpack


```javascript
// webpack.config.js

module.exports = {
    entry: './main.js',
    output: {
        filename: 'bundle.js'
    },
    resolve: {
        // you can now require('file') instead of require('file.coffee')
        extensions: ['', '.js', '.json', '.coffee']
    },
    module: {
        loaders: [
        { test: /\.coffee$/, loader: 'coffee-loader' },
        {
            test: /\.js$/,
            loader: 'babel-loader',
            query: {
                presets: ['es2015', 'react']
            }
        }
        ]
    },
};
```
