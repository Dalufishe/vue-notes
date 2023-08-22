# Vue 過濾器

過濾器就是函式的另一種撰寫方式。

```html
<div id="root">
  <span>當前格式化時間: {{time | timeFmter}}</span>
</div>
<script>
  const vm = new Vue({
    el: "#root",
    data: {
      time: Date.now(),
    },
    filters: {
      timeFmter(v) {
        return dayjs(v).format("YYYY-MM-DD HH:mm:ss");
      },
    },
  });
</script>
```

使用過濾器相較於一般函式 (或者說方法)，在小型計算中，擁有更高的可讀性。

