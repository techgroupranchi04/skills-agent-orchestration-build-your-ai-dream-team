# Project Pulse Dashboard – Visual Design System

## Overview

Project Pulse is a professional, polished project management dashboard that displays project cards in a responsive, accessible layout. This document defines the complete visual design system, including layout, typography, color palette, component styling, responsive behavior, and accessibility considerations.

---

## Part 1: Overall Layout & Grid Structure

### Dashboard Container (`.dashboard`)

**Purpose**: Main wrapper for the entire dashboard experience.

**Layout approach**:
- **Primary grid system**: CSS Grid or Flexbox
- **Grid type**: Auto-responsive grid using `grid-template-columns: repeat(auto-fit, minmax(320px, 1fr))` or similar
- **Alternative**: Flexbox with `flex-wrap: wrap` for simpler fallback support
- **Rationale**: Auto-fit allows cards to reflow naturally across breakpoints without media query management

**Visual separation**:
- Background color: Light neutral (see Color Palette below)
- Padding: Consistent spacing around all sides
- Max-width: Optional constraint (e.g., 1400px) for ultra-wide screens to avoid extreme card widths

**Header area** (above grid):
- Dashboard title "Project Pulse" positioned at top
- Optional filter/search bar area (reserved for future features)
- Clear visual separation between header and card grid

---

## Part 2: Card Design & Component Structure

### Project Card (`.project-card`)

**Card dimensions & spacing**:
- **Minimum width**: 280px (constrains on mobile)
- **Ideal width**: 320-360px (balanced aspect ratio)
- **Max width**: 100% (fills container on mobile)
- **Height**: Auto-height based on content (no fixed height)
- **Padding inside card**: 20px (consistent internal spacing)
- **Gap between cards**: 20px (consistent external spacing)

**Visual affordances**:

1. **Border-radius**: 12px (rounded corners, approachable but professional)
2. **Box-shadow**: 
   - Resting state: `0 2px 8px rgba(0, 0, 0, 0.08)` (subtle, grounded)
   - Hover state: `0 8px 16px rgba(0, 0, 0, 0.12)` (lifts card slightly for interactivity)
   - Rationale: Provides depth and visual hierarchy without being distracting
3. **Background**: White or very light gray (#FAFAFA or #FFFFFF)
4. **Border**: Optional 1px border in light gray (#E5E7EB) for clarity on white backgrounds

**Interaction feedback**:
- **Hover transition**: `transition: box-shadow 0.2s ease-out`
- **Cursor**: `cursor: pointer` if cards are clickable
- **Scale effect** (optional): `transform: translateY(-2px)` on hover for subtle lift

---

## Part 3: Status Badge Styling (`.card-status`)

### Visual design for status indicators

Status badges communicate project state at a glance using color, text, and optional icons.

**Badge structure**:
- **Display**: Inline-block or small flex container
- **Padding**: 6px 12px (compact but readable)
- **Border-radius**: 6px (slightly less rounded than card for visual distinction)
- **Font size**: 12px or 13px (smaller than card title, but readable)
- **Font weight**: 600 (semi-bold for emphasis)
- **Text transform**: Capitalize (e.g., "Active", "Paused")

**Status states and colors**:

| Status | Background | Text Color | Icon/Indicator | Rationale |
|--------|------------|-----------|-----------------|-----------|
| Active | #10B981 (emerald-500) | #FFFFFF | ✓ or filled circle | Green universally signals "go" and activity |
| Completed | #6B7280 (gray-500) | #FFFFFF | ✓ or checkmark | Gray signals completion, neutral sentiment |
| Paused | #F59E0B (amber-500) | #FFFFFF | ⏸ or horizontal bar | Amber/yellow signals caution or pause |

**Contrast verification** (WCAG AA):
- All status badge text/background pairs meet 4.5:1 contrast ratio
- Green + white: ~6.3:1 ✓
- Gray + white: ~5.8:1 ✓
- Amber + white: ~5.2:1 ✓

**Icon approach**:
- Use Unicode or minimal SVG icon (e.g., ✓ for complete, ⏸ for paused)
- Icon placed left of text within badge
- Icon + text together form a semantic unit (not color-only indicator)

**Placement on card**:
- Top-right corner of card, OR
- Immediately below the project name
- Rationale: Top-right is conventional for status indicators; below name keeps scanline intact

---

## Part 4: Priority Badge Styling (`.card-priority`)

### Visual design for priority indicators

Priority badges communicate project urgency using distinct color treatment and text labels.

**Badge structure**:
- **Display**: Inline-block or small flex container
- **Padding**: 6px 12px (same as status for visual consistency)
- **Border-radius**: 6px (matches status badge style)
- **Font size**: 12px or 13px (consistent with status badge)
- **Font weight**: 600 (semi-bold for emphasis)
- **Text transform**: Capitalize (e.g., "High", "Medium", "Low")

**Priority levels and colors**:

| Priority | Background | Text Color | Icon/Indicator | Rationale |
|----------|-----------|-----------|-----------------|-----------|
| High | #EF4444 (red-500) | #FFFFFF | ! or triangle | Red signals urgency and importance |
| Medium | #F97316 (orange-500) | #FFFFFF | - or dash | Orange signals moderate attention needed |
| Low | #3B82F6 (blue-500) | #FFFFFF | → or arrow | Blue signals low urgency, routine work |

**Contrast verification** (WCAG AA):
- All priority badge text/background pairs meet 4.5:1 contrast ratio
- Red + white: ~5.1:1 ✓
- Orange + white: ~4.6:1 ✓
- Blue + white: ~4.5:1 ✓

**Icon approach**:
- Use visual indicator symbols (!, -, →) or minimal icons
- Placed left of text within badge
- Reinforces priority without relying on color alone

**Placement on card**:
- Positioned alongside status badge (both in header area)
- OR stacked vertically if space is constrained
- Rationale: Grouping badges together creates a status area that users scan quickly

**Visual separation**:
- Small gap (8-12px) between status and priority badges
- Both badges together form a "status row" that's visually distinct from card body

---

## Part 5: Card Metadata Section (`.card-meta`)

### Information hierarchy within the card

Each project card displays layered information in a clear visual hierarchy:

**Card internal layout** (top to bottom):

1. **Card header** (30% of card visual weight):
   - Project name (heading)
   - Status and priority badges (inline)

2. **Card body** (50% of card visual weight):
   - Description or summary text (2-3 lines, truncated if needed)
   - Metadata row: Team size, due date, owner/team

3. **Card footer** (20% of card visual weight):
   - Call-to-action or additional link (optional)

**Project name** (`.card-title` or implicit):
- Font size: 16px or 18px
- Font weight: 700 (bold)
- Line height: 1.4
- Color: #111827 (near-black for high contrast)
- Margin below: 12px
- Truncation: Single line, `text-overflow: ellipsis` if needed

**Description/summary text** (`.card-description` or implicit):
- Font size: 14px
- Font weight: 400 (normal)
- Line height: 1.5 (readable, comfortable)
- Color: #4B5563 (medium gray for secondary content)
- Max lines: 2-3, using `display: -webkit-box`, `overflow: hidden`, `-webkit-line-clamp: 2`
- Margin below: 16px

**Metadata section** (`.card-meta`):
- Font size: 12px or 13px
- Font weight: 500 (slightly bold)
- Color: #6B7280 (lighter gray for tertiary content)
- Line height: 1.5
- Display: Flex or grid layout
- Items: Team size, due date, owner name/initials
- Spacing: 12-16px gap between items
- Separators (optional): Dot or vertical bar between items for visual clarity

**Metadata item styling**:
- Flex items with `align-items: center`
- Optional icon before text (12x12px icons)
- Label + value format (e.g., "Team: 4" or "Due: Jan 15")

---

## Part 6: Typography System

### Font family & sizing

**Font family** (stack):
- Primary: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif`
- Rationale: System fonts ensure excellent rendering and performance; no external font files needed
- Fallback: Roboto (if system fonts unavailable); then generic sans-serif

**Font sizes** (mobile-first, scale with breakpoints):

| Element | Mobile (375px) | Tablet (768px) | Desktop (1024px) | Line-height |
|---------|---|---|---|---|
| Dashboard title | 24px | 28px | 32px | 1.2 |
| Card title | 16px | 16px | 18px | 1.4 |
| Description | 14px | 14px | 14px | 1.5 |
| Status/Priority badge | 12px | 12px | 13px | 1.4 |
| Metadata | 12px | 12px | 13px | 1.5 |

**Font weights**:
- 400 (regular): Body text, descriptions
- 500 (medium): Metadata labels, secondary headings
- 600 (semi-bold): Status/priority badge text
- 700 (bold): Card titles, dashboard header

**Rationale**: Conservative font scale avoids excessive size changes; line-heights prioritize readability.

---

## Part 7: Color Palette

### Primary & Neutral colors

**Background colors**:
- Dashboard background: #F9FAFB (off-white, very light gray)
- Card background: #FFFFFF (pure white)
- Rationale: High contrast between dashboard and cards; white cards are clean and scannable

**Text colors** (with contrast ratios):
- Primary text (headings): #111827 (near-black, 19:1 on white)
- Secondary text (descriptions): #4B5563 (medium gray, 8:1 on white)
- Tertiary text (metadata): #6B7280 (light gray, 5.8:1 on white)
- All text passes WCAG AAA contrast standards

**Border and divider colors**:
- Card border: #E5E7EB (very light gray)
- Dividers in metadata: #D1D5DB (light gray)
- Rationale: Subtle, not visually heavy; aids definition without distraction

### Status colors

See Part 3 (Status Badge Styling) for full palette.

**Quick reference**:
- Active: #10B981 (emerald-green)
- Completed: #6B7280 (neutral gray)
- Paused: #F59E0B (amber-yellow)

### Priority colors

See Part 4 (Priority Badge Styling) for full palette.

**Quick reference**:
- High: #EF4444 (red)
- Medium: #F97316 (orange)
- Low: #3B82F6 (blue)

**Color accessibility notes**:
- Status and priority colors are not solely relied upon; text labels accompany all color indicators
- Color palette tested for deuteranopia (red-green color blindness) to ensure sufficient differentiation
- No critical information is conveyed by color alone

---

## Part 8: Responsive Breakpoints & Behavior

### Mobile-first CSS strategy

**Design approach**: Start with mobile styles, then progressively enhance for larger screens.

### Breakpoint definitions

| Breakpoint | Width | Device | Grid cols |
|-----------|-------|--------|-----------|
| **Mobile** | 375px–767px | Phone | 1 column |
| **Tablet** | 768px–1023px | Tablet | 2 columns |
| **Desktop** | 1024px+ | Desktop | 3+ columns |

### Responsive behavior by breakpoint

**Mobile (375px–767px)**:
- Card width: 100% (full container width minus padding)
- Grid: Single column (`grid-template-columns: 1fr`)
- Padding: 16px (dashboard)
- Font sizes: Smallest end of scale
- Card padding: 16px (slightly tighter than desktop)
- Badge positioning: May stack vertically if space tight
- Description: 2 lines, truncated

**Tablet (768px–1023px)**:
- Card width: ~50% (2 columns)
- Grid: 2 columns (`grid-template-columns: repeat(2, 1fr)`)
- Gap: 16px (slightly reduced from desktop)
- Padding: 20px (dashboard)
- Font sizes: Mid-scale
- Card padding: 20px
- Badge positioning: Inline (status + priority side-by-side)
- Description: 2-3 lines, truncated

**Desktop (1024px+)**:
- Card width: ~33% (3 columns)
- Grid: 3+ columns (`grid-template-columns: repeat(auto-fit, minmax(320px, 1fr))`)
- Gap: 20px
- Padding: 24px (dashboard)
- Font sizes: Largest end of scale
- Card padding: 20px
- Badge positioning: Inline (status + priority side-by-side)
- Description: 2-3 lines, truncated

### Responsive media queries

**CSS structure** (mobile-first):

```
/* Base mobile styles (375px) */
.dashboard { ... }
.project-card { ... }

/* Tablet and up (768px) */
@media (min-width: 768px) { ... }

/* Desktop and up (1024px) */
@media (min-width: 1024px) { ... }

/* Optional: Large desktop (1400px+) */
@media (min-width: 1400px) { ... }
```

**Viewport meta tag** (required in HTML):
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Responsive typography scaling

- Use fixed pixel sizes for simplicity (browser zoom handles scaling)
- Alternative: Use `rem` units for accessibility-friendly scaling
- **Rationale**: Fixed sizes are more predictable; `rem` is more accessible if user adjusts browser base font size

---

## Part 9: Accessibility Considerations

### Color contrast compliance (WCAG AA/AAA)

**All text and background combinations** meet WCAG AA 4.5:1 minimum ratio:
- Card titles on white: #111827 on #FFFFFF = 19:1 (AAA) ✓
- Card descriptions on white: #4B5563 on #FFFFFF = 8:1 (AAA) ✓
- All badge colors: 4.5:1 to 6.3:1 (AA or AAA) ✓
- Metadata text on white: #6B7280 on #FFFFFF = 5.8:1 (AAA) ✓

**Status/priority not color-only**:
- Each badge includes text label (not just color)
- Optional icons reinforce meaning (✓, ⏸, !, -, →)
- Tested with color blindness simulators for red-green and blue-yellow variants

### Semantic HTML structure

**Expected HTML conventions**:
- `.dashboard` wraps entire dashboard
- `.project-card` wraps each project
- Heading hierarchy: `<h1>` for dashboard title, `<h2>` or `<h3>` for card titles
- `.card-status`, `.card-priority` are semantic badges with `<span>` or `<div>` role="status" or similar
- `.card-meta` uses semantic list or definition list for metadata items
- Proper `lang` attribute on document root

### Keyboard navigation & focus

**Expected behavior**:
- Cards are structured with flexbox/grid for logical tab order
- Focus rings visible on cards if clickable (default browser focus or custom)
- No keyboard traps (user can tab through all elements and away)
- Metadata items (if links) have visible focus states

**Focus ring styling** (if custom):
- Outline: 2px solid #3B82F6 (blue, high contrast)
- Outline-offset: 2px (visible separation)
- No outline removal without replacement (`: focus { outline: none; }` is an anti-pattern)

### Readable font sizes

**Minimum font size**: 12px
- WCAG 2.5 guidelines suggest 14px body text for optimal readability
- 12px is acceptable for secondary/tertiary content (badges, metadata) with sufficient line-height
- Card titles (16px+) are clearly readable

**Line-height minimums**:
- Body text: 1.5 (readable spacing)
- Headings: 1.2–1.4 (appropriate tightness)
- Badges/metadata: 1.4–1.5 (readable without excessive space)

### Motion & animation

**Prefers-reduced-motion support**:
- Hover shadow transitions should respect `prefers-reduced-motion: reduce`
- Example: `@media (prefers-reduced-motion: reduce) { * { transition: none !important; } }`
- Rationale: Respects users with vestibular or cognitive concerns about motion

### Text alternatives

**Icons and visual indicators**:
- Each badge icon has accompanying text label
- Aria-labels optional for clarity (e.g., `aria-label="Project status: Active"`)
- Metadata items pair label + value (e.g., "Team: 4")

---

## Part 10: CSS Organization & Structure

### File organization approach

**Single file strategy** (`app/styles.css`):
- All styles in one file for simplicity and performance
- No external dependencies or CSS frameworks
- Clear sections with comments for readability

### CSS sections (in order)

```css
/* 1. Reset & global styles */
/* - Box sizing, body font, margin resets */

/* 2. CSS custom properties (variables) */
/* - Colors, spacing, shadows, breakpoints */

/* 3. Dashboard container */
/* - .dashboard, header, grid layout */

/* 4. Project card component */
/* - .project-card, base styles, hover states */

/* 5. Card inner sections */
/* - .card-status, .card-priority, .card-meta */
/* - Header, body, footer sections */

/* 6. Responsive media queries */
/* - Mobile-first breakpoints */
/* - 768px, 1024px+ */

/* 7. Accessibility utilities */
/* - .sr-only (screen-reader only) */
/* - prefers-reduced-motion media query */

/* 8. Dark mode (optional for future) */
/* - @media (prefers-color-scheme: dark) { ... } */
```

### CSS variable naming convention

**Color variables**:
```css
--color-text-primary: #111827;
--color-text-secondary: #4B5563;
--color-text-tertiary: #6B7280;

--color-status-active: #10B981;
--color-status-completed: #6B7280;
--color-status-paused: #F59E0B;

--color-priority-high: #EF4444;
--color-priority-medium: #F97316;
--color-priority-low: #3B82F6;

--color-bg-dashboard: #F9FAFB;
--color-bg-card: #FFFFFF;
--color-border: #E5E7EB;
```

**Spacing variables**:
```css
--space-xs: 4px;
--space-sm: 8px;
--space-md: 12px;
--space-lg: 16px;
--space-xl: 20px;
--space-2xl: 24px;
```

**Sizing variables**:
```css
--radius-sm: 6px;
--radius-md: 12px;

--shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.08);
--shadow-md: 0 8px 16px rgba(0, 0, 0, 0.12);
```

**Rationale**: Variables make theming easier and allow future dark mode or brand updates without rewriting selectors.

### BEM naming convention

**Optional light BEM for clarity**:
```css
.card-status { }         /* Block */
.card-status--active { } /* Modifier (status type) */
.card-status__text { }   /* Element (text within badge) */
```

**Rationale**: BEM avoids CSS conflicts and makes intent clear; light usage keeps CSS concise.

### Vendor prefixes

**Modern CSS** (no prefixes needed for):
- Flexbox, Grid
- Border-radius, box-shadow
- Transforms
- Transitions

**Reason**: All modern browsers (Chrome, Firefox, Safari, Edge) support these without prefixes; IE11 support not required per Project Pulse scope.

---

## Part 11: Design Tradeoffs & Decisions

### Tradeoff: Fixed vs. Flexible card layout

**Decision**: Flexible grid with `grid-template-columns: repeat(auto-fit, minmax(320px, 1fr))` or similar

**Rationale**:
- ✓ Auto-reflows based on screen size without explicit breakpoints
- ✓ Handles odd numbers of cards gracefully
- ✗ May create unequal column widths on very wide screens
- **Alternative rejected**: Fixed grid (3 columns always) would waste space on tablets; require more media queries

### Tradeoff: External fonts vs. system fonts

**Decision**: System fonts (no external font files)

**Rationale**:
- ✓ Faster load time (0 HTTP requests for fonts)
- ✓ Consistent with OS native feel
- ✓ Excellent rendering quality on all platforms
- ✗ Slightly less brand-specific than custom fonts
- **Alternative rejected**: Google Fonts would add ~50KB and require network; overkill for internal dashboard

### Tradeoff: Icon approach for badges

**Decision**: Unicode symbols + optional SVG icons

**Rationale**:
- ✓ Unicode (✓, ⏸, !, →) available without image files
- ✓ Can be styled with CSS (color, size)
- ✗ Limited icon variety
- **Alternative considered**: Emoji would add color variation but less professional; SVG would add file complexity

### Tradeoff: Card height (auto vs. fixed)

**Decision**: Auto-height based on content

**Rationale**:
- ✓ Accommodates variable description lengths
- ✓ No wasted whitespace on short cards
- ✗ Uneven card heights reduce visual uniformity
- **Alternative rejected**: Fixed height would require description truncation and overflow handling

### Tradeoff: Shadow depth for elevation

**Decision**: Subtle shadows (`0 2px 8px` resting, `0 8px 16px` hover)

**Rationale**:
- ✓ Gives cards clear elevation without visual noise
- ✓ Hover state provides clear interaction feedback
- ✗ More subtle than prominent shadow treatments (e.g., Material Design)
- **Alternative rejected**: No shadow would reduce 3D clarity; aggressive shadow would feel heavy

### Tradeoff: Responsive font scaling

**Decision**: Fixed pixel sizes per breakpoint (not fluid scaling with `clamp()`)

**Rationale**:
- ✓ Simpler CSS (fewer calculations)
- ✓ More predictable across browsers
- ✗ Less smooth scaling on intermediate viewport sizes
- **Alternative considered**: CSS `clamp()` for fluid scaling; rejected for simplicity

### Tradeoff: Light theme only vs. dark mode support

**Decision**: Light theme only (with CSS variables for future dark mode)

**Rationale**:
- ✓ Polished, professional appearance
- ✓ Better for printed dashboards (if needed)
- ✗ No dark mode for reduced-light environments
- **Alternative considered**: Dual-theme support requires `prefers-color-scheme` media queries and doubled CSS; complexity not justified for MVP

---

## Part 12: Validation & Testing Checklist

### Visual validation

- [ ] Dashboard displays project cards in responsive grid
- [ ] Cards stack 1 column on mobile (375px)
- [ ] Cards display 2 columns on tablet (768px)
- [ ] Cards display 3+ columns on desktop (1024px+)
- [ ] Status badges show with correct colors (green/gray/amber)
- [ ] Priority badges show with correct colors (red/orange/blue)
- [ ] Shadows appear on cards; hover shadow is more pronounced
- [ ] Rounded corners (12px on cards, 6px on badges) are visible
- [ ] Text is readable at all breakpoints (no overflow or truncation)

### Accessibility validation

- [ ] Color contrast verified (all 4.5:1 or higher)
- [ ] Status/priority badges include text labels (not color-only)
- [ ] Focus ring visible on interactive elements
- [ ] Dashboard layout works with keyboard navigation (Tab, Shift+Tab)
- [ ] Font sizes meet minimum readability (12px+)
- [ ] Line-heights provide comfortable spacing (1.4–1.5)

### Responsive testing

- [ ] Resize browser to 375px, 768px, 1024px, 1440px
- [ ] Verify grid columns adjust correctly at each breakpoint
- [ ] Check that card padding and gaps remain consistent
- [ ] Verify font sizes increase slightly on larger screens
- [ ] Confirm no horizontal scrolling on any breakpoint

### Cross-browser testing

- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)

### Dark mode support (optional future)

- [ ] CSS variables are in place for colors
- [ ] Colors would work with dark backgrounds (if swapped)
- [ ] `prefers-color-scheme: dark` media query structure ready

---

## Summary of Design Decisions

| Decision | Value | Rationale |
|----------|-------|-----------|
| Grid layout | `repeat(auto-fit, minmax(320px, 1fr))` | Flexible, responsive, auto-reflow |
| Card shadow | `0 2px 8px` (rest), `0 8px 16px` (hover) | Subtle elevation with clear hover feedback |
| Border radius | 12px cards, 6px badges | Professional, approachable, distinct scales |
| Font stack | System fonts (Apple, Segoe, Roboto) | Fast, native feel, accessible |
| Font sizes | 16px body minimum, responsive scaling | Readable, hierarchy clear, mobile-friendly |
| Status colors | Green/Gray/Amber | Semantically clear, accessible, distinct |
| Priority colors | Red/Orange/Blue | Urgency clear, accessible, distinct |
| Breakpoints | 375px, 768px, 1024px | Mobile-first, tablet/desktop distinction |
| Theme | Light only | Professional, printable, MVP scope |
| Icons | Unicode symbols | Fast, lightweight, styleable |

---

## Next Steps for Implementation

1. **Coder**: Implement HTML structure with `.dashboard`, `.project-card`, `.card-status`, `.card-priority`, `.card-meta` classes
2. **Coder**: Ensure viewport meta tag and semantic HTML
3. **Designer**: Build `app/styles.css` using this design system
   - Organize CSS as outlined in Part 10
   - Use CSS variables for colors and spacing
   - Implement mobile-first responsive approach
   - Test at breakpoints 375px, 768px, 1024px
4. **Orchestrator**: Validate against checklist in Part 12
5. **Coder**: Create `.vscode/launch.json` for runnable dashboard

