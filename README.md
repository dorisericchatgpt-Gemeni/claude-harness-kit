# claude-harness-kit

一套從個人 Claude Code harness 抽出來、去除私人脈絡後公開的設定包：模型分工與 token 紀律、輸出表達規範、幾個通用 skill，以及在 Claude Code 裡直接呼叫 ChatGPT（Codex）與 Gemini（Antigravity）的 plugin。

*English: A de-personalized Claude Code harness kit — model-routing and token discipline docs, output-style rules, a few general-purpose skills, and a plugin marketplace for calling ChatGPT (Codex) and Gemini (Antigravity) from inside Claude Code. Docs are in Traditional Chinese.*

## 內容

| 路徑 | 是什麼 |
|---|---|
| `docs/model-routing/` | Claude 與 ChatGPT/Codex 的模型分工、effort、token 用量、subagent 分工 |
| `docs/output-style/` | 回答風格、品味 lens、行為四原則、跨 agent 回報紀律 |
| `templates/CLAUDE.md`、`templates/AGENTS.md` | 可直接複製到你專案根目錄的精簡模板 |
| `plugins/harness-skills/` | 6 個 skill：academic-humanizer、advisor-dialogue、concept-tutor、difficult-workplace-conversations、voice-layer、skill-creator，附問題分析方法論 wiki |
| `plugins/cross-vendor/` | 呼叫 Gemini 的 subagent、`/cross-vendor:ask-gemini`、環境檢查 `/cross-vendor:doctor` |

## 安裝（Claude Code）

```
/plugin marketplace add dorisericchatgpt-Gemeni/claude-harness-kit
/plugin install harness-skills@claude-harness-kit
/plugin install cross-vendor@claude-harness-kit
/plugin install codex@claude-harness-kit
/cross-vendor:doctor
```

`codex` 直接從 OpenAI 官方 [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) 抓取，本 repo 不含其程式碼。

呼叫 ChatGPT、Gemini 前，你得先自己裝好 Codex CLI 與 Antigravity CLI 並各自登入，這一步 plugin 無法代勞；額度走各自帳號。完整新手步驟見 [plugins/cross-vendor/README.md](plugins/cross-vendor/README.md)。

規範文件與模板不需要安裝，讀了覺得合用就複製進你的 `CLAUDE.md` / `AGENTS.md` 再刪改。

## 授權

- 本 repo 自寫部分：MIT，見 [LICENSE](LICENSE)。
- 第三方 skill 保留原授權，見 [plugins/harness-skills/THIRD_PARTY_NOTICES.md](plugins/harness-skills/THIRD_PARTY_NOTICES.md)。
- voice-layer 附帶的 AI 寫作破綻清單改編自 Wikipedia，依 CC BY-SA 4.0 釋出。
