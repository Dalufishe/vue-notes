# Vue 指令

Vue 除了之前提過的 `v-bind`、`v-model` 等指令語法之外，還有一些常用的指令。
Vue 指令用作標籤內和 Vue 或系統 (真實 DOM) 相關的邏輯操作。

### v-text

`v-text` 的作用是在標籤中撰寫元素內容 (等同於替代版的插值語法)。

```html
<div id="root">
  <span v-text="name"></span>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: { name: "Fish" },
  });
</script>
```

### v-html

`v-html` 的作用是在標籤中撰寫元素內容，並支持結構的解析 (html)。

```html
<div id="root">
  <span v-html="name"></span>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: { name: "<h1>Fish</h1>" },
  });
</script>
```

請注意，在頁面注入 html 內容有嚴重的安全性問題，當牽扯到用戶輸入，恐會造成 XSS 腳本攻擊，造成頁面破壞或 cookie 盜取等問題。

### v-clock

`v-clock` 是一個特殊屬性，在 Vue 創建並接管容器後，會刪除 v-clock 屬性。

使用 css 搭配 v-clock 可以解決模組載入時間過長 (可能是網速過慢) 導致頁面錯誤加載 (載入 Vue 模板, 如 `{{name}}`) 問題。

```html
<style>
  [v-clock] {
    display: none;
  }
</style>
<div id="root" v-clock>
  <span>{{name}}</span>
</div>
<script>
  const vm = new Vue({
    ...
  });
</script>
```

原理:

1. 在 Vue 尚未加載時，v-clock 只是一個 html 屬性，可使用 css 隱藏。
2. 當 Vue 載入並接管容器，v-clock 被視為 Vue 指令，其被刪除則使 css 效果消失，元素則顯示出來。

### v-once

`v-once` 的作用於，節點初次動態渲染內容後，即被視為靜態內容了。

v-once 用於獲取 Vue 管理的數據之初始值，或為計算做優化。

### v-pre

`v-pre` 告訴 Vue 直接跳過編譯階段 (模板解析)，直被視為靜態內容了。

何 `v-once` 一樣被用於優化。

### 自訂義指令

Vue 也提供方法操作自訂義指令。

```html
<div id="root">
  <h2><span v-text="n"></span></h2>
  <h2><span v-big="n"></span></h2>
  <button @click="n++">click</button>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: { n: 0 },
    directives: {
      big(element, binding) {
        element.innerText = binding.value * 10;
      },
    },
  });
</script>
```

`directives` 配置分為物件式和函數式:

- 函數式: 傳入一個函式。
- 物件式: 傳入三個函式，bind(), inserted(), update()。

函數式自訂義令指會在模板被解析時調用，然而，第一次解析元素尚未掛載，故需要物件式自訂義指令進行更複雜的操作。
