# utilities
紀錄一些實際用到，解決某些情境的小程式

## Next.js

### 1. RouteParamsServerStore
- 在 page.tsx or layout.tsx 解析完 url 後，全域儲存 url path or params
- 在 server component 取得後，作為 fetch 參數
- 採用 promise 實作，避免在組件中，尚未取得解析完的 url 參數前，就先執行了 fetch 導致參數為空
