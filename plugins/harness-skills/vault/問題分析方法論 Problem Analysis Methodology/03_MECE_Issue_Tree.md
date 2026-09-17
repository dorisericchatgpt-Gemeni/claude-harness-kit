---
title: MECE + Issue Tree — McKinsey 問題拆解法
type: methodology-note
category: problem-decomposition
created: 2026-05-07
tags: [methodology, problem-decomposition, McKinsey, consulting, MECE]
---

# MECE + Issue Tree

## 一句話定義

> **MECE** (Mutually Exclusive, Collectively Exhaustive): A grouping principle stating that subcategories must not overlap and must together cover the whole.
> **Issue Tree**: A hierarchical decomposition of a top-level problem into MECE sub-problems, each branchable into further sub-issues until reaching actionable hypotheses.

中文：把大問題切成「彼此不重疊、加起來完整覆蓋」的子問題樹。

## 起源

- **MECE** 由 Barbara Minto 在 1960 年代後期於 McKinsey 提出，後成為其 *Pyramid Principle* 的基礎（見 [[04_SCQA_Pyramid_Principle]]）
- **Issue Tree** 是 MECE 的視覺化形式，是顧問業（McKinsey, BCG, Bain）的標配工具

## 核心問題清單

切 MECE issue tree 時要逐層問：

1. **這個 root 問題用一句話講是什麼？** （不能寫「分析公司營收」這種模糊命題；要寫「為什麼 Q3 營收下滑 18%？」）
2. **第一刀怎麼切？** 切完之後問自己：
   - 這幾個分支**互斥**嗎？(沒有 overlap？)
   - 這幾個分支**窮盡**嗎？(加起來涵蓋全部可能？)
3. **每個分支再問同樣兩題**，直到分到「可以實際去做 / 去查 / 去量」的葉節點為止
4. **哪一支最可能是答案？** 這叫 hypothesis-driven — 不要平均分配資源到每一支
5. **如果第一刀切錯了，怎麼換刀？** 常見替代切法：時間軸 / 地理 / 客戶區隔 / 產品線 / 流程階段 / 數量 vs 品質

## MECE 的常見「切刀法」

| 切法 | 例子 | 何時用 |
|---|---|---|
| **時間軸** | before/during/after | 因果分析、流程診斷 |
| **空間 / 結構** | 上中下游、北中南 | 系統性問題 |
| **量 vs 質** | 是不是有？有的話多少？ | 二元問題 |
| **內 vs 外** | internal cause / external cause | 歸因分析 |
| **加減乘除** | 營收 = 客戶數 × 客單價 × 頻次 | 有公式可套的指標 |
| **Process 階段** | 進貨 → 加工 → 出貨 | 工程 / 製造問題 |
| **2×2 矩陣** | 高/低 × 強/弱 | 策略選擇 |

研究問題上的應用例子（小腦 BCI 研究）：

```
為什麼小腦 Purkinje cell 的 spike 訊號可以拿來做 BCI？
├── (A) 訊號層面：Purkinje cell 真的編碼可解碼的運動意圖嗎？
│   ├── (A1) 已知 Purkinje cell 編碼什麼？
│   ├── (A2) 編碼方式是 rate-coding 還是 timing-coding？
│   └── (A3) 訊號能否用線性 decoder 解出？
├── (B) 量測層面：能不能量到夠好的訊號？
│   ├── (B1) GCaMP6f 在 Purkinje cell 的 SNR？
│   ├── (B2) 16 Hz 夠快嗎？
│   └── (B3) Cranial window 穩定性？
└── (C) 系統層面：能不能即時 close-loop？
    ├── (C1) Decoding latency 上限多少？
    ├── (C2) 動物行為任務怎麼設計？
    └── (C3) Reward 機制？
```

A / B / C 互斥、加起來窮盡（不漏「為什麼可以做」的任何面向）。

## 何時用

- 大問題抽象到不知道從哪下手時
- Grant proposal 的 Specific Aims 排版（每個 Aim 是一支主分支）
- Project planning（決定哪一支先做、哪一支可以暫緩）
- Debug 一個失敗的實驗 / 系統（從 root cause 往下切）

## 何時不用

- 問題已經夠 specific 不用拆
- 需要創意發散時（MECE 是收斂工具不是發散工具）
- 答案需要跨支整合時（樹狀結構強迫切割，但有些問題本質是 graph）

## 常見誤用 / 失敗 pattern

| 錯誤 | 例子 | 修正 |
|---|---|---|
| 不互斥 | 「年輕人 / 學生 / 上班族」(學生跟上班族可能重疊) | 改成「全職學生 / 在職 / 無業」 |
| 不窮盡 | 「iOS / Android 用戶」(漏 web、漏 KaiOS) | 加 "Other" bucket 或重新切 |
| 切太多刀 | 第一層 8 支 | 控制在 3–5 支，太多代表抽象層次選錯 |
| 切的維度不一致 | 「按時間 / 按產品 / 按地區」混在同一層 | 一層只用一個維度 |
| 沒做 hypothesis-driven | 平均分析每一支 | 先猜哪一支最可能，集中火力驗證 |

## 與其他方法的關係

- **配合 [[04_SCQA_Pyramid_Principle]]**：Issue tree 拆完之後，用 Pyramid 由下而上總結成「結論先行」的論述
- **配合 [[05_5_Whys_Fishbone]]**：Fishbone 是 issue tree 的「根因專用」變體
- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier Q1（你想做什麼）的答案就是 issue tree 的 root
- **被 advisor-dialogue 使用**：當使用者帶來的問題太大時，用 issue tree 強迫他切

## 給 learning-notes skill 的應用提示

當使用者問的是 **大型 / 抽象主題**（如「我想學 BCI」、「想了解半導體產業」）時：

1. 在 `00_教學大綱總覽.md` 的「章節結構」section，必須是一棵 MECE issue tree
2. 第一層分支控制在 3–5 個，每個分支必須能用一句話講清楚
3. 檢查互斥性：兩個分支的內容能不能放到對方檔案裡？如果可以，沒切乾淨
4. 檢查窮盡性：有沒有「Other / 雜項」？如果有，可能切的維度錯了
5. 章節編號（01, 02, 03...）對應 tree 的 leaf node

## 參考來源

- [Issue Trees — StrategyU](https://strategyu.co/issue-tree/)
- [MECE principle — Wikipedia](https://en.wikipedia.org/wiki/MECE_principle)
- [MECE Framework McKinsey — MBA Crystal Ball](https://www.mbacrystalball.com/blog/strategy/mece-framework/)
- [Distilling the Essence of the McKinsey Way: The Problem-Solving Cycle](https://scispace.com/pdf/distilling-the-essence-of-the-mckinsey-way-the-problem-2o7pbxet70.pdf)
- Minto B., *The Pyramid Principle: Logic in Writing and Thinking* (1987)
