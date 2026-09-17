# 🎛️ Claude 模型分工使用規範（Fable / Opus / Sonnet Cost-Tiering Policy）

> 來源：作者本機 harness 規範，已去除個人脈絡。最後同步：2026-09-17

**目的**：Fable 5.1 只在**最關鍵節點**動用，而且先過 §2 的帳號方案閘門（Pro 暫停）；其餘由 Opus / Sonnet 分工完成。
**目標**：整體比「純 Opus Max 全程」更省，且**關鍵輸出品質等於或優於**單一強模型。

---

## 0. 核心判斷（先讀這段，別被行銷騙）

- **「又便宜又全面碾壓」不存在。** 獨立評測（RouterArena、LLMRouterBench）發現多數自動 router 連簡單 baseline 都贏不了，商用產品自報數字不可信。
- **可靠的贏法只有兩條笨功夫：**
  1. **任務分層** —— 80% 機械工作丟便宜模型 → 這是省錢的來源。
  2. **關鍵節點加驗證** —— 20% 重要輸出用 Fable + 一道紅隊/驗證 → 這是贏過單次 Opus 的來源。
- **為什麼能贏純 Opus Max**：純 Opus 在瑣事上浪費能力，且單次前向**沒有驗證迴路**；把預算集中在刀口就贏了。
- **人工路由 > 自動路由**：你判斷「這是不是關鍵節點」比任何 router 準。本規範是**紀律**，不是自動化。

---

## 1. 三層模型分工

| 層 | 模型 | 負責 | 佔比 |
|---|---|---|---|
| **執行層** | **Sonnet** | 檔案編輯、搜尋、跑腳本、資料整理、格式化、只讀研究（當 subagent）、first draft | ~70% |
| **指揮/推理層** | **Opus** | 規劃、架構決策、非瑣碎除錯、綜合、寫作、判斷、當 orchestrator 指揮 subagents | ~25% |
| **關鍵層** | **Fable 5.1** | Max 方案才啟用（§2 閘門）；只在下方 checklist 全中的節點動用 | ~5% |

預設驅動用 **Opus 當指揮**，把大量只讀/機械工作 **spawn 成 Sonnet subagent**（主 context 也乾淨）。

---

## 2. 升級到 Fable 的判準（Critical-Node Checklist）

### 先過帳號方案閘門

任何形式動用 Fable 之前（建議使用者 `/model fable`、spawn `model: "fable"`、`claude -p --model fable`），先跑 `claude auth status` 看 `subscriptionType`：

| 結果 | 做法 |
|---|---|
| `pro` | **暫停 Fable。** 關鍵節點改成 Opus + `/effort max`，再加一道驗證（Opus 紅隊或跨廠商交叉審查） |
| `max` | 可以用，照下面的 checklist 與 §6 的 effort 起手級 |
| 查不到，或跟 `~/.claude.json` 的 `oauthAccount.organizationType` 對不上 | 當成 `pro` 處理，並告訴使用者兩邊不一致 |

如果你會在不同方案的帳號之間切換，**每次動用前都要重查，不能沿用上次的結果**。也不要拿 `auth status` 的 email 推方案：作用中的登入憑證（`~/.claude/.credentials.json`）與較早抓的 profile 快取（`~/.claude.json`）寫入時間不同，切換帳號後會不同步。方案以 `subscriptionType` 為準。

Max 方案也不保證 Fable 含在額度內。官方文件只寫「依方案與座位等級，Fable 可能改扣 usage credits」（[model-config](https://code.claude.com/docs/en/model-config)）。所以只要 Claude Code 跳出 usage credits 的確認提示，或 `/model` 的 Fable 那一列標「Requires usage credits」，就代表這次要另外付費：停下來問使用者，不要自己按同意。

`claude -p` 與 Agent SDK 不會跳確認提示，要扣就直接扣。因此非互動批次（eval、跨廠商辯論腳本）一律不帶 Fable，除非使用者在當次對話明確同意。

### 關鍵節點 checklist

**只有以下多數成立才動用 Fable**（cascade 原則：先便宜試，卡住才升級，別預防性使用）：

- [ ] **高風險 + 難逆**：決策塑造大量下游步驟（架構選型、研究方向、證明的關鍵引理、核心建模假設）。
- [ ] **Opus 已試且卡住 / 反覆繞圈 / 明確表達不確定**（在「已展示的困難」上升級，不是想像的困難）。
- [ ] **位於難度前沿**：新穎推理、微妙數學、跨域綜合，Fable 的邊際能力真的有差。
- [ ] **一次要對**：大型交付物的最終綜合、關鍵正確性檢查。

**反例（永遠別用 Fable）**：機械編輯、搜尋、跑程式、格式化、例行問答、first draft、任何便宜重做即可的東西。

---

## 3. 三個實作模式（借自別人可行的設計）

### A. Cascade（FrugalGPT 式）— 省錢主力
先 Sonnet/Opus 試 → 只在**展示出真的難**時才升級 Fable。不要「保險起見」先開 Fable。

### B. Orchestrator-Worker（Anthropic 多 agent 式）— 廣度任務提質
Opus 分解任務 → 平行 spawn 多個 Sonnet worker → Opus 綜合。
⚠️ **代價：token ~15×**。只在**廣度型**任務（多方向研究、掃大量檔案）用，別在窄推理任務疊。

### C. Verify / Red-team（MoA aggregator / LLM-as-judge 式）— 關鍵節點提質
關鍵輸出不要「生成完就信」。加一道對抗檢查：
- **窄用 Fable 當「驗證者」**：Opus 生成 → Fable 只紅隊/查關鍵論點（短、比全程生成便宜）。官方 API 實測支持這個方向：Opus 5 當執行者、Fable 5.1 當 advisor 是量到最準的組合，比 Opus 5 單跑預設高 3.5 分，每次嘗試的花費還略少（$7.69）。限 Max 方案（§2）。
- 或跑 **MoA 式綜合**：多 proposer（可用免費/便宜模型）+ 強 aggregator 綜合。
  - ⚠️ aggregator 用弱模型會成為**最弱環節**；真決策時換成強模型。
  - ⚠️ Self-MoA 教訓：**窄而硬的推理**題，單一強模型多次取樣常勝過混弱模型 → MoA 用在**決策/分析綜合**，不要用在硬推理。

---

## 4. 在 Claude Code 裡怎麼落地

1. **主線**：`/model` 設 Opus（指揮力好）或 Sonnet（更省），依當下任務。
2. **委派**：只讀/機械工作 → `Agent(subagent_type:"general-purpose", model:"sonnet")`，要求回傳 < 200 字 bullets。
3. **關鍵節點**：先過 §2 方案閘門。Max：手動 `/model fable`，effort 先用 `low` 或 `medium`（§6），處理完**立刻切回**。Pro：留在 Opus，`/effort max` 想完再降回。人工路由最可靠。
4. **決策/分析綜合節點**：跨廠商辯論（多家模型獨立作答→交叉批評→終審）。
5. **非互動批次**：`claude -p` 與 Agent SDK 不帶 Fable（§2）。

---

## 5. 日常 routing 速查

| 情境 | 用 |
|---|---|
| 改檔、搜尋、跑腳本、格式化、抓資料 | **Sonnet**（含 subagent） |
| 規劃、架構、除錯、寫作、綜合、判斷 | **Opus** |
| 架構/研究方向大決策、卡住的硬題、最終正確性把關 | **Fable**（切進切出；Pro 方案改 Opus + `max`） |
| 多方向研究、掃大量檔 | **Opus 指揮 + Sonnet subagents**（B） |
| 重大決策要對抗檢查 | **MoA 式綜合** 或 **Opus 生成→Fable 紅隊**（C） |

---

## 6. Effort 分級（第二個旋鈕）

**模型 = 每個 token 的能力；effort = 每回合花多少 token 去想。兩者成本相乘，要分開決定。**

### 先確認這幾件事實（2026-07-25 CLI 二進位查證，2026-09-17 對官方文件複核）

| 事實 | 含意 |
|---|---|
| 完整刻度 `low / medium / high / xhigh / max` | 共 5 級 |
| `settings.json` 的 `effortLevel` **只收到 `xhigh`** | 平常用 `/effort max` 單場升、用完降回；整段 session 都要 `max` 才設環境變數 `CLAUDE_CODE_EFFORT_LEVEL=max` |
| Fable 5.1 / Opus 5 / Sonnet 5 的預設 effort **全是 `high`**（官方 Models overview） | 「Fable 預設 max」是錯的 |
| agent frontmatter **支援 `effort`**，接受完整五級 `low/medium/high/xhigh/max` | **可以綁在 subagent 上**，刻度與 session 端一致。（欄位的 describe 字串漏列 `xhigh`，那是文件不全，不是限制） |
| agent 未設 `effort` 時繼承 session effort（官方 sub-agents 文件確認） | 只寫 `model: sonnet` 會跑成 **Sonnet + 你的 session effort**，並沒有省到思考量 |
| agent 未設 `model` 時依序取 `CLAUDE_CODE_SUBAGENT_MODEL` → 主對話模型；內建 Explore 繼承主對話、上限 Opus | 沒寫 `model` 的 agent 在 Opus session 裡就是跑 Opus |
| `ultracode` = `xhigh` 的別名 | 看到這個字不是另一級 |

### 官方實測（effort 起手級的依據）

來源：[Optimizing for cost and intelligence](https://platform.claude.com/docs/en/about-claude/models/optimizing-for-cost-and-intelligence)，數字照原文。

- **研究／知識型工作**（WideSearch、DeepWideSearch、BrowseComp、GDPval，測 Fable 5）：`medium` 準確度跟預設 `high` 一樣，成本是預設的 70–87%；`low` 掉 1–3 分，成本省三分之一到一半。
- **Fable 5.1 低 effort 比 Sonnet 便宜**：SWE-bench Pro 上 Fable 5.1 `low` 解 88.6%、每解一題 $0.54；Sonnet 5 預設 77.4%、$0.84。
- **難題不等於要高 effort**：DeepResearch Bench II 上 Fable 5.1 的 low／medium／high 分數幾乎相同，每題成本卻從 $4.66 漲到 $7.12。
- **先便宜跑、失敗再重跑**：Opus 5 全部先用 `low`，失敗的 16% 用預設重跑，通過率約 93%、每題 $0.45；全部用預設是 91.7%、$0.93。

### 分級表

下表刻度在 session 與 agent frontmatter 兩端通用。解析器另接受整數，但官方文件未承諾，本規範一律只用具名等級。

| 模型 | effort | 用在哪 |
|---|---|---|
| **Sonnet** | `medium` | 機械工作：改檔、格式化、跑腳本、抓資料、只讀 subagent |
| | `high` | first draft、需要一點自我檢查的實作（如程式生成 agent 自審） |
| | `xhigh` | 少用。Sonnet 撞到要推理的邊界時，通常該**換 Opus** 而不是加 effort |
| | ~~`max`~~ | **不要**。把錢加在弱模型的思考量上是反模式 |
| **Opus** | `medium` | 純研究、查資料、讀文獻、整理筆記的 session（上面實測：準確度不掉、成本少 13–30%） |
| | `high` | 日常指揮、規劃、綜合、寫作（模型預設）← **持久基線設在這** |
| | `xhigh` | 非瑣碎除錯、架構決策、跨檔案推理、長時間 coding／agent 任務 |
| | `max` | 單一難點：卡住的 bug、一次要對的推導、難逆決策前的最後一想。用完切回 |
| **Fable**（限 Max，§2） | `low` / `medium` | 起手級。上面實測：低 effort 的 Fable 每解一題比預設的 Sonnet 還便宜，研究型任務升 effort 分數幾乎不動 |
| | `high` | low／medium 實際跑過、錯在「沒推完」時才升 |
| | `max` | 單一卡住的難點，用完降回 |

### 該轉哪個旋鈕（判斷準則）

先問：**是模型不夠強，還是想得不夠久？**

- 錯在**知識 / 品味 / 架構** → 升**模型**
- 錯在**漏看分支 / 沒推完 / 少驗一步** → 升 **effort**
- 兩者都不確定 → **先升 effort**（便宜得多），仍失敗再升模型
- 有客觀對錯可判（測試、數值比對）→ **先便宜跑、失敗再重跑**：全部用 `low`，只把失敗的在預設級重跑（上面實測：同樣通過率、一半的錢）

### 落地機制

1. 持久基線：`~/.claude/settings.json` 的 `effortLevel` 設 `high`。純研究 session 用 `/effort medium`，coding／除錯用 `/effort xhigh`。
2. `max`：單場手動提，跟 Fable 一樣「切進切出」；整段 session 都要才用 `CLAUDE_CODE_EFFORT_LEVEL=max`。
3. Subagent：`model` 與 `effort` **都能在 agent 定義的 frontmatter 指定**。只寫 `model` 會讓它繼承 session effort，等於只降模型沒降思考量——要真的省，兩個都要寫。

```yaml
---
name: my-generator
model: sonnet
effort: high      # 不寫就繼承 session effort
---
```

---

## 7. Token 紀律 / Subagent 分工（所有任務適用）

省 token 的核心：**別讓主對話 context 被只讀的大量資料汙染**。

- **原始資料不得進主對話 context**。規則本體是這句，手段依序取用：
  1. **來源有 API 或資料在磁碟 → 寫腳本代打**：原始檔落 scratchpad，只 print 要的欄位並 `| tail -N` 封頂。
  2. **篩選需要判斷力**（讀長文挑相關段落、跨檔判相關性）→ spawn `Agent(subagent_type:"general-purpose", model:"sonnet")`，prompt 自包含、回傳 < 200 字 bullets。
  3. **結果本來就小** → 直接調工具。

  腳本排第一，因為它回傳**可驗證的原始欄位**而不是轉述，而且不必付 subagent 冷啟的固定成本；subagent 沒有被退休，只是從預設降成第二選擇，專門處理格式字串做不了的判斷工作。
- **主對話只做**：分析、綜合、判斷、機率校準、寫作、寫操作、Read < 200 行單檔、套模板、短 Edit/Write。
- **開工前先宣告打算怎麼收資料**——這一條永遠要做。要不要**停下來等回覆**，看既有授權涵不涵蓋：使用者已經給了範圍與條件、或這次請求本身就是叫你去查，宣告完直接跑；只有在成本會超乎他預期（大量平行 spawn、付費 API、超出他講的範圍）時才停下來等。真正要防的是**默默自己跑 search**（把上萬 tokens 塞進主對話 context），不是每次都再問一次。
- **同主題 follow-up 帶 `session_id`**（支援 session 的研究工具）：省 token 且更精準。
- **獨立查詢在同一 message 內平行 spawn**，不要串行。
- **目標**：主對話 input token 盡量低。

---

## 8. 反模式（省錢殺手，別做）

- ❌ 預防性開 Fable「保險」——絕大多數節點 Opus 就夠。
- ❌ Fable 做機械工作（搜尋/編輯/跑程式）。
- ❌ Pro 方案下用 Fable，或帳號方案兩邊資料對不上時照用（§2 閘門）。
- ❌ 開了 Fable 直接配 `max`——先 `low`／`medium`，實際跑過不夠才升。
- ❌ `claude -p` 或 Agent SDK 帶 Fable——不會跳確認就扣 usage credits。
- ❌ 在便宜/窄任務上疊多 agent —— token 15× 爆炸卻沒提質。
- ❌ 信自動 router 的自報數字 —— 你的人工判斷更準。
- ❌ MoA 用最弱模型當 aggregator —— 收尾是最吃能力的環節。

---
**一句話**：**便宜模型幹粗活、Opus 當大腦、Fable 只在刀口、關鍵輸出加一道驗證。** 省的是粗活的錢，贏的是刀口 + 驗證。
