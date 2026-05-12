# AI 能源消耗 × 成本效益研究報告

> 整理時間：2026年5月
> 資料來源：arXiv、IEA、Goldman Sachs、Capgemini、Gartner、MIT、A16Z、Google/Microsoft 環境報告

---

## 一、AI 訓練的碳排放

### 關鍵數據
- **GPT-3 訓練**：耗電約 1,287 MWh，產生 502–552 噸 CO₂eq（≒ 5 輛車終生排放）
- **BLOOM 訓練**：使用再生能源，碳排僅 25 噸（比 GPT-3 少 96%）
- **Strubell et al. (2019)**：訓練一個大型 NLP 模型（含神經架構搜尋）產生 626,155 磅 CO₂，相當於 125 趟紐約—北京來回機票
- 訓練是一次性成本，但**推論的終身累積碳排遠超過訓練**（可達數千倍）

### 來源
- Strubell et al. (2019)「Energy and Policy Considerations for Deep Learning in NLP」https://arxiv.org/abs/1906.02629
- LLMCarbon 研究

---

## 二、AI 推論的能源與水資源消耗

### 關鍵數據
- **ChatGPT（2023 年全年）**：用水量 40–60 億公升；每次對話約 500 毫升
- **GPT-4 單次查詢**：約為 Google 搜尋的 10 倍能耗
- **全球 AI 資料中心用電**：2022 年約 460 TWh → 2026 年 IEA 預估達 1,000 TWh
- **Google 溫室氣體排放**：比 2019 年高出 +48%
- **Microsoft 碳排放**：自 2020 年起增加 +29%

---

## 三、AI 投資的成本效益

### 市場現況
- API 費用 18 個月內降低約 99%（從 $60 → $0.15 / 百萬 tokens）；A16Z 記錄每年降 10 倍趨勢
- 企業 ROI：僅 **25%** 的企業有顯著回報（Capgemini 2024，調查 1,000+ 家企業）
- **Gartner 預測**：30% 的 PoC 專案最終會被放棄

### 批評聲音
- **Goldman Sachs 2024**《Gen AI: Too Much Spend, Too Little Benefit?》：質疑 1 兆美元投資能否回收
- **MIT Acemoglu (2024)**：考量實際成本後，AI 僅能自動化 4.6% 的任務，10 年 GDP 效益僅 +0.5%（遠低於樂觀預估的 7%）
- **OpenAI 2024**：預計年度虧損達 50 億美元，現行 API 低價由投資人資本補貼

---

## 四、Green AI 倡議者與解決方案

### 學術研究者

#### Roy Schwartz, Jesse Dodge, Noah A. Smith, Oren Etzioni (AI2)
- 論文：「Green AI」(2020, Communications of the ACM)
- https://www.researchgate.net/publication/335592175_Green_AI
- **核心主張**：
  - 定義「Red AI」= 以暴力算力追求 SOTA；「Green AI」= 以效率為優先
  - 要求 AI 論文在準確率之外，也報告效率指標（FLOPs、能耗）
  - 使用小型、任務專屬模型，而非大型通用模型

#### Carole-Jean Wu et al. (Meta AI)
- 論文：「Sustainable AI: Environmental Implications, Challenges, and Opportunities」(2022)
- https://arxiv.org/abs/2111.00364
- **核心建議**：
  - Right-size（模型規模配合任務需求）
  - 採用模型壓縮技術
  - 碳感知排程（Carbon-aware scheduling）
  - 強制要求 AI 模型的環境影響揭露

### 組織與計劃

#### Green Software Foundation (GSF)
- https://greensoftware.foundation/
- 成員：Microsoft、Google、Intel、Accenture 等
- **主要工具**：
  - Software Carbon Intensity (SCI) 規範：標準化碳排計量方式
  - Carbon Aware SDK（開源）：依電網碳強度排程工作負載
  - 整合 WattTime API 與 Electricity Maps 即時碳強度資料

#### Climate Change AI (CCAI)
- https://www.climatechange.ai/
- 非營利研究倡議組織
- 雙向使命：用 AI 解決氣候問題 + 讓 AI 本身更環保

#### MLCommons
- https://mlcommons.org/
- 成員：Google、Meta、Microsoft、NVIDIA 等
- MLPerf 基準測試現已納入**能源效率指標**

### 開源工具

#### CodeCarbon
- https://codecarbon.io/
- Python 套件，追蹤 ML 程式碼的碳排放（用電量 × 電網碳強度）
- 支援 Weights & Biases、MLflow 整合

#### Carbontracker（哥本哈根大學）
- https://github.com/lfwa/carbontracker
- 追蹤深度學習訓練的能耗與碳足跡

---

## 五、實用解決方案清單

| 方法 | 說明 | 量化效果 |
|------|------|----------|
| **使用更小的模型** | 依任務選用最小夠用的模型，不要預設用 GPT-4 | 每次查詢節省約 10 倍能耗 |
| **知識蒸餾（Distillation）** | 訓練小模型模仿大模型（如 DistilBERT） | 體積小 40%、速度快 60%、保留 97% 性能 |
| **量化（Quantization）** | 降低數值精度（FP32 → INT8） | 模型大小減少 4–8 倍 |
| **剪枝（Pruning）** | 移除冗餘神經連接 | 模型大小減少 4–8 倍 |
| **遷移學習（Transfer Learning）** | 微調預訓練模型，不從頭訓練 | 訓練時間減少 60–80% |
| **高效架構** | 使用 MobileNet、TinyBERT 等輕量架構 | MobileNet 參數量比 VGG-16 少 30 倍 |
| **碳感知排程** | 電網碳排最低時（夜間、風力充足時）才執行批次工作 | 電網碳強度依時間地點可差 2–10 倍 |
| **Right-sizing** | 複雜度配合任務，簡單任務用簡單模型 | 核心原則 |
| **測量碳足跡** | 在 ML 流程中整合 CodeCarbon 或 Carbontracker | 可見才可優化 |
| **報告效率指標** | 發表模型時同時報告能耗、FLOPs | 推動業界透明化 |

---

## 六、關鍵引言

> 「使用最小夠用的模型才是降低 AI 碳足跡最有效的方法。」
> — Lasse Nørfeldt，Dell Technologies 永續專家

> 「不要用大鐵錘當手術刀。」
> — VentureBeat AI Sustainability 報導

---

## 七、總結：個人使用者能做什麼？

1. **選模型**：簡單任務用 GPT-4o mini / Haiku / Flash，不要預設用最新最大的模型
2. **批次處理**：需要大量處理時，選在離峰時段（碳排較低）執行
3. **重複使用**：善用對話歷史，避免重複送出類似 prompt
4. **關注效率標章**：選擇有碳揭露、使用再生能源的 AI 服務商
5. **倡議**：要求 AI 公司公開環境影響報告（參考 Google、Microsoft 模式）

---

*資料來源整理自：arXiv、IEA 2024、Goldman Sachs 2024、Capgemini 2024、Gartner、MIT Acemoglu 2024、A16Z、Green Software Foundation、Wikipedia Green AI、Labellerr、VentureBeat、CrossML*
