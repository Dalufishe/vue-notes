# Vue 生命週期

Vue 組件有一系列的掛載、更新、銷毀流程，其稱為生命週期。
Vue 提供了一系列的生命週期函數，會在對應的時間點調對應的函數。

### 掛載流程

#### beforeCreate

Vue 實體物件剛建立，還無法訪問 data 或 methods。

例: this 中還尚未有 n 屬性及 add 方法。

```html
<div id="root">
  <h2>當前的 n 值是: {{n}}</h2>
  <button @click="add">add</button>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      n: 1,
    },
    methods: {
      add() {
        this.n++;
      },
    },
    beforeCreate() {
      console.log(this);
      debugger;
    },
  });
</script>
```

#### created

Vue 實體物件創立了一段時間，已可以訪問 data 或 methods。

```html
<div id="root">
  <h2>當前的 n 值是: {{n}}</h2>
  <button @click="add">add</button>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      n: 1,
    },
    methods: {
      add() {
        this.n++;
      },
    },
    created() {
      console.log(this);
      debugger;
    },
  });
</script>
```

#### beforeMount

模板及虛擬 DOM 剛解析完成時調用。此時頁面是模板狀態，並且不能操作真實 DOM。

#### mounted

將虛擬 DOM 轉為真實 DOM，並把真實 DOM 放入頁面 (掛載) 後調用 mounted。
其中 this 指向 vm。

例: 計時器在掛載後啟用。

```html
<div id="root">
  <h2 :style="{opacity}">歡迎學習 Vue</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      opacity: 1,
    },
    methods: {
      change() {
        setInterval(() => {
          this.opacity -= 0.01;
          if (this.opacity <= 0) {
            this.opacity = 1;
          }
        }, 16);
      },
    },
    mounted() {
      this.change();
    },
  });
</script>
```

### 更新流程

#### beforeUpdate

數據更新時觸發，此時數據是新的，但頁面仍是舊的。

#### updated

頁面完成更新，此時數據是新的，但頁面也是新的。

### 銷毀流程

#### beforeDestroy

當調用 vm 上的 $destroy() 方法，組件會進入銷毀程序。

beforeDestroy 會在即將銷毀時調用，此時數據、方法都是可用的。

注意: 在銷毀程序中修改數據均不會造成頁面更新。

#### destroyed

基本上可忽略。