---
title: MOC - 問題分析方法論 Problem Analysis Methodology
tags: [moc, methodology, meta]
aliases: [Methodology MOC, 方法論 MOC]
type: moc
---

# 🧠 MOC：問題分析方法論 Problem Analysis Methodology

> **Map of Content**
> 本檔是公開快照：只列出隨 `harness-skills` plugin 附帶的條目（01–15、23，以及 24／25 的程序與調用規格）

## 📖 領域簡介

這是一個 **meta-level** 領域 — **不是研究某個生物 / 物理現象，而是研究「怎麼問對問題」本身**。

來源：管理顧問業（McKinsey, Amazon）+ 學術研究方法論（DARPA, NIH）+ 批判性思考（Socrates, Toulmin）+ 決策科學（Klein, Pearl）的方法論精華。

它被整合進 learning-notes skill 的 Step 1.5「Apply Methodology Layer」強制流程，未來任何學習筆記產出時都會自動走過方法論檢查。

## 🧭 主題地圖

<!-- wiki-index:auto-start -->

### 📚 方法論主題（快照）

- [[問題分析方法論 Problem Analysis Methodology/00_教學大綱總覽|問題分析方法論 Problem Analysis Methodology]] — 按使用情境分類（A–G 研究與論證 / **I. 制度與宏觀結構分析** / **J. 行為、決策與理論壓力測試**）

### 🗂️ 子筆記快速索引

#### A. 形成研究問題 (Research Question Formation)
- [[問題分析方法論 Problem Analysis Methodology/01_Heilmeier_Catechism|01 Heilmeier Catechism]] — DARPA 8 問
- [[問題分析方法論 Problem Analysis Methodology/02_FINER_PICO|02 FINER + PICO]] — 醫學研究問題篩選
- [[問題分析方法論 Problem Analysis Methodology/12_Popper_Falsifiability|12 Popper Falsifiability]] — 可證偽性

#### B. 拆解大問題 (Problem Decomposition)
- [[問題分析方法論 Problem Analysis Methodology/03_MECE_Issue_Tree|03 MECE + Issue Tree]] — McKinsey 拆解
- [[問題分析方法論 Problem Analysis Methodology/04_SCQA_Pyramid_Principle|04 SCQA + Pyramid Principle]] — Minto 結構化
- [[問題分析方法論 Problem Analysis Methodology/05_5_Whys_Fishbone|05 5 Whys + Fishbone]] — 根因分析

#### C. 檢驗論證強度 (Argument Validation)
- [[問題分析方法論 Problem Analysis Methodology/07_Socratic_Method|07 Socratic Method]] — 蘇格拉底追問
- [[問題分析方法論 Problem Analysis Methodology/08_Toulmin_Argumentation|08 Toulmin Argumentation]] — 論證六元素
- [[問題分析方法論 Problem Analysis Methodology/09_Steelman_Red_Team|09 Steelman + Red Team]] — 逆向自我攻擊

#### D. 預判失敗 (Failure Prediction)
- [[問題分析方法論 Problem Analysis Methodology/06_Pre_mortem|06 Pre-mortem]] — Klein 假設失敗回推

#### E. 實驗與因果推論 (Experimental Design & Causal Inference)
- [[問題分析方法論 Problem Analysis Methodology/13_Bradford_Hill|13 Bradford Hill]] — 因果性 9 條
- [[問題分析方法論 Problem Analysis Methodology/14_DOE_Confounding|14 DOE + Confounding]] — 實驗設計與混淆
- [[問題分析方法論 Problem Analysis Methodology/15_Observable_Method_Fit|15 Observable-Method Fit]] — 量測層方法論（兩份實驗室教學提問清單）

#### F. 反推使用者需求 (Customer-Driven Design)
- [[問題分析方法論 Problem Analysis Methodology/11_Working_Backwards|11 Working Backwards]] — Amazon PR/FAQ

#### G. 確保認知層次 (Cognitive Depth)
- [[問題分析方法論 Problem Analysis Methodology/10_Bloom_Taxonomy|10 Bloom Taxonomy]] — 認知層次六級

#### I. 制度與宏觀結構分析 (Institutional & Macro-Structural Analysis)
- [[問題分析方法論 Problem Analysis Methodology/23_Weber_Institutional_Economic_Analysis|23 Weber Institutional Economic Analysis]] — 韋伯制度經濟分析法：以「可計算性」為主變數；政治租金 vs 市場報酬、家計/經營分離、傳統主義摩擦力、「常數不能解釋變數」因果紀律
- [[問題分析方法論 Problem Analysis Methodology/24_Weber_Historical_Institutional_Analysis/02_韋伯式經濟史分析方法|24 Weber Historical Institutional Analysis]] — 可重用的歷史制度分析分支：制度維度、行動者、對照案例、因果角色、條件合取、反事實與來源審計；見 [[問題分析方法論 Problem Analysis Methodology/24_Weber_Historical_Institutional_Analysis/10_跨Skill調用規格|跨 skill 調用契約]]

#### J. 行為、決策與理論壓力測試 (Behavior, Decision & Theory Stress Testing)
- [[問題分析方法論 Problem Analysis Methodology/25_Thaler_Behavioral_Anomaly_Analysis/02_異常驅動的理論壓力測試方法|25 Anomaly-Driven Theory Stress Test]] — 凍結 benchmark，以 critical test、artifact ladder、direct／adversarial replication、domain ladder、mechanism discrimination 與 holdout 更新理論；見 [[問題分析方法論 Problem Analysis Methodology/25_Thaler_Behavioral_Anomaly_Analysis/07_行為機制鑑別矩陣|行為機制鑑別矩陣]] 及 [[問題分析方法論 Problem Analysis Methodology/25_Thaler_Behavioral_Anomaly_Analysis/10_跨Skill調用規格|跨 skill 調用契約]]

<!-- wiki-index:auto-end -->

## 🛠️ 與 skill 的整合

| Skill                  | 如何使用本 MOC                                                                                     |
| ---------------------- | --------------------------------------------------------------------------------------------- |
| `learning-notes`       | Step 1.5「Apply Methodology Layer」強制走訪 — 依主題類型自動載入對應方法論筆記、注入 Steelman/Bloom/Toulmin 等 sections |
| `advisor-dialogue`     | 一問一答對話時，從 A–G 七類框架抽具體問題                                                                       |
| `so-what` / 金融分析          | 用 I 類（23 Weber）做制度體檢：可計算性計分卡、政治租金比重、家計/經營分離、需求類型（大眾 vs 訂製）                              |
| `paper-review`         | 論文 review 時用 08 Toulmin + 09 Steelman + 12 Popper 三件組                                         |
| `concept-tutor` / `problem-finding` / `so-what` | 行為、決策、replication 或市場異常任務，調用 25 的 benchmark—anomaly—mechanism—boundary—welfare 分層 |

## 📊 概覽（Dataview）

````dataview
TABLE
  file.mtime AS "最後更新"
FROM "問題分析方法論 Problem Analysis Methodology"
SORT file.name ASC
````

## 🌱 待補主題（Stubs）

- [ ] **Bayesian reasoning / 貝氏推理** — 從先驗到後驗的決策框架
- [ ] **Counterfactual thinking / 反事實思考** — Pearl causal hierarchy
- [ ] **Systems thinking / 系統思考** — Donella Meadows 槓桿點
- [ ] **OODA Loop** — Boyd 觀察 → 定向 → 決定 → 行動
- [ ] **First Principles Thinking** — Musk / Aristotle 原理推理

## 📚 共用參考資料

每份子筆記末尾都有完整引用。共用書單：

- Minto B., *The Pyramid Principle* (1987)
- Popper K., *The Logic of Scientific Discovery* (1959)
- Toulmin S., *The Uses of Argument* (1958)
- Klein G., *Sources of Power* (1998)
- Pearl J., *Causality* (2nd ed., 2009)
- Anderson L.W. & Krathwohl D.R., *A Taxonomy for Learning, Teaching, and Assessing* (2001)
- Bryar C. & Carr B., *Working Backwards* (2021)
