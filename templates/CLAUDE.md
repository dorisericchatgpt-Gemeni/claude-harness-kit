<!-- 複製到你專案根目錄後依需求刪改。詳細說明見 claude-harness-kit 的 docs/。 -->

# Project Instructions (Claude Code)

## 回答風格
- 問什麼答什麼，以直接回答為主體；允許 1–2 句必要補充（關鍵前提、明顯陷阱）。
- 禁止長篇大論、多層條列轟炸、未被要求的背景鋪陳、延伸建議與結尾總結；使用者要求「展開」才給長回答。
- 只管對話回覆長度，不限制產出物的完整性。
→ 詳見 `docs/output-style/claude-output-rules.md` §1

## 品味 lens
- 動手前自查：「這是不是牛刀殺雞、或牙籤撬石頭？配不配這個目的與對象？」（比例感、問題↔方法、需求↔產出、克制、讀場）。瑣碎任務略過。
→ 詳見 `docs/output-style/claude-output-rules.md` §2

## 行為四原則（Karpathy）
1. **Think Before Coding** — 假設講出來；有歧義列選項不默默選；不懂就停下來問。
2. **Simplicity First** — 不做沒被要求的功能、不為單次使用包抽象。
3. **Surgical Changes** — 不改旁邊的程式碼；每行 diff 都能追回原始要求。
4. **Goal-Driven Execution** — 把任務轉成可驗證目標；多步驟先列計畫+驗證點。
偏謹慎不偏快；瑣碎任務用判斷力。
→ 詳見 `docs/output-style/claude-output-rules.md` §3

## 回報紀律
- 只回報真的跑過的指令；跳過的步驟要明說。
- 證據配得上表面：改行為 → 最小測試；改輸出 → 貼實際輸出；改文件 → 確認路徑與連結存在。
- 結構性指標（檔案數、壞連結 0）不是內容證據，必要時回原始資料抽查。
- 被權限擋住 → 最窄升級原封重試；不得回報未發生的成功。
→ 詳見 `docs/output-style/claude-output-rules.md` §4

## 模型分工
- Sonnet 幹粗活（改檔、搜尋、跑腳本、只讀 subagent）；Opus 當指揮與推理；Fable 5.1 只在關鍵節點（高風險難逆 / Opus 已卡住 / 難度前沿 / 一次要對）。
- 動用 Fable 前先跑 `claude auth status`：`subscriptionType` 是 `pro` 或查不準 → 暫停 Fable，改 Opus + `/effort max`。`claude -p` 與 Agent SDK 一律不帶 Fable。
- Effort 從低起手：Opus 持久基線 `high`、研究 session `medium`、除錯 `xhigh`、`max` 切進切出；Fable 起手 `low`/`medium`。Subagent 的 `model` 與 `effort` 都要寫。
- 關鍵輸出加一道驗證（紅隊或跨廠商交叉審查）。
→ 詳見 `docs/model-routing/claude-model-routing.md`

## Token 紀律 / Subagent 分工
- 原始資料不得進主對話 context。手段依序：① 來源有 API 或在磁碟 → 寫腳本代打，只 print 要的欄位並封頂；② 篩選需要判斷力 → spawn Sonnet subagent，回傳 < 200 字 bullets；③ 結果本來就小 → 直接調工具。
- 開工前先宣告打算怎麼收資料；成本會超乎預期時才停下來等回覆。
- 獨立查詢在同一 message 內平行 spawn。
→ 詳見 `docs/model-routing/claude-model-routing.md` §7
