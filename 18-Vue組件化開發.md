# Vue 組件化開發

組件，就是實現應用中局部功能的代碼和資源的集合。
組件化開發表示貫徹組件思想的編程方式。

### 為甚麼使用組件化開發 ?

現在網頁中，一個介面通常很複雜。
組件化開發可以做到簡化編碼，復用編碼，並提高運行效率。

### Vue 非單文件組件

表示一個文件中可以有多個組件。

#### 建立組件

使用 `Vue.extend()` 建立組件。
其中傳入引數為一配置項，和 Vue 實例幾乎一致。

注意:

1. 組件配置不能傳入 el。
2. data 配置必須是函數 (物件有引用關係，不得使用物件式)。
3. 使用 template 配置組件模板。

```js
const School = Vue.extend({
  template: `
    <div>
      <h2>學校名稱: {{name}}</h2>
      <h2>學校地址: {{address}}</h2>
    </div>
          `,
  data() {
    return {
      name: "新竹高中",
      address: "新竹",
    };
  },
});

const Sutdent = Vue.extend({
  template: `
  <div>
      <h2>學生姓名: {{name}}</h2>
      <h2>學生年齡: {{age}}</h2>
  </div>
          `,
  data() {
    return {
      name: "Dalufishe",
      age: 18,
    };
  },
});
```

#### 註冊組件

在 Vue 實例物件中 使用 components 配置項註冊組件。

```js
const vm = new Vue({
  el: "#root",
  components: { School, Sutdent },
});
```

#### 使用組件

```html
<div id="root">
  <School></School>
  <hr />
  <Student></Student>
</div>
```

#### 組件的注意點

- 關於組件名:

1. 推薦使用 CamelCase 命名 or kebab-case 命名法。
2. CamelCase 命名需要有建構工具支撐。

- name 配置項:

可為組件新增一 name 配置項，作為提示性組件名稱 (開發工具顯示)。

- 關於自閉寫法:

組件可以使用自閉寫法 `<hello/>`，但須要有構建工具支撐。

- Vue.extend() 簡寫

可直接撰寫配置對象，Vue 內部會幫你自動調用 Vue.extend()

完整寫法:

```js
const Component = Vue.extend({
    ...
})
```

簡寫:

```js
const Component = {
    ...
}
```

#### VueComponent

使用 Vue.extend() 建立出來的組件為 VueComponent，為一構造函數。
注意: Vue.extend() 每次調用都會返回 `新的` VueComponent 構造函數。

Vue 會在解析模板時將建立 VueComponent 實例，簡稱 vc。
組件配置中的 data, methods, watch, compututed 中的函數的 this 值均是 vc。

重點: vc 幾乎等於 vm (差別體現在配置項及局部性)，可以理解 vc 為小型的 vm (組件的運作機制幾乎就是 ViewModel)。

`VueComponent.prototype.__proto__ === Vue.prototype`

### Vue 單文件組件

表示一個文件中只包含有一個組件。
使用單文件組件是 Vue 開發主流的操作，對整體的開發體驗，組件化思想有緊密的結合。

#### .vue

Vue 使用後綴名 `.vue` 表示單文件組件。

和 scss, less 類似，瀏覽器無法直接讀取 .vue，需在構建階段進行編譯處理。我們可以使用 webpack loader 或構建工具編譯 vue 文件。

#### 語法

template 撰寫結構，script 撰寫邏輯，style 撰寫樣式。

```vue
<template>
  <div class="demo">
    <h2>學校名稱: {{ name }}</h2>
    <h2>學校地址: {{ address }}</h2>
  </div>
</template>

<script>
export default {
  name: "School",
  data() {
    return {
      name: "新竹高中",
      address: "新竹",
    };
  },
};
</script>

<style>
.demo {
  background: orange;
}
</style>
```
