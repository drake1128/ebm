# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a web-based educational platform for Evidence-Based Medicine (EBM) teaching at National Taiwan University's Hsinchu Hospital (新竹台大分院). All content is in Traditional Chinese (zh-TW).

## Technology Stack

- **No build system** - Static HTML files that run directly in browsers
- **React 18.2.0** via CDN (not npm/webpack)
- **Babel Standalone 7.23.5** for browser-based JSX transpilation
- **Google Fonts**: Noto Sans TC, Playfair Display, Source Sans Pro, Crimson Pro

## Development

**No build commands needed.** Simply edit HTML files and open them in a browser or deploy to any static web server.

To test locally, open any HTML file directly in a browser or use a simple HTTP server:
```bash
python -m http.server 8000
# or
npx serve
```

## Architecture

Each HTML file is a self-contained single-page application:
- `index.html` - Main landing page with navigation to all modules
- `*.html` - Individual educational modules (15 total)

### Module Structure

Every module file follows this pattern:
1. **Header**: Navigation with back button
2. **Hero Section**: Gradient background with module title
3. **Lesson Navigation**: Tabs for different topics within the module
4. **Content Areas**: Interactive cards with learning materials
5. **Quiz Section**: Multiple-choice questions with score tracking
6. **Footer**: Team information

### Data Patterns

Lessons array:
```javascript
const lessons = [
    {id: 1, title: '標題', sub: '副標題', color: '#0077B6', sections: [...]}
];
```

Quiz array:
```javascript
const quiz = [
    {q: '問題', o: ['選項1', '選項2', '選項3', '選項4'], c: 0, e: '解釋'}
    // c = correct answer index (0-based), e = explanation
];
```

### Styling Conventions

- Inline styles with template literals
- Color themes per module (primary: #0077B6, varies by module)
- Gradient backgrounds: `linear-gradient(135deg, color1, color2)`
- Callout boxes use semantic colors: tips (blue), good (green), info (teal), warning (orange), error (red)

## Content Guidelines

- All text must remain in Traditional Chinese (zh-TW)
- Medical content follows JAMA Rational Clinical Examination format where applicable
- Maintain accuracy of clinical formulas and diagnostic criteria
- Quiz explanations should be educational and evidence-based

---

## JAMA Rational Clinical Examination PDF Conversion Workflow

When a new PDF file is added to this folder, follow this workflow:

### Step 1: Identify JAMA Rational Clinical Exam PDF

Check if the PDF is from JAMA Rational Clinical Examination series by looking for:
- Title format: "Does This Patient Have [Condition]?" or similar clinical question
- JAMA journal citation
- "The Rational Clinical Examination" series header
- Content including sensitivity, specificity, likelihood ratios (LR+/LR-)

If the PDF is NOT from JAMA Rational Clinical Examination, skip this workflow.

### Step 2: Extract Key Information from PDF

Extract the following from the PDF:
1. **Clinical Question** - The main diagnostic question (e.g., "Does This Patient Have ACS?")
2. **Chinese Title** - Translate the topic to Traditional Chinese
3. **Citation** - Author(s), JAMA year, volume, pages
4. **JAMA Article URL** - Find the online link (format: `https://jamanetwork.com/journals/jama/fullarticle/[ARTICLE_ID]`)
5. **Key Clinical Findings** with LR+ and LR- values
6. **Risk Scores/Decision Rules** if applicable
7. **Clinical Cases** for application examples

### Step 3: Create HTML Educational Module

Create a new file named `jama-[topic-slug].html` following the existing template pattern:

```javascript
// Required Structure:
const lessons = [
    { id: 1, title: '[Chinese Title]', sub: '[English Subtitle]', color: '#XXXXXX' },
    // ... 4-5 lessons covering:
    // - Overview/Definition
    // - Risk Factors/Symptoms with LR values
    // - Physical Exam/Diagnostic Tests
    // - Clinical Decision Rules/Scores
    // - Clinical Application Cases
];

const quiz = [
    {
        q: '[Question in Chinese]',
        o: ['Option 1', 'Option 2', 'Option 3', 'Option 4'],
        c: 0,  // correct answer index (0-based)
        e: '[Explanation with evidence from the article]'
    },
    // ... 10 quiz questions covering key concepts
];
```

### Required HTML Module Components:

1. **Header** - Navigation back to `jama-rational-exam.html`
2. **Hero Section** with:
   - JAMA Rational Clinical Examination badge
   - English question title (e.g., "Does This Patient Have ACS?")
   - Chinese subtitle
   - Citation (Author et al. JAMA Year;Vol:Pages)
   - Link to original article: `閱讀原文 Read Full Article`
3. **Learning Objectives** - 4 key objectives in Chinese
4. **Lesson Content** - Evidence-based content with:
   - Tables showing LR+, LR-, sensitivity, specificity
   - Clinical decision rules/scores
   - `.tip`, `.good`, `.danger`, `.info` callout boxes
   - `.formula` boxes for key equations
5. **Quiz Section** - 10 multiple-choice questions with explanations
6. **Footer** - Team: 新竹台大分院教學部 | 謝慕揚 MD, PhD, FESC | 黃沛銓 MD | 黃國良

### Color Theme Selection:

Choose a unique color theme based on category:
- Cardiology: Red tones (`#C62828`, `#AD1457`)
- Critical Care: Blue tones (`#1565C0`, `#0277BD`)
- Neurology: Blue/Purple (`#1E88E5`, `#5E35B1`)
- Pulmonology: Teal/Cyan (`#00838F`, `#00695C`)
- Musculoskeletal: Brown (`#6D4C41`, `#795548`)
- Pediatric: Green (`#5B8C5A`, `#2E7D32`)

### Step 4: Update jama-rational-exam.html

After creating the new module, update the `modules` array in `jama-rational-exam.html`:

```javascript
// Add to modules array (around line 42-53):
{
    id: '[topic-slug]',
    title: '[Chinese Title]',
    titleEn: '[English Title - the clinical question]',
    href: 'jama-[topic-slug].html',
    icon: '[Emoji]',
    color: '#XXXXXX',
    colorBg: '#XXXXXX',  // Lighter version
    year: XXXX,
    citation: '[Author] et al. JAMA YYYY;Vol:Pages',
    category: '[cardio|critical|neuro|pulm|msk|pediatric]',
    keywords: ['keyword1', 'keyword2', ...],
    isNew: true,
    status: 'online'
}
```

**Important**:
- Set `isNew: true` for newly created modules
- Update existing `isNew: true` modules to `isNew: false` if appropriate
- If replacing a "coming soon" placeholder, change `status: 'coming'` to `status: 'online'`

### Step 5: Verification Checklist

Before completion, verify:
- [ ] HTML file opens correctly in browser
- [ ] All lessons display properly
- [ ] Quiz functions correctly (scoring, explanations)
- [ ] Link to original JAMA article works
- [ ] Back button navigates to jama-rational-exam.html
- [ ] New module appears in jama-rational-exam.html with correct filtering
- [ ] Search finds the module by keywords

### Example File Reference

Use `jama-chest-pain-acs.html` as the primary template reference for:
- Complete HTML structure
- React component patterns
- Styling conventions
- Quiz implementation
- Lesson content organization
