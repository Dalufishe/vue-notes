# Vue mixins

Vue mixins (混入) 設計來復用配置項。

將配置項混入多個 vue 組件:

定義 (mixin.js):

```js
export default {
  methods: {
    showName() {
      alt(this.name);
    },
  },
  mounted() {
    alert("Hello");
  },
};
```

使用 (vue component):

```html
<script>
  import mixin from "../mixin";

  export default {
    name: "Student",
    data() {
      return {
        name: "張三",
        sex: "男",
      };
    },
    mixins: [mixin],
  };
</script>
```


### 優先級

當數據發生衝突，其優先級為 props > data > mixins。

### 全局混入

```js
Vue.mixin(混入1);
Vue.mixin(混入2);
```


