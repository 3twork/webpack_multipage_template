# webpack_multipage_kit

基于 Webpack 开发和构建 传统多页面静态站点的前端工程化方案，支持ie8+
同时适用于 PC 端和移动端。

## Requirements
* node `^5.0.0`
* yarn `^0.23.0` or npm `^3.0.0`

## 功能
- ES6语法支持
- IE8兼容
- 前端工程化
- 支持响应式
- 模块化
- 组件化
- 开发、调试和构建
- 集成 PostCSS、Sass

## Installation 安装

```bash
$ https://github.com/3twork/webpack_multipage_kit <my-project-name>
$ cd <my-project-name>
$ npm i
$ npm start //开始开发和调试
$ npm run build //压缩打包
$ npm run server //发布运行本地服务器
```
## 全局补丁
## 添加 polyfill
按需引入 polyfill，提高浏览器兼容性。
polyfill 在 `/src/public/js/polyfill.js` 文件中引入：
```js
// 1) Object.assign
Object.assign = require('object-assign')

// 2) Promise
if (typeof Promise === 'undefined') {
    require('promise/lib/rejection-tracking').enable()
    window.Promise = require('promise/lib/es6-extensions.js')
}

// 3) Fetch
// ------------------------------------
// Fetch polyfill depends on a Promise implementation, so it must come after
// the feature check / polyfill above.
if (typeof window.fetch === 'undefined') {
    require('whatwg-fetch')
}
// 3) 第三方工具库
if (typeof window._ === 'undefined') {
    require('lodash')
}
```

## 样式编写规范
请参照 BEM 规范，详情见：[https://github.com/zhaotoday/bem](https://github.com/zhaotoday/bem)，下面是一个例子：  
HTML 代码：
```html
<nav class="nav">
  <a href="#" class="nav__item nav__item--normal">正常状态</a>
  <a href="#" class="nav__item nav__item--active">当前状态</a>
  <a href="#" class="nav__item nav__item--hover">鼠标移上时的状态</a>
</nav>
```
Sass 代码：
```scss
.nav {
  &__item {
    &--normal {
    }
    &--active {
    }
    &--hover {
    }
  }
}
```
## 响应式开发
 ```npm i -D include-media```
```scss
@import "~include-media/dist/_include-media.scss";

$breakpoints: (phone: 320px, tablet: 768px, desktop: 1024px);

.selector {
  @include media("<=tablet") {
    background-color: red;
  }

  @include media(">tablet", "<desktop") {
    background-color: yellow;
  }

  @include media(">=desktop") {
    background-color: green;
  }
}
```

# 目录结构
```shell

.
├── README.md
├── bower.json
├── build
│   ├── filePath.js
│   ├── tool
│   │   ├── getFile.js
│   │   ├── logger.js
│   │   └── watchDirs.js
│   ├── webpack.config.base.js
│   ├── webpack.config.dev.js
│   └── webpack.config.production.js
├── config
│   ├── bin
│   │   └── server.js
│   └── setting.js
├── package-lock.json
├── package.json
├── src
│   ├── layout
│   │   ├── head
│   │   └── polyfill
│   ├── public
│   │   ├── img
│   │   ├── js
│   │   └── style
│   └── view
│       ├── about
│       └── home
└── static
    └── favicon.ico

```

