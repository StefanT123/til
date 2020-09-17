# Create alias for JS path

Creating a Webpack alias for my base JavaScript path allows me to avoid using relative paths when importing components.
[Link to webpack doc](https://webpack.js.org/configuration/resolve/#resolvealias)
```js
// webpack.config.js

const path = require('path');

module.exports = {
  //...
  resolve: {
    alias: {
      Utilities: path.resolve(__dirname, 'src/utilities/'),
      Templates: path.resolve(__dirname, 'src/templates/')
    }
  }
};

// in some file
import Utility from 'Utilities/utility';
import Template from 'Templates/template';
```

If you're using Laravel mix, you can set this in your `webpack.mix.js` file using the `webpackConfig()` method
```js
// webpack.mix.js
mix.webpackConfig({
    resolve: {
        alias: {
            '@': path.resolve('resources/js'),
        },
    },
});

// in some file
import Layout from '@/Compontnts/Layout';
```
