# Vue 列表渲染

Vue 使用 `v-for` 指令處理列表渲染 (所謂的列表渲染，是將一系列數據使用條列式的形式渲染出來)。

### v-for

在 Vue 中，我們透過迴圈的形式做列表渲染，使用 `v-for` 指令:

```html
<li v-for="value in data"></li>
```

or

```
<li v-for="value of data"></li>
```

#### 遍歷 Array

參數一: 值
參數二: 索引

```html
<div id="root">
  <h2>人員列表</h2>
  <ul>
    <li v-for="(user, index) in users">{{user.name}}-{{user.age}}</li>
  </ul>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      users: [
        { id: "001", name: "Dalufishe", age: 18 },
        { id: "002", name: "Yang", age: 19 },
        { id: "003", name: "Chad", age: 17 },
      ],
    },
  });
</script>
```

#### 遍歷物件

參數一: 值
參數二: 鍵

```html
<div id="root">
  <h2>人員列表</h2>
  <ul>
    <li v-for="(value, key) in user">{{key}}-{{value}}</li>
  </ul>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      user: { id: "001", name: "Dalufishe", age: 18 },
    },
  });
</script>
```

#### 遍歷字串

參數一: 字元
參數二: 索引

```html
<div id="root">
  <h2>人員列表</h2>
  <ul>
    <li v-for="(char, index) in string">{{char}}-{{index}}</li>
  </ul>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      string: "Hello World",
    },
  });
</script>
```

#### 遍歷指定次數

參數一: 數字
參數二: 索引

```html
<div id="root">
  <h2>人員列表</h2>
  <ul>
    <li v-for="(number, index) in 3">{{number}}-{{index}}</li>
  </ul>
</div>
<script>
  const vm = new Vue({
    el: "#root",
  });
</script>
```

### key

在做列表渲染時，最正確的寫法需添加 key。key 作為給節點添加一個唯一標示。

Q: 為甚麼需要添加唯一標示？
A: Vue 在做 VDOM diffing 運算時，對動態生成的列表中的節點須確保新舊一致性。否則，恐會造成效率低 (重複生成 DOM  ) 及數據錯亂等問題。

#### 錯誤示範: 不加 key

不加 key，節點間沒有唯一標示，Vue 會按照默認行為上到下比對 VDOM，造成不必要的效能消耗，並可能會造成數據錯亂。

#### 錯誤示範: 使用 index 當 key

此舉等同於自欺欺人。行為上和不加 key 一致，會造成問題。

#### 正確示範: 正確設定唯一標示

使用節點數據提供的唯一標示 (如 uuid)，正確比對 VDOM。