# el 和 data 的變化

### el

el 除了在 Vue 構造方法內指定容器元素，也可以使用 `$mount` 方法設置。
使用 $mount 更加靈活，可搭配邏輯使用，如計時器。

第一種寫法 (屬性式):

```ts
new Vue({
  el: "#root",
  data: {
    message: "World",
  },
});
```

第二種寫法 (掛載式):

```ts
new Vue({
  data: {
    message: "World",
  },
}).$mount("#root");
```

### data

data 除了指定物件，也可以指定函式 (為了組件化開發)。

第一種寫法 (物件式):

```ts
new Vue({
  el: "#root",
  data: {
    message: "World",
  },
});
```

第二種寫法 (函數式):

```ts
new Vue({
  el: "#root",
  data() {
    return {
      message: "World",
    };
  },
});
```
