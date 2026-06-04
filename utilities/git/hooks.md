# Git

## hooks

### 保護指定遠端分支，不可直接推送

團隊規定某些分支必須經過 pr 才可合併

可在本機專案目錄中加入 git hoos 做防護

如在 push 前檢查分支名稱

避免在關鍵分支直接推送

`專案/.git/hooks/pre-push`

注意沒有副檔名

```
#!/bin/sh

CURRENT_BRANCH=$(git rev-parse --abbrev-ref HEAD)
PROTECTED_BRANCHES="develop|qa|production"

# echo current: $CURRENT_BRANCH, protected: $PROTECTED_BRANCHES

if [[ "$CURRENT_BRANCH" =~ ^($PROTECTED_BRANCHES)$ ]]; then
    echo "===================================================" >&2
    echo "🚨 [阻擋 Push] 您目前在受保護的 $CURRENT_BRANCH 分支，禁止直接推播！" >&2
    echo "===================================================" >&2
    exit 1
fi

exit 0 # 回傳 0，允許推播

```

如果發生權限問題

可以在專案根目錄開啟 git bash

輸入以下指令賦予執行權限

```bash
chmod +x .git/hooks/pre-push
```
