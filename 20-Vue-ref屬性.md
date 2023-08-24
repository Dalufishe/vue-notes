# Vue ref 屬性

當我們在 Vue 中有操作節點的需求時，會通過 ref 和 $refs 達成。

使用 ref 屬性標示，$refs 獲取節點。

對原生標籤設置 ref，獲取到的是原生 DOM:

```html
<template>
  <div>
    <h1 ref="h1dom">{{ msg }}</h1>
    <button @click="showDOM">點我輸出訊息</button>
    <School />
  </div>
</template>

<script>
  import School from "./components/School.vue";

  export default {
    name: "App",
    components: { School },
    data() {
      return {
        msg: "歡迎學習 Vue",
      };
    },
    methods: {
      showDOM() {
        console.log(this.$refs.h1dom);
      },
    },
  };
</script>
```

對組件設置 ref，獲取到的是組件實例物件。
