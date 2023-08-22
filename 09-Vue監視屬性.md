# Vue 監視屬性

在某些情況下，我們需要監視某屬性發生的變化，已進行相對應的操作。

```html
<div id="root">
  <button @click="changeValue">切換</button>
</div>
<script>
  new Vue({
    el: "#root",
    data: {
      v: true,
    },

    methods: {
      changeValue() {
        this.v = !this.v;
      },
    },
    watch: {
      v: {
        handler(newValue, oldValue) {
          console.log(newValue, oldValue);
        },
      },
    },
  });
</script>
```

配置 watch，指定屬性並加上 handler，該 handler 會在屬性發生變化執行，並傳入兩參數，代表變化前 / 後的值。

除了在初始化 Vue 實例配置監視屬性，也可以使用 vm.$watch() 動態配置監視屬性。

### 立即監視

監視屬性默認情況是當屬性值發生變化而執行。使用立即監視，可使的屬性在初始化時 handle 被額外調用一次。

配置 immediate 屬性為 true，開啟立即監視。

### 深度監視

Vue 在默認情況下是淺層監視，即為監視的值是該值本身。

```html
<div id="root">
  <button @click="number.a--">-</button>
  <span>{{number.a}}</span>
  <button @click="number.a++">+</button>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      number: { a: 0, b: 0 },
    },
    watch: {
      number: {
        handler() {
          console.log("hello");
        },
      },
    },
  });
</script>
```

如上，number 監視的是 number 物件本身，而非其中屬性，故屬性值變化不會打印 "Hello"。

可對該監視配置 `deep` 屬性為 true，則可以開啟深度監視，達成監視其中屬性的效果 (打印 "Hello")。

```html
<div id="root">
  <button @click="number.a--">-</button>
  <span>{{number.a}}</span>
  <button @click="number.a++">+</button>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      number: { a: 0, b: 0 },
    },
    watch: {
      number: {
        deep: true,
        handler() {
          console.log("hello");
        },
      },
    },
  });
</script>
```

### 完整寫法 & 簡寫

當不需要使用配置項，則可使用簡寫:

完整 (配置項):

```js
new Vue({
  el: "#root",
  data: { v: true },
  methods: {
    changeValue() {
      this.v = !this.v;
    },
  },
  watch: {
    v: {
      handler(newValue, oldValue) {
        console.log(newValue, oldValue);
      },
    },
  },
});
```

簡寫 (使用 function 簡寫):

```js
new Vue({
  el: "#root",
  data: { v: true },
  methods: {
    changeValue() {
      this.v = !this.v;
    },
  },
  watch: {
    v(newValue, oldValue) {
      console.log(newValue, oldValue);
    },
  },
});
```

### 監視屬性 vs 計算屬性

在牽扯到數據的計算時，使用監視屬性或計算屬性均可達到一樣的效果，但是:

- 計算屬性較監視屬性更簡潔，內部對於數據的自動監測大於監視屬性的命令式操作。
- 計算屬性功能較為限縮，自動監測只能用於做數據的變化，監視屬性則可以做更複雜的操作。
- 計算屬性的計算過程是整合在屬性中的，使用監視屬性則是獨立於屬性外。