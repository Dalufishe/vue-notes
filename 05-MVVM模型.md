# MVVM 模型

MVVM 是一軟體架構，由下列三點組成:

1. M: 模型 (Model)
2. V: 視圖 (View)
3. VM: 視圖模型 (ViewModel)

模型通常表示數據、數據模型；視圖則表示 GUI；視圖模型則表示他們之間溝通的橋樑 (通常是雙向的)。

### Vue 中的 MVVM

Vue 在設計上一定程度參考了 MVVM 模型 (model-view-viewmodel)。模型 (M) 在 Vue 中對應 data 中的數據，視圖 (V) 在 Vue 中對應模板及 DOM，視圖模型 (VM) 對應到 Vue 引擎本身，負責數據綁定。

```txt
Model (數據) <-> ViewModel (數據綁定) <-> View (模板)
```

因此我們通常使用 vm 作為 Vue 實體的變數名。
