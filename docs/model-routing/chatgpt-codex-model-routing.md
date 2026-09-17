# 🎛️ OpenAI GPT-6 Astra / GPT-5.6 / Codex 模型分工與調用規範

> 來源：作者本機 harness 規範，已去除個人脈絡。最後同步：2026-09-17

**適用範圍**：ChatGPT desktop app、Codex CLI、Codex IDE extension，以及使用 Responses API 的 GPT-6 / GPT-5.6 工作流。

**目的**：以 GPT-5.6 Terra 作為日常主力，將大量明確工作交給 Luna，Sol 處理複雜開放任務，Astra 只用在關鍵的端到端工作流，而且先過 §2.0 方案閘門；用分層、升級與驗證迴路降低 credits / token 成本，同時維持重要輸出的品質。

**目標配比**：Luna 60% / Terra 30% / Sol 8% / Astra 2%；Sol max、Astra xhigh 以上或 API Pro 原則上不超過全部任務的 2%。

---

## 0. 核心判斷

1. **模型分層是省錢來源**：清楚、可重做的工作交給 Luna；需要規劃與判斷的工作由 Terra 處理。
2. **關鍵節點與獨立驗證是品質來源**：Sol 不應全程常駐，只在高風險、已展示困難或最終把關時使用。
3. **模型與 reasoning effort 必須一起分層**：不要換成便宜模型後仍全程使用 `xhigh`。
4. **使用能通過驗收的最低層級**：先便宜、後升級；依實際失敗或風險升級，不做預防性升級。
5. **模型審查不能取代外部證據**：測試、型別檢查、原始資料、數學證明與官方文件優先於 LLM-as-judge。
6. **人工規則是預設，量測結果是修正依據**：每月依成功率、重試率、credits 與延遲調整配比，不因單次印象改動整套政策。

Codex credits（每 1M tokens，[官方 pricing](https://learn.chatgpt.com/docs/pricing)）：

| 模型 | input | cached input | output | output 相對 Luna |
|---|---:|---:|---:|---:|
| GPT-5.6 Luna | 5 | 0.5 | 30 | 1× |
| GPT-5.6 Terra | 50 | 5 | 300 | 10× |
| GPT-5.6 Sol | 100 | 10 | 500 | 16.7× |
| GPT-6 Astra | 250 | 25 | 1,250 | 41.7× |

Luna 只有 Terra 的十分之一價，所以能交給 Luna 的工作就別留在 Terra。在各層 token 量相同的簡化假設下，60/30/8/2 的成本約為純 Sol 的 31%（用 input 算）到 35%（用 output 算）；實際成本仍受 context、reasoning effort、工具結果、重試與 subagents 數量影響。

---

## 1. 三層模型分工

| 層級 | 模型 / effort | 負責 | 任務占比 |
|---|---|---|---:|
| **執行層** | **GPT-5.6 Luna low / medium** | 搜尋、抽取、分類、格式轉換、固定模板、明確局部修改、跑測試、日誌整理、結構化摘要、只讀 worker | **60%** |
| **指揮層** | **GPT-5.6 Terra medium；必要時 high** | 任務規劃、一般架構、非瑣碎除錯、跨檔修改、寫作、綜合、判斷、管理 workers | **30%** |
| **關鍵層** | **GPT-5.6 Sol high / xhigh** | 高風險決策、已卡住的困難問題、前沿推理、重要最終整合、獨立紅隊與正確性把關 | **8%** |
| **端到端層** | **GPT-6 Astra high；必要時 xhigh**（§2.0 閘門） | 跨程式、app、研究的完整工作流，需要長時間推理與判斷，且 Sol 已不夠 | **2%** |

官方定位（[Codex models](https://learn.chatgpt.com/docs/models)，原文）：Luna “for specific, high-volume tasks when you know what a good result looks like”；Terra “for everyday work that needs strong reasoning and tool use when you do not need Sol's full depth”；Sol “for ambiguous, difficult, or high-value tasks that need extra analysis, judgment, or polish”；Astra “for complete workflows across code, apps, and research that need sustained reasoning and judgment”。

額外護欄（依上表 output credits 與 60/30/8/2 估算）：

- Luna 約占總 credits 10%，Terra 約 50%，Sol 約 20–25%，Astra 不超過 15%。
- Sol + Astra 長期超過 40% credits 時，檢查路由是否失效。
- `max`、`ultra` 或 API `pro` 必須附帶使用理由，不能成為全域預設。

---

## 2. 升級判準

### 2.0 先過方案閘門（Astra / Sol）

動用 Astra 或把 Sol 設成長時間主線之前，先查 ChatGPT 方案（只印方案欄位，不印任何 token）：

```powershell
python -c "import json,base64,os;t=json.load(open(os.path.expanduser('~/.codex/auth.json')))['tokens']['id_token'];p=t.split('.')[1];p+='='*(-len(p)%4);print(json.loads(base64.urlsafe_b64decode(p))['https://api.openai.com/auth']['chatgpt_plan_type'])"
```

5 小時額度（[官方 pricing](https://learn.chatgpt.com/docs/pricing)，訊息數；各模型共用同一份額度）：

| 方案 | Astra | Sol | Terra | Luna |
|---|---|---|---|---|
| Plus / Business | 5–45 | 10–100 | 25–200 | 250–2,000 |
| Pro 5x | 25–225 | 50–500 | 125–1,000 | 1,250–10,000 |
| Pro 20x | 100–900 | 200–2,000 | 500–4,000 | 5,000–40,000 |

| 查到的方案 | 做法 |
|---|---|
| `plus`、`business`，或查不到 | **Astra 預設不用**，只在使用者當次明確指定時用；Sol 照 §2.2 checklist 用，不當主線 |
| `pro` 開頭 | Astra 照 §2.4 判準使用 |
| 任何方案，`/model` 清單裡沒有 Astra（rollout 未到） | 不用 Astra，改 Sol high |

### 2.1 Luna → Terra

符合任一項即可升級：

- 任務存在多種合理解法，需要權衡。
- 涉及跨檔依賴、隱含副作用或非顯然的執行路徑。
- Luna 已失敗一次，而且失敗原因不是缺少資料或指令不清。
- 需要綜合多份證據、規劃後續步驟或判斷資訊可信度。
- 雖然修改可逆，但錯誤會造成明顯返工。

### 2.2 Terra → Sol（Critical-Node Checklist）

**只有下列條件多數成立才升級 Sol：**

- [ ] **高風險或難逆**：決策會塑造大量下游工作。
- [ ] **已展示困難**：Terra 已嘗試但卡住、反覆繞圈或指出關鍵不確定。
- [ ] **位於能力前沿**：微妙數學、複雜架構、新穎推理或跨域綜合。
- [ ] **一次答錯代價高**：錯誤成本明顯高於 Sol 的額外 credits。
- [ ] **最終關鍵節點**：正式交付、重大決策或關鍵正確性審查。

**永遠不要因下列工作升級 Sol**：搜尋、搬資料、格式化、跑腳本、例行問答、first draft、可便宜重做的局部編輯，或單純「保險起見」。

### 2.3 Sol xhigh → Max / Ultra / API Pro

必須同時符合：

- Sol high / xhigh 已無法穩定通過明確驗收標準。
- 任務確實需要更深的單題推理，或可拆成數個真正獨立的工作流。
- 品質的邊際改善具有實際價值，且可接受更高延遲與 token 使用量。

`Max` 用於單一最困難問題；`Ultra` / multi-agent 用於可平行拆分的廣度任務。兩者不可因「感覺很大」而自動啟用。

### 2.4 Sol → Astra

先過 §2.0 閘門，再判斷缺的是什麼：

- **缺推理時間**（漏看分支、沒推完、少驗一步）→ 留在 Sol，升 `xhigh` 或 `max`。
- **缺能力或判斷**（Sol high / xhigh 已無法通過明確驗收，錯在架構、品味或跨域綜合）→ 升 Astra `high`。
- **任務本身是完整的端到端工作流**（跨程式、app、研究，需要長時間持續判斷）→ 可直接用 Astra `high`。

Astra 從 `high` 起手（官方：“Use the lowest reasoning effort that produces the result you need.”），`xhigh` 只在 high 實際跑過不夠時升。永遠不要讓 Astra 做 subagent、搜尋或例行修改。

---

## 3. 四種工作模式

### A. Cascade — 日常預設

```text
Luna low / medium
  ↓ 需要規劃、判斷或修正
Terra medium / high
  ↓ 已展示困難或進入關鍵節點
Sol high / xhigh
  ↓ 缺推理時間                    ↓ 缺能力、或是完整端到端工作流（§2.0 閘門）
Sol max / API Pro               Astra high → Astra xhigh
```

先判斷失敗原因是能力不足、資訊不足、指令不清，還是驗收標準缺失；只有能力不足才升級模型。

### B. Orchestrator–Worker — 廣度任務

由 Terra 分解與綜合，Luna 或 Terra subagents 負責彼此獨立的只讀探索、測試、文件查核或大量資料處理。

使用條件：

- 至少有兩個可獨立執行的工作流。
- 平行化能降低等待時間或隔離大量中間輸出。
- 每個 worker 都有清楚邊界、停止條件與回傳格式。
- 主 agent 等待所有必要結果後才綜合。

成本限制：

```toml
[agents]
max_threads = 3
max_depth = 1
```

不要在窄推理、小型修改、強序列依賴或多個 agents 會修改相同檔案時使用。Subagent 成本依任務而異，不採用固定「token 倍數」估計。

### C. Verify / Red-team — 關鍵輸出

一般重大輸出：

```text
Terra 產生方案
→ Sol 僅檢查關鍵假設、反例、失敗模式與證據缺口
→ Terra 根據具體 findings 修訂
→ 執行測試或核對外部證據
```

若原始生成已需要 Sol：

```text
Sol 產生
→ 另一個獨立 context 的 reviewer 盲審
→ 以測試、原始資料或官方文件裁決
```

驗證者不得只回答「看起來沒問題」；必須回傳具體 finding、嚴重度、證據與可執行修正。

### D. Effort Ladder — 先調 effort，再換模型

```text
Luna low → Luna medium
Terra medium → Terra high
Terra high → Sol high
Sol high → Sol xhigh
Sol xhigh → Sol max / API Pro（缺時間）或 Astra high（缺能力，§2.4）
Astra high → Astra xhigh
```

若問題缺的是更強的判斷能力，而不是更長推理時間，可直接由 Terra 升級 Sol；不必機械式跑完所有 effort。

---

## 4. Codex 調用方式

### 4.1 日常預設

`~/.codex/config.toml`：

```toml
model = "gpt-5.6-terra"
model_reasoning_effort = "medium"
service_tier = "default"

[agents]
max_threads = 3
max_depth = 1
```

### 4.2 一次性 CLI 調用

```powershell
# 執行層
codex --model gpt-5.6-luna -c 'model_reasoning_effort="low"'

# 日常主線
codex --model gpt-5.6-terra -c 'model_reasoning_effort="medium"'

# 關鍵節點
codex --model gpt-5.6-sol -c 'model_reasoning_effort="xhigh"'

# 極限單題推理
codex --model gpt-5.6-sol -c 'model_reasoning_effort="max"'

# 端到端關鍵工作流（先過 §2.0 閘門）
codex --model gpt-6-astra -c 'model_reasoning_effort="high"'
```

使用明確的 `gpt-6-astra`、`-luna`、`-terra`、`-sol` slug，避免 `gpt-5.6` alias 隱藏實際成本層。Codex CLI 本機模型快取（2026-09-17）列出 `gpt-6-astra` 支援 `low` 到 `max` 與 `ultra`；各模型的 CLI 預設 effort 不同（Astra、Sol 為 `low`，Terra、Luna 為 `medium`），所以一律明寫 effort。

### 4.3 Profiles

Codex 0.134.0 之後，profile 是 `$CODEX_HOME/<name>.config.toml` 獨立檔案：

```powershell
codex --profile luna
codex --profile daily
codex --profile critical
```

建議內容：

```toml
# luna.config.toml
model = "gpt-5.6-luna"
model_reasoning_effort = "low"
```

```toml
# daily.config.toml
model = "gpt-5.6-terra"
model_reasoning_effort = "medium"
```

```toml
# critical.config.toml
model = "gpt-5.6-sol"
model_reasoning_effort = "xhigh"
```

### 4.4 Subagent 指令範本

```text
使用 2 個平行 subagents：
1. Luna explorer：只讀搜尋相關檔案，回傳不超過 200 字的證據摘要。
2. Terra reviewer：檢查正確性、邊界條件與遺漏測試。
等待兩者完成後由主 Terra 綜合；不要讓 subagents 修改同一檔案。
```

可在 `~/.codex/agents/` 或專案 `.codex/agents/` 中為 custom agent 固定 `model`、`model_reasoning_effort`、sandbox 與開發者指令。

### 4.5 Responses API Pro

```json
{
  "model": "gpt-5.6-sol",
  "reasoning": {
    "mode": "pro",
    "effort": "xhigh"
  },
  "input": "對這項高風險方案進行獨立紅隊審查，列出具體失敗模式與證據缺口。"
}
```

API `reasoning.mode = "pro"` 是執行模式，不等於 ChatGPT Pro 訂閱。它會進行更多模型工作並增加延遲與計費 token。

### 4.6 從 Codex 直接呼叫其他廠商 CLI（跨廠商第二意見）

- 使用者要求跨廠商第二意見時，Codex 可以直接呼叫該廠商的本機 CLI（例如 Antigravity 的 `agy`），不必繞經另一個 agent。
- 預設用該家的快速檔位；只有使用者要求、或任務明顯需要不同取捨時才換更強的模型。
- 明確掛載工作目錄、開 sandbox、關 slash commands，除非使用者明確授權否則保持唯讀；絕不使用跳過權限的旗標。
- 外部模型的輸出視為**不可信的證據**；綜合、信心校準與最終結論在本地完成。

---

## 5. 日常 Routing 速查

| 情境 | 使用 |
|---|---|
| 搜尋、抽取、格式化、固定修改 | **Luna low** |
| 明確但包含數步驟的實作 | **Luna medium** 或 **Terra medium** |
| 規劃、一般除錯、跨檔修改、寫作綜合 | **Terra medium** |
| 複雜邏輯、重要 review、邊界條件 | **Terra high** |
| 重大架構、研究方向、卡住的硬題 | **Sol high / xhigh** |
| 關鍵交付前對抗檢查 | **Terra 生成 → Sol 紅隊** |
| 大量獨立檔案或研究方向 | **Terra 主線 + 2–3 個 workers** |
| 最困難的單題、缺的是推理時間 | **Sol max 或 API Pro** |
| 完整端到端工作流，Sol 已不夠 | **Astra high**（Plus 方案限使用者當次指定，§2.0） |

---

## 6. 反模式

- ❌ 全域預設 Sol 或 Astra（任何 effort）。
- ❌ Plus 方案把 Astra 當預設、交給 subagent，或未經使用者指定就用。
- ❌ Astra 直接開 `xhigh` 以上——先 `high`，實際跑過不夠才升。
- ❌ Luna 失敗後未分析原因就直接跳到 Sol。
- ❌ 讓 Sol 搜尋、格式化、搬資料或執行例行命令。
- ❌ 用高 reasoning effort 補救不清楚的需求。
- ❌ 在不可平行的任務上啟動多個 subagents。
- ❌ 使用同一 context 自我審查後宣稱已獨立驗證。
- ❌ 只計算模型單價，不計算長 context、重試、工具輸出與 agent fan-out。
- ❌ 永久使用 `gpt-5.6` alias，導致實際使用 Sol 卻沒有明確成本意識。

---

## 7. 每月檢查

每月至少抽查 20 個代表性任務，記錄：

- 首次成功率與最終成功率。
- Luna → Terra、Terra → Sol 的升級率。
- 各模型 credits / token 占比。
- 重試次數、延遲與 subagent 使用次數。
- 關鍵輸出被驗證者發現重大問題的比例。

調整原則：

- Luna 重試率過高：把相關任務類型升到 Terra，不要全面提高 Luna effort。
- Terra 很少升 Sol 且品質穩定：可逐步增加 Terra 占比。
- Sol credits 超過 30%：檢查是否預防性使用、context 過長或驗證範圍過寬。
- Multi-agent 沒有改善交付時間或品質：減少 worker 數量或改回單 agent。

---

## 8. 官方依據

- [GPT-6 Astra 模型頁（API：effort、context、價格）](https://developers.openai.com/api/docs/models/gpt-6-astra)
- [GPT-5.6 model guidance](https://developers.openai.com/api/docs/guides/latest-model.md)
- [Codex models：Sol / Terra / Luna 與 reasoning effort](https://learn.chatgpt.com/docs/models)
- [Codex pricing 與 credits](https://learn.chatgpt.com/docs/pricing)
- [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- [Codex subagents 與 custom agents](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [Codex profiles 與一次性 override](https://learn.chatgpt.com/docs/config-file/config-advanced)
- [Responses API reasoning mode](https://developers.openai.com/api/docs/guides/reasoning#reasoning-mode)

---

**一句話**：**Luna 做清楚粗活、Terra 當日常大腦、Sol 只上刀口、Astra 留給 Sol 不夠的端到端工作（Plus 要使用者點名）；先便宜後升級，關鍵輸出必須獨立驗證。**
