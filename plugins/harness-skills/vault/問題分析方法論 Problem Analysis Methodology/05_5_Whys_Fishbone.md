---
title: 5 Whys + Fishbone (Ishikawa) — 根因分析雙工具
type: methodology-note
category: problem-decomposition
created: 2026-05-07
tags: [methodology, root-cause-analysis, lean, six-sigma, Toyota]
---

# 5 Whys + Fishbone (Ishikawa)

## 一句話定義

> **5 Whys**: A linear, depth-first technique that asks "why?" iteratively (typically 5 times) to drill from a symptom to its root cause.
> **Fishbone Diagram (Ishikawa Diagram)**: A breadth-first visual tool that classifies potential causes into categories (commonly People, Process, Technology, Environment) before drilling down.

中文：**5 Whys 是「縱向深挖」，Fishbone 是「橫向分類」**。常合併使用：先用 Fishbone 找出所有可能的因，再對最可疑那支用 5 Whys 挖到底。

## 起源

- **5 Whys**：Sakichi Toyoda（豐田創辦人）1930 年代發展，後成為 Toyota Production System 與 Lean 的核心工具
- **Fishbone**：Kaoru Ishikawa（石川馨）1960 年代為造船業品質管理而設計，因形似魚骨得名

## 5 Whys — 核心問題清單

### 操作流程

1. 把問題寫成一句話（**症狀 / 現象**，不是猜測的原因）
2. 問「為什麼會發生？」→ 寫下答案 1
3. 對答案 1 再問「為什麼？」→ 寫下答案 2
4. 重複 3–7 次（5 是經驗值，不是硬規則）
5. 直到答案進入「**系統 / 結構 / 政策層級**」（個人錯誤不是 root cause）

### 例子（你的領域）

**現象**：兩光子鈣訊號影像有大量 motion artifact

- Why 1: 為什麼有 motion artifact？→ 動物頭在動
- Why 2: 為什麼頭在動？→ Head-fix 不夠穩
- Why 3: 為什麼不夠穩？→ Head-post 黏合面積太小
- Why 4: 為什麼面積太小？→ Cranial window 大小限制了黏合範圍
- Why 5: 為什麼受限於 window 大小？→ Window 直徑與 head-post 設計沒一起優化

✅ Root cause = **設計流程沒整合**（系統層），不是「動物在動」（症狀層）

## Fishbone — 核心問題清單

### 結構

```
              People  Process  Technology
                 \       |       /
                  \      |      /
         ─────────[Problem]
                  /      |      \
                 /       |       \
           Environment  Materials  Measurement
```

### 標準 6 大類別 (6M, 製造業)

| 類別 | 中文 | 適用問題 |
|---|---|---|
| **M**an / People | 人員 | 訓練不足？經驗差異？溝通問題？ |
| **M**achine / Technology | 機器 / 技術 | 設備老舊？校準？相容性？ |
| **M**ethod / Process | 方法 / 流程 | SOP 缺失？步驟錯？流程冗餘？ |
| **M**aterial | 材料 | 試劑批次？樣本品質？來源？ |
| **M**easurement | 量測 | 儀器精度？校準？讀值方法？ |
| **M**other Nature / Environment | 環境 | 溫濕度？光？震動？電磁干擾？ |

### 學術研究改良版（推薦）

| 類別 | 適用問題 |
|---|---|
| **Theory / Model** | 假說錯了？模型過簡？ |
| **Experimental Setup** | 設備？校準？protocol？ |
| **Subject / Sample** | 受試者異質性？樣本污染？批次效應？ |
| **Analysis / Statistics** | 模型選錯？多重比較？outlier 處理？ |
| **Researcher** | 訓練？bias？溝通？ |
| **Environment** | 物理環境（溫度、震動）？社會環境（lab 文化、資源）？ |

### 操作流程

1. 把問題寫在魚頭
2. 畫出 6 條主骨（6M 或自訂）
3. 對每條主骨**獨立**腦力激盪 — 列出所有可能的 cause
4. 對每個 cause 再分次級 cause（成為「魚刺」）
5. 全部畫完後，**標記最可疑的 2–3 個**
6. 對最可疑那幾個套 5 Whys 挖到底

## 5 Whys + Fishbone 整合工作流

```
1. Fishbone 發散：列出所有可能因（廣度）
2. 投票 / 證據評估：選出最可疑 2–3 個
3. 5 Whys 收斂：對每個可疑 cause 縱向挖到 root
4. 行動：root cause 對應到具體可改的動作
```

## 何時用

- 實驗結果出問題、不知道哪裡錯時
- Post-mortem 分析（[[06_Pre_mortem]] 是 pre，這是 post）
- Code debug 找不到 root cause 時
- 製程 / 流程 / 系統異常診斷

## 何時不用

- 多因素同時作用（Fishbone 假設 cause 可分類，但有些是交互效應）
- 需要量化因果強度時（Fishbone/5 Whys 是定性工具，要量化請用 [[14_DOE_Confounding]] 或 [[13_Bradford_Hill]]）
- 探索性研究（這兩個工具是「找錯誤原因」用，不是「探索新現象」用）

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| 5 Whys 停在「人為錯誤」 | 繼續問為什麼這個人會犯這個錯（系統 / 訓練 / 流程問題） |
| 5 Whys 變成猜測接龍 | 每一層都要有證據支持，不是憑感覺 |
| 5 Whys 線性思考漏掉並聯 cause | 配合 Fishbone 補橫向視角 |
| Fishbone 類別亂塞（同一個 cause 出現在多支） | MECE 原則違反，重新分類 |
| Fishbone 列了 50 個 cause 沒收斂 | 強制標記前 3 名繼續挖 |
| 找到 root cause 沒對應行動 | Root cause 必須**可執行修改**才有用 |

## 與其他方法的關係

- **配合 [[06_Pre_mortem]]**：Pre-mortem 是 fishbone 的「假設未來」版本（假設專案失敗了，列出 fishbone 的所有 cause）
- **配合 [[03_MECE_Issue_Tree]]**：Fishbone 是 MECE issue tree 的根因專用變體
- **配合 [[14_DOE_Confounding]]**：Fishbone 找出可能 cause 後，DOE 用實驗驗證哪些是真的 cause
- **被 advisor-dialogue 使用**：當使用者帶來「實驗失敗 / bug / 異常結果」類問題時主用

## 給 learning-notes skill 的應用提示

當使用者問的是 **「為什麼 X 不 work / 為什麼 X 失敗」** 類型題目時：

1. 必須先用 Fishbone 列出所有可能因（學術版 6 類別）
2. 對最可疑 2–3 支套 5 Whys 至少 5 層
3. Root cause 必須在「系統 / 結構 / 設計」層，不是「個人錯誤」
4. 每個 root cause 必須對應到一個可執行行動
5. 在筆記中保留 Fishbone 圖（用 mermaid 或 ASCII art）

## 參考來源

- [Cause and Effect Analysis: Using Fishbone Diagram and 5 Whys — Visual Paradigm](https://www.visual-paradigm.com/project-management/fishbone-diagram-and-5-whys/)
- [Root Cause Analysis: Integrating Ishikawa Diagrams and the 5 Whys — iSixSigma](https://www.isixsigma.com/cause-effect/root-cause-analysis-ishikawa-diagrams-and-the-5-whys/)
- [Fishbone Diagram & The 5 Whys — LA County Public Health (PDF)](http://publichealth.lacounty.gov/qiap/docs/Topic3-Fishbone.pdf)
- [Fishbone Diagram: Finding the Root Cause — GoLeanSixSigma](https://goleansixsigma.com/fishbone-diagram/)
- Ishikawa K., *Guide to Quality Control* (1976)
