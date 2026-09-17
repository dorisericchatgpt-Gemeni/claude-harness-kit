---
title: Bradford Hill criteria — 因果性 9 條
type: methodology-note
category: experimental-design
created: 2026-05-07
tags: [methodology, causal-inference, epidemiology, Bradford-Hill, observational-study]
---

# Bradford Hill criteria

## 一句話定義

> A set of 9 viewpoints proposed by Sir Austin Bradford Hill (1965) to assess whether an observed **statistical association** is likely to reflect a **causal relationship**, particularly in observational (non-randomized) studies where direct experimental manipulation is impossible.

中文：在無法做隨機對照實驗時（流行病學、生態學、歷史資料），用這 9 個面向綜合判斷「相關性」是不是「因果性」。

## 起源

Sir Austin Bradford Hill（英國流行病學家）1965 年於 Royal Society of Medicine 演講 *The Environment and Disease: Association or Causation?*。背景是當時「吸菸 → 肺癌」爭議，無法做 randomized trial（不能強迫人吸菸），需要從 observational data 推因果。Hill 提出 9 條 viewpoints（不是 strict criteria — 他自己強調不能機械套用）。後成為流行病學、藥物安全評估、環境健康的標準工具。

## 九條核心問題清單

每一條都是一個問題：

| # | Criterion | 中文 | 核心問題 | 例子（吸菸-肺癌） |
|---|---|---|---|---|
| 1 | **Strength** | 強度 | 相關係數**多大**？effect size 多強？ | 吸菸者得肺癌風險是非吸菸者 9–25 倍 |
| 2 | **Consistency** | 一致性 | **不同**人、地、時間、研究都看到嗎？ | 1950s–現在，全球各國研究都顯示同向 |
| 3 | **Specificity** | 特異性 | 這個原因**只**導致這個結果嗎？ | 吸菸特別關聯到肺癌（相對其他癌） |
| 4 | **Temporality** | 時序 | 原因**先**於結果嗎？(必要條件) | 吸菸習慣早於肺癌診斷 |
| 5 | **Biological gradient** (Dose-response) | 劑量反應 | **越多**原因 → **越多**結果？ | 每天抽越多支、得肺癌風險越高 |
| 6 | **Plausibility** | 機制合理 | 有**生物學機制**可解釋嗎？ | 焦油中的致癌物作用於支氣管上皮 |
| 7 | **Coherence** | 整體一致 | 跟既有知識**不衝突**嗎？ | 跟細胞 / 動物實驗一致 |
| 8 | **Experiment** | 實驗證據 | **介入**後結果改變嗎？ | 戒菸 → 肺癌風險下降 |
| 9 | **Analogy** | 類比 | **相似的因果**已被證實嗎？ | 其他化學物質吸入 → 肺病已知 |

## Hill 自己的關鍵警告

Hill 在原演講最後特別強調：

> 「**None of my nine viewpoints can bring indisputable evidence for or against the cause-and-effect hypothesis**...What they can do, with greater or less strength, is to help us to make up our minds on the fundamental question — is there any other way of explaining the set of facts before us?」

意思：
1. **沒有任何單一條是 sufficient 或 necessary**
2. 不要當 checkbox 用 — 要綜合判斷
3. **核心問題是**：「除了因果性，還有什麼能解釋這個 pattern？」(類似 [[09_Steelman_Red_Team]] 的 alternative explanations 概念)

## Temporality 是唯一必要條件

9 條中只有 **Temporality（時序）** 是邏輯必要：原因不可能在結果之後發生。其他 8 條都是強度判準。

→ 任何 cross-sectional study（橫斷研究）天生不能滿足 temporality，所以無法強推因果。

## 替代解釋的清單（必須一一排除）

當你觀察到 X 跟 Y 有關聯時，因果不是唯一可能：

| 替代解釋 | 描述 | 例子 |
|---|---|---|
| **Chance** | 純機運 | 樣本太小 |
| **Bias** | 系統性誤差 | Selection bias / measurement bias |
| **Confounding** | 第三變因 | 吸菸者也常喝酒 → 真兇是誰？ |
| **Reverse causation** | Y → X 不是 X → Y | 早期肺病讓人想吸菸抑制咳嗽？ |
| **Selection effects** | 樣本本身已 biased | 醫院樣本不能代表全人口 |

→ 排除這 5 個替代解釋之後再用 Hill 9 條才有意義。

## 何時用

- Observational study（無法 randomize）
- 流行病學
- 藥物 post-market safety surveillance
- 環境健康（污染 → 疾病）
- 歷史 / 社會科學的因果推論
- 重大決策（公共政策、臨床指南）

## 何時不用

- 已有 RCT 數據（隨機對照實驗就是因果，不需要 Hill）
- 純 mechanistic 研究（生物機制本身就是因果鏈）
- Hill 自己強調：**緊急公衛決策**時不應卡在嚴格 9 條（如 cholera outbreak 不能等 dose-response 數據才行動）

## 現代擴展與爭議

| 後續發展 | 說明 |
|---|---|
| **Mendelian randomization** | 用基因變異作為「天然隨機化」工具，補強 Hill |
| **Causal DAGs (Pearl)** | Judea Pearl 用因果圖形式化 confounding，比 Hill 更精確 |
| **Counterfactual framework** | Rubin causal model — 用 potential outcomes 定義因果 |
| **批評** | Hill 9 條太定性、機械套用易誤導；現代 prefers DAG + counterfactual |

不過 Hill 仍是**入門 + 快速判斷**的最實用工具。

## 例子（你的領域）

假設你觀察到：「Cerebellar Purkinje cell firing rate 上升 → 動物 reaching 動作更精準」

Hill 9 條檢驗：
1. Strength: r = 0.7 → 強
2. Consistency: 6 隻動物都看到 → 一致
3. Specificity: 只在 reaching task 期間，rest 時無關 → 特異
4. **Temporality**: firing rate 上升在 movement onset **之前** ← **關鍵**
5. Dose-response: 高 firing 對應更精準動作？
6. Plausibility: Purkinje cell → DCN → motor cortex 的解剖學支持
7. Coherence: 跟 Marr-Albus theory 一致
8. Experiment: optogenetic 抑制 Purkinje cell → 動作變差？
9. Analogy: motor cortex M1 firing 跟動作關聯類似

→ 全部過 → 強支持因果。任何一條沒過 → 必須補實驗。

## 與其他方法的關係

- **配合 [[14_DOE_Confounding]]**：DOE 設計實驗排除 confounding；Hill 用在無法 DOE 的情境
- **配合 [[12_Popper_Falsifiability]]**：Hill 不是 falsification 工具而是 corroboration 工具，但兩者都關心「替代解釋」
- **配合 [[09_Steelman_Red_Team]]**：Hill criterion 8 (experiment) 和 alternative explanations 檢驗就是 red team 的本質
- **被 advisor-dialogue 使用**：當使用者帶來 observational data / correlation 結果時，必問 Hill 9 條

## 給 learning-notes skill 的應用提示

當筆記涉及 **observational data / correlation / 相關性** 時：

1. 必須有一個 **「因果性檢驗 (Bradford Hill)」** section
2. 9 條逐一回答（即使只能填 3 條也要列出哪 6 條未滿足）
3. **必須**有「替代解釋」section — 列出 chance / bias / confounding / reverse causation / selection 各自怎麼排除
4. 如果只滿足 < 5 條 → 結論必須降級為「相關性」而非「因果性」
5. Temporality 沒滿足 → 直接 flag 不能推因果

## 參考來源

- [Bradford Hill criteria — Wikipedia](https://en.wikipedia.org/wiki/Bradford_Hill_criteria)
- Hill A.B., *The Environment and Disease: Association or Causation?*, *Proc R Soc Med* (1965) — 原始論文
- [The Bradford Hill Criteria — National Library of Medicine review](https://pmc.ncbi.nlm.nih.gov/articles/PMC4589117/)
- Pearl J., *Causality* (2nd ed., 2009) — 現代因果推論框架
- Rothman K.J. & Greenland S., *Modern Epidemiology* (3rd ed., 2008)
