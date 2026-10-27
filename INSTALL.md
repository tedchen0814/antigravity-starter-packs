# 給 AI Agent 的安裝說明（AntiGravity 懶人包）

使用者把這個 repo 的網址給你，說要安裝時，照下面做。**假設使用者完全不懂技術**，用繁體中文與白話說明，不要用 MCP、CLI 這類詞而不解釋。

## 這一步只做一件事

把 16 份技能手冊（`.agents/skills/` 底下 16 個資料夾）複製到**全域技能資料夾** `~\.gemini\config\skills\`。

**這一步不會**安裝任何軟體、不登入任何服務、不修改 MCP 設定。真正的設定與安裝，是安裝完成後在新對話裡由 `00-install-all` 導覽，一次一項、逐項徵求同意。

## 步驟

1. **先說明並等同意。** 告訴使用者：「我要把 16 份技能手冊複製到你電腦的 AntiGravity 技能資料夾，不會安裝軟體或登入任何東西。要繼續嗎？」收到同意才動手。
2. **取得檔案**（放在暫存資料夾，不要放在雲端硬碟）：
   - 有 Git：`git clone --depth 1 https://github.com/tedchen0814/antigravity-starter-packs.git "$env:TEMP\antigravity-starter-packs"`
   - 沒有 Git：不要先裝 Git，改下載壓縮檔：
     ```powershell
     $zip = Join-Path $env:TEMP 'antigravity-starter-packs.zip'
     Invoke-WebRequest https://github.com/tedchen0814/antigravity-starter-packs/archive/refs/heads/main.zip -OutFile $zip
     Expand-Archive $zip -DestinationPath $env:TEMP -Force
     ```
     解壓後的資料夾名稱是 `antigravity-starter-packs-main`。
3. **複製技能。** 目標資料夾 `$HOME\.gemini\config\skills\`（不存在就建立）。若已有同名資料夾，**先搬到備份資料夾** `$HOME\.gemini\config\skills-backup\<日期時間>\`，不要直接刪除。
   ```powershell
   $src = Join-Path $env:TEMP 'antigravity-starter-packs\.agents\skills'   # 用 zip 時改成 antigravity-starter-packs-main
   $dest = Join-Path $HOME '.gemini\config\skills'
   $backup = Join-Path $HOME ".gemini\config\skills-backup\$(Get-Date -Format yyyyMMdd-HHmmss)"
   New-Item -ItemType Directory -Force $dest | Out-Null
   Get-ChildItem $src -Directory | ForEach-Object {
     $target = Join-Path $dest $_.Name
     if (Test-Path $target) { New-Item -ItemType Directory -Force $backup | Out-Null; Move-Item $target $backup }
     Copy-Item -Recurse $_.FullName $target
     Write-Host "已安裝 $($_.Name)"
   }
   ```
4. **驗證。** 確認 `$dest` 底下有 16 個本懶人包的資料夾，且每個資料夾內都有 `SKILL.md`。如果使用者原本就有其他技能，只數本包的 16 個，不要把總數當成 16。
5. **清理暫存。** 說明暫存資料夾位置，詢問是否刪除；同意才刪。
6. **收尾**，用白話告訴使用者：
   - 已安裝 16 份技能手冊，有備份的話說明備份位置。
   - 請**關閉 AntiGravity 再重新開啟**，開一個**新的對話**。
   - 在新對話輸入「**開始**」，我會問你想用 AntiGravity 做什麼，再一步一步帶你設定。
   - 到這裡還沒有安裝任何軟體、沒有登入任何東西。

## 不要做的事

- 不要在這一步順便做環境檢查、登入 GitHub、設定 MCP 或安裝其他工具。
- 不要把 token、API key 貼進對話，也不要寫進 repo。
- 失敗時（例如網路、權限）把完整錯誤訊息回報給使用者，不要自己換方案。
