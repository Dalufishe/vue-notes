# Vue 條件渲染

在 Vue 中我們可以使用 `v-show` 或 `v-if` 做條件渲染。

### v-show

v-show 指定 true / false，控制節點的顯示與否 (底層控制 display: none)。

```html
<div id="root">
  <h2 v-show="false">{{name}}</h2>
</div>
```

### v-if

v-if 指定 true / false，控制節點的掛載與否。

```html
<div id="root">
  <h2 v-if="false">{{name}}</h2>
</div>
```

注意: v-if 可搭配 v-else-if, v-else 使用，做更複雜的判斷 & 優化。

### v-if 與 template

當需要條件渲染一系列節點，除了在各節點上重複撰寫條件，將節點包裹住並在父節點做條件渲染是更佳的解法。

```html
<div id="root">
  <h2 v-show="false">Angular</h2>
  <h2 v-show="false">React</h2>
  <h2 v-show="false">Vue</h2>
</div>
```

改成

```html
<div id="root">
  <div v-show="false">
    <h2>Angular</h2>
    <h2>React</h2>
    <h2>Vue</h2>
  </div>
</div>
```

然而，這種做法會破壞 dom 結構，使用 Vue template，可撰寫不會在頁面顯示的節點，故不會破壞結構 (類似 React 的 Fragment)。

```html
<div id="root">
  <template v-if="false">
    <h2>Angular</h2>
    <h2>React</h2>
    <h2>Vue</h2>
  </ㄔ>
</div>
```

注意: template 只能搭配 `v-if` 使用。
