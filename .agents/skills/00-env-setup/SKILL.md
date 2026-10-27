---
name: 00-env-setup
description: AntiGravity 2 環境建置。使用者要建置環境、安裝開發工具或檢查版本時使用。
---

# 環境建置

1. 以 `agy --version`、`git --version`、`gh --version`、`node --version`、`npm --version`、`uv --version` 做唯讀快篩。
2. **Git 是後續所有項目的前置條件，一定要有**：沒有就先說明「版本控制工具，後續幾乎所有項目都會用到」，經使用者同意再安裝，使用者不同意就停在這裡，不繼續其他項目。其餘工具只安裝任務真正需要且缺少的；先說明來源、影響與是否需系統管理員權限，經使用者同意再裝。Windows 可用 winget（例如 `winget install --id Git.Git -e`、`winget install --id OpenJS.NodeJS.LTS -e`、`winget install --id astral-sh.uv -e`）；裝完要開新的 PowerShell 視窗再檢查版本。沒有 winget 時，請使用者從官網下載安裝，不要自己找替代來源。
3. AntiGravity 2 登入或信任資料夾需使用者親自確認。
4. 驗收版本、登入狀態與一個 sandbox 唯讀任務；缺少選用工具不算失敗。
