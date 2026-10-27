# AntiGravity 2 懶人包

給研發人員與初學者使用的十六個 Skills，安裝到**全域**技能資料夾（`~\.gemini\config\skills\`），在任何資料夾開啟 AntiGravity 2 都能用。每個主題獨立，不把 Codex、Claude 或 OpenCode 的專用設定帶進 AntiGravity 2。

## 安裝

```powershell
git clone https://github.com/tedchen0814/antigravity-starter-packs.git
Set-Location .\antigravity-starter-packs
$dest = Join-Path $HOME '.gemini\config\skills'
New-Item -ItemType Directory -Force $dest | Out-Null
Get-ChildItem .\.agents\skills -Directory | ForEach-Object {
  $target = Join-Path $dest $_.Name
  if (Test-Path $target) { Remove-Item -Recurse -Force $target }
  Copy-Item -Recurse $_.FullName $target
  Write-Host "已安裝 $($_.Name) -> $target"
}
```

- 同名的舊版會被覆蓋；之後更新 repo，重跑一次即可。
- 裝完**重新啟動 AntiGravity**（`agy`），在任何資料夾輸入 `/skills`，應看到十六個技能。
- 若 `/skills` 沒有出現這十六個，請確認 `~\.gemini\config\skills\` 底下有各技能資料夾，且每個資料夾內有 `SKILL.md`。
- 在本 repo 資料夾內開啟時，`.agents/skills/` 的專案技能優先於全域同名技能。
- 全域技能會在每個專案的每個對話載入名稱與說明；只選當下任務需要的技能使用，不要一次安裝所有外部服務。

## 主題

| 編號 | 技能 | 用途 |
|---|---|---|
| 00 | `00-env-setup` | 環境快篩 |
| 00A | `00-install-all` | 全包檢查清單，不自動大量安裝 |
| 01 | `01-notebooklm` | NotebookLM 連接規劃 |
| 02 | `02-essentials` | 新手必要工具 |
| 03 | `03-github` | GitHub CLI |
| 04 | `04-github-obsidian` | GitHub＋Obsidian |
| 05 | `05-obsidian` | Obsidian 專案筆記 |
| 06 | `06-second-brain` | 第二大腦結構 |
| 07 | `07-supabase` | Supabase 最小權限連接 |
| 08 | `08-firebase` | Firebase 專案連接 |
| 09 | `09-ollama` | 本機 Ollama |
| 10 | `10-gemini` | Gemini API 安全設定 |
| 11 | `11-workspace` | 專案初始化 |
| 12 | `12-draw` | 生圖工作流 |
| 13 | `13-chezmoi` | 安全同步設定 |
| 14 | `14-vercel` | Vercel CLI／MCP 與測試部署 |

## 共通安全線

- Windows 指令使用 PowerShell。
- 先檢查版本與登入狀態，不直接重裝。
- API key、OAuth token、Cookie、個人資料不進 repo 或對話輸出。
- MCP、Browser、CLI 先唯讀驗證；寫入、公開、刪除前取得確認。
- 不關閉權限確認（AntiGravity 沒有 Claude Code 的 `--dangerously-skip-permissions`，但同樣不要把工具設成免確認）。

本版只收錄 AntiGravity 2 可執行的技能。

MIT License
