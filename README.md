# 安装

#### 兼容性 {#兼容性}

Vue **不支持** IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有[兼容 ECMAScript 5 的浏览器](https://caniuse.com/#feat=es5)。

#### 更新日志 {#更新日志}

最新稳定版本：

每个版本的更新日志见 [GitHub](https://github.com/vuejs/vue/releases)。

### Vue Devtools {#vue-devtools}

在使用 Vue 时，我们推荐在你的浏览器上安装 [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools)。它允许你在一个更友好的界面中审查和调试 Vue 应用。

### 直接用 `<script>` 引入 {#直接用-script-引入}

直接下载并用 `<script>` 标签引入，`Vue` 会被注册为一个全局变量。

在开发环境下不要使用压缩版本，不然你就失去了所有常见错误相关的警告![开发版本](https://vuejs.org/js/vue.js)包含完整的警告和调试模式 [生产版本](https://vuejs.org/js/vue.min.js)删除了警告，KB min+gzip

#### CDN {#cdn}

我们推荐链接到一个你可以手动更新的指定版本号：

```text
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.13/dist/vue.js"></script>
```

你可以在 [cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue/) 浏览 NPM 包的源代码。

Vue 也可以在 [unpkg](https://unpkg.com/vue@/dist/vue.js) 和 [cdnjs](https://cdnjs.cloudflare.com/ajax/libs/vue//vue.js) 上获取 \(cdnjs 的版本更新可能略滞后\)。

请确认了解[不同构建版本](http://localhost:4000/docs/install.html#对不同构建版本的解释)并在你发布的站点中使用**生产环境版本**，把 `vue.js` 换成 `vue.min.js`。这是一个更小的构建，可以带来比开发环境下更快的速度体验。

### NPM {#npm}

在用 Vue 构建大型应用时推荐使用 NPM 安装[\[1\]](http://localhost:4000/docs/install.html#footnote-1)。NPM 能很好地和诸如 [webpack](https://webpack.js.org/) 或 [Browserify](http://browserify.org/) 模块打包器配合使用。同时 Vue 也提供配套工具来开发[单文件组件](http://localhost:4000/docs/single-file-components.html)。

```text
# 最新稳定版
$ npm install vue
```

### 命令行工具 \(CLI\) {#命令行工具-cli}

Vue 提供了一个[官方的 CLI](https://github.com/vuejs/vue-cli)，为单页面应用快速搭建 \(SPA\) 繁杂的脚手架。它为现代前端工作流提供了 batteries-included 的构建设置。只需要几分钟的时间就可以运行起来并带有热重载、保存时 lint 校验，以及生产环境可用的构建版本。更多详情可查阅 [Vue CLI 的文档](https://github.com/vuejs/vue-docs-zh-cn/blob/master/vue-cli/README.md#介绍)

CLI 工具假定用户对 Node.js 和相关构建工具有一定程度的了解。如果你是新手，我们强烈建议先在不用构建工具的情况下通读[指南](http://localhost:4000/docs/)，在熟悉 Vue 本身之后再使用 CLI。

### 对不同构建版本的解释 {#对不同构建版本的解释}

在 [NPM 包的 `dist/` 目录](https://cdn.jsdelivr.net/npm/vue/dist/)你将会找到很多不同的 Vue.js 构建版本。这里列出了它们之间的差别：

|  | UMD | CommonJS | ES Module |
| --- | --- | --- | --- | --- |
| **完整版** | vue.js | vue.common.js | vue.esm.js |
| **只包含运行时版** | vue.runtime.js | vue.runtime.common.js | vue.runtime.esm.js |
| **完整版 \(生产环境\)** | vue.min.js | - | - |
| **只包含运行时版 \(生产环境\)** | vue.runtime.min.js | - | - |

#### 术语 {#术语}

* **完整版**：同时包含编译器和运行时的版本。
* **编译器**：用来将模板字符串编译成为 JavaScript 渲染函数的代码。
* **运行时**：用来创建 Vue 实例、渲染并处理虚拟 DOM 等的代码。基本上就是除去编译器的其它一切。
* [**UMD**](https://github.com/umdjs/umd)：UMD 版本可以通过 `<script>` 标签直接用在浏览器中。jsDelivr CDN 的[https://cdn.jsdelivr.net/npm/vue](https://cdn.jsdelivr.net/npm/vue) 默认文件就是运行时 + 编译器的 UMD 版本 \(`vue.js`\)。
* [**CommonJS**](http://wiki.commonjs.org/wiki/Modules/1.1)：CommonJS 版本用来配合老的打包工具比如 [Browserify](http://browserify.org/) 或 [webpack 1](https://webpack.github.io/)。这些打包工具的默认文件 \(`pkg.main`\) 是只包含运行时的 CommonJS 版本 \(`vue.runtime.common.js`\)。
* [**ES Module**](http://exploringjs.com/es6/ch_modules.html)：ES module 版本用来配合现代打包工具比如 [webpack 2](https://webpack.js.org/) 或 [Rollup](https://rollupjs.org/)。这些打包工具的默认文件 \(`pkg.module`\) 是只包含运行时的 ES Module 版本 \(`vue.runtime.esm.js`\)。

#### 运行时 + 编译器 vs. 只包含运行时 {#运行时--编译器-vs-只包含运行时}

如果你需要在客户端编译模板 \(比如传入一个字符串给 `template` 选项，或挂载到一个元素上并以其 DOM 内部的 HTML 作为模板\)，就将需要加上编译器，即完整版：

```text
// 需要编译器
new Vue({
  template: '<div>{{ hi }}</div>'
})

// 不需要编译器
new Vue({
  render (h) {
    return h('div', this.hi)
  }
})
```

当使用 `vue-loader` 或 `vueify` 的时候，`*.vue` 文件内部的模板会在构建时预编译成 JavaScript。你在最终打好的包里实际上是不需要编译器的，所以只用运行时版本即可。

因为运行时版本相比完整版体积要小大约 30%，所以应该尽可能使用这个版本。如果你仍然希望使用完整版，则需要在打包工具里配置一个别名：



