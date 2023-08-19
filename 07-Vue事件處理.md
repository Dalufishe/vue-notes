# Vue 事件處理

我們使用 `v-on:事件名稱` 指令語法做事件處理 (事件監聽):

```html
<div id="root">
  <h2>Hello {{name}}</h2>
  <button v-on:click="handleClick">click</button>
</div>
```

在 `methods` 區存儲方法:
注意: 在 methods 區存儲的方法跟 data 區存儲的數據差別在於 methods 區不做數據代理 (沒有 \_methods 也沒有 getter & setter，因為方法沒有更動的必要)。methods 區定義的方法最終都會出現在 vm 物件上。

```ts
new Vue({
  el: "#root",
  data: {
    name: "World",
  },
  methods: {
    handleClick() {
      alert("Hello");
    },
  },
});
```

被監聽器執行的方法，會帶有一 event 參數及一指向 vm 物件 的 this 值。

```ts
new Vue({
  el: "#root",
  data: {
    name: "World",
  },
  methods: {
    handleClick(evt) {
      alert(evt);
      alret(this);
    },
  },
});
```

`v-on:事件名稱` 也可簡寫為 `@事件名稱`。

```html
<div id="root">
  <button @click="handleClick">click</button>
</div>
```

### 無指定參 vs 指定參方法

若未對方法指定參數，方法會自動帶 event 物件。

```html
<div id="root">
  <button @click="handleClick">click</button>
</div>
```

```ts
new Vue({
  el: "#root",
  methods: {
    handleClick(evt) {
      alert(evt);
    },
  },
});
```

若對方法指定參數，則默認情況會丟失 event 物件，但可對其配置佔位符 `$event` 取回物件 (無關順序 & js 語法，其為 vue 模板解析器的規則)。

```html
<div id="root">
  <button @click="handleClick(321, $event)">click</button>
</div>
```

```ts
new Vue({
  el: "#root",
  methods: {
    handleClick(number, evt) {
      alert(evt);
    },
  },
});
```

### 事件修飾符

Vue 提供了一系列事件修飾符 (共 6 個)，用於簡化事件操作 (事件本身)。

1. prevent 修飾符

阻止默認行為，等同於 js 中 evt.preventDefault()。

```html
<div id="root">
  <button @click.prevent="handleClick">click</button>
</div>
```

2. stop 修飾符

阻止冒泡行為，等同於 js 中 evt.stopPropagation()。

```html
<div id="root">
  <button @click.stop="handleClick">click</button>
</div>
```

3. once 修飾符

事件只觸發一次。

```html
<div id="root">
  <button @click.once="handleClick">click</button>
</div>
```

4. capture 修飾符

使用事件的捕獲模式。

```html
<div id="root">
  <button @click.capture="handleClick">click</button>
</div>
```

5. self 修飾符

只有在 evt.target 是當前操作的元素才觸發事件 (類似 stop，但更加靈活)。

```html
<div id="root">
  <button @click.self="handleClick">click</button>
</div>
```

6. passive 修飾符

事件的默認行為立即執行，無需等待事件回調執行完畢。
注意: 不是所有事件都需等待，如 wheel 事件需要，scroll 則不用。

```html
<div id="root">
  <button @click.passive="handleClick">click</button>
</div>
```

### 事件別名

Vue 提供了一系列事件別名，用於簡化事件操作 (鍵盤事件)。

- enter
- delete
- esc
- space
- tab
- up
- down
- left
- right
- caps-lock
- ctrl
- alt
- shift
- meta
- a ~ z
- ...

例:

JS 處裡鍵盤邏輯:

```html
<div id="root">
  <input type="text" placeholder="按下 Enter 提示輸入" @keyup="showInfo" />
</div>
<script>
  Vue.config.productionTip = false;
  const vm = new Vue({
    el: "#root",
    data: {},
    methods: {
      showInfo(e) {
        if (e.key === "Enter") console.log(e.target.value);
      },
    },
  });
</script>
```

使用 Vue 提供的事件別名:

```html
<div id="root">
  <input
    type="text"
    placeholder="按下 Enter 提示輸入"
    @keyup.enter="showInfo"
  />
</div>
<script>
  Vue.config.productionTip = false;
  const vm = new Vue({
    el: "#root",
    data: {},
    methods: {
      showInfo(e) {
        console.log(e.target.value);
      },
    },
  });
</script>
```

#### 系統修飾鍵

系統修飾鍵 ctrl、alt、shift、meta 有一些特別的機制:

搭配 keyup: 按下 ctrl + 某鍵，放開該鍵觸發。

```js
  <input
    type="text"
    placeholder="按下 Enter 提示輸入"
    @keyup.ctrl="showInfo"
  />
```

搭配 keydown: 按下 ctrl 觸發 (正常運作)。

```js
  <input
    type="text"
    placeholder="按下 Enter 提示輸入"
    @keydown.ctrl="showInfo"
  />
```

指定 ctrl 按鍵，在 keydown 的含意是均要被按下，並非二擇一:

```js
  <input
    type="text"
    placeholder="按下 Enter 提示輸入"
    @keydown.ctrl.y="showInfo"
  />
```

#### 自訂義事件別名

```js
Vue.config.keyCodes.confirm = 13;
```

```html
<div id="root">
  <input
    type="text"
    placeholder="按下 Enter 提示輸入"
    @keyup.confirm="showInfo"
  />
</div>
<script>
  Vue.config.productionTip = false;
  const vm = new Vue({
    el: "#root",
    data: {},
    methods: {
      showInfo(e) {
        console.log(e.target.value);
      },
    },
  });
</script>
```
