# Vue 導入

你可以`手動配置環境`或使用`構建工具`將 Vue 導入到項目中。

### 手動配置環境

#### 下載 Vue 或使用 CDN

```html
<script type="text/javascript" src="./vue.js"></script>
```

#### 使用 Vue

1. 想讓 Vue 工作，必須實體化 Vue 物件，並傳入配置項。
2. 為 Vue 指定容器元素 (root)，使其能被使用。
3. root 容器中的代碼被稱作 `Vue 模板`

#### Vue 注意事項

1. 一個 html 元素僅能被一個 Vue 物件託管。
2. 一個 Vue 物件僅能託管一個 html 元素。

```html
<body>
  <div id="root">
    <h1>Hello {{message}} !</h1>
  </div>
  <script>
    new Vue({
      el: "#root",
      data: {
        message: "World",
      },
    });
  </script>
</body>
```

### 使用構建工具
