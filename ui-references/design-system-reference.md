# Master UI Design Reference System
Compiled from 5 exhaustive source scans (224+ blocks, 3 site specs) | Jan 29, 2026

## Sources
- **Board 1:** https://www.are.na/yihui-h/ui-research-qyev-e16pwu — 108 blocks (UI theory, navigation, animation, spatial interfaces, game UI, chat patterns, knowledge tools)
- **Board 2:** https://www.are.na/frank-zvx_rhub2fk/ui-ux-uqgmlf-rw1i — 116 blocks (fintech dashboards, mobile apps, AI interfaces, component patterns, color palettes)
- **Site Spec 1:** https://ana.sh — Bento grid dashboard (Next.js + Tailwind + DaisyUI)
- **Site Spec 2:** https://ufotimeline.com — Dark timeline archive (Inter, opacity-based system)
- **Site Spec 3:** https://www.doingcoolstuff.xyz — Studio directory (PP Neue Montreal, warm + electric accent)

---

## 1. CORE DESIGN PRINCIPLES

### 1.1 UI Density
- **Formula:** UI Density = Value / (Time + Space) -- Matthew Strom
- **4 dimensions:** Visual density, Information density, Design density, Temporal density
- Dense layouts for data apps (Pro Trader). Spacious for consumer (Clean Minimal).
- Whitespace carries semantic meaning -- it is not wasted space.

### 1.2 Progressive Reduction
- UI simplifies as user gains expertise (LayerVault)
- Show fewer labels, tooltips, guides for returning users
- Reduce visual complexity over time
- Distinct from progressive disclosure: disclosure reveals on demand, reduction removes permanently based on mastery

### 1.3 Focus by Negation
- Dim/blur everything except the focus target (Kevin Powell CSS)
- Use opacity reduction + backdrop-blur to direct attention
- Apply to: modal overlays, onboarding highlights, active card expansion
- Siblings go to opacity 0.3-0.5, blur(4-8px)

### 1.4 Fluid Interfaces (WWDC18 / Apple)
- Responsive: react immediately to user input, no waiting for animation completion
- Redirectable: user can change direction mid-gesture
- Spring-based: physics simulations, not keyframe animations
- Gesture-driven: direct manipulation feels natural
- Interruptible: animations can be cancelled and redirected at any point

### 1.5 Pure UI
- UI = f(state) -- deterministic mapping from data to visual output (Guillermo Rauch)
- Given the same state, always render the same UI
- No side effects in render path
- State drives everything: loading, error, empty, populated, selected

### 1.6 Content-First Design (Facebook Paper)
- Chrome disappears, content fills the screen
- Gesture-driven navigation (swipe, pinch, tilt)
- Physics-based animations feel natural (Pop framework, spring animations)
- Full-bleed imagery, edge-to-edge content
- Navigation through content itself, not heavy nav bars

### 1.7 "Every Screen Should Be a Poster" (Persona 5)
- Game UI as art form -- treat every state as a design opportunity
- Bauhaus-inspired menus, bold composition
- Even loading screens and transitions deserve design attention
- "Juice" in product design: satisfying feedback, weight, physicality

### 1.8 Typography Hierarchy > Font Choice
- Size differentiation matters more than typeface variety (Frank Rausch / UIKonf)
- System fonts perform better on mobile
- Consistent vertical rhythm
- Max 2-3 fonts: display, body, mono
- Reading distance affects optimal font size

### 1.9 Spatial Interface Design
- Canvas-based UIs allow free-form arrangement (Cartographist, Semilattice, Kinopio)
- Spatial position carries meaning (proximity = relationship)
- Zoom levels reveal/hide detail (semantic zoom)
- Tools from the spatial software taxonomy: freeform canvases, node graphs, nested outlines

### 1.10 Cards as Journeys, Not Just Containers
- Each card tells a micro-story (Airbnb trips pattern)
- Ticker -> position -> progress -> outcome
- Self-contained narrative in every entry
- Mixed content types in grid (Polaroid photos + data widgets on ana.sh)

### 1.11 Celebration Moments
- Confetti, reveal animations, milestone badges for wins/streaks (Maybe Financial onboarding)
- Collectible welcome cards, leather/metal textures, gamification
- GitHub-style heatmaps for streak visualization
- Mad-libs style goal setting for engagement

### 1.12 Glassmorphism & Depth
- Semi-transparent backgrounds + backdrop-blur = layered depth (Granola AI)
- White/70-80% opacity cards with hairline border = glass effect
- Better than drop shadows for modern feel
- Creates visual hierarchy through transparency, not elevation
- Specific: rgba(255,255,255,0.8) + blur(12px) + saturate(1.5) from ana.sh

### 1.13 Micro-Interactions Are Mandatory
- Every hover, every tap needs a response (designspells.com)
- Satisfying feedback on completing actions (checkmarks, ripples)
- Easter eggs that add personality
- Time-of-day responsive UI (Poke app changes throughout day)
- Cursor-following hover effects (Luma buttons)
- Smooth sheet/modal transitions
- Pulsing animations for urgency states (iOS battery)
- Color-cycling animations (Google search caret)
- Dead UI feels broken.

### 1.14 iOS Navigation Patterns (Frank Rausch)
1. **Drill-Down:** hierarchical lists, horizontal animations indicate depth
2. **Flat:** tab bar (iPhone) / sidebar (iPad)
3. **Pyramid:** sibling navigation, horizontal swipe between peers
4. **Hub-and-Spoke:** return to hub to switch contexts
5. **High-Friction Modal:** requires explicit Done/Cancel to dismiss
6. **Low-Friction Modal:** swipe-down or tap-outside dismiss
7. **Non-Modal Overlays:** don't block interaction, may auto-dismiss
8. **State Change:** view variations without hierarchy change (toggle, segmented control)
9. **Step-by-Step:** linear wizard in modal overlay
10. **Content-Driven:** hyperlinks teleport user anywhere (web-style)

### 1.15 Chat & Messaging UI (Prabros)
- 10 chat ideas: time-shift (schedule sends), quick-stash (save for later), swipe triage (bulk manage)
- Adjacent Possible: push beyond standard UI kit
- Novel interface explorations for conversational design

### 1.16 Information Architecture
- Toast notifications deprecated by GitHub (Primer) -- use inline feedback instead
- Scroll landmarks: semantic scroll position indicators
- Loading psychology: animated progress reduces perceived wait by 11%
- Structural editing for writing/knowledge tools

---

## 2. COMPLETE COLOR SYSTEMS

### 2.1 ana.sh Gray Scale (Light Theme Foundation)
```
#FFFFFF  — card backgrounds
#F9FAFB  — page background
#F2F4F7  — secondary bg
#EAECF0  — borders, dividers
#D0D5DD  — disabled elements
#98A2B3  — muted text, card headers
#667085  — secondary text
#475467  — body text
#344054  — strong text
#182230  — near-black
#101828  — headings, maximum contrast
```
- Brand purple accent: **#7A5AF8**
- Card hover shadow: `0 4px 6px -1px rgba(62,28,150,0.05)`
- Container inset shadow: `inset 0 2px 4px rgba(62,28,150,0.05)`
- Dot pattern bg: `radial-gradient(#eaecf0 1.25px, transparent 1.25px)` at 20px spacing

### 2.2 ufotimeline.com Opacity System (Dark Theme Foundation)
Base: **#191a1e** with chalk texture overlay
All elements built from white at various opacities:
```
Text Opacity Scale:
1.0   — headings, maximum emphasis
0.95  — active nav items
0.85  — badges, important labels
0.70  — body text (DEFAULT)
0.60  — labels, captions
0.50  — secondary info
0.40  — tertiary info
0.30  — muted, de-emphasized
0.20  — year headers, barely visible

Background Opacity Scale:
0.15  — toggle track
0.10  — filter border
0.08  — pill backgrounds
0.06  — borders, timeline line
0.05  — header shadow
0.04  — hover background, footer
```

### 2.3 ufotimeline.com Category Colors
```
#febe02  — News / gold
#ea4c89  — Documentaries / pink
#4183c4  — Famous Cases / blue
#eb4823  — Sightings / red
#30a14e  — Books / green
#36bdaa  — Spotlight / teal
#b05bff  — Quotes / purple
```
**Usage pattern:** border-left 4px solid, pill border + tint at rgba(color,0.15), glow box-shadow 0 0 7px rgba(color,0.5), text color. **Never as full background fills.**

### 2.4 doingcoolstuff.xyz Palette (Warm + Electric)
```
--sand:       #fcf6ec  — page background
--dark-sand:  #e5ddce  — borders, dividers
--blue:       #283cff  — primary accent (electric)
--white:      #ffffff  — card backgrounds
--light-blue: #e0e8fb  — selected state bg
--mid-blue:   #99b2f2  — hover/secondary accent
--black:      #040f36  — text, headings
```
Card hover shadow: `0 4px 10px #dad0bf`

### 2.5 Named Palette Collection (from Board 2 analysis)

**Dark Fintech:**
```
#0B0E11  — background (near-black)
#00C853  — gains / green
#FF1744  — losses / red
#7A5AF8  — purple accent
#36bdaa  — teal accent
```

**Warm SaaS (Kinsta-inspired):**
```
#3C2415  — deep brown sidebar
#FDF6EE  — warm cream content area
#F57C00  — orange data accents
```

**Pastel Gradient:**
```
Iridescent cyan → pink → peach gradient
Glassmorphism cards over gradient
AI Stylist subscription app pattern
```

**Bold Monochromatic (Ekhi Solar):**
```
#F5C518  — bold yellow primary
#F57C00  — orange secondary
Editorial serif for data presentation
Progress bars as primary data display
```

**Earth Tones (Claude Code Wrapped):**
```
#C97B4B  — terracotta accent
Warm cream backgrounds
Monospace labels
GitHub contribution heatmap style
```

**Purple/Magenta (Habit Tracker):**
```
Violet gradient backgrounds
Magenta heatmap cells
Purple/magenta as engagement color
```

### 2.6 Semantic Color Badges (Sparkle UI Kit)
```
Purple  — info / informational
Blue    — settings / configuration
Green   — success / positive
Yellow  — warning / caution
Red     — error / negative / loss
```

### 2.7 Suggested Trading App Palette (doingcoolstuff.xyz adapted)
```
--bg:       #fcf6ec  — warm background (reduces eye strain for long sessions)
--text:     #283cff  — electric blue text/accent
--gain:     #00c853  — green for profit
--loss:     #ff1744  — red for loss
--neutral:  #e5ddce  — neutral/border
--selected: #e0e8fb  — selected state
```

---

## 3. TYPOGRAPHY

### 3.1 Font Recommendations
- **Display/Headings:** Playfair Display (serif, luxury), Agrandir (ana.sh original), PP Neue Montreal (doingcoolstuff.xyz, PangramPangram foundry)
- **Body/UI:** Inter (universal, Google Fonts, ufotimeline.com), Space Grotesk (geometric alternative)
- **Data/Code:** JetBrains Mono (monospace for numbers, code blocks)
- **Substitution rule:** For trading app, use Inter (free, excellent tabular figures) instead of Agrandir

### 3.2 Type Scale (ana.sh)
```
xs:   12px  — card headers, badges, timestamps
sm:   14px  — secondary text, labels
base: 16px  — body text
lg:   18px  — emphasized body
xl:   20px  — section headers
2xl:  24px  — page subtitles
3xl:  30px  — page titles
4xl:  36px  — hero display
```

### 3.3 doingcoolstuff.xyz Type System
```
heading-large:  42px / 42px line-height (1:1 ratio, very tight)
heading-medium: 32px
body-large:     16px / 22px line-height
body-small:     13px / 17px line-height
button-small:   11px / 13.5px, weight 500
button-large:   13px, uppercase, letter-spacing 0.5px
button-filter:  13px, uppercase
```

### 3.4 ufotimeline.com Type
```
Body:  15px, line-height 1.5em, font-weight 300 (light)
Title: 16px, font-weight 600
Pills: 11px, within rounded containers
```

### 3.5 Typography Rules
- Font-weight hierarchy: 300 (light body) → 400 (regular) → 500 (medium/labels) → 600 (semibold titles) → 700 (bold headings)
- Card headers: 12px, font-weight 500, muted color (#98A2B3)
- Monospace for all numerical data in trading context
- Tabular figures (font-variant-numeric: tabular-nums) for aligned number columns
- Max 2-3 font families per page

---

## 4. SPACING & LAYOUT

### 4.1 Spacing Scale (4px base)
```
xs:   4px
sm:   8px
md:   12px (tight grid gaps)
md+:  16px (standard padding)
lg:   20px
lg+:  24px
xl:   32px
2xl:  48px
3xl:  64px+
```
Never use arbitrary pixel values. Everything on the 4px grid.

### 4.2 Grid Systems

**ana.sh Bento Grid:**
- Responsive 3-5 columns
- Gap: 12px (md:gap-3 in Tailwind)
- Padding: 12px per card
- Cards span variable column/row counts
- Container: overflow hidden

**doingcoolstuff.xyz Studio Grid:**
- Flex-wrap layout
- Desktop: 4 columns (25%)
- Tablet: 3 columns
- Mobile: 1 column
- Horizontal padding: 12px per card
- Vertical margin: 30px between rows

**ufotimeline.com Single Column:**
- Max-width: 1024px, centered
- Single column feed
- Entries stacked vertically with border-bottom separators

### 4.3 Border Radius Scale
```
Sharp/Data:  2-4px   — Pro Trader, data tables, Luxury
Standard:    8-12px  — Light theme, general cards
Soft:        16px    — ana.sh cards (1rem), modern default
Pill:        24px+   — buttons, filter chips in Clean Minimal
Full pill:   1000px  — doingcoolstuff.xyz filter pills
Circle:      50%     — avatars, status dots, thumbnails
```

### 4.4 Breakpoints
```
Mobile:  < 640px   (1 column, full-screen nav)
Tablet:  640-1024px (2-3 columns)
Desktop: 1024px+    (3-5 columns, sidebar visible)
```

### 4.5 Container Patterns
- doingcoolstuff.xyz navbar: fixed, 64px height, 1px border bottom
- doingcoolstuff.xyz filter bar: sticky, top 64px, 80px height, overflow auto (horizontal scroll)
- ufotimeline.com scrolled header: pill nav, max-width 600px, border-radius 34px, backdrop-filter blur(4px)
- Hidden scrollbar for clean panel edges (all browsers: -webkit-scrollbar + scrollbar-width: none)

---

## 5. COMPONENT PATTERNS

### 5.1 Cards

**ana.sh Card:**
```css
background: #FFFFFF;
border: 1px solid #EAECF0;
border-radius: 1rem; /* 16px */
overflow: hidden;
/* hover: */
box-shadow: 0 4px 6px -1px rgba(62,28,150,0.05);
transform: scale(1.05);
transition: 150ms cubic-bezier(0.4, 0, 0.2, 1);
```

**ufotimeline.com Entry Card (Inset Glow Pattern):**
```css
background: transparent; /* NEVER solid bg */
border-bottom: 1px solid rgba(255,255,255,0.06);
/* hover: */
background: rgba(255,255,255,0.04);
padding-left: 14px; /* shift right on hover */
/* NO drop shadows -- only transparent + inset subtle edge light */
```

**doingcoolstuff.xyz Card:**
```css
border: 1px solid #e5ddce; /* --dark-sand */
border-radius: 4px;
/* hover: */
box-shadow: 0 4px 10px #dad0bf;
transition: all 0.2s;
```

**3D Card Tilt (ana.sh):**
- Parent container: `perspective: 800px`
- Card rotates on mouse move via JS
- Glassmorphism variant: `rgba(255,255,255,0.8) + blur(12px) + saturate(1.5)`

**Football Player Card Pattern:**
- Hero element centered with stats arranged around it
- Perfect for ticker/position cards: symbol centered, Greeks around edges

### 5.2 Buttons

**3-State Filter Toggle (doingcoolstuff.xyz):**
```
Default:  transparent bg, border visible
Hover:    white bg, border visible
Active:   --blue (#283cff) bg, white text
```
- border-radius: 1000px (full pill)
- padding: 6px 12px
- uppercase text
- font-size: 13px

**General Button Scale:**
- Small: 11px text, 6px 12px padding
- Medium: 13px text, 8px 16px padding
- Large: 16px text, 12px 24px padding
- Always pill radius for primary CTAs

### 5.3 Tags & Badges

**doingcoolstuff.xyz Tags:**
```css
border: 1px solid #283cff; /* --blue */
background: white;
border-radius: 20px;
padding: 6px 8px;
font-size: 11px;
```

**Sparkle UI Kit Semantic Badges:**
- Purple = info, Blue = settings, Green = success, Yellow = warning, Red = error
- Consistent across light and dark modes

**Tag Taxonomy Variants (Board 2):**
- User tags with avatars
- Status tags with semantic colors
- Country tags with flag icons
- Category tags with category icons

### 5.4 Filter Pills

**ufotimeline.com Category Pills:**
```css
font-size: 11px;
background: rgba(255,255,255,0.08);
border-radius: 12px;
border: 1px solid rgba(category-color, 0.15);
/* active: category color as text + stronger border */
```

**doingcoolstuff.xyz Filter Bar:**
- Sticky below navbar (top: 64px)
- Horizontal scroll, overflow auto
- Hidden scrollbar
- Pills: 1000px radius, uppercase, 3-state toggle

### 5.5 Tables

**Table Anatomy (Board 2 diagram):**
- Stub head (row label column)
- Spanner labels (column group headers)
- Row groups (visual grouping of related rows)
- Summary cells (totals, averages)
- Footnotes below table
- Alternating row backgrounds or hairline separators (not both)

### 5.6 Charts & Data Visualization

**Dashboard Patterns (Kinsta, Agrotech, Artemis):**
- Key metrics in top KPI cards with sparklines
- Charts below fold
- Before/after comparisons with AI insight badges
- Nested donut charts for composition
- Stacked area charts for time-series
- Multi-color vs monochrome as design choice

**Chart Specific:**
- Line charts with gradient fills (area under line)
- Minimal axis labels
- Touch-interactive data points
- Dark bg makes colored data pop
- P95/P99 percentile display with threshold sparklines
- Horizontal bar rankings for leaderboard/sector data
- Market flow histogram (OKX Trading)
- Sector category grid layout

**Mini Charts:**
- Sparklines in KPI cards (Artemis Terminal)
- Semi-circular gauges (Budget tracker)
- GitHub-style contribution heatmaps (Habit tracker, Claude Code Wrapped)
- Progress rings / fitness rings (ana.sh -> Portfolio rings)

### 5.7 Forms

**Form Variants (Board 2):**
- Email + button combo in 10 color themes
- Light/dark mode pairs for each variant
- Input: full-width, pill or rounded rectangle
- CTA button attached to input (inline) or below (stacked)

**Filter Modal (Board 2):**
- Chip selection for multi-select
- Color swatch pickers
- Dual-range slider for numeric ranges
- Glassmorphism backdrop

### 5.8 Navigation

**Tab Bar / Sidebar:**
- Mobile: bottom tab bar (iOS flat pattern)
- Tablet/Desktop: collapsible sidebar (dark sidebar + light content)
- Active state: filled icon + label, accent color

**Scrolled Header (ufotimeline.com):**
```css
max-width: 600px;
border-radius: 34px; /* pill */
backdrop-filter: blur(4px);
/* transforms from full-width to centered pill on scroll */
```

**Sticky Filter Bar (doingcoolstuff.xyz):**
```css
position: sticky;
top: 64px; /* below fixed navbar */
height: 80px;
overflow: auto; /* horizontal scroll */
```

### 5.9 Status Indicators

**Status Dots (ana.sh):**
- Green: pulsing (ping animation, 1s cycle) = online/active
- Gray: static = offline/inactive
- Red: pulsing = error/alert

**Timeline Dots (ufotimeline.com):**
- 16px outer circle + 6px inner dot
- Category-colored
- On vertical border-left 4px solid rgba(255,255,255,0.06)

### 5.10 Modals & Overlays

**High-Friction Modal:** requires explicit Done/Cancel, no tap-outside dismiss
**Low-Friction Modal:** swipe-down or tap-outside dismiss
**Non-Modal Overlays:** don't block interaction, may auto-dismiss (tooltips, toasts)
**Note:** GitHub deprecated toasts (Primer accessibility) -- prefer inline feedback

### 5.11 Chat / AI Interface Patterns

**From Board 2 AI comparison (9 apps):**
- Greeting styles vary: personal name, time-of-day, capability prompt
- Input designs: single line, expanding textarea, attached action chips
- Mode selection: tabs, dropdown, segmented control
- Prompt suggestions: cards, chips, categorized lists
- Code blocks with syntax highlighting + copy button
- Sidebar conversation history

---

## 6. ANIMATION & INTERACTION

### 6.1 Timing Scale
```
Instant:    < 100ms   — no animation, feel simultaneous
Quick:      150ms     — button clicks, toggles, state changes (ana.sh default)
Standard:   200ms     — card transitions, hover effects (doingcoolstuff.xyz, ufotimeline.com)
Smooth:     300ms     — modal open/close, theme toggle (ufotimeline.com toggle: 0.3s)
Luxurious:  500ms+    — only for luxury/elegant themes, editorial reveals
```

### 6.2 Easing Functions
```
Standard:      cubic-bezier(0.4, 0, 0.2, 1)  — ana.sh default, Material Design
Spring/Bouncy: cubic-bezier(0.34, 1.56, 0.64, 1) — overshoot, playful (Paper)
Ease-out:      ease-out — elegant/luxury, decelerating
Ease-out-quart: custom — doingcoolstuff.xyz nav easing
Linear:        linear — ONLY for looping animations (ticker tape, glow pulse, breathing)
```

### 6.3 Spring Physics (Facebook Paper / Pop Framework)
- Spring animations defined by tension + friction (not duration)
- Gestures drive animation state directly (velocity passed to spring)
- Interruptible: redirect mid-animation without jarring stops
- Use for: card throws, pull-to-refresh, swipe navigation, bouncy buttons
- CSS approximation: `cubic-bezier(0.34, 1.56, 0.64, 1)` for overshoot

### 6.4 Micro-Interaction Library

**Breathing Light (Apple):**
- Sinusoidal brightness cycle
- 4-second period
- For ambient indicators: charging, syncing, online status
- `animation: breathe 4s ease-in-out infinite`

**Card Hover (ufotimeline.com):**
- Background: transparent -> rgba(255,255,255,0.04)
- Padding shift: 0 -> padding-left 14px
- Thumbnail grows: 64px -> 74px
- Share icons grow on hover
- All transitions: 0.2s ease

**Card Hover (ana.sh):**
- Scale: 1.0 -> 1.05
- Shadow appears: 0 4px 6px -1px rgba(62,28,150,0.05)
- Transition: 150ms cubic-bezier(0.4, 0, 0.2, 1)

**Card Hover (doingcoolstuff.xyz):**
- Shadow appears: 0 4px 10px #dad0bf
- Transition: all 0.2s

**Button Press:**
- Scale: 1.0 -> 0.98 on :active
- Spring back to 1.0 on release

**Status Ping (ana.sh):**
```css
@keyframes ping {
  0% { transform: scale(1); opacity: 1; }
  75%, 100% { transform: scale(2); opacity: 0; }
}
animation: ping 1s cubic-bezier(0, 0, 0.2, 1) infinite;
```

**Focus Glow (cursor-following):**
- Radial gradient tracks mouse position on card
- `background: radial-gradient(circle at ${x}px ${y}px, rgba(accent,0.15), transparent 50%)`

**Scroll-Linked Animations:**
- Progress indicator tied to scroll position
- Parallax depth on scroll
- Header transforms on scroll (full -> pill in ufotimeline.com)

### 6.5 Transition Defaults
```css
/* ana.sh */
transition: all 150ms cubic-bezier(0.4, 0, 0.2, 1);

/* ufotimeline.com */
transition: all 0.2s ease;

/* doingcoolstuff.xyz */
transition: all 0.2s;
/* nav: ease-out-quart, 200ms */
```

---

## 7. LOADING STATES

### 7.1 Psychology of Waiting (Mercury/Facebook Research)
- Animated progress bars reduce perceived wait by **11%**
- Skeleton screens reduce perceived wait more than spinners
- Users prefer determinate progress (knowing how much is left)
- Backward-moving progress feels slower -- always move forward

### 7.2 Loading Decision Tree
```
< 1 second:     No indicator needed
1-3 seconds:    Skeleton screen (shimmer gradient animation)
3-10 seconds:   Indeterminate progress bar (animated)
10+ seconds:    Determinate progress with percentage
```

### 7.3 Skeleton Screen Pattern
- Placeholder shapes match final content layout
- Shimmer gradient animation sweeps left-to-right
- Gray rectangles for text lines, circles for avatars, rounded rects for cards
- Never use spinners for content loading

---

## 8. FINTECH / TRADING-SPECIFIC PATTERNS

### 8.1 Crypto Wallet (Solana - Board 2 Block 22)
- Dark mode mandatory for trading
- Purple CTAs (#7A5AF8)
- Red/green P&L coloring (semantic, universal)
- Token list with logos, scrollable
- Balance prominently displayed

### 8.2 Artemis Terminal (Board 2 Block 28)
- Deep dark navy background
- KPI cards with embedded sparklines
- Horizontal bar rankings (sector comparison)
- Multi-line time-series charts
- Dense information layout

### 8.3 OKX Trading (Board 2 Block 43)
- BTC dominance chart (donut/pie)
- Market flow histogram
- Whale trade real-time feed
- Sector category grid
- Economic calendar integration

### 8.4 Stonks Platform (Board 2 Block 103)
- Bid/auction UI with countdown timer
- Real-time activity feed
- Share slider (quantity selection)
- Ranked bidder list
- Bold colors on dark bg, playful-professional balance

### 8.5 Performance Metrics (Board 2 Block 66)
- P95/P99 percentile displays
- Threshold sparklines (inline mini charts)
- Error breakdown lists
- Color-coded severity levels

### 8.6 Trading Color Convention
```
Gain/Profit:    #00C853 (green)
Loss:           #FF1744 (red)
Neutral/Flat:   #98A2B3 (gray) or #e5ddce (warm neutral)
Active/Open:    #7A5AF8 (purple) or #36bdaa (teal)
Warning/DTE:    #febe02 (gold/amber)
```

### 8.7 Trading Data Display Rules
- Always use monospace/tabular figures for prices and quantities
- Right-align numerical columns
- Color-code P&L: green positive, red negative, gray zero
- Sparklines next to KPI numbers
- Countdown timers for expiration (DTE)
- Real-time activity feeds with timestamp + action + value
- Heatmaps for sector/position overview

---

## 9. SITE REFERENCE SPECIFICATIONS

### 9.1 ana.sh — Complete CSS Spec

**Stack:** Next.js + Tailwind CSS + DaisyUI
**Font:** Agrandir (substitute Inter for trading app)

**Page Background:**
```css
background-color: #f9fafb;
background-image: radial-gradient(#eaecf0 1.25px, transparent 1.25px);
background-size: 20px 20px;
```

**Gray Scale:** (see Section 2.1)

**Cards:**
```css
background: #FFFFFF;
border: 1px solid #EAECF0;
border-radius: 1rem; /* 16px */
overflow: hidden;
```

**Card Hover:**
```css
box-shadow: 0 4px 6px -1px rgba(62,28,150,0.05);
transform: scale(1.05);
transition: all 150ms cubic-bezier(0.4, 0, 0.2, 1);
```

**Container Shadow:**
```css
box-shadow: inset 0 2px 4px rgba(62,28,150,0.05);
```

**Card Headers:** 12px, font-weight 500, color #98A2B3

**Status Dots:**
- Green: pulsing (ping animation 1s)
- Gray: static offline

**Glassmorphism:**
```css
background: rgba(255,255,255,0.8);
backdrop-filter: blur(12px) saturate(1.5);
```

**3D Card Tilt:** perspective 800px on parent container

**Grid:** responsive 3-5 columns, gap 12px (md:gap-3), padding 12px

**Transitions:** `all 150ms cubic-bezier(0.4, 0, 0.2, 1)`

**Widget Mapping for Trading App:**
| ana.sh Widget | Trading App Equivalent |
|---|---|
| Weather | Market Status (open/closed/pre-market) |
| Fitness rings | Portfolio rings (profit / loss / theta) |
| Currently Listening | Current Position (active trade) |
| Status | Market open/closed indicator |
| Map | Sector heatmap |
| Blog | Trade journal entries |
| CatGPT | AI assistant / Groq chatbot |
| Photos | Chart screenshots |

### 9.2 ufotimeline.com — Complete CSS Spec

**Font:** Inter (Google Fonts)
**Dark Background:** #191a1e with chalk texture overlay

**Body Text:**
```css
font-size: 15px;
line-height: 1.5em;
font-weight: 300;
color: rgba(255,255,255,0.7); /* 0.7 opacity = default body */
```

**Text Opacity Scale:** (see Section 2.2)
**Background Opacity Scale:** (see Section 2.2)
**Category Colors:** (see Section 2.3)

**Category Color Usage Pattern:**
```css
/* Left border accent */
border-left: 4px solid var(--category-color);

/* Pill with tint */
background: rgba(var(--category-color-rgb), 0.15);
border: 1px solid rgba(var(--category-color-rgb), 0.3);

/* Glow effect */
box-shadow: 0 0 7px rgba(var(--category-color-rgb), 0.5);

/* Text */
color: var(--category-color);
```
**Key rule: Category color as accent, NEVER as full background fill.**

**Timeline:**
```css
border-left: 4px solid rgba(255,255,255,0.06);
/* Dots: */
.dot-outer { width: 16px; height: 16px; }
.dot-inner { width: 6px; height: 6px; }
```

**Entry Cards:**
```css
background: transparent;
border-bottom: 1px solid rgba(255,255,255,0.06);
transition: all 0.2s ease;
```

**Entry Hover:**
```css
background: rgba(255,255,255,0.04);
padding-left: 14px; /* shift right */
/* thumbnail: 64px -> 74px */
/* share icons grow */
```

**Title:** 16px, font-weight 600, color #fff

**Date Pills:**
```css
font-size: 11px;
background: rgba(255,255,255,0.08);
border-radius: 12px;
```

**Scrolled Header:**
```css
max-width: 600px;
border-radius: 34px;
backdrop-filter: blur(4px);
/* pill-shaped, centered */
```

**Max-width:** 1024px centered

**Theme Toggle:**
- localStorage persistence
- Track: 38x24px
- Transition: 0.3s

**Key Design Patterns:**
1. **Inset Glow Cards** -- never solid bg or drop shadows, only transparent + inset subtle edge light
2. **Category Color as Accent, Not Fill** -- colors in left borders, pill tints, text, never full backgrounds
3. **White at Various Opacities** -- everything from white at different opacity levels on dark
4. **Subtle Hover Shifts** -- bg transparent->0.04, padding shift, thumbnail grow, icon grow

### 9.3 doingcoolstuff.xyz — Complete CSS Spec

**Font:** PP Neue Montreal (PangramPangram foundry), weights 400/500

**Colors:** (see Section 2.4)

**Type Scale:** (see Section 3.3)

**Navbar:**
```css
position: fixed;
height: 64px;
border-bottom: 1px solid #e5ddce; /* --dark-sand */
```

**Filter Bar:**
```css
position: sticky;
top: 64px;
height: 80px;
overflow: auto; /* horizontal scroll */
```

**Filter Pills:**
```css
border-radius: 1000px;
padding: 6px 12px;
text-transform: uppercase;
font-size: 13px;
/* 3-state: */
/* default: transparent bg */
/* hover: white bg */
/* active: #283cff bg, white text */
```

**Studio Grid:**
```css
display: flex;
flex-wrap: wrap;
/* Desktop: 25% (4 columns) */
/* Tablet: 33.33% (3 columns) */
/* Mobile: 100% (1 column) */
padding: 0 12px; /* per card horizontal */
margin-bottom: 30px; /* per card vertical */
```

**Card Images:**
```css
border: 1px solid #e5ddce;
border-radius: 4px;
transition: all 0.2s;
/* hover: */
box-shadow: 0 4px 10px #dad0bf;
```

**Tags:**
```css
border: 1px solid #283cff; /* --blue */
background: white;
border-radius: 20px;
padding: 6px 8px;
font-size: 11px;
```

**Scrollbar:** completely hidden (all browsers)
```css
::-webkit-scrollbar { display: none; }
scrollbar-width: none; /* Firefox */
```

**Nav Easing:** ease-out-quart, 200ms

**Mobile Nav:** full-screen #283cff (blue) bg, #fcf6ec (cream) text, 42px nav links

**Content:** 1,051 studios catalogued across Brand, Digital, Motion categories

**Applicable Trading Patterns:**
- Warm bg (#fcf6ec) + electric accent (#283cff) reduces eye strain for long sessions
- Sticky filter bar for watchlist/screener filters
- Pill tag system for sector labels, alert badges, position status
- 4-column card grid with 12px gutters
- Hidden scrollbar for clean panel edges
- 3-state filter toggle (transparent/hover/active)

---

## 10. RESOURCE LINKS

### 10.1 Design Pattern Libraries
- https://www.designspells.com/ — Micro-interactions & magic details catalog
- http://mobbin.com — 300K+ mobile/web app screenshots
- https://www.buttons.cool/buttons — Button CSS examples
- https://www.doingcoolstuff.xyz/ — 1,051 design studios (Brand, Digital, Motion)
- https://handheld.design/ — Mobile design patterns
- https://imperavi.com/books/web-interface-handbook/ — UI fundamentals book

### 10.2 Tools & Platforms
- https://www.napkin.ai/ — Text-to-visual AI
- https://www.granola.ai/ — AI notepad with glassmorphic UI
- https://www.pampam.city/ — Custom interactive maps
- https://distill.id/ — Bookmark/idea playground
- https://observablehq.com/ — Data visualization notebooks
- https://untools.co/ — Thinking tools and mental models
- https://twenty.com/ — Open-source CRM (UI reference)
- https://app.artemisanalytics.com/ — Crypto analytics terminal
- https://8marketcap.com/ — Market cap ranking visualization
- https://origamiarchive.com/ — Origami prototyping archive

### 10.3 Design Theory & Learning
- https://matthewstrom.com/writing/ui-density/ — UI density principles (4 categories)
- https://frankrausch.com/ios-navigation — 10 iOS navigation patterns
- https://layervault.tumblr.com/post/42361566927/progressive-reduction — Progressive reduction
- https://blog.mercury.io/the-psychology-of-waiting-loading-animations-and-facebook/ — Loading psychology
- https://rauchg.com/2015/pure-ui — Pure UI essay (UI = f(state))
- https://darkblueheaven.com/spatialinterfaces/ — Spatial interfaces essay
- https://nightingaledvs.com/dark-sky-weather-data-viz/ — Data viz case study (Dark Sky)
- https://primer.style/accessibility/toasts/ — Why GitHub deprecated toasts
- https://tonsky.me/blog/tahoe-icons/ — Icon design principles
- https://avital.ca/notes/a-closer-look-at-apples-breathing-light.html — Breathing light animation analysis
- https://justfuckinguse.com/ — Opinionated tech recommendations

### 10.4 Interface Explorations & Research
- https://prabros.com/adjacent-possible/ — Novel interface explorations
- https://prabros.com/chat-ui-ideas/ — 10 chat UI ideas (time-shift, quick-stash, swipe triage)
- https://alexanderobenauer.com/labnotes/000/ — Future of personal computing
- https://szymonkaliski.com/projects/cartographist/ — Browser for rabbit-holing (spatial browsing)
- https://www.semilattice.xyz/ — PKM interface concepts
- https://notbor.ing/words/the-most-satisfying-checkbox — Game feel in product design ("juice")
- https://notbor.ing/words/paper-at-10 — Facebook Paper 10-year retrospective

### 10.5 Design Systems & Guidelines
- https://vercel.com/design/guidelines — Vercel web design guidelines
- https://about.instagram.com/blog/engineering/on-building-a-fluid-user-interface — Threads fluid UI (Instagram engineering)

### 10.6 Beau-Approved Site References (study for look & feel)
- **https://ana.sh/** — Bento Grid Dashboard (full spec in Section 9.1)
- **https://ufotimeline.com/** — Dark Timeline Archive (full spec in Section 9.2)
- **https://www.doingcoolstuff.xyz/** — Studio Directory (full spec in Section 9.3)

---

## 11. ICON LIBRARIES

24 icon libraries identified from Board 2 Icons channel:
- **Feather** — simple, clean, open-source (feathericons.com)
- **Phosphor** — flexible, 6 weights (phosphoricons.com)
- **Material Icons** — Google's system (fonts.google.com/icons)
- **Remix Icon** — open-source, neutral style (remixicon.com)
- **Tabler Icons** — 4,000+ SVG icons (tabler-icons.io)
- **Lordicon** — animated icons (lordicon.com)
- **Heroicons** — by Tailwind team (heroicons.com)
- **Lucide** — Feather fork, actively maintained (lucide.dev)
- **Ionicons** — Ionic framework icons (ionic.io/ionicons)
- **Bootstrap Icons** — 1,800+ icons (icons.getbootstrap.com)
- **Boxicons** — 1,500+ icons (boxicons.com)
- **Radix Icons** — minimal, 15x15 (icons.radix-ui.com)
- **Streamline** — 100K+ icons (streamlinehq.com)
- **Iconoir** — open-source, SVG (iconoir.com)
- **css.gg** — 700+ pure CSS icons (css.gg)
- **Coolicons** — 400+ free (coolicons.cool)
- **Akar Icons** — perfectly rounded (akaricons.com)
- **Eva Icons** — 480+ beautifully crafted (akveo.github.io/eva-icons)
- **Unicons** — 4,500+ icons (iconscout.com/unicons)
- **Simple Icons** — brand logos (simpleicons.org)
- **Flagpack** — country flags (flagpack.xyz)
- **Cryptocurrency Icons** — coin/token logos (cryptoicons.co)
- **Font Awesome** — the classic (fontawesome.com)
- **Majesticons** — 720+ icons (majesticons.com)

**Recommended for Trading App:**
- **Phosphor** (primary — flexible weights, clean)
- **Lucide** (alternative — Tailwind ecosystem)
- **Cryptocurrency Icons** (token logos)
- **Flagpack** (country/market flags)

---

## 12. TRADING APP THEME MAPPING (Market Elites)

### 12.1 Widget Mapping (ana.sh -> Market Elites)
| ana.sh Widget | Market Elites Feature |
|---|---|
| Weather | Market Status (open/closed/pre-market/after-hours) |
| Fitness rings | Portfolio rings (profit ring / loss ring / theta decay ring) |
| Currently Listening | Current Active Position |
| Status dot | Market open/closed indicator |
| Map | Sector heatmap (treemap visualization) |
| Blog | Trade journal |
| CatGPT | Groq AI assistant |
| Photos | Chart screenshots / trade setups |

### 12.2 Category Mapping (ufotimeline.com -> Market Elites)
| UFO Category | Trading Category | Color |
|---|---|---|
| News | Market News / Signals | #febe02 gold |
| Documentaries | Research / Analysis | #ea4c89 pink |
| Famous Cases | Notable Trades | #4183c4 blue |
| Sightings | New Opportunities | #eb4823 red |
| Books | Contracts / Documents | #30a14e green |
| Spotlight | Wheel Positions | #36bdaa teal |
| Quotes | P&L Entries | #b05bff purple |

### 12.3 Theme-Specific Application

**Pro Trader:**
- Dense layout (UI density article: maximize Value / (Time + Space))
- Dashboard patterns (Kinsta, Agrotech, Artemis Terminal)
- Monospace numbers, tabular figures
- Sparklines in KPI cards
- Dark Fintech palette (#0B0E11 bg)
- Minimal decoration, maximum data
- ufotimeline.com opacity system for text hierarchy

**Luxury Fintech:**
- Generous whitespace as luxury signal
- Glassmorphism depth (Granola / ana.sh)
- 300ms+ ease-out transitions
- Serif display font (Playfair Display), gold accents
- Warm SaaS palette (#FDF6EE cream)
- Breathing light animation for ambient status

**80s Retro:**
- Neon glow micro-interactions (designspells.com)
- Category glow pattern from ufotimeline.com (box-shadow 0 0 7px)
- Animated gradients, CRT/scanline overlays
- Bold display typography
- Spring physics for bouncy interactions

**Fun/Playful:**
- Bouncy spring animations (Facebook Paper physics, Pop framework)
- Onboarding celebrations (Maybe Financial: confetti, collectible cards)
- Blob shapes, tilted cards (3D tilt from ana.sh)
- Mad-libs goal setting, streak gamification
- Pastel gradient palette

**Clean Minimal:**
- Content-first (Facebook Paper: chrome disappears)
- System fonts, single accent color
- No shadows, separator lines only (ufotimeline.com hairline borders)
- doingcoolstuff.xyz warm bg + electric accent
- Hidden scrollbar, clean panel edges
- 3-state filter pills

**Light:**
- ana.sh gray scale (#F9FAFB bg, #EAECF0 borders)
- Dot pattern background
- White cards with subtle purple-tinted shadows
- 16px border radius, scale(1.05) hover
- Status dots with ping animation

**Dark:**
- ufotimeline.com system (#191a1e bg, white at opacity levels)
- Inset glow cards (no solid bg, no drop shadows)
- Category color as accent, not fill
- Chalk texture overlay
- Subtle hover shifts (bg 0->0.04, padding shift, thumbnail grow)

### 12.4 Cross-Theme Patterns (Apply Everywhere)
1. **Skeleton loading** for all data fetches (never spinners)
2. **Focus by negation** for modals and pickers
3. **Progressive reduction** for returning users
4. **Spring physics** for interactive elements (at minimum, button press feedback)
5. **Micro-interactions on every interactive element** (hover, press, focus)
6. **Monospace/tabular figures** for all numerical data
7. **Semantic P&L coloring** (green/red/gray)
8. **Inline feedback** instead of toasts (GitHub/Primer finding)
9. **Scroll landmarks** for long pages
10. **4px spacing grid** -- no arbitrary values

---

*This reference contains every hex code, pixel value, timing function, easing curve, and resource URL from 5 exhaustive scans of Beau's core UI research. It is the single source of truth for Market Elites design decisions.*

---

## Section 13: UI Effects Skill Base (70+ Techniques)
**Full catalog:** `C:\Users\Beau_\Documents\ui-effects-skill-base.md` (2,084 lines)
**Sources:** MagicUI, Hover.dev, Aceternity UI, Codrops, Godly.website, animations.dev

### Categories (all with implementable CSS/JS code):
1. **Cursor Effects** — Custom follower with lerp, spotlight/flashlight, magnetic attraction, trail/particles, following pointer
2. **Hover Effects** — 3D card tilt, glow border follow, slide highlight, lift+shadow, gradient border rotation, shimmer sweep, clip-path reveal, image zoom+overlay
3. **Scroll Animations** — Fade-up (IntersectionObserver), stagger children, parallax, sticky reveal, 3D container scroll, line progress, horizontal scroll, CSS scroll-driven
4. **Loading/Entrance** — Staggered entrance, skeleton loading, typewriter, word-by-word fade, counter roll-up, blur-to-sharp
5. **Micro-Interactions** — Click ripple, button press/squash, confetti burst, toggle switch, copy-to-clipboard feedback
6. **Text Effects** — Gradient text, scramble/decode, split character, underline draw, shiny text (MagicUI), line shadow
7. **Background Effects** — Gradient mesh, aurora/northern lights, dot grid/grid bg, noise/grain texture, beams, sparkles/star field, meteors, ripple circles
8. **Card Effects** — 3D flip, card stack, evervault encrypted, animated pin, glowing stars, bento grid
9. **Button Effects** — Magnetic, morphing shape, shimmer (MagicUI), wet paint (Hover.dev), rainbow border, background slide
10. **Data Visualization** — Animated counter with easing, progress ring, bar chart grow, sparkline draw
11. **Layout Animations** — Accordion (grid-template-rows), tab transitions, marquee/infinite scroll, masonry, carousel snap, modal/drawer, countdown flip
12. **Advanced** — Spring physics (stiffness/damping/mass), FLIP technique, View Transitions API, scroll-driven CSS, container queries, GPU acceleration, orbit, radar sweep, lamp effect

### Essential Reference Values:
- **Easings:** smooth-out `(0.23,1,0.32,1)`, spring `(0.34,1.56,0.64,1)`, elastic `(0.68,-0.55,0.265,1.55)`, snappy `(0.4,0,0.2,1)`
- **Timing:** micro 50-150ms, quick 200-300ms, standard 300-500ms, dramatic 500-800ms, ambient 1000ms+, stagger 50-100ms
- **Shadows:** 5 elevation levels from `0 1px 3px` to `0 25px 50px`
- **Blur:** subtle 4px, medium 8px, heavy 12-20px, glass 40-80px
