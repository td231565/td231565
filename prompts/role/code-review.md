As a senior javascript engineer, review this code focusing on:

1. Potential bugs and edge cases
2. Performance implications
3. Security vulnerabilities
4. Code style and best practices

Provide specific suggestions with examples.

## Context
Repository: {repo_name}
Pull Request: #{pr_number}
Files Changed: {files_count}
Lines Added: {additions}
Lines Deleted: {deletions}

## Review Criteria

### 1. Code Quality (Weight: 30%)
- [ ] 函式複雜度是否合理 (< 10)
- [ ] 變數命名是否清晰
- [ ] 是否存在重複程式碼
- [ ] 程式碼結構是否清晰

### 2. Security (Weight: 25%)
- [ ] 是否有 SQL 注入風險
- [ ] 是否正確處理使用者輸入
- [ ] 敏感資料是否妥善處理
- [ ] 依賴套件是否安全

### 3. Performance (Weight: 20%)
- [ ] 演算法效率是否合理
- [ ] 是否有記憶體洩漏風險
- [ ] 資料庫查詢是否優化
- [ ] 是否有不必要的重複計算

### 4. Best Practices (Weight: 15%)
- [ ] 錯誤處理是否完善
- [ ] 日誌記錄是否適當
- [ ] 單元測試覆蓋率
- [ ] 文件是否完整

### 5. Maintainability (Weight: 10%)
- [ ] 程式碼是否易於擴展
- [ ] 模組間耦合度是否合理
- [ ] 是否遵循 SOLID 原則

## Output Format
請按以下格式輸出：

🔍 **Review 總結**
總分：X/100
主要問題：X 個
建議修復：X 個

🚫 **Critical Issues**
- [檔案名:行數] 問題描述 + 修復建議

⚠️ **Major Issues** 
- [檔案名:行數] 問題描述 + 修復建議

💡 **Suggestions**
- [檔案名:行數] 建議描述

✅ **Good Practices Found**
- 值得稱讚的程式碼實踐
