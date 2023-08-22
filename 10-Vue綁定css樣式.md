# Vue 綁定 css 樣式

### class 綁定樣式

我們可以在 Vue 中使用 class 去處理樣式，並透過 `v-bind:class` 或 `:class` 來綁定樣式，並使用 Vue 操作。

#### 字串寫法

```html
<style>
  .a {
    color: red;
  }
  .b {
    color: blue;
  }
</style>
<div id="root">
  <h2 :class="color" @click="color='b'">{{name}}</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      name: "Dalufishe",
      color: "a",
    },
  });
</script>
```

#### Array 寫法

`:class` 除了可以解析字串表達式，傳入 Array 也可被解析，為一系列 class。

```html
<style>
  .a {
    color: red;
  }
  .b {
    background-color: blue;
  }
</style>
<div id="root">
  <h2 :class="color">{{name}}</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      name: "Dalufishe",
      color: ["a", "b"],
    },
  });
</script>
```

#### 物件寫法

`:class` 也可以傳入一 obj，並指定 true / false 值，為選擇性的 class。

```html
<style>
  .a {
    color: red;
  }
  .b {
    background-color: blue;
  }
</style>
<div id="root">
  <h2 :class="color">{{name}}</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      name: "Dalufishe",
      color: {
        a: true,
        b: false,
      },
    },
  });
</script>
```

### style 綁定樣式

我們也可以在 Vue 中使用 style 內聯樣式去處理樣式，並透過 `v-bind:style` 或 `:style` 來綁定樣式，並使用 Vue 操作。

#### 字串寫法

```html
<div id="root">
  <h2 :style="h2Style">{{name}}</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      name: "Dalufishe",
      h2Style: "font-size: 36px;",
    },
  });
</script>
```

#### 物件寫法

使用 Vue 提供的物件寫法更加簡單。

```html
<div id="root">
  <h2 :style="h2Style">{{name}}</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      name: "Dalufishe",
      h2Style: {
        fontSize: "36px",
      },
    },
  });
</script>
```

#### Array 寫法

使用物件寫法的樣式物件，可以透過 Array 進行包裹。

```html
<div id="root">
  <h2 :style="[h2Style, h2Style2]">{{name}}</h2>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      name: "Dalufishe",
      h2Style: { fontSize: "36px" },
      h2Style2: { backgroundColor: "red" },
    },
  });
</script>
```
