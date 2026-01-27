# EBM Teaching Platform - Comprehensive Improvement Plan 2026

> **Document Purpose**: Consolidate improvement ideas and future development directions for the Evidence-Based Medicine educational platform.
>
> **Created**: 2026-01-26
> **Team**: 新竹台大分院教學部 | 謝慕揚 MD, PhD, FESC | 黃沛銓 MD | 黃國良

---

## Table of Contents

1. [Current Platform Status](#current-platform-status)
2. [Completed Features (2026)](#completed-features-2026)
3. [New Proposal: R Language Integration](#new-proposal-r-language-integration)
4. [Content Improvement Plan](#content-improvement-plan)
5. [Technical Enhancement Plan](#technical-enhancement-plan)
6. [User Experience Improvements](#user-experience-improvements)
7. [Implementation Priorities](#implementation-priorities)
8. [待辦事項：醫學資料庫介紹](#待辦事項醫學資料庫介紹)
9. [Discussion Notes](#discussion-notes)

---

## Current Platform Status

### Platform Overview

| Metric | Value |
|--------|-------|
| Total Modules | 24 (6 core + 18 JAMA) |
| Total Code Lines | ~28,000 lines HTML |
| Quiz Questions | 200+ questions |
| Badge System | 35+ achievements |
| Technology | React 18.2.0 (CDN), no build system |

### Existing Modules

**Core EBM Modules (6)**
- Critical Appraisal (文獻評讀基礎)
- Diagnostic Study (診斷研究評讀)
- Prognosis Study (預後研究評讀)
- RCT Appraisal (隨機對照試驗評讀)
- Systematic Review (統合分析評讀)
- Literature Search (文獻搜尋技巧) - with PICO tool

**JAMA Rational Clinical Examination (18)**
- ACS/Chest Pain, Syncope, Hypertension (Cardiology)
- Bacteremia, Fluid Responsiveness, Difficult Intubation (Critical Care)
- Delirium, Decision Capacity, Head Trauma (Neurology)
- Pleural Effusion, OSA (Pulmonology)
- Hip OA (MSK), LUTS/BOO (Urology)
- Ectopic Pregnancy (OB/GYN), Pediatric HTN (Pediatrics)
- Cirrhosis, GI Bleed, Wound Infection (Others)

**Coming Soon**
- Pulmonary Embolism (PE)
- Deep Vein Thrombosis (DVT)

### Strengths Assessment

| Area | Rating | Notes |
|------|--------|-------|
| Content Quality | ★★★★☆ | Evidence-based, JAMA-sourced |
| Gamification | ★★★★★ | 35+ badges, sophisticated logic |
| Progress Tracking | ★★★★☆ | localStorage-based, comprehensive |
| Mobile Support | ★★★☆☆ | Responsive but not optimized |
| Accessibility | ★★☆☆☆ | Needs ARIA, keyboard nav |
| Code Architecture | ★★★★☆ | Clean React patterns, some duplication |

---

## Completed Features (2026)

### January 2026 Accomplishments

| Date | Feature | Impact |
|------|---------|--------|
| 2026-01-11 | Literature Search + PICO Builder | High |
| 2026-01-17 | Delirium & Decision Capacity modules | Medium |
| 2026-01-17 | Cirrhosis & Wound Infection modules | Medium |
| 2026-01-18 | 35-badge gamification system | High |
| 2026-01-18 | Interactive case-based learning (ACS) | High |
| 2026-01-18 | Share button (QR, LINE, Email) | Medium |

---

## New Proposal: R Language Integration

### Overview

**Proposal**: Add educational content teaching learners how to use R for EBM statistical calculations.

**Rationale**:
- R is widely used in medical research and biostatistics
- Provides reproducible statistical analysis
- Empowers learners to go beyond calculators to understand underlying statistics
- Bridges gap between clinical knowledge and research methodology

### Scope Assessment

#### Option A: Minimal Integration (Recommended Start)
**Effort**: Low-Medium | **Impact**: Medium

Add a new module "EBM 統計實作：R 語言入門" with:
- Basic R syntax introduction
- Pre-written code snippets for common EBM calculations
- No interactive R environment (just educational content)

**Content Ideas**:
```r
# 範例：計算敏感度與特異度
sensitivity <- TP / (TP + FN)
specificity <- TN / (TN + FP)

# 範例：計算 Likelihood Ratio
LR_positive <- sensitivity / (1 - specificity)
LR_negative <- (1 - sensitivity) / specificity

# 範例：2x2 table analysis
library(epiR)
epi.tests(dat, conf.level = 0.95)
```

**Pros**:
- Simple to implement (just HTML content)
- No backend needed
- Users copy code to run locally

**Cons**:
- Users must have R installed
- No interactivity within the platform

---

#### Option B: Interactive R with WebR
**Effort**: High | **Impact**: High

Integrate [WebR](https://docs.r-wasm.org/webr/latest/) - R compiled to WebAssembly that runs in browser.

**Features**:
- Live R console in the browser
- Pre-loaded EBM datasets
- Interactive tutorials (run code, see results)
- No installation required

**Content Ideas**:
1. **Diagnostic Test Calculator**
   - Input raw 2x2 data → Calculate Se, Sp, PPV, NPV, LR+, LR-

2. **Meta-analysis Basics**
   - Pooled estimates with `meta` package
   - Forest plot generation

3. **Sample Size Calculation**
   - Power analysis for diagnostic studies

4. **ROC Curve Analysis**
   - AUC calculation
   - Optimal cutoff determination

**Technical Requirements**:
```html
<!-- WebR Integration Example -->
<script type="module">
  import { WebR } from 'https://webr.r-wasm.org/latest/webr.mjs';
  const webR = new WebR();
  await webR.init();

  // Run R code in browser
  const result = await webR.evalR('2 + 2');
  console.log(await result.toNumber()); // 4
</script>
```

**Pros**:
- Fully interactive
- No R installation needed
- Powerful learning experience

**Cons**:
- Initial load time (~20-50MB WebAssembly)
- Complex implementation
- May not work on all browsers/devices
- Maintenance overhead

---

#### Option C: Hybrid Approach
**Effort**: Medium | **Impact**: Medium-High

Create educational content with:
1. Static R code examples (copy-paste)
2. Link to pre-configured RStudio Cloud workspace
3. Downloadable R scripts

**Implementation**:
- Create `r-for-ebm.html` module
- Host R scripts in `/r-scripts/` folder
- Link to free RStudio Cloud/Posit Cloud workspace with pre-loaded packages

**Pros**:
- Balance of effort and functionality
- Users get real R experience
- No complex WebR integration

**Cons**:
- Requires external service (RStudio Cloud)
- Users need to create account

---

### Recommended R Integration Roadmap

| Phase | Content | Complexity |
|-------|---------|------------|
| Phase 1 | R 語言基礎介紹 + EBM 公式程式碼 | Low |
| Phase 2 | Downloadable R scripts for each JAMA module | Low |
| Phase 3 | Link to pre-configured RStudio Cloud workspace | Low |
| Phase 4 | (Optional) WebR integration for live code execution | High |

### Suggested Module Structure: R for EBM

```javascript
const lessons = [
    {
        id: 1,
        title: 'R 語言基礎',
        sub: 'Basic R Syntax for Medical Statistics',
        topics: ['變數與資料型態', '基本運算', '向量與矩陣', '安裝與載入套件']
    },
    {
        id: 2,
        title: '診斷研究統計',
        sub: 'Diagnostic Test Statistics in R',
        topics: ['2x2 表格建立', 'Se/Sp/PPV/NPV 計算', 'LR+/LR- 計算', '信賴區間']
    },
    {
        id: 3,
        title: '治療研究統計',
        sub: 'Treatment Effect Statistics',
        topics: ['RR/OR/ARR 計算', 'NNT/NNH 計算', '生存分析基礎', 'Kaplan-Meier']
    },
    {
        id: 4,
        title: '統合分析入門',
        sub: 'Introduction to Meta-analysis',
        topics: ['meta 套件使用', '效果量計算', '異質性檢驗', 'Forest plot']
    },
    {
        id: 5,
        title: '實戰應用',
        sub: 'Practical Applications',
        topics: ['完整案例分析', '報告撰寫', '資料視覺化', '可重現研究']
    }
];
```

### R Package Recommendations

| Purpose | Package | Notes |
|---------|---------|-------|
| Diagnostic tests | `epiR` | Se, Sp, LR, predictive values |
| Meta-analysis | `meta`, `metafor` | Forest plots, pooled estimates |
| ROC analysis | `pROC` | AUC, optimal cutoff |
| Sample size | `pwr`, `epiR` | Power calculations |
| Visualization | `ggplot2` | Publication-quality graphs |
| Survival | `survival`, `survminer` | Kaplan-Meier, Cox |
| Reporting | `rmarkdown`, `knitr` | Reproducible reports |

---

## Content Improvement Plan

### Priority 1: Complete Pending Modules

| Module | Status | Effort |
|--------|--------|--------|
| Pulmonary Embolism (PE) | Coming Soon | Medium |
| Deep Vein Thrombosis (DVT) | Coming Soon | Medium |

### Priority 2: High-Yield New Topics

| Topic | Category | Clinical Relevance |
|-------|----------|-------------------|
| Acute Kidney Injury | Nephrology | Very High |
| Heart Failure Assessment | Cardiology | Very High |
| Pneumonia Diagnosis | Pulmonology | High |
| Stroke/TIA Evaluation | Neurology | High |
| Appendicitis | Surgery/EM | High |
| Urinary Tract Infection | Infectious | Medium |

### Priority 3: Specialty Learning Tracks

Create guided learning paths:

1. **Internal Medicine Track**
   - Core EBM → Diagnostic Study → Relevant JAMA modules
   - Suggested order and prerequisites

2. **Emergency Medicine Track**
   - Focus: ACS, Syncope, PE, DVT, Head Trauma, GI Bleed

3. **Critical Care Track**
   - Focus: Bacteremia, Fluid Responsiveness, Difficult Intubation

4. **Primary Care Track**
   - Focus: Hypertension, OSA, LUTS, Hip OA

### Priority 4: Enhanced Case-Based Learning

Expand interactive cases (currently only in ACS module) to:
- [ ] Syncope case
- [ ] PE/DVT case
- [ ] Fluid responsiveness case
- [ ] Delirium case

---

## Technical Enhancement Plan

### Priority 1: Code Architecture

**Problem**: Badge definitions and progress tracking code duplicated in every module (~200 lines × 24 files).

**Solution**: Extract to shared JavaScript file.

```
/js/
  ├── badges.js          # Badge definitions
  ├── progress-tracker.js # localStorage API
  ├── category-modules.js # Module categorization
  └── utils.js           # Shared utilities
```

**Benefit**:
- Reduce total codebase by ~4,000 lines
- Easier maintenance
- Consistent behavior across modules

### Priority 2: Progressive Web App (PWA)

**Files to Add**:
- `manifest.json` - App metadata
- `sw.js` - Service worker for offline caching
- Icons (192x192, 512x512)

**Benefits**:
- Offline access after first load
- Install on home screen
- Push notifications for daily reminders

### Priority 3: Accessibility (a11y)

| Issue | Solution | Priority |
|-------|----------|----------|
| No keyboard navigation | Add keyboard shortcuts (N/P/Q) | High |
| Missing ARIA labels | Add to interactive elements | High |
| Color contrast | Verify WCAG 2.1 AA compliance | Medium |
| Focus indicators | Add visible focus styles | Medium |
| Screen reader | Test with NVDA/VoiceOver | Low |

### Priority 4: Performance

| Optimization | Impact |
|--------------|--------|
| Lazy load images | Faster initial load |
| Code splitting | Smaller bundle per page |
| Preload critical fonts | Prevent FOUT |
| Service worker caching | Instant repeat visits |

---

## User Experience Improvements

### Quick Wins (Low Effort)

- [ ] Dark mode toggle
- [ ] Font size adjustment (S/M/L)
- [ ] "Back to top" floating button
- [ ] Print-friendly CSS
- [ ] Keyboard shortcuts
- [ ] Loading state animations

### Medium Effort

- [ ] Bookmark/favorite modules
- [ ] Reading progress indicator
- [ ] Quiz shuffle mode
- [ ] Timed quiz option
- [ ] Notes & annotations

### Higher Effort

- [ ] Flashcard system with spaced repetition
- [ ] Mobile bottom navigation bar
- [ ] Swipe gestures for navigation
- [ ] Audio narration (Web Speech API)
- [ ] Video content integration

---

## Implementation Priorities

### Consolidated Priority Matrix

| Rank | Item | Effort | Impact | Category |
|------|------|--------|--------|----------|
| 1 | PE & DVT modules | Medium | High | Content |
| 2 | Code refactor (shared JS) | Medium | High | Technical |
| 3 | Dark mode | Low | Medium | UX |
| 4 | R for EBM (Phase 1) | Medium | Medium | Content |
| 5 | Keyboard shortcuts | Low | Medium | UX |
| 6 | PWA conversion | Medium | Medium | Technical |
| 7 | Expand case-based learning | High | High | Content |
| 8 | Flashcard system | High | Medium | Feature |
| 9 | R for EBM (Phase 2-3) | Medium | Medium | Content |
| 10 | WebR integration (Phase 4) | Very High | High | Feature |

### Suggested Development Phases

**Phase A: Foundation (1-2 months)**
- Complete PE & DVT modules
- Extract shared JavaScript
- Add dark mode
- Basic R for EBM content

**Phase B: Enhancement (2-3 months)**
- PWA conversion
- More JAMA modules (AKI, Heart Failure)
- R scripts for each module
- Quiz improvements

**Phase C: Advanced (3-6 months)**
- Flashcard system
- Mobile optimization
- RStudio Cloud integration
- Specialty learning tracks

**Phase D: Future (6+ months)**
- WebR live coding (if feasible)
- Video content
- Backend for cross-device sync
- Study group features

---

## 待辦事項：醫學資料庫介紹

> **建議來源**：黃國良 — 感謝他的寶貴建議！

### 目標

在網站內新增「醫學資料庫介紹」專區，幫助學員了解現代臨床決策支援工具。

---

### 資料庫 1：OpenEvidence

| 項目 | 內容 |
|------|------|
| **網站** | [openevidence.com](https://www.openevidence.com/) |
| **建置年份** | 2022 年（由 Daniel Nadler 創立，哈佛大學博士、Kensho 創辦人）|
| **總部** | 美國邁阿密 |

#### 設計理念

OpenEvidence 是一款專為醫師設計的 **AI 臨床決策輔助工具**（AI Copilot for Doctors）。其核心理念包括：

- **即時查證 (Point-of-Care)**：在臨床現場快速提供實證醫學答案
- **證據導向 (Evidence-Based)**：答案來源於經過驗證的醫學文獻
- **醫師專用**：僅供經過驗證的醫療專業人員使用
- **高可信度**：與 NEJM、JAMA Network、AMA 等權威機構合作

#### 如何使用

1. **註冊驗證**：以醫師身份註冊並通過驗證
2. **提問方式**：輸入臨床問題（如："What is the first-line treatment for community-acquired pneumonia?"）
3. **獲取答案**：AI 會根據最新實證文獻提供答案，並附上參考文獻來源
4. **臨床應用**：將答案整合至臨床決策過程中

#### 特色功能

- 自然語言問答介面
- 引用具體文獻來源
- 支援複雜臨床情境查詢
- 超過 40% 美國執業醫師使用

#### 參考資料

- [OpenEvidence 官網](https://www.openevidence.com/)
- [OpenEvidence - Wikipedia](https://en.wikipedia.org/wiki/OpenEvidence)
- [Contrary Research 報告](https://research.contrary.com/company/openevidence)

---

### 資料庫 2：UpToDate（含 UpToDate Expert AI）

| 項目 | 內容 |
|------|------|
| **網站** | [uptodate.com](https://www.uptodate.com/) |
| **建置年份** | 1992 年（由腎臟科醫師 Dr. Burton "Bud" Rose 創立）|
| **母公司** | Wolters Kluwer（2008 年收購）|

#### 設計理念

UpToDate 是全球最廣泛使用的 **實證醫學臨床決策支援系統**，其核心理念包括：

- **由醫師為醫師設計 (By Clinicians, For Clinicians)**：內容由超過 7,600 位醫學專家編撰
- **持續更新**：每日更新最新實證，幫助醫師保持知識同步
- **涵蓋全科**：超過 25 個專科領域的完整內容
- **30 年信譽**：自 1992 年以來持續服務全球臨床醫師

#### 如何使用

1. **訂閱存取**：透過醫院或個人訂閱取得帳號
2. **搜尋主題**：輸入疾病名稱、藥物或臨床問題
3. **閱讀專題**：瀏覽由專家撰寫的系統性回顧文章
4. **藥物查詢**：使用 Lexicomp 查詢藥物資訊
5. **計算工具**：使用內建醫學計算機

#### UpToDate Expert AI（2025 年新功能）

Wolters Kluwer 於 2025 年第四季推出 **UpToDate Expert AI**，結合生成式 AI 技術：

- **自然語言問答**：直接用自然語言提問，獲得結構化答案
- **Clinical Intelligence**：模擬專家臨床推理過程
- **多層驗證**：答案經過嚴格的驗證框架確保準確性
- **無縫整合**：與現有 UpToDate 內容完美整合

#### 參考資料

- [UpToDate 官網](https://www.wolterskluwer.com/en/solutions/uptodate)
- [Wolters Kluwer 30 週年公告](https://www.wolterskluwer.com/en/news/wolters-kluwer-celebrates-30-years-of-uptodate)
- [UpToDate Expert AI 發布](https://www.wolterskluwer.com/en/news/uptodate-expert-ai-genai-clinical-decision-support)

---

### 待辦清單

- [x] 建立 `database-guide.html` 頁面 ✅ (2026-01-27)
- [x] 加入 OpenEvidence 介紹與使用教學 ✅ (2026-01-27)
- [x] 加入 UpToDate 介紹與使用教學 ✅ (2026-01-27)
- [x] 製作比較表（功能、價格、適用情境）✅ (2026-01-27)
- [x] 新增至 `index.html` 導覽選單 ✅ (2026-01-27)
- [ ] 考慮加入其他資料庫（如 DynaMed、ClinicalKey）

---

## Discussion Notes

### R Language Integration - Key Questions

1. **Target Audience**
   - Residents who already use R?
   - Complete beginners to programming?
   - Both (with tiered content)?

2. **Learning Objectives**
   - Understand the math behind EBM statistics?
   - Actually perform analyses for research?
   - Both?

3. **Technical Comfort Level**
   - Is code-in-browser (WebR) valuable enough to justify complexity?
   - Or is "copy code to RStudio" sufficient?

4. **Maintenance Burden**
   - R packages update frequently
   - Who will maintain R code examples?

### Recommendations

**Start Small**: Begin with Option A (static R code examples) to gauge interest. If users engage, expand to Option C (hybrid with RStudio Cloud).

**Avoid Premature Optimization**: Don't build WebR integration until there's clear demand for in-browser R execution.

**Consider Alternatives**:
- Python (Jupyter notebooks via JupyterLite also runs in browser)
- Could offer both R and Python tracks

---

## Appendix: Resource Links

### R for Medical Statistics

- [epiR package documentation](https://cran.r-project.org/package=epiR)
- [meta package for meta-analysis](https://cran.r-project.org/package=meta)
- [WebR - R in the browser](https://docs.r-wasm.org/webr/latest/)
- [RStudio Cloud](https://posit.cloud/)

### EBM Resources

- [JAMA Rational Clinical Examination](https://jamanetwork.com/collections/6257/the-rational-clinical-examination)
- [CEBM Oxford](https://www.cebm.ox.ac.uk/)
- [Cochrane Handbook](https://training.cochrane.org/handbook)

### Technical References

- [PWA Documentation](https://web.dev/progressive-web-apps/)
- [WebR Documentation](https://docs.r-wasm.org/webr/latest/)
- [React 18 Documentation](https://react.dev/)

---

## Version History

| Date | Version | Changes |
|------|---------|---------|
| 2026-01-26 | 1.0 | Initial comprehensive plan created |
| 2026-01-27 | 1.1 | 新增「醫學資料庫介紹」待辦事項（OpenEvidence、UpToDate）— 感謝黃國良建議 |

---

*This document consolidates DEVELOPMENT-ROADMAP.md and IMPROVEMENTS.md with new R integration proposal.*
