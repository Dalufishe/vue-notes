# Vue props

props 用於組件之間做通信。

### 對組件傳入屬性

- 使用普通屬性傳入，值的部分是字串。

```vue
<template>
  <div>
    <Student name="Dalufishe" sex="男" age="18" />
  </div>
</template>
```

- 若需要傳入數字、布林值等類型，請使用 v-bind 屬性 (可傳入表達式)。

```vue
<template>
  <div>
    <Student name="Dalufishe" sex="男" :age="18 + 1" />
  </div>
</template>
```

### 配置屬性

- 簡單接收:

```vue
<script>
export default {
  name: "Student",
  data() {
    return {
      msg: "我是一個全端開發者",
    };
  },
  props: ["name", "sex", "age"],
};
</script>
```

- 類型限制接收:

```vue
<script>
export default {
  name: "Student",
  data() {
    return {
      msg: "我是一個全端開發者",
    };
  },
  props: {
    name: String,
    age: Number,
    sex: String,
  },
};
</script>
```

- 完整寫法接收 (類型限制、必要性限制、預設值) :

```vue
<script>
export default {
  name: "Student",
  data() {
    return {
      msg: "我是一個全端開發者",
    };
  },
  props: {
    name: {
      type: String,
      required: true,
    },
    age: {
      type: Number,
      default: 99,
    },
    sex: {
      type: String,
      required: true,
    },
  },
};
</script>
```

### 使用屬性

```vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <h2>學生姓名: {{ name }}</h2>
    <h2>學生年齡: {{ age }}</h2>
    <h2>學生性別: {{ sex }}</h2>
  </div>
</template>
```

### 注意事項

1. 傳入的屬性是不建議被修改的 (當有修改屬性的必要時，將屬性轉為 data，並修改 data)。

```vue
<script>
export default {
  name: "Student",
  data() {
    return {
      msg: "我是一個全端開發者",
      myAge: this.age,
    };
  },methods: {
    updateAge(){
        this.myAge++
    }
  }
  props: ["name", "sex", "age"],
};
</script>
```

2. 特殊屬性是不能被傳入的 (如 key)。