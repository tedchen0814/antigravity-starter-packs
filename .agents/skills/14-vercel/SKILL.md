---
name: 14-vercel
description: 在 AntiGravity 2 連接 Vercel（CLI、官方 MCP、測試部署）。使用者提到 Vercel、部署網站、串接 Vercel 或預覽網址時使用。
---

# 連接 Vercel

1. 檢查 `node --version`；缺少就先說明並取得確認後再裝 Node.js LTS。
2. 檢查 `vercel --version`；缺少才執行 `npm i -g vercel@latest`。
3. `vercel whoami` 確認登入；未登入時請使用者在可見 PowerShell 執行 `vercel login`（瀏覽器授權）。沒有帳號請使用者自行到 https://vercel.com/signup 註冊 Hobby 方案。
4. 官方 MCP 位址為 `https://mcp.vercel.com`（HTTP）。依 AntiGravity 2 的 MCP 設定方式加入，授權由使用者在瀏覽器完成；先唯讀列出專案驗證。
5. 測試部署：在空資料夾建 `vercel-test/index.html`，先 `vercel --yes`（預覽網址），使用者確認後才 `vercel --prod --yes`（正式）。
6. 選配：`vercel link --yes` 與 `vercel git connect` 綁定 GitHub repo，push 後自動部署；綁定前先確認。
7. 測試完成後詢問是否以 `vercel project rm vercel-test` 刪除測試專案；刪除前取得確認。

安全線：`.vercel/` 不 commit；API key 用 `vercel env add`，不寫進 repo 或對話。

回報：Vercel CLI 版本、登入帳號、MCP 授權狀態、測試網址、是否綁定 GitHub。
