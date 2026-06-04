# Harness 概念

Harness Engineering 鷹架工程

Agent = Model + Harness

軟體工程的競爭力已從「寫程式碼的速度」轉向「設計 AI 執行環境 (Harness) 的能力」

## 概念

- 運作閉環：Harness 將 AI 置於「行動 -> 觀察 -> 修正」的迴圈中，人類掌舵、代理執行，透過測試失敗等感測訊號讓 AI 修正重試。
- 效能差異：相同模型在不同 Harness 下表現差異極大，有實測指出，同樣使用 Claude Opus 模型，在 Cursor 與 Claude Code 中表現相差甚大。
- 對抗脈絡腐化 (Context Rot)：輸入過多 token 會降低精準度，建議維持 Context Window 使用率在 40-60%，避免雜訊、錯誤去覆蓋有效約束。
- 三層工程：
  - Prompt Engineering：單次對話的措辭優化。
  - Context Engineering：最大化有效訊號，避免雜訊干擾。
  - Harness Engineering：建構執行環境、工具、沙箱和約束機制。

## Harness 的七大元件

- 系統提示詞：定義目標、規則與環境。
- 工具集：提供原子化且定義清晰的工具 (如 MCP 標準)。
- 沙箱環境：隔離執行以確保安全運作。
- 記憶機制：將記憶外部化，如使用精簡的 AGENTS.md (建議 60-100 行內) 與 Append-only 事件日誌。
- 編排邏輯：利用 Sub-Agent 作為脈絡防火牆，將子任務交給低成本模型，主模型僅做協調。
- Hooks/Middleware：攔截與處理生命週期事件 (如自動壓縮記憶)。
- 架構約束：透過 CI、Linters 等機械化關卡強制約束 AI 行為。

## 導入路線圖

1. Level 1：建立 AGENTS.md + Linting + Auto Testing。
2. Level 2：導入 Sub-Agent 分工與共用工具。
3. Level 3：建立自訂 Middleware 與技術債回收機制。
