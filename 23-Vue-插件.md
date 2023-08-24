# Vue 插件

Vue 插件使你的 Vue 應用更加強大。

### 使用插件

在 Vue 註冊插件，可以在 Vue 應用使用到插件所提供的功能。

```js
Vue.use(plugin1);
```

### 定義插件

定義插件，可接收 Vue 構造函數，透過此構造函數加強 Vue 本身的功能。

```js
export const plugin1 = {
  install(Vue) {
    // 定義全局過濾器
    Vue.filter("slice4", function (str) {
      return str.slice(0, 4);
    });

    // 定義全局 components
    Vue.component(...)
    
    //定義全局方法

    Vue.prototype.xxx = ...
  },
};
```
