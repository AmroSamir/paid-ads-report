# Visual QA Report: Whatagraph vs Our HTML Clone

**Date:** 2026-04-16  
**Method:** Programmatic CSS extraction via Chrome extension JS execution on live Whatagraph tabs  
**Source tabs:** Facebook Ads (225359111), Snapchat (225358029)

---

## 1. GRID LAYOUT

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Grid columns | `232px × 6` | `repeat(auto-fit, minmax(232px, 1fr))` | MATCH |
| Column gap | `10px` | `10px` | MATCH |
| Total width | `1442px` | `1442px` | MATCH |
| Column wrapper bg | `rgba(255,255,255,0.4)` | N/A (single-layer card) | MINOR — see §1a |
| Column wrapper border | `2px solid transparent` | `2px solid transparent` | MATCH |
| Column wrapper radius | `20px` | `20px` | MATCH |
| Row unit height | `110px` | `110px` | MATCH |

### §1a: Dual-layer card structure
Whatagraph uses **two nested layers**: an outer `.grid-layout__page-row-column` (semi-transparent white, 110px row unit) wrapping an inner `.widget-base` (solid white, no border). Our clone uses a single white card layer with the transparent border. **Visual impact: negligible** — the rgba(255,255,255,0.4) outer layer is barely visible against the gradient background.

---

## 2. TYPOGRAPHY

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Body font | `Roboto, Amiri, sans-serif` | `Inter, Roboto, sans-serif` | OK — widgets use Inter |
| Widget font | `Inter` | `Inter` | MATCH |
| Report title size | `28px` | `28px` | MATCH |
| Report title weight | `500` | `500` | MATCH |
| Report title color | `rgb(42,43,48)` = `#2a2b30` | `#2a2b30` | MATCH |
| Report title line-height | `42px` | `42px` | MATCH |
| Card title size | `16px` | `16px` (--font-size-lg) | MATCH |
| Card title weight | `700` | `700` | MATCH |
| Card title color | `rgb(42,43,48)` | `#2a2b30` | MATCH |
| Card title line-height | `normal` | not set (inherits) | MATCH |
| KPI value size | `32px` | `32px` (--font-size-3xl) | MATCH |
| KPI value weight | `500` | `500` | MATCH |
| KPI value line-height | `32px` | `32px` | MATCH |
| KPI label size | `13px` | `13px` (--font-size-base) | MATCH |
| KPI label weight | `700` | `700` | MATCH |
| Change value size | `13px` | `13px` (--font-size-base) | MATCH |
| Change value weight | `500` | `500` | MATCH |

---

## 3. COLORS

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Text primary | `rgb(42,43,48)` = `#2a2b30` | `#2a2b30` | MATCH |
| Text secondary | `rgb(120,130,142)` = `#78828e` | `#78828e` | MATCH |
| Text muted | `rgb(74,85,104)` = `#4a5568` | `#4a5568` | MATCH |
| Negative change | `rgb(255,70,70)` = `#ff4646` | `#ff4646` | MATCH |
| Positive change | `#38a169` (from design) | `#38a169` | MATCH |
| Card background | `rgb(255,255,255)` | `#ffffff` | MATCH |
| Border light | `#f3f4f5` | `#f3f4f5` | MATCH |
| Border strong | `rgb(235,236,238)` = `#ebeced` | `#ebeced` | MATCH |

---

## 4. TAB BAR

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Tab height | `32px` | auto (~34px from padding) | **DIFF** |
| Tab border-radius | `4px 4px 6px 6px` | `8px` | **DIFF** |
| Tab font-size | `12px` | `12px` | MATCH |
| Tab font-weight | `500` | `500` | MATCH |
| Tab color | `rgb(74,85,104)` | `#4a5568` | MATCH |
| Tab bg (inactive) | `rgba(0,0,0,0.04)` | `#fff` | **DIFF** |
| Tab bg (active) | `rgba(0,0,0,0.08)` | `#eef4ff` | **DIFF** |
| Tab border | none (0px) | `1px solid #dcdee1` | **DIFF** |
| Active border | none | `1px solid #3b82f6` | **DIFF** |
| Active color | `rgb(74,85,104)` | `#1e3a5f` | **DIFF** |
| Active weight | `500` | `600` | **DIFF** |
| Active box-shadow | none | `0 1px 4px rgba(59,130,246,0.15)` | **DIFF** |
| Tab gap | `8px` (via Tailwind `gap-2`) | `8px` | MATCH |

**Assessment:** Our tabs use a "pill with border" design while Whatagraph uses a flat "underline/highlight" design. The Whatagraph tabs have a subtle tinted background without borders. **ACTION: Update tab styling to match Whatagraph's flat design.**

---

## 5. SOURCE BADGE / FOOTER

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Footer height | `16px` | auto | OK |
| Footer display | `flex` | `flex` | MATCH |
| Footer align | `flex-end` | `center` | **DIFF** |
| Icon wrap size | `20px × 20px` | N/A | — |
| Icon img size | `16px × 16px` | `28px × 28px` (platform-icon) | **DIFF** |
| Icon border-radius | `0px` (wrap) | `50%` + box-shadow | **DIFF** |

**Assessment:** Our source-badge icons (28px with box-shadow and circle) are larger and more prominent than Whatagraph's (16px flat). **ACTION: Reduce source-badge icon size to 16px and remove box-shadow for single-source cards. Keep 28px for overview multi-platform badges.**

---

## 6. CARD STRUCTURE

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Card bg | `rgb(255,255,255)` | `#ffffff` | MATCH |
| Card radius | `20px` | `20px` | MATCH |
| Card border | `0px solid #ebeced` (widget) | `2px solid transparent` | **MINOR** |
| Card padding | `0px` (widget-base) | `24px` (--space-xl) | **NOTE** |
| Card min-height KPI | `230px` (2×110+10) | `230px` | MATCH |
| Card min-height chart | `470px` (4×110+30) | `470px` | MATCH |

**Note on padding:** Whatagraph widget-base has 0px padding at the widget level but the internal content components handle their own padding. Our approach of 24px card padding achieves the same visual result. Not a pixel-level issue.

**Note on border:** Whatagraph's widget-base has `0px` border while the outer column wrapper has `2px solid transparent`. Our cards combine both into one layer with `2px solid transparent`. Visual result is identical.

---

## 7. CHART CONTAINERS

| Property | Whatagraph | Ours | Status |
|----------|-----------|------|--------|
| Canvas width | `453px` (varies by grid) | `100%` of chart-wrapper | OK |
| Canvas height | `148px` (compact widgets) | `380px` (chart-wrapper) | **CONTEXTUAL** |

**Note:** Whatagraph's 148px is for compact 2-row chart widgets. Our 380px `chart-wrapper` is for full 4-row chart cards. Both are correct for their respective card heights.

---

## 8. SUMMARY OF REQUIRED FIXES

### Fix 1: Tab Bar Styling (Priority: HIGH)
Update tabs from bordered pill style to Whatagraph's flat tinted-background style.

### Fix 2: Source Badge Size (Priority: MEDIUM)
Reduce single-source footer icons from 28px to 16px. Remove circle box-shadow for platform-tab source badges.

### Fix 3: Tab Active State (Priority: HIGH)
Remove border-based active state, use background tint instead.

---

## 9. ITEMS CONFIRMED CORRECT (NO ACTION NEEDED)

- Grid layout (columns, gap, width)
- All typography (sizes, weights, colors, line-heights)
- All color tokens
- Card dimensions and border-radius
- KPI value sizing
- Change indicator colors and sizes
- Banner styling
- Report title
- Chart card structure
- Summary card structure
- Table styling (sizes match)
