# Vue 數據代理

Vue 在數據中 (Model) 中參雜了數據代理機制。

其內部使用了 ES6 的 Object.defineProperty() 實現。

### Object.defineProperty()

Object.defineProperty() 為 ES6 推出的元編程函數，其功能為對物件屬性進行高級配置，如可列舉性、可寫入、可刪除等。

Object.defineProperty() 傳入三個引數，物件、屬性名和配置項:

```ts
let person = {
  name: "Eason",
  sex: "M",
};

Object.defineProperty(person, "age", {
  enumerable: true,
  configurable: true,
  writable: true,
});
```

Object.defineProperty() 有個特殊的配置 get，表示選擇器 (getter)，其機制為每當屬性被訪問，則會調用其中的 get 方法。

案例:

將 person 物件 age 屬性設置 getter，其返回 number。

```ts
let number = 18;
let person = {
  name: "Eason",
  sex: "M",
};

Object.defineProperty(person, "age", {
  enumerable: true,
  configurable: true,
  get() {
    return number;
  },
});
```

當 number 發生改變，age 屬性也會發生改變 (數據綁定)。

```bash
person.age
>> 18

number = 16;
person.age
>> 16
```

Vue 本身的數據綁定以及數據代理的實現均是透過以上方式實現。

### 數據代理

通過一個物件，對另一個物件中屬性進行操作，稱數據代理。

例:

obj2 代理 obj

```ts
let obj = { x: 100 };
let obj2 = {};

Object.defineProperty(obj2, "x", {
  get() {
    return obj.x;
  },
  set(value) {
    obj.x = value;
  },
});
```

Vue 在設計 MVVM 架構數據操作的時候，使用了兩個物件表示數據 (data 及 vm 物件)，他們之間實現數據綁定 (data 發生改變，vm 物件也發生改變，反之亦然)，其稱作數據代理，為了簡化開發而生。

### Vue 設計思想

Vue 為了讓編碼更加方便，設計了數據代理。

當沒有數據代理，模板操作數據都須直接訪問原始的 data 物件 (等同於 vm 中的 \_data 屬性)，其操作會變得極為麻煩:

```html
<div id="root">
  <h1>學校名稱: {{_data.name}}</h1>
  <h1>學校地址: {{_data.address}}</h1>
</div>
```

有了數據代理，數據能在 vm 物件上被訪問:

```html
<div id="root">
  <h1>學校名稱: {{name}}</h1>
  <h1>學校地址: {{address}}</h1>
</div>
```
