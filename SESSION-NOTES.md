# Market Elites - Session Notes (Feb 8, 2026)

## How to Pick Up Where We Left Off

Open Claude Code and say:
```
I'm continuing work on the Market Elites wheel platform at C:\Users\Beau_\Documents\wheel
Read SESSION-NOTES.md in that directory for full context on what we've done and what's next.
```

## Repo Info
- **Repo:** github.com/elitesbeau/elitesbeau.github.io (renamed from "wheel")
- **Branch:** `main` (GitHub Pages auto-deploys from main)
- **Live site:** https://elitesbeau.github.io
- **Single-file app:** `index.html` (~9,000+ lines)
- **Local dir:** `C:\Users\Beau_\Documents\wheel` (folder name unchanged)

## What Was Done Feb 8 (Session 2 — Latest)

### Firebase Delete Bug Fix (commit c6424b1)
- **Root cause:** `loadPostsFromFirebase()` and `listenToFirebasePosts()` used `{ id: child.key, ...child.val() }` — when a post had a pre-set `id` (like `'cc-' + Date.now()`), the spread from `child.val()` overwrote the Firebase key with the original id. So `deletePostFromFirebase()` tried to delete a non-existent path.
- **Fix 1:** Reversed spread order to `{ ...child.val(), id: child.key }` — Firebase key always wins
- **Fix 2:** Strip `id` from post data before `push()` to prevent storing conflicting ids
- **Fix 3:** Added `_deletedPostIds` Set to prevent real-time listener from re-adding deleted posts before Firebase confirms

### Inline Roll Flow (commit 635af45)
- Roll suggestions now open an inline form directly in the position modal (no more navigating to calculator tab)
- Form fields: Cost to Buy Back (per share), New Strike, New Expiration (Friday dropdown), New Premium (per share)
- `confirmInlineRoll()`: calculates real P&L = (original premium - buyback cost) × contracts × 100, moves old to history, creates new position with roll tracking
- Deleted old `rollToCalc()` function

### Roll P&L + Linkage Display (commit de290c1)
- Added "Cost to Buy Back Current Position" field to roll form (was missing — P&L was always 0)
- P&L now calculated correctly with buyback cost and fees
- **Active positions:** Blue "Roll #N" badge + "from $X" subtitle
- **Position detail modal:** Roll info banner with total premium across rolls
- **History:** "Rolled" label + arrow showing new strike, "Called Away" label for those entries

### Realized vs Unrealized Premium (commit 635af45)
- **Green change box:** Shows "$X realized · $Y pending" breakdown with better spacing (flex-column layout)
- **Monthly income goal:** Only counts closed trades (realized) toward the goal. Pending shown as "(+$Y pending)"
- **Goals history:** Each month shows pending amount separately
- **Analytics hero:** Changed "Total Premium Collected" to "Total Premium" with realized/pending split
- **Profile stats:** Shows realized with pending noted separately
- Added `getMonthlyPending()` helper function alongside `getMonthlyPremium()`

### Expiration Date Dropdowns (commit c6424b1)
- Replaced text inputs with Friday date `<select>` dropdowns everywhere:
  - Admin signal form (`adminExp`)
  - Admin roll form (`rollNewExp`)
  - User inline roll form
- `getExpDateOptions()` generates next 12 Fridays
- Chain picker fallback: if selected date isn't in dropdown, auto-adds it

### Other Fixes (commits 298ba08, ecf1d53, f908bbc, 951446f, 0acf014)
- **Estimated chain expirations:** Now calculates next 6 actual Fridays instead of fixed day offsets
- **Add Position layout:** Stacked ticker input + Load Chain button vertically (was cramped horizontal)
- **Change box:** Now includes history P&L (was only counting open positions)
- **Master Portfolio:** Added `renderMasterPortfolio()` to admin panel using `computePortfolioStats()`
- **CC delete fix:** CC deletion only removes ccHistory entry, not the entire wheel position
- **Firebase race condition:** `deletePost()` now awaits Firebase delete before re-rendering
- **Close CC button:** Added to manage positions panel with `closeCCOnWheel()` function

### Test User Readiness Audit (commit 2121332)
- Fixed silent catch blocks: assignment sync, earnings fetch, leaderboard sync all now log warnings
- **Site is safe for test users** — auth works, admin locked, no secrets exposed
- Known gaps for later: Stripe payment link, EmailJS, Apple Sign In

### Repo Renamed
- `elitesbeau/wheel` → `elitesbeau/elitesbeau.github.io`
- Live URL: `https://elitesbeau.github.io` (cleaner, no `/wheel/` path)
- Local remote updated to match

## What Was Done Feb 8 (Session 1)

### Unusual Whales API Removal (commit 7f58831)
- Removed entire Intel tab + UW integration (248 lines deleted) — too expensive

### Admin Panel Layout Fix (commit da6f471)
- Stacked vertically: CSP/CC toggle centered → full-width ticker input → full-width Load button

### Assignment Alerts + User Copy Flow (commit 6cd99c9)
- `renderAlertsFeed()` shows cards for assigned/called/winner status changes
- "I was assigned too" button for users who copied the trade

### CC Signal Linking + Duplicate Fix (commit 0b35937)
- CC signals show "Covered by X assigned shares" badge
- `parseExpDate()` utility for "Feb 14" style dates

### DTE Badge Fix (commits f7fdd86, e38a05e)
- Red for ≤3 days only. Orange removed entirely.

### Admin Chain Strike Range (commit 318b3d4)
- CSP: 1 above + 25 below. CC: 1 below + 25 above.

### Admin Wheel Flow Overhaul (commit fda5cd7)
- Bracket mismatch fix, Called Away guard, orphan CC cleanup, open signals filter
- Full lifecycle: Sell CSP → Assigned → Sell CC → Called Away → Complete

## Key Functions (for reference)
- `markPostAssigned(postId, post)` — CSP assigned → creates wheel position
- `sellCCOnWheel(wheelId)` — sell CC against assigned shares
- `calledAwayWheel(wheelId)` — shares called away, complete wheel
- `markPostCalled(postId, post)` — CC called, triggers calledAwayWheel
- `deletePost(postId)` — deletes post + linked wheel + orphaned CCs
- `renderAdminPosts()` — admin post list with context-aware action buttons
- `renderSignals()` — premium user signals view
- `renderWheelPositions()` — manage positions panel
- `parseExpDate(exp)` — handles "Feb 14" style dates
- `getExpDateOptions()` — generates next 12 Friday `<option>` tags
- `startInlineRoll()` — renders inline roll form in position modal
- `confirmInlineRoll()` — executes roll with P&L calculation
- `getMonthlyPremium()` — realized (closed) premium for a month
- `getMonthlyPending()` — unrealized (open) premium for a month
- `renderMasterPortfolio()` — admin portfolio stats panel

## What Was Done Jan 29
(See previous session notes — chain picker fix, kanban board, 7 UI themes)

## What Was Done Jan 28
(See previous session notes — Firebase UID auth, Twelve Data, Groq AI, Discord, position entry)

## What's Next

### Still Needs Config
- Stripe Payment Link → `STRIPE_PAYMENT_LINK` constant in code
- Apple Sign In → Enable in Firebase Console
- Discord webhook → Admin panel → Notification Settings
- EmailJS → Setup for email alerts

### Remaining Issues / Debt
- Options chain relies on Yahoo Finance via CORS proxies (fragile)
- Video attribution wrong on 4 (content fine, credits wrong)
- FMP earnings uses demo API key (falls back to estimates)
- Consider theme preview/selector UI
- User mentioned wanting date dropdowns for ALL date inputs — Add Position still uses `type="date"` (native picker, probably fine)

### User Feedback from Testing
- Roll flow works inline now but user should verify P&L math with real trades
- Green box spacing improved but user may want further tweaks
- Premium realized/pending distinction is new — watch for confusion

## Tech Stack
- Single HTML file (no build tools)
- Firebase Auth (Google, Apple, Email) + Realtime Database
- Twelve Data API (stock quotes) + Yahoo Finance (options chain)
- Groq API / Llama 3.3 70b (AI chatbot)
- Stripe Payment Links (premium)
- EmailJS (email alerts)
- Discord webhooks (signal alerts)
- Alpaca API (broker sync)
- Google Fonts: Inter, Playfair Display, Orbitron, JetBrains Mono, Space Grotesk

## Local Dev
```bash
cd C:\Users\Beau_\Documents\wheel
npx http-server -p 3000 -o
```
Then open http://localhost:3000
