# Vue 數據綁定

將 Vue 數據繫結到模板稱作數據綁定。在 Vue 中，數據綁定分為單向數據綁定及雙向數據綁定兩種。

### 單向數據綁定

單向數據綁定，數據僅能從 Vue 單向傳送至模板。過去我們使用 `v-bind` 做數據對接屬於單向數據綁定。

```html
<!-- value 改變，頁面會改變。但從 input 做輸入，value 不會改變 -->
單向數據綁定: <input type="text" v-bind:value="value" /> 
```

### 雙向數據綁定

雙向數據綁定需透過 `v-model` 操作，可理解成連鎖反應:

```html
<!-- value 改變，頁面會改變。input 做輸入，value 會改變 -->
雙向數據綁定: <input type="text" v-model:value="value" />
```


需注意，v-model 只能在表單類元素 (輸入類元素) 使用。

v-model:value 可省略成 v-model (因為 v-model 默認就是收集 value 內的值)。

### 原理 & 實現

Vue 數據綁定使用了 Object.defineProperty() getter & setter 技術實現。當數據發生改變，setter 會對頁面做響應式變化 (model -> view)，getter 則會保證數據的一致 (view -> model)。