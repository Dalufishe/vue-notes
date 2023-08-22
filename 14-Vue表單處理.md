# Vue 表單處理

### v-model

我們在 Vue 中使用 v-model 操作雙向綁定。他是表單處理最核心的一部份。
注意: v-model 默認收集 value 值，此 value 值並非 html 標籤的 value 值，為 Vue 內部使用。

### form

通常我們使用 form 來包裝表單。
在現在 Web 開發，我們已經不使用 form 預設的頁面跳轉、action 發請求的寫法，單純作為頁面結構 & 使用方法。

取消 form submit 方法的預設行為: `@submit.prevent`

### input 的注意項

1. 若 input type 為 "text"，v-model 收集的是 value 值，用戶輸入的就是 value 值。
2. 若 input type 為 "radio"，v-model 收集的是 value 值，且要給標籤配置 value 值。
3. 若 input type 為 "checkbox":
   1. v-model 的初始值非 Array，那麼收集到的是 value 值為標籤的 checked 值，是 boolean。
   2. v-model 的初始值是 Array，那麼收集到的就是 value 值組成的 Array。

### v-model 的三個配置項

- lazy: 失去焦點再收集數據。
- number: 收集輸入內有效的數字 (原先是收集字串)。
- trim: 對輸入首尾做空格過濾。