# Vue 計算屬性

在某些情況下，數據是一被計算的值。

### 使用表達式

使用表達式計算數據如下:

```html
<div id="root">
  姓: <input type="text" v-model="firstName" />
  <br />
  名: <input type="text" v-model="lastName" />
  <br />
  姓名: <span>{{firstName.slice(0, 3) + this.lastName.slice(0, 3)}}</span>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      firstName: "張",
      lastName: "三",
    },
  });
</script>
```

這在簡單計算下是可行的，但當計算稍微複雜，則在可讀性 (冗長的代碼) 及效能會有不好的影響 (大量重複計算)。

### 使用 methods

使用 methods 計算數據如下:

```html
<div id="root">
  姓: <input type="text" v-model="firstName" />
  <br />
  名: <input type="text" v-model="lastName" />
  <br />
  姓名: <span>{{fullName()}}</span>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      firstName: "張",
      lastName: "三",
    },
    methods: {
      fullName() {
        return this.firstName.slice(0, 3) + this.lastName.slice(0, 3);
      },
    },
  });
</script>
```

使用 methods 讓可讀性大大提升。然而，每當模板被重新解析 (數據發生變化)，方法都會被調用，使數據被重新計算，故效能仍不佳。

### 使用計算屬性

使用計算屬性計算數據如下:

```html
<div id="root">
  姓: <input type="text" v-model="firstName" />
  <br />
  名: <input type="text" v-model="lastName" />
  <br />
  姓名: <span>{{fullName}}</span>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      firstName: "張",
      lastName: "三",
    },
    computed: {
      fullName: {
        get() {
          return this.firstName.slice(0, 3) + this.lastName.slice(0, 3);
        },
      },
    },
  });
</script>
```

計算屬性使用了 getter + 緩存 & 依賴監視，大幅降低不必要的效能消耗。

- 當初次讀取計算屬性時，getter 被調用 (進行一次計算)。
- 當內部依賴數據發生改變 (this.firstName 或 this.lastName)，getter 被調用 (進行一次計算)。

若計算屬性有改動的必要，也可設置 setter。

### 完整寫法 & 簡寫

大部分情況沒有使用 setter 的必要，則可使用簡寫:

完整 (getter):

```js
 computed: {
      fullName: {
        get() {
          return this.firstName.slice(0, 3) + this.lastName.slice(0, 3);
        },
      },
    },
```

簡寫 (使用 function 簡寫):

```js
 computed: {
      fullName: function(){
          return this.firstName.slice(0, 3) + this.lastName.slice(0, 3);
         }

    },
```
