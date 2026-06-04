# 重排 Reflow 與重繪 Repaint

## 核心影響

**重排 Reflow**
- 當 dom 的幾何屬性，如：寬高、位置改變時，或結構變化時，瀏覽器需要重新計算元素在畫面上的位置與大小
- 範例：resize window、text size、add/remove dom、read offsetWith
- 重排一定會重繪，因為位置變了，一定要重畫
- 渲染過程最昂貴的操作之一，一個元素重排，可能父元素、子元素、相鄰元素都要重排
- 瀏覽器要重新 render tree、計算座標，需要 CPU 大量運算

**重繪 Repaint**
- 外觀樣式改變，但不影響佈局
- 範例：`background-color`、`color`、`visibility`、`outline`
- 重繪不一定重排

**阻塞主執行緒 Main Tread Blocking**

- 兩者都是同步 Synchronous 操作，執行時會阻塞 JavaScript 執行及使用者互動，頻繁觸發（如 `scroll`）可能導致畫面卡頓

**重排最昂貴，重繪相對便宜，合成最快**

## Best Practices

- 避免修改樣式後，立即讀取佈局屬性，如 `offsetWith`, `scrollTop` 等，瀏覽器為了回傳正確數值，會執行重排
- 避免頻繁地單獨修改 style，如分別改 `width`, `height`, `left`
- <table> 內的變動，都可能導致整張表格重新計算佈局
- 批次修改 dom，透過切換 class 或一次寫入多個樣式
- 使用 `documentFragment` 在記憶體中組裝好元素，再一次插入 dom
- 優先使用 `transform`, `opacity`，這些屬性由合成器 Compositor 處理，跳過重排與重繪，由 GPU 負責處理，效能極佳
- 使用 `requestAnimationFrame` 將視覺更新操作安排在下次的重繪前執行，避免在 `scroll`, `resize` 這樣的高頻事件中運算
- 像動畫區塊這樣可能頻繁變動的元素，可用 `will-change: transform` 提示瀏覽器提升為獨立圖層，限制重排與重繪在此圖層內

## 對現代瀏覽器來說，是否仍是需要考慮的效能議題？

是。但評估角度已從「跑不跑得動」轉變為「使用者體驗是否流暢（60 FPS+）」及「裝置功耗」

**1. 效能瓶頸在於「主執行緒」**

瀏覽器的 JS 運算、樣式、佈局重排、重繪都在「同一個主執行緒」執行，如果某個操作佔用太多時間，就會卡住並影響使用者互動，導致頁面卡頓

**2. 強制同步佈局**

若邏輯不當，例如在迴圈中交錯讀取佈局和寫入樣式，瀏覽器會被迫暫停優化，反覆執行「計算 > 渲染 > 計算 > 渲染」

**3. 開發者錯覺**

可能在 macbook pro 開發，但使用者在舊款手機操作，CPU 運算能力相差極大，也對行動裝置的耗電有極大影響

## 檢測

可以透過 Chrome devtools 的 Performance 面板檢測 layout 分數
