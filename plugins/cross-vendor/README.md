# cross-vendor：在 Claude Code 裡問 ChatGPT（Codex）和 Gemini

裝好之後，你可以在 Claude Code 裡直接：

- 用 `/codex:rescue <任務>` 把工作交給 **ChatGPT 的 Codex**（OpenAI 官方 plugin）
- 用 `/cross-vendor:ask-gemini <問題>` 問 **Gemini**（透過 Google Antigravity 的 `agy` CLI）
- 用 `/cross-vendor:doctor` 檢查上面兩個是不是都準備好了

適合拿來要「第二意見」：同一個問題讓不同公司的模型各看一次。

## 先講清楚兩件事

1. **兩家 CLI 的登入無法代勞。** Codex 要用你的 ChatGPT 帳號登入，agy 要用你的 Google 帳號登入，都必須你本人在瀏覽器完成。本 plugin 不會、也不能幫你登入或安裝。
2. **額度走各自的帳號，不吃 Anthropic 的 token。** 問 Codex 用的是你 ChatGPT 方案的額度，問 Gemini 用的是你 Google / Antigravity 帳號的額度。

## 安裝步驟（完全新手版）

### ① 安裝 Claude Code

照官方文件安裝並登入：https://code.claude.com/docs/en/setup

### ② 安裝 Codex CLI，並用 ChatGPT 帳號登入

官方來源：https://github.com/openai/codex

在終端機（macOS 的「終端機」、Windows 的 PowerShell）執行其中一個：

```bash
npm install -g @openai/codex        # 需要先裝 Node.js
brew install --cask codex           # macOS 有 Homebrew 的話
```

裝好後登入：

```bash
codex login
```

選 **Sign in with ChatGPT**，在跳出的瀏覽器頁面登入。確認登入成功：

```bash
codex login status
```

### ③ 安裝 Antigravity CLI（agy），並登入 Google 帳號

官方來源：https://antigravity.google/docs/cli/install/

macOS / Linux：

```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

Windows（PowerShell）：

```powershell
irm https://antigravity.google/cli/install.ps1 | iex
```

裝完**關掉終端機再重開**，然後執行一次：

```bash
agy
```

第一次執行會開瀏覽器請你登入 Google 帳號。登入後可以跑這個確認，能列出模型就代表成功：

```bash
agy models
```

### ④ 在 Claude Code 裡安裝 plugin

打開 Claude Code，依序輸入：

```
/plugin marketplace add dorisericchatgpt-Gemeni/claude-harness-kit
/plugin install cross-vendor@claude-harness-kit
/plugin install codex@claude-harness-kit
```

第三行的 `codex` 是 **OpenAI 官方的 Codex plugin**：本 marketplace 只是登記它的位置，安裝時直接從上游 [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc)（Apache-2.0）抓取，這個 repo 不含它的程式碼。

如果你比較想走 OpenAI 官方的 marketplace，第三行改成下面兩行（**兩種擇一，不要兩個都裝**）：

```
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
```

裝完重開 Claude Code。

### ⑤ 檢查環境

```
/cross-vendor:doctor
```

它會列出 Codex CLI、Codex 登入、agy、Codex plugin 的狀態，缺什麼就印出該跑的指令。它**只檢查，不會自動安裝或登入**。agy 的登入狀態沒辦法在不觸發登入流程的情況下檢查，所以會標成「未檢查」，照步驟 ③ 自己確認即可。

### ⑥ 試用

問 Gemini：

```
/cross-vendor:ask-gemini 用三句話解釋什麼是 CAP 定理
```

指定模型（名稱先用 `agy models` 查）：

```
/cross-vendor:ask-gemini --model <agy models 裡的名稱> 這段程式碼有沒有 race condition？
```

交給 Codex（ChatGPT）：

```
/codex:rescue 幫我找出這個 repo 裡測試失敗的原因
```

Codex plugin 的其他指令（`/codex:review`、`/codex:setup` 等）見上游 README：https://github.com/openai/codex-plugin-cc

## 為什麼 ChatGPT 那邊不自己做一套

OpenAI 已經有官方維護的 Claude Code plugin，功能完整（背景執行、code review、續接 session），自己重做只會更舊、更難維護，所以這裡直接登記上游。本 plugin 只補上 Gemini 這一端和一個共用的環境檢查。

## Gemini 轉發的安全設計

`/cross-vendor:ask-gemini` 背後是 `antigravity` subagent，它：

- 永遠以 `--sandbox --disable-slash-commands` 執行 agy，**不會**加 `--dangerously-skip-permissions` 或 `--mode accept-edits`
- 只把目前的 git repo 根目錄（不在 repo 裡就用目前目錄）掛給 agy 讀，不掛上層或家目錄
- 用 quoted heredoc 傳遞問題文字，避免問題內容被 shell 當成指令執行
- 把 agy 的輸出原文包在 `<agy-output>` 裡帶回，標明那是外部模型產生的不可信文字

已知的 agy 行為坑（寫在 subagent 裡，這裡提醒你）：

- **agy 沒有寫入權時可能謊報「已完成」。** 它說改了檔案不代表真的改了，請自己確認。
- **headless 模式會靜默拒絕需要授權的工具**，這時會回一段「無輸出、需要 command 權限」的訊息，屬正常現象。
- 問題很大時 agy 可能要跑好幾分鐘，請耐心等。

## 疑難排解

| 症狀 | 處理 |
|---|---|
| 找不到 `codex` 或 `agy` | 重開終端機與 Claude Code；仍不行就跑 `/cross-vendor:doctor` 看建議 |
| agy 回「沒有開啟 workspace」 | 請在一個專案資料夾裡開 Claude Code 再試 |
| agy 回模型或 effort 錯誤 | 先跑 `agy models` 看可用名稱；名稱已含 `-high`/`-low` 時不要再加 `--effort` |
| `/codex:rescue` 說 Codex 沒準備好 | 在 Claude Code 裡跑 `/codex:setup`，或在終端機跑 `codex login` |

## 授權

本 plugin 以 MIT 授權釋出。OpenAI 的 Codex plugin 屬於其上游 repo，授權為 Apache-2.0。
