---
title: DOE + Confounding — 實驗設計與混淆變因
type: methodology-note
category: experimental-design
created: 2026-05-07
tags: [methodology, DOE, Fisher, confounding, randomization, controls]
---

# Design of Experiments (DOE) + Confounding

## 一句話定義

> **DOE**: A systematic approach to planning experiments — using **randomization, replication, blocking, and control variables** — so that observed effects can be attributed unambiguously to manipulated factors rather than confounding influences.
> **Confounding**: A third variable that is correlated with both the supposed cause and the supposed effect, distorting the apparent relationship between them.

中文：DOE 是「設計能講清楚因果的實驗」的方法論；Confounding 是「會讓你誤判因果的搗亂變因」。

## 起源

- **DOE**：Ronald Fisher 在英國 Rothamsted 農業實驗站 1920 年代發展。經典書 *The Design of Experiments* (1935) 提出 randomization、replication、blocking、factorial designs 等核心概念。
- **Confounding**：統計學長期概念，現代由 Judea Pearl 用 causal graphs (DAG) 形式化（*Causality*, 2000）。

## DOE 的四大支柱（Fisher 原則）

### 1. Randomization（隨機化）

**為什麼**：把所有**未知**的混淆變因平均分配到各組。

**怎麼做**：
- 受試者隨機分到 treatment / control
- 量測順序隨機化
- 樣品在 plate 上的位置隨機化

**例子（你的領域）**：6 隻動物分 control / experimental，**不能**「先做完 3 隻 control 再做 3 隻 experimental」 — 必須交錯隨機，避免 day-to-day 變因混入。

### 2. Replication（重複）

**為什麼**：估計 noise，提升 statistical power。

**兩種 replication**：
| 類型 | 意義 | 何時必要 |
|---|---|---|
| **Technical replication** | 同樣本量多次 | 評估儀器誤差 |
| **Biological replication** | 不同樣本（動物 / 細胞批） | 評估 biological variability — **這個才能 generalize** |

**常見錯誤**：用 technical replication 數量充當 biological N（n=1 動物 × 100 trials ≠ n=100）。

### 3. Blocking（區組）

**為什麼**：**已知的**混淆變因（如 batch、性別、時間）分組控制，比 randomization 更有效。

**例子**：
- 如果一天只能跑 4 隻動物，把每天當一個 block，**每天**都做 2 control + 2 experimental — 避免「day」變成混淆
- 多天實驗 → 每天的 batch effect 被 blocking 控制

### 4. Control Variables（控制變因）

**為什麼**：保持其他條件**恆定**，讓變化只來自 manipulated factor。

**控制清單**（你的領域）：
- 動物年齡 / 性別 / 基因背景一致
- 麻醉深度
- 室溫 / 濕度 / 照明
- Imaging session 時間（早上 vs 下午有差）
- 操作者（不同人手法不同）

## DOE 設計類型

| 設計 | 用途 | 例子 |
|---|---|---|
| **Completely Randomized** | 簡單比較 | A vs B 兩組 |
| **Randomized Block** | 控制已知變因 | 每隻動物內 within-subject 比較 |
| **Factorial (2^k)** | 多因子交互 | 同時測 light × temperature 4 組合 |
| **Latin Square** | 三因子各 n levels | 順序效應控制 |
| **Crossover** | 受試者當自己的對照 | 藥物先吃 A 再吃 B |
| **Split-plot** | 兩層 randomization | 大棚 × 小區 |

## Confounding — 核心問題清單

設計實驗時逐一檢查：

1. **有哪些已知變因**會同時影響 cause 跟 effect？(列出 ≥ 5 個)
2. 對每個已知變因：用 **randomization** 控制？**blocking** 控制？還是**保持恆定**控制？
3. **未知變因**怎麼辦？→ 只能靠 randomization
4. **Reverse causation**：Y → X 而不是 X → Y，怎麼排除？
5. **Selection bias**：樣本本身就 biased？怎麼避免？
6. **Mediator vs Confounder**：你以為的 confounder 其實是 mediator（在因果鏈上）？

## Confounding 的三種類型

| 類型 | 結構 | 例子 |
|---|---|---|
| **Common cause confounder** | Z → X, Z → Y | 年齡同時影響吸菸 (X) 和肺癌 (Y) |
| **Common effect (collider) — DON'T condition!** | X → Z ← Y | 病人住院 (Z) 受症狀 X 跟 Y 都影響；按住院分層會引入假關聯 |
| **Mediator** | X → Z → Y | 吸菸 → 焦油沉積 → 肺癌；不是 confounder，不要 control 否則消除真實 effect |

**Pearl 的 backdoor criterion**：control 那些**封住 backdoor path** 的變因；**不要** control mediator 跟 collider。

## 你的領域實例

### 例子 1：兩光子 imaging 中的 confounding

研究「16 Hz vs 1 Hz imaging 對 SNR 的影響」：

| 潛在 confounder | 怎麼控制 |
|---|---|
| GCaMP6f 表現量（不同動物有差） | Within-subject design — 同一動物先 16 Hz 再 1 Hz |
| 動物清醒程度 | 固定 imaging 時段 + 行為 monitoring |
| Photobleaching（先做的會比較亮） | **必須** counterbalance 順序（half 先 16 先 1，half 反之） |
| Motion artifact | 用 motion correction algorithm + 量化 reject rate |
| Day-to-day batch | Blocking by day |

### 例子 2：BCI decoder accuracy 比較

研究「LightGBM vs LSTM 解碼動物意圖」：

| Confounder | 控制方式 |
|---|---|
| 訓練資料量不同 | 固定 N_train |
| 超參數調整投入時間不同 | 兩個各給 100 次 trial 的 grid search |
| 測試集 leakage | 嚴格 train/val/test split + temporal split (沒 look-ahead) |
| 動物個體差異 | Cross-validate across animals |

## 何時用

- **任何需要因果推論的實驗**
- 比較兩個方法 / 兩種 treatment / 兩個演算法
- 工程系統優化（factorial design 找最佳參數組合）
- 臨床試驗
- A/B testing

## 何時不用 / 限制

- 觀察性研究（用 [[13_Bradford_Hill]]）
- 倫理上不能 randomize 的情況
- 案例研究 / 質性研究
- 探索式 imaging（沒有 specific hypothesis）

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| 用 technical replication 充當 N | Biological N 才能 generalize |
| 沒 randomize 順序（先做 control 再 experimental） | 強制 counterbalance / interleave |
| Block 沒包含到關鍵變因（day, batch） | 列出所有 known confounders 再決定 block 哪些 |
| 控制太多變因（包括 mediator） | 區分 mediator vs confounder — Pearl backdoor criterion |
| Sample size 沒做 power analysis | 先算 N，再做實驗，不是事後補 |
| 多重比較沒 correct | Bonferroni / FDR / pre-register comparisons |
| Pre-register 沒做（HARKing 風險） | 寫 pre-registration document，固定 hypothesis 跟 analysis plan |

## 與其他方法的關係

- **配合 [[12_Popper_Falsifiability]]**：DOE 是「設計**能 falsify** 假說的實驗」的方法論
- **配合 [[13_Bradford_Hill]]**：兩者互補 — DOE 用於 RCT 可行情境，Hill 用於 observational
- **配合 [[15_Observable_Method_Fit]]**：observable 選對之後，DOE 決定怎麼設計實驗去量它
- **配合 [[02_FINER_PICO]]**：DOE 把 PICO 的 I (Intervention) 和 C (Comparison) 操作化
- **被 advisor-dialogue 使用**：當使用者談「實驗設計」時主用

## 給 learning-notes skill 的應用提示

當筆記涉及 **實驗設計 / 比較研究** 時：

1. 必須有 **「實驗設計 (DOE)」** section
2. 必須列出 **「Confounding 變因清單」**（至少 5 個 + 控制方式）
3. 必須說明 **randomization / blocking / replication** 怎麼做
4. 必須說明 **biological N vs technical N**
5. 必須有 **power analysis** （計算 N 的依據）
6. 如果 pre-register 適用 → 註明已 pre-register 或計畫 pre-register

## 參考來源

- [Guide to Experimental Design — Scribbr](https://www.scribbr.com/methodology/experimental-design/)
- [Confounding variable — Wikipedia](https://en.wikipedia.org/wiki/Confounding)
- [Experiments and Hypotheses — Biology LibreTexts](https://bio.libretexts.org/Courses/Lumen_Learning/Biology_for_Majors_I_(Lumen)/03:_Module_1-_Introduction_to_Biology/3.14:_Experiments_and_Hypotheses)
- [Experimental Design in Psychology](https://psyforu.com/experimental-design-in-psychology-from-hypotheses-to-results/)
- Fisher R.A., *The Design of Experiments* (1935)
- Montgomery D.C., *Design and Analysis of Experiments* (10th ed., 2019) — 標準教科書
- Pearl J., *Causality: Models, Reasoning, and Inference* (2nd ed., 2009)
