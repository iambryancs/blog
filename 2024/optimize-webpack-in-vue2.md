# Steps
- Use Speed Measure Plugin to debug webpack build time - https://github.com/stephencookdev/speed-measure-webpack-plugin
- Track your build time evolution to detect big evolution before merge
- Apply fixes
- Follow webpack performances recommandations
- Look at webpack 5 new caching strategies
- Keep your webpack config up to date


## speed-measure-webpack-plugin

### config
```js
// vue.config.js
const SpeedMeasurePlugin = require("speed-measure-webpack-plugin");

const smp = new SpeedMeasurePlugin({
  outputTarget: './smp.dat',
});

module.exports = {
  //...
  //...
  configureWebpack: smp.wrap({
    optimization: {
      splitChunks: {
        chunks: 'all'
      }
    }
  })
}
```

### output
```sh
 more client/smp.dat


 SMP  ⏱
General output time took 3 mins, 26.98 secs

 SMP  ⏱  Loaders
mini-css-extract-plugin, and
css-loader, and
postcss-loader, and
sass-loader took 1 min, 38.33 secs
  module count = 3
css-loader, and
postcss-loader, and
sass-loader took 1 min, 38.3 secs
  module count = 3
mini-css-extract-plugin, and
css-loader, and
vue-loader, and
postcss-loader, and
sass-loader, and
cache-loader, and
vue-loader took 1 min, 34.77 secs
  module count = 158
css-loader, and
vue-loader, and
postcss-loader, and
sass-loader, and
cache-loader, and
vue-loader took 1 min, 34.75 secs
  module count = 158
vue-loader, and
mini-css-extract-plugin, and
css-loader, and
postcss-loader, and
cache-loader, and
vue-loader took 1 min, 24.48 secs
  module count = 257
css-loader, and
vue-loader, and
postcss-loader, and
cache-loader, and
vue-loader took 1 min, 24.086 secs
  module count = 253
cache-loader, and
thread-loader, and
babel-loader, and
cache-loader, and
vue-loader took 1 min, 11.45 secs
  module count = 1049
modules with no loaders took 1 min, 10.68 secs
  module count = 3196
cache-loader, and
cache-loader, and
babel-loader, and
vue-loader, and
cache-loader, and
vue-loader took 1 min, 5.83 secs
  module count = 1116
cache-loader, and
vue-loader, and
eslint-loader took 1 min, 5.5 secs
  module count = 1111
mini-css-extract-plugin, and
css-loader, and
postcss-loader took 47.44 secs
  module count = 24
css-loader, and
postcss-loader took 46.71 secs
  module count = 24
cache-loader, and
thread-loader, and
babel-loader, and
eslint-loader took 22.67 secs
  module count = 292
url-loader took 12.64 secs
  module count = 163
css-loader, and
vue-loader, and
postcss-loader took 4.74 secs
  module count = 2
cache-loader, and
thread-loader, and
babel-loader took 4.16 secs
  module count = 30
vue-loader, and
mini-css-extract-plugin, and
css-loader, and
postcss-loader, and
mini-css-extract-plugin, and
css-loader, and
postcss-loader took 3.074 secs
  module count = 2
file-loader took 1.87 secs
  module count = 8
cache-loader, and
vue-loader took 0.799 secs
  module count = 10
vue-loader, and
cache-loader, and
babel-loader, and
vue-loader, and
cache-loader, and
vue-loader, and
eslint-loader took 0.549 secs
  module count = 1096
vue-loader, and
cache-loader, and
thread-loader, and
babel-loader, and
cache-loader, and
vue-loader, and
eslint-loader, and
eslint-loader took 0.503 secs
  module count = 1031
vue-loader, and
mini-css-extract-plugin, and
css-loader, and
postcss-loader, and
cache-loader, and
vue-loader, and
eslint-loader took 0.117 secs
  module count = 249
vue-loader, and
mini-css-extract-plugin, and
css-loader, and
postcss-loader, and
sass-loader, and
cache-loader, and
vue-loader, and
eslint-loader took 0.075 secs
  module count = 158
html-webpack-plugin took 0.028 secs
  module count = 1
script-loader took 0.001 secs
  module count = 1
raw-loader took 0.001 secs
  module count = 1
vue-loader took 0 secs
  module count = 1
```

## Sass

### uninstall node-sass
```sh
❯ npm uninstall node-sass
npm WARN ag-grid-vue@21.2.2 requires a peer of vue-property-decorator@^7.2.0 but none is installed. You must install peer dependencies yourself.
npm WARN eslint-config-airbnb@18.2.1 requires a peer of eslint-plugin-jsx-a11y@^6.4.1 but none is installed. You must install peer dependencies yourself.
npm WARN eslint-config-airbnb@18.2.1 requires a peer of eslint-plugin-react@^7.21.5 but none is installed. You must install peer dependencies yourself.
npm WARN eslint-config-airbnb@18.2.1 requires a peer of eslint-plugin-react-hooks@^4 || ^3 || ^2.3.0 || ^1.7.0 but none is installed. You must install peer dependencies yourself.
npm WARN vue-ckeditor2@2.1.5 requires a peer of ckeditor@>= 4 but none is installed. You must install peer dependencies yourself.
npm WARN vue-mapbox@0.4.1 requires a peer of mapbox-gl@^0.53.0 but none is installed. You must install peer dependencies yourself.
npm WARN vue-mapbox-geocoder@0.2.0 requires a peer of mapbox-gl@^0.53.0 but none is installed. You must install peer dependencies yourself.
npm WARN vue-mapbox-geocoder@0.2.0 requires a peer of vue-mapbox@^0.2.0 but none is installed. You must install peer dependencies yourself.
npm WARN vue-mapbox-geocoder@0.2.0 requires a peer of @mapbox/mapbox-gl-geocoder@^3.1.1 but none is installed. You must install peer dependencies yourself.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.3.3 (node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.3.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.13 (node_modules/watchpack-chokidar2/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.13 (node_modules/webpack-dev-server/node_modules/fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})

removed 91 packages and audited 2708 packages in 15.052s

158 packages are looking for funding
  run `npm fund` for details

found 158 vulnerabilities (12 low, 52 moderate, 58 high, 36 critical)
  run `npm audit fix` to fix them, or `npm audit` for details
```

### after removing node-sass, build still works - why? so node-sass is not needed?

### installed sass
```sh
npm i --save-dev sass
```

### then build, warnings:
```sh
Deprecation Warning: Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.

Recommendation: math.div($spacer, 2) or calc($spacer / 2)

More info and automated migrator: https://sass-lang.com/d/slash-div

   ╷
16 │ $spacer-sm: ($spacer / 2);
   │              ^^^^^^^^^^^
   ╵
    src/assets/scss/vuexy/_variables.scss 16:14                      @import
    src/assets/scss/vuexy/components/horizontalNavMenuItem.scss 1:9  @import
    stdin 2:9                                                        root stylesheet

```

### sass-loader upgrade
- dropped node 12 support in https://github.com/webpack-contrib/sass-loader/releases/tag/v13.0.0
- running `npm install --save-dev sass-loader` on node v14.21.3 installs `+ sass-loader@14.1.1`

### tried building again
#### packages installed:
```sh
"sass": "^1.74.1",
"sass-loader": "^14.1.1",
```

#### error:
```sh
 ERROR  Failed to compile with 1 error                                                           1:11:54 PM

 error  in ./src/assets/scss/main.scss

TypeError: this.getOptions is not a function


 @ ./src/main.js 79:0-33
 @ multi ./src/main.js
```
#### reason:
sass-loader@^11.x.x requires webpack 5
ref: https://stackoverflow.com/questions/66082397/typeerror-this-getoptions-is-not-a-function

#### current installed:
```sh
❯ npm list | grep webpack
│ └─┬ webpack@4.47.0
```

long-term goal, update to webpack 5 https://webpack.js.org/migrate/5/

#### remove sass-loader
```sh
npm uninstall sass-loader
```

#### install sass-loader v10
```sh
npm install --save-dev sass-loader@^10
...
...
+ sass-loader@10.5.2
```

#### run build again, error:
```sh
 ERROR  Failed to compile with 1 error                                                           1:29:57 PM

 error  in ./src/assets/scss/main.scss

SassError: Can't find stylesheet to import.
   ╷
11 │ @import "vuexy/extraComponents/awesomeSwiper";
   │         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   ╵
  src/assets/scss/vuexy/_extraComponents.scss 11:9  @import
  src/assets/scss/main.scss 15:9                    root stylesheet


 @ ./src/main.js 79:0-33
 @ multi ./src/main.js
```

- fixed by removing `vuexy/` from the paths of all imports in `_extraComponents.scss`
- moved smp.dat inorder to create a new file