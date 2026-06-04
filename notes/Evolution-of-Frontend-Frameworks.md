# 前端框架演變史

前端框架問世時，為了好的效能採用 virtual dom，為什麼現在為了效能，又要直接操作 dom，有什麼不一樣？

## 第一階段
**代表技術：jQuery, vanilla js**
- 方式：直接操作 dom
- 做法：$('#name').text('Allen') 或 document.getElementById('name').textContent = 'Allen'

**Issue**
- 效能低落：頻繁讀寫 dom 導致瀏覽器不斷重排 Reflow 及重繪 Repaint
- 難以維護：容易產生義大利麵程式碼，難以追蹤哪一行程式碼做了什麼事，邏輯難懂

## 第二階段
**代表技術：AngularJS 1.x**
- 方式：雙向綁定、髒檢查 dirty checking
- 做法：最開始引入「數據驅動」的概念

**Issue**
- 他的髒檢查機制 Digest Cycle 在每次數據變動時，會檢查所有綁定的變數，頁面綁定元素超過某個數量閾值（可能 2000+），效能呈現斷崖式下跌

## 第三階段
**代表技術：React, Vue2**
- 方式：直接操作 dom 太慢，JavaScript 計算很快，所以用 JS 算好後再批次更新 dom
- 做法：用 virtual dom 透過 diff 演算法，將多次變更合併成一次最少 dom 操作
- 開發者只需關心「資料」、「狀態」，不用管「怎麼更新 dom」
- VDOM 是 JavaScript 物件，所以沒有一定要渲染成 HTML，也能渲染成 mobile app 原生元件，如 React Native

## 第四階段
**代表技術：Svelte, SolidJS, Vue Vapor Mode**
- 方式：JS 計算 VDOM diff 也是成本，在編譯階段先分析出更新資料的路徑
- 做法：在編譯階段 Build time 就靜態分析出「當變數 A 改變時，只需更新節點 B」
- Signal 機制：資料變動時，觸發對應的 DOM 更新方法，不需要比對整棵樹

---

## 核心問題解析

**Q：為什麼前端框架初期不直接操作 dom？**
A：當時缺乏強大的「編譯器靜態分析」技術。在沒有編譯器輔助的前提下，要實現數據驅動畫面更新，只有兩個方法：
1. 髒檢查：如 AngularJS，效能差
2. VDOM：如 React，雖然有 diff 開銷，但在當時已是執行效能最好的方法，反正 JS 計算遠快於 dom 操作

**Q：現在的「直接操作 dom」和過去有何不同？**
A：用完全不同的方式在操作 dom
1. 命令式：如 jQuery，開發者自己手寫，靠人力維護
 
依賴強大的 Runtime 暴力算出結果，在每次資料變動時全部比對一次

2. 宣告 + 生成：如 Vapor mode，開發者寫宣告式語法，如 `<div>{{ count }}</div>`，編譯器會分析出「資料與 dom 的連接路徑」，生成最佳化的 dom 操作程式碼

依賴強大的 Compiler 靜態分析，將分析工作從柳欠轉移到打包階段，瀏覽器只執行最單純的 JS 操作
