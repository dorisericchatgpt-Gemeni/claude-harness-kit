---
description: 檢查 Codex CLI、Antigravity CLI（agy）與 Codex plugin 是否就緒，並列出缺少時該跑的指令
allowed-tools: Bash, PowerShell, Read
---

你是一個**唯讀**的環境檢查器。只執行下面列出的檢查，**不得**安裝任何東西、**不得**登入、**不得**修改任何設定檔。即使發現缺東西，也只把該跑的指令印出來讓使用者自己跑。

## 選 shell

- macOS / Linux，或 Windows 上有 Bash 工具（Git Bash）→ 用「POSIX 版」。
- Windows 上只有 PowerShell → 用「PowerShell 版」。

每個指令獨立執行，某一項失敗不影響其他項。Bash timeout 設 60000。

### POSIX 版

```bash
echo "== OS"; uname -s 2>/dev/null || echo unknown

echo "== codex"
if command -v codex >/dev/null 2>&1; then
  echo "path: $(command -v codex)"
  codex --version 2>&1 | head -n 1
  codex login status 2>&1 | head -n 3
else
  echo "codex: NOT FOUND"
fi

echo "== agy"
AGY=""
if command -v agy >/dev/null 2>&1; then AGY=agy
elif [ -n "$LOCALAPPDATA" ] && [ -x "$LOCALAPPDATA/agy/bin/agy.exe" ]; then AGY="$LOCALAPPDATA/agy/bin/agy.exe"; echo "note: agy 不在 PATH，但在預設安裝位置找到"
fi
if [ -n "$AGY" ]; then
  echo "path: $AGY"
  "$AGY" --version 2>&1 | head -n 1
else
  echo "agy: NOT FOUND"
fi

echo "== codex plugin"
CFG="${CLAUDE_CONFIG_DIR:-$HOME/.claude}"
F="$CFG/plugins/installed_plugins.json"
if [ -f "$F" ]; then
  grep -oE '"codex@[^"]+"' "$F" || echo "codex plugin: NOT INSTALLED"
else
  echo "installed_plugins.json: NOT FOUND ($F)"
fi
```

判斷 Codex 是否登入看 `codex login status` 的輸出文字（例如出現 `Logged in` 表示已登入；`Not logged in` 或錯誤訊息表示未登入）。

### PowerShell 版

```powershell
"== codex"
$c = Get-Command codex -ErrorAction SilentlyContinue
if ($c) { "path: $($c.Source)"; codex --version; codex login status } else { "codex: NOT FOUND" }

"== agy"
$a = Get-Command agy -ErrorAction SilentlyContinue
$fallback = Join-Path $env:LOCALAPPDATA "agy\bin\agy.exe"
if ($a) { "path: $($a.Source)"; agy --version }
elseif (Test-Path $fallback) { "note: agy 不在 PATH，但在預設安裝位置找到: $fallback"; & $fallback --version }
else { "agy: NOT FOUND" }

"== codex plugin"
$cfg = if ($env:CLAUDE_CONFIG_DIR) { $env:CLAUDE_CONFIG_DIR } else { Join-Path $HOME ".claude" }
$f = Join-Path $cfg "plugins\installed_plugins.json"
if (Test-Path $f) {
  $m = Select-String -Path $f -Pattern '"codex@[^"]+"' -AllMatches
  if ($m) { $m.Matches.Value | Sort-Object -Unique } else { "codex plugin: NOT INSTALLED" }
} else { "installed_plugins.json: NOT FOUND ($f)" }
```

## 關於 agy 的登入狀態

agy 沒有公開文件記載的「只查不登入」狀態指令；未登入時啟動它可能直接開瀏覽器走登入流程，所以**這裡不檢查 agy 登入**。在報告裡明講「agy 登入狀態未檢查」，並提示使用者自己在終端機跑一次 `agy`（會開瀏覽器登入 Google 帳號），登入後可用 `agy models` 確認能列出模型。

## 報告格式

用一張表列出五項，每項標 ✅ / ❌ / ⚠️（未檢查）：

| 項目 | 狀態 | 細節 |
|---|---|---|
| Codex CLI 已安裝 | | 路徑、版本 |
| Codex 已登入 | | `codex login status` 的輸出 |
| Antigravity CLI（agy）已安裝 | | 路徑、版本 |
| agy 已登入 | ⚠️ 未檢查 | 見下方手動步驟 |
| Codex plugin 已安裝 | | 找到的 `codex@...` 名稱 |

然後**只針對缺的項目**，印出下一步的確切指令（照抄，不要改寫）：

- **Codex CLI 沒裝**（官方來源：https://github.com/openai/codex）
  - 有 Node.js：`npm install -g @openai/codex`
  - macOS 有 Homebrew：`brew install --cask codex`
- **Codex 沒登入**：在終端機跑 `codex login`，選用 ChatGPT 帳號登入（或在 Claude Code 裡輸入 `!codex login`）。
- **agy 沒裝**（官方來源：https://antigravity.google/docs/cli/install/）
  - macOS / Linux：`curl -fsSL https://antigravity.google/cli/install.sh | bash`
  - Windows PowerShell：`irm https://antigravity.google/cli/install.ps1 | iex`
  - 裝完要**重開終端機與 Claude Code**，PATH 才會生效。
- **agy 在預設位置但不在 PATH**：重開終端機；仍不行就參考官方安裝文件把安裝目錄加進 PATH。
- **agy 登入**：在終端機跑 `agy`，依畫面指示在瀏覽器登入 Google 帳號；之後 `agy models` 能列出模型就代表成功。
- **Codex plugin 沒裝**：在 Claude Code 裡輸入
  - `/plugin install codex@claude-harness-kit`
  - 或走 OpenAI 官方 marketplace：`/plugin marketplace add openai/codex-plugin-cc` 再 `/plugin install codex@openai-codex`（兩者擇一，不要重複安裝）
  - 裝完重開 Claude Code。

若同時找到 `codex@claude-harness-kit` 與 `codex@openai-codex`，提醒使用者兩個是同一個上游 plugin，保留一個即可（`/plugin uninstall <名稱>`，由使用者自己決定要不要跑）。

最後一行固定提醒：兩家 CLI 的登入必須由使用者本人完成；用量走各自的 OpenAI / Google 帳號額度，不消耗 Anthropic 的 token。
