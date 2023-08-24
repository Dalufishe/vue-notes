# Vue-cli

`vue-cli` 是 Vue 官方提供的標準化開發的構建工具 (開發平台)。

### 具體步驟

1. 全局安裝

```bash
npm i @vue/cli -g
```

2. 建立 vue-cli 項目

```bash
vue create FILE_NAME
```

3. 啟動開發伺服器

```bash
npm run serve
```

### vui-cli 項目結構

- `bable.config.js` : babel 配置文件，用於 ES5 轉換。
- `vue.config.js` : Vue 配置文件。
- `src/main.js` : Vue 項目入口文件。
- `src/components` : Vue 組件存放區。
- `src/assets` : Vue 資源存放區。
- `public/index.html` : html 索引文件 (會再進行編譯)。

### render 屬性

使用 ES6 導入 Vue，默認導入是運行版的 Vue (`vue.runtime.esm.js`)，缺乏模板解析器。

- 缺乏模板解析器，此段程式不可執行。

```js
new Vue({
  template: `<App/>`,
  components: { App },
}).$mount("#app");
```

- 解決方法:

```js
new Vue({
  render: (h) => {
    return h(App);
  },
}).$mount("#app");
```

#### 為甚麼導入運行版的 Vue ?

為了減少體積。使用 vue-cli 構件 Vue 項目，在 .vue 模板被編譯成 .js 時順帶解析模板，轉為 js 讀得懂的結構體，之後 Vue 在瀏覽器改動數據不再是重新解析模板，而是重新解析 js 結構體。

### 修改默認配置

Vue cli 隱藏了所有 webpack 相關的配置，若想查看具體的 webpack 配置，請執行 `vue inspect > output.js`
若想修改 webpack 默認配置，請在 `vue.config.js` 中間接進行配置。

```js
const { defineConfig } = require("@vue/cli-service");
module.exports = defineConfig({
});
```

常用配置: 

1. pages: 配置路徑、檔名相關。
2. lintOnSave: 是否在每次存檔做 lint 檢查 (建議關閉，開發到一定階段再一次性檢查)。