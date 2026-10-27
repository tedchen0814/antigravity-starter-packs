---
name: 05-obsidian
description: 在 AntiGravity 2 連接或建立 Obsidian 專案筆記。使用者提到 Obsidian、vault、駕駛艙或專案筆記時使用。
---

# 連接 Obsidian

## 先確認

1. 掃描使用者已指定或可確認的 vault（含 `.obsidian` 子資料夾的位置）；列出候選**請使用者確認**，不要自己挑。
2. 問使用者：這個 vault 有沒有不想讓 AI 讀取的私密資料夾？有的話，先把規則寫進 vault 根目錄 `AGENTS.md`（例如「不讀取、不搜尋、不引用 `<私密資料夾>/`，也不要透過任何工具對它做列出、讀取、寫入、移動、刪除」）。這是規則，不是技術鎖，請如實告知使用者。
3. 預設只讀入口與相關筆記，不廣泛掃描私人內容。

## 用 MCP 連接 vault（需要工具層級的讀寫時）

1. **不要做全域安裝**（不要 `npm install -g`），也不要直接指向某個 `.cmd` 檔；改用 `npx.cmd` 啟動並**鎖定版本**。
2. AntiGravity 的 MCP 設定檔有兩份，**要同步修改**：
   - `~\.gemini\config\mcp_config.json`
   - `~\.gemini\antigravity\mcp_config.json`
3. 改之前，兩份都先備份成 `mcp_config.json.bak-<日期時間>`。
4. 在 `mcpServers` 加入（保留既有項目，不要覆蓋）：
   ```json
   "obsidian": {
     "command": "npx.cmd",
     "args": ["-y", "@bitbonsai/mcpvault@0.15.0", "<VAULT_PATH>"]
   }
   ```
   macOS／Linux 把 `command` 改成 `npx`。JSON 裡的反斜線要寫成 `\\`；路徑含中文或空白沒關係，放在 `args` 即可。
5. 重新啟動 AntiGravity 後驗證：**只列出 vault 最上層資料夾**，確認讀得到；再做一次讀取與一次寫入測試（寫入前先告知要建立哪個測試筆記，測完詢問是否刪除）。
6. 載入失敗時，**把完整錯誤訊息貼給使用者，不要自己換方案**，也不要改成全域安裝。
7. 沙箱可能誤報「檔案不存在」；結果與實際不符時，請使用者在自己的 PowerShell 確認。

> 版本號 `0.15.0` 是撰寫時驗證過的版本；要升級時先告知使用者，不要自動用 `@latest`。

## 建立駕駛艙

建立前先確認路徑與欄位；記錄進度、下一步、決策與踩坑。

## 安全線

不保存帳密、token、個人資料或可公開 repo 不該出現的私密內容。

回報：vault 路徑、私密資料夾規則是否已寫入、兩份設定檔是否同步、讀取／寫入測試結果。
