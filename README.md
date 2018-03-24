## electron-node-loader

This Webpack modules allows you to load a native Node.js C++ addon that can be shipped inside an Electron application.

_Usage:_

Let's picture an application folder:
```
project/
├── dist/
├── src/
│   └── main.js
└── scripts/
    └── addon.node
```
From your JavaScript code, you should be importing your custom module that way:
```javascript
import * as addon from '../scripts/addon.node';

...

addon.doStuff();
```

When building your Electron app during development, add this rule to your Webpack config file:
```javascript
loaders: [
  {
    test: /\.node?$/,
    use: 'electron-node-loader'
  }
]
```

If you're using `electorn-builder` for production, just replace `electron-node-loader` with `electron-node-loader&prod=true`. You also need to add these lines in your `package.json`:
```json
"files": [
  "!scripts",
],
"extraResources": [
  "scripts/*.node",
]
```
That way, your native addons with be shipped in a special `resources` directory inside of your app and your production JavaScript will be looking for them at runtime with a relative path.
