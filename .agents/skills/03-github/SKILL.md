---
name: 03-github
description: 在 AntiGravity 2 連接與驗證 GitHub CLI。使用者說連接 GitHub、建立 repo、commit 或 push 時使用。
---

# 連接 GitHub

1. 檢查 `git --version`（應已在 00 處理）、`gh --version`、`gh auth status`。缺 GitHub CLI 時先說明用途，經同意再裝（Windows：`winget install --id GitHub.cli -e`；macOS：`brew install gh`），裝完開新的終端機再檢查。
2. 登入需使用者在瀏覽器完成；不顯示 token。
3. 先在指定專案讀取 status、remote 與 diff。
4. 建 repo 預設私有；公開、commit、push 前列出目標與檔案並確認。
5. push 後以 `gh repo view` 與遠端 commit 回讀驗證。
