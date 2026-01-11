# EBM Educational Site - Development Roadmap

This document outlines future development suggestions for enhancing the Evidence-Based Medicine educational platform.

---

## Completed Features

### Literature Search Training (Completed 2026-01-11)
- [x] Guide learners through PubMed/Cochrane search strategies
- [x] PICO question builder tool that generates search terms
- [x] 8 clinical templates by specialty
- [x] Direct links to open PubMed/Cochrane with generated search
- [x] 5 lessons covering PICO, Boolean operators, MeSH, Cochrane, advanced tips
- [x] 10-question quiz with explanations

**File:** `literature-search.html`

---

## Content Enhancements

### 1. Case-Based Learning Modules
- [ ] Add real clinical scenarios where learners apply EBM concepts
- [ ] Example: "A 55-year-old male presents with chest pain... calculate post-test probability"
- [ ] Walk through the 5A's of EBM: Ask, Acquire, Appraise, Apply, Assess

### 2. Interactive Calculators
- [ ] LR+/LR- calculator
- [ ] Pre/post-test probability calculator (Fagan nomogram)
- [ ] NNT/NNH calculator
- [ ] 2x2 table builder (sensitivity/specificity from raw data)
- [ ] Let users input their own values and see results dynamically

---

## Technical Features

### 3. Progress Tracking
- [ ] Use localStorage to save quiz scores and completed modules
- [ ] Show a dashboard of learner progress across all modules
- [ ] Badge/certificate system for completing module sets

### 4. Spaced Repetition Review
- [ ] Flashcard system for key concepts (diagnostic criteria, LR values)
- [ ] Schedule review reminders based on forgetting curves

### 5. Mobile App (PWA)
- [ ] Convert to Progressive Web App for offline access
- [ ] Add `manifest.json` and service worker for installability
- [ ] Test on mobile devices during clinical rotations

---

## Pedagogical Improvements

### 6. Difficulty Levels
- [ ] **Beginner**: Concepts and definitions
- [ ] **Intermediate**: Applying formulas
- [ ] **Advanced**: Critical appraisal of real papers

### 7. Journal Club Module
- [ ] Template for structured paper critique
- [ ] Checklist tools:
  - [ ] CONSORT for RCTs
  - [ ] PRISMA for systematic reviews
  - [ ] STARD for diagnostic studies

### 8. Quick Reference Cards
- [ ] Downloadable/printable summaries for each JAMA Rational Exam topic
- [ ] Pocket cards with key LR values for bedside use

---

## Community Features

### 9. Question Bank Expansion
- [ ] Allow faculty to contribute questions
- [ ] Tag questions by specialty (內科、外科、急診、兒科、etc.)
- [ ] Export/import question sets

---

## Priority Suggestions (Next Steps)

Recommended order based on educational value and effort:

| Priority | Feature | Effort | Value |
|----------|---------|--------|-------|
| 1 | Interactive Calculators | Medium | High |
| 2 | Progress Tracking (localStorage) | Low | High |
| 3 | Case-Based Learning | High | High |
| 4 | PWA Conversion | Medium | Medium |
| 5 | Journal Club Module | Medium | Medium |

---

## Changelog

| Date | Feature | Status |
|------|---------|--------|
| 2026-01-11 | Literature Search Training with PICO Builder | Completed |
| 2026-01-07 | Initial roadmap created | - |

---

*Last Updated: 2026-01-11*
*For: 新竹台大分院 EBM Education Platform*
