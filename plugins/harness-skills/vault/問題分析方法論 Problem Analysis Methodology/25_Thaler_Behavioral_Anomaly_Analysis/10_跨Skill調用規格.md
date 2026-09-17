---
title: 異常驅動的理論壓力測試——跨 Skill 調用規格
aliases:
  - Behavioral Anomaly Method Invocation Contract
  - Theory Stress Test Skill Contract
created: 2026-07-30
type: methodology-contract
method_id: behavioral-anomaly-theory-stress-test
status: reusable
tags:
  - methodology
  - behavioral-economics
  - replication
  - mechanism-identification
  - skill-routing
---

# 異常驅動的理論壓力測試——跨 Skill 調用規格

**所屬分支：** 00_教學大綱總覽  
**完整程序：** [[02_異常驅動的理論壓力測試方法]]  
**機制鑑別：** [[07_行為機制鑑別矩陣]]

> [!important] 方法契約
> 當任務要判斷一個理論、理性 benchmark、行為機制或市場主張是否經得起反例、重現與場域檢驗時，不能只列 bias 或故事；必須分開 **benchmark、prediction error、artifact、replication、generalization、mechanism、boundary 與 decision/welfare implication**。

## 一、觸發條件

符合任一項即可考慮調用：

1. 使用者問某個模型、常識或「理性行為」假設是否符合現實。
2. 任務涉及拍賣、合作、公平、風險、損失、時間偏誤、心理帳戶、偏好引出、效用預測或金融錯價。
3. 需要判斷實驗室效果能否外推到 field、專業者、高 stakes 或市場。
4. 有「研究已重現」「現實也有，所以機制被證明」等需要拆層的說法。
5. 研究發現 anomaly，準備加入新變數、行為機制或政策介入。
6. 需要區分 no-free-lunch、price-is-right、law of one price 與可實作套利。
7. 想把反例轉成新研究問題、實驗、產品設計或決策 guardrail。

### 不應觸發

- 單純查定義、日期或翻譯；
- 沒有理論 benchmark 的一般性人物心理猜測；
- 使用者只要表達偏好，沒有要檢驗其一致性或後果；
- 純歷史制度分岔問題：優先用 [[../24_Weber_Historical_Institutional_Analysis/10_跨Skill調用規格|Weber]]；
- 已有清楚 causal estimate，只需做算術或格式整理。

## 二、必要輸入

至少取得：

- **Benchmark**：被測的模型與規範／描述地位；
- **Domain**：人群、情境、stakes、時間與制度；
- **Observable**：選擇、價格、WTP/WTA、效用、MPC 或其他結果；
- **Prediction**：方向、範圍與實質門檻；
- **Evidence**：原設計、樣本、資料或可定位文本；
- **Competing mechanisms**：至少一個替代解釋；
- **Decision use**：結論將改變什麼。

若缺 benchmark，只能輸出「可疑現象」，不能宣稱 anomaly。若缺機制分歧操弄，只能說「與 H 一致」，不能說「H 已被證明」。

## 三、標準六階段

1. **Benchmark**：凍結模型、前提、domain、observable 與預測。
2. **Break**：預先定義 anomaly；選 sharp critical test。
3. **Replicate**：走 artifact ladder，做 direct／adversarial replication。
4. **Generalize**：沿 domain ladder 檢查 stakes、人群、程序、field 與樣本外。
5. **Discriminate**：讓候選機制產生分歧預測；維護 rescue ledger。
6. **Revise**：做最小理論更新、holdout 比較、boundary map 與 welfare gate。

完整十二步見 [[02_異常驅動的理論壓力測試方法]]。

## 四、強制輸出

### 完整模式

至少包含：

1. 一句話 benchmark 與 domain；
2. benchmark–prediction–anomaly 表；
3. artifact ladder；
4. direct replication 與 generalization 分開的 evidence ladder；
5. 相鄰機制的 divergence table；
6. 最強標準模型 rescue 與其可觀察預測；
7. 效果出現、縮小、消失或反轉的 boundary map；
8. 最小理論修正與 holdout test；
9. 來源層級；
10. decision／welfare implication 與不可推出之事。

### 快速模式

輸出六欄即可：

| Benchmark | Anomaly | 最強 artifact／rescue | 證據層級 | 未區辨機制 | 會改變的決策 |
|---|---|---|---|---|---|

## 五、各 Skill 的調用方式

| Skill | 何時調用 | 必須增加的輸出 |
|---|---|---|
| `learning-notes` | 行為經濟、決策理論、實驗結果、replication 或市場異常主題 | benchmark、anomaly、Then/Now 證據層級、機制邊界、Steelman |
| `advisor-dialogue` | 使用者要 sanity-check 理論、實驗或行為解釋 | 一次一問，依序逼出 benchmark、observable、artifact、分歧預測與 falsifier |
| `concept-tutor` | 解釋 bias、behavioral mechanism、EMH 或套利限制 | 定義之外，補近親機制、識別操弄、適用邊界與不可推出之事 |
| `problem-finding` | 從反常現象產生研究問題 | 把「再找一個 bias」升級為 benchmark failure、mechanism race、boundary 或 field-translation 問題 |
| `so-what` | 把行為或市場研究轉成決策含義 | 分開現象、機制與福利；加入可逆 guardrail、使用者槓桿與副作用 |
| `paper-review` | 論文主張 anomaly、replication、behavioral mechanism | 檢查 benchmark 是否凍結、artifact ladder、effect shrinkage、mechanism overclaim 與 holdout prediction |

## 六、與 Weber 方法的聯合路由

若問題同時有「理論失敗」與「制度異質性」，依序：

1. 本方法判斷 benchmark 是否真的失敗；
2. [[../24_Weber_Historical_Institutional_Analysis/10_跨Skill調用規格|Weber 方法]]拆行動者、控制權、制度條件與對照案例；
3. 回到本方法測試制度條件是否預測效果量與邊界；
4. 用 [[../15_Observable_Method_Fit|Observable–Method Fit]]確認量測沒有把行為、偏好、福利或價格混為一談。

### 聯合輸出

```text
M0 在條件 D1 失敗
→ 候選心理機制 H
→ 制度條件 I 改變 H 的表現或套利修正能力
→ 在 D2 預測效果縮小／擴大／消失
→ 以新樣本或對照案例檢驗
```

## 七、來源標籤

所有輸出使用：

- `[直接證據]`
- `[由文本／資料推導]`
- `[外部紅隊／跨理論補充]`
- `[當代延伸]`
- `[待驗證]`

「與某機制一致」不得改寫成「證明某機制」；「作者聲稱已重現」不得改寫成「獨立 replication 已完成」。

## 八、常見失敗

- 先貼 bias 名稱，再回頭挑證據。
- 規範模型描述失敗，便宣稱模型完全無用。
- 把所有行為納入任意效用函數，便宣稱理性模型永不可能失敗。
- 只看 p-value，不看效果量、縮小與實質門檻。
- 把同方向 field association 當 direct replication。
- 將相鄰機制合併成一個模糊心理詞。
- 價格看似荒謬，卻沒有 identical-payoff benchmark。
- 錯價存在，便宣稱有可擴張的套利策略。
- 從 anomaly 直接推出強制介入。

## 九、原典案例庫

- 03_拍賣社會偏好與參照依賴_第1至4章：共同價值、合作、公平、ownership 與 reference point。
- 04_風險時間與心智帳戶_第5至8章：EUT、Rabin calibration、present bias、mental accounts。
- 05_偏好建構與金融錯價_第9至12章：procedure invariance、experienced utility、EMH、一價定律。
- 06_科學哲學_複製外部效度與理論更新：replication、generalization、cumulative science 與新模型責任。
- 08_Antigravity分析核查表：metadata、數字、機制混淆與過度外推的紅隊示範。

## Steelman 反方立場

不是每個出現行為、replication 或市場價格的任務都需要完整十二步；過度調用會把簡單概念解釋變成方法審判。只有在使用者要評估主張真偽、機制、泛化、介入或獲利時才啟動；純定義與低風險說明維持輕量。即使觸發，也應選能改變結論的最小輸出模式。

## Bloom 高階理解檢核

- **L4**：把一句「這個 bias 已在 field 證明」拆成至少四個可分離主張。
- **L5**：判斷一個任務應用快速模式或完整模式，說明省略哪些步驟不會改變決策。
- **L6**：為新 skill 寫一條路由，使它只在 benchmark、機制或福利確實需要判定時調用本契約。
