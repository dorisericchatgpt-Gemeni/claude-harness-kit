---
title: Observable-Method Fit — 量測層方法論
type: methodology-note
category: experimental-design
created: 2026-05-07
tags: [methodology, measurement, biophysics, optical-microscopy, observable]
---

# Observable-Method Fit

## 一句話定義

> A measurement-level methodology that forces explicit alignment between (1) the **physical observable** being measured, (2) the **biological / physical mechanism** it maps to, and (3) the **method** used to measure it — exposing mismatches before they ruin the experiment.

中文：**「量什麼 / 它代表什麼 / 怎麼量」必須三件事互相對齊**。是一份實驗室教學提問清單（第二份）背後的方法論。

## 起源

這份方法論不是某一個人發明的，而是**實驗物理學 / 生物物理學 / 光學顯微術**共同的隱性傳統，由一份光學顯微實驗室的教學提問清單顯性化。底層哲學可追溯到：

- Bridgman, *The Logic of Modern Physics* (1927) — 操作主義 (operationalism)：「概念的意義就是測量它的步驟」
- Heisenberg's measurement-disturbance principle — 測量本身會改變被測對象
- 現代光學顯微術的 SNR / resolution / phototoxicity trade-off 文獻

## 兩份實驗室教學提問清單（原文）

### 第一份：問題層

1. 你想研究什麼**生物系統**？
2. 這個系統為什麼**重要**？
3. 目前**已知**什麼？
4. 真正**未知**的是什麼？
5. 這個問題為什麼需要**實驗量測**？
6. 為什麼不能只靠 **AI、文獻整理或直覺推論**得到答案？

### 第二份：量測層

1. 你的研究問題是否需要**修改**？
2. 你最主要想量測的 **physical observable** 是什麼？
3. 這個 observable 對應到什麼**生物意義**？
4. 你會使用哪一種主要**光學顯微鏡方法**？
5. 為什麼這個方法**適合**量測這個 observable？
6. 這個 observable 和方法有哪些**限制**？

## 量測層 6 問擴展版（加入 controls 與 artifacts）

把第二份清單擴展為完整的量測層方法論：

### Q1. Physical observable 是什麼？

不只問「量什麼」，要問：

- **物理量是什麼**？(光強 / 螢光強度 / 電壓 / 電流 / 力 / 位移...)
- **單位**是什麼？(光子數 / nA / μm / kPa)
- **動態範圍**多大？(min – max)
- **時間解析度**？(Hz)
- **空間解析度**？(μm)

→ 這四個維度（物理量、單位、動態範圍、時空解析）寫不出來 → observable 沒定義好。

### Q2. Biological / physical meaning 是什麼？

- 這個 observable 變化代表**機制**上發生什麼？
- 是**直接量測**還是**間接 proxy**？
- 如果是 proxy，**proxy → 真量** 的對應關係多好？

例子：「GCaMP fluorescence ↑」對應「[Ca²⁺]i ↑」，但這是間接的：
- 鈣濃度只是 spike 的 proxy
- GCaMP 動力學會 distort 真實時間訊號
- Saturation 後不再線性

→ 必須列出 proxy 鏈：fluorescence → [Ca²⁺]i → spike rate → neural activity → 行為意義

### Q3. Method 選擇與 fit 評估

選方法時的判準：

| 維度 | 問題 |
|---|---|
| **時間解析度** | Method 能不能跟上 observable 的時間尺度？ |
| **空間解析度** | 能不能解析到 observable 對應的結構？ |
| **SNR** | Method noise 比 signal 小嗎？ |
| **Penetration** | 觀察深度跟系統需求 match？ |
| **FOV** | 涵蓋範圍夠不夠？ |
| **Phototoxicity** | 會不會 perturb 系統本身？ |
| **Specificity** | 量到的真的是 observable 不是別的？ |

### Q4. Method 的 trade-off（必選一邊）

光學量測的鐵律 — 你**不可能同時最佳化所有維度**：

```
        SNR
         │
         │
         │     × 你的工作點
         │
         │
         └──────────── Speed
        /
       /
      Resolution
```

- 提高 speed → 必須降 SNR 或 resolution（光子數有限）
- 提高 SNR → 必須降 speed 或加大照度（誘發 photodamage）
- 提高 resolution → 必須降 FOV 或 speed
- 提高 penetration → 必須降 resolution（散射限制）

**Trade-off 的明確化是這個方法論的核心**：必須畫出你選的工作點，並解釋為什麼這個 trade-off 對你的 observable 是合理的。

### Q5. Limitations & Artifacts（必填）

每一種 method 都有偽訊號（artifact）會偽裝成 observable：

| Method | 常見 artifact |
|---|---|
| Two-photon imaging | Motion artifact / PMT shot noise / out-of-focus background |
| Wide-field | Hemodynamic noise / out-of-focus blur |
| Electrophysiology | EMG cross-talk / 60 Hz noise / electrode drift |
| FRET | Bleed-through / direct excitation |
| Patch clamp | Series resistance / capacitive transients |

→ 必須列：
1. **這個 method 不能量到什麼**（dynamic range 外、解析度外、specificity 外）
2. **哪些 artifact 會偽裝成 observable**
3. **怎麼 ruling out artifact**（control + post-hoc 分析）

### Q6. Controls — 沒這個就無法說服自己

Negative control（沒 effect 應該看到什麼）：
- 沒打入 GCaMP 的動物 → 應該沒 fluorescence signal
- Heat-killed 細胞 → 應該沒鈣訊號
- 沒給 task 的 baseline → 訊號 distribution 應該怎樣

Positive control（已知有 effect 應該看到什麼）：
- Calcium ionophore → 應該爆 fluorescence
- 已知 active 的 brain region → 應該有 signal
- 既有文獻已驗證的 protocol → 應該重現

**沒有 positive control 你怎麼知道你的 setup 在 work？** 這是新手最常忽略的問題。

## 領域應用實例

### 例子：「想研究小腦學習機制」

**問題層 (Round 1)**：
- Q1 (生物系統): Cerebellar Purkinje cell network in awake mice
- Q2 (重要性): Cerebellar dysfunction → ataxia, motor learning deficit; BCI signal source 候選
- Q3 (已知): Marr-Albus theory, climbing fiber error signal, LTD at PF-PC synapse
- Q4 (未知): Spike timing pattern during natural reaching tasks, single-trial decodability
- Q5 (為何要實驗): Theory 都基於 trial-averaged data，single-trial dynamics 是新 question
- Q6 (為何不靠 AI / 文獻): No public dataset of cerebellar spike during reaching at single-cell resolution

**量測層 (Round 2)**：
- Q1 (修改問題?): 收緊到「single-trial Purkinje spike timing during reaching」
- Q2 (Observable): GCaMP6f fluorescence dF/F0 → spike rate (deconvolved); 單位 ΔF/F (%) → spikes/s
- Q3 (Bio meaning): Spike rate 對應 PC inhibitory output → DCN → motor cortex
- Q4 (Method): Two-photon Lissajous scanning @ 16 Hz, 1×1 mm FOV, GCaMP6f
- Q5 (適合性): 16 Hz 跟得上 GCaMP6f decay (~200 ms); single-cell resolution; awake imaging 可行
- Q6 (限制):
  - GCaMP6f 不能解 100Hz spike train（dynamics 太慢）
  - Motion artifact during reaching
  - Lissajous trajectory 在 corner 區 sampling 不均
  - 只能看 superficial PCs (z < 300 μm)

**Controls**:
- Negative: Non-injected mice; resting (no task) baseline
- Positive: Optogenetic stim of climbing fiber → 應該看到 complex spike

→ 整個方法論走完，問題從「想研究小腦」變成「在 awake mice 用 16 Hz 兩光子量 superficial Purkinje cells 在 reaching 時的 single-trial GCaMP6f dF/F，並 deconvolve 出 spike rate」 — 這才是可執行的研究問題。

## 何時用

- **每次**設計新實驗
- 寫 paper Methods section 之前
- 跟教授討論方向時的對話骨架
- 評估別人的論文（用這 6 問檢驗他們的 design）

## 何時不用

- 純理論研究
- 已建立 SOP 的常規量測（雖然定期回顧也有益）

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| 先選 method 再找 observable | 強迫倒過來：先寫 observable，再選 method |
| Observable 沒寫單位 / 動態範圍 | 補上四維度（物理量、單位、範圍、解析） |
| 沒區分 direct measurement vs proxy | 寫出完整 proxy 鏈 |
| 沒列 trade-off | 強迫畫出工作點 + 解釋取捨 |
| 沒 positive control | 沒這個你怎麼知道 setup 在 work？ |
| 沒列 method 不能量什麼 | 強迫列「out of dynamic range / out of resolution / out of specificity」三項 |

## 與其他方法的關係

- **配合 [[02_FINER_PICO]]**：observable = PICO 的 O；method = PICO 的 I
- **配合 [[14_DOE_Confounding]]**：observable 確定後用 DOE 設計實驗
- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier Q3「what's new in your approach」要在 method 跟 observable 兩維度都展開
- **配合 [[12_Popper_Falsifiability]]**：observable 必須夠 specific 才能 falsify
- **被 advisor-dialogue 使用**：對量測類研究是核心提問框架（直接源自原始提問清單）

## 給 learning-notes skill 的應用提示

當筆記涉及 **實驗 / 量測 / 系統 build / 光學 / 生物物理** 時：

1. 必須有 **「研究問題層 6 問」** section（第一份清單原文）
2. 必須有 **「量測層 6 問」** section（第二份清單擴展版）
3. Observable 必須寫四維度：物理量、單位、動態範圍、時空解析
4. 必須有 **「Trade-off 工作點」** section（畫圖 / 表格）
5. 必須有 **「Controls (negative + positive)」** section
6. 必須列 **「Method 不能量到什麼 + Artifacts」**
7. 這份筆記是這個資料夾跟其他 domain（光學顯微術 / BCI）連接的核心橋樑

## 參考來源

- 光學顯微實驗室教學提問清單（原始 source）
- Helmchen F. & Denk W., *Deep tissue two-photon microscopy*, Nature Methods (2005)
- Chen T.-W. et al., *Ultrasensitive fluorescent proteins for imaging neuronal activity*, Nature (2013) — GCaMP6 benchmark
- Bridgman P.W., *The Logic of Modern Physics* (1927) — 操作主義
- Mertz J., *Introduction to Optical Microscopy* (2nd ed., 2019) — 顯微術 trade-off 標準參考
