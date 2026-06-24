# MOGUL INC. — COMPLETE GAME SPECIFICATION
## Version 1.0 | Roblox UI-Only Business Empire Game

---

# TABLE OF CONTENTS

1.  Game Overview
2.  Visual Design System
3.  Industry System
4.  Country Database (55 countries)
5.  Branch System
6.  Staff System
7.  Executive System
8.  Research & Development
9.  Brand Reputation System
10. Stock Market System
11. Board Decisions (65 types)
12. Events & News System
13. Investor Contracts
14. Seasonal & Prestige System
15. Social Features
16. Unique Features
17. UI Screen Layouts
18. Monetization
19. Technical Architecture
20. All Player Choices — Master List
21. Implementation Notes

---

# SECTION 1: GAME OVERVIEW

## Concept
Mogul Inc. is a 100% UI-based Roblox idle tycoon game. No 3D world, no avatars running around.
Players build a global franchise empire starting from a single branch, expanding across 55 countries,
managing staff, executives, research, stock markets, and rival companies — all through clean menus
and panels. Directly inspired by "Franchise Empire" on Roblox but rebuilt from scratch with working
save systems, meaningful choices, and features that game doesn't have.

## Key Pillars
- Every upgrade decision has a real tradeoff (no "obviously correct" choices)
- Offline income that matters (players come back to a satisfying catch-up)
- Social flex layer (leaderboard, dossier, Breaking News moments)
- Long-term retention via seasonal IPO resets and legacy multipliers
- Works on mobile and desktop equally well

## Starting Conditions
- Starting Cash: $250,000 (750,000 with Starter Bundle gamepass)
- Starting Country: USA (always unlocked)
- Starting Branches: 0
- Starting Staff: 0
- Starting Brand Score: 50

---

# SECTION 2: VISUAL DESIGN SYSTEM

## Color Palette

### Base Colors
```
BACKGROUND_PRIMARY:    #09090E   (very dark navy-black, main backdrop)
BACKGROUND_SECONDARY:  #111118   (surface, cards)
BACKGROUND_TERTIARY:   #1A1A24   (elevated surface, modals)
BACKGROUND_HOVER:      #222230   (hover state on interactive elements)

BORDER_SUBTLE:         rgba(255,255,255,0.06)
BORDER_DEFAULT:        rgba(255,255,255,0.10)
BORDER_STRONG:         rgba(255,255,255,0.18)

TEXT_PRIMARY:          #EEEEF5   (headings, important values)
TEXT_SECONDARY:        #8A8A9A   (descriptions, labels)
TEXT_MUTED:            #4A4A60   (disabled, placeholders)
TEXT_INVERSE:          #09090E   (text on light backgrounds)
```

### Accent Colors
```
GREEN_DEFAULT:         #22C55E   (money, income, success, positive)
GREEN_BG:              rgba(34,197,94,0.08)
GREEN_BORDER:          rgba(34,197,94,0.22)
GREEN_TEXT:            #4ADE80

AMBER_DEFAULT:         #F59E0B   (warnings, caution, board decisions)
AMBER_BG:              rgba(245,158,11,0.08)
AMBER_BORDER:          rgba(245,158,11,0.22)

RED_DEFAULT:           #EF4444   (crisis, danger, loss, negative)
RED_BG:                rgba(239,68,68,0.08)
RED_BORDER:            rgba(239,68,68,0.22)

BLUE_DEFAULT:          #3B82F6   (information, stock market)
BLUE_BG:               rgba(59,130,246,0.08)
BLUE_BORDER:           rgba(59,130,246,0.22)

PURPLE_DEFAULT:        #8B5CF6   (executives, premium, prestige)
PURPLE_BG:             rgba(139,92,246,0.08)
PURPLE_BORDER:         rgba(139,92,246,0.22)

TEAL_DEFAULT:          #14B8A6   (R&D, research, tech)
TEAL_BG:               rgba(20,184,166,0.08)
TEAL_BORDER:           rgba(20,184,166,0.22)

PINK_DEFAULT:          #EC4899   (staff, social features)
PINK_BG:               rgba(236,72,153,0.08)
PINK_BORDER:           rgba(236,72,153,0.22)

GOLD_DEFAULT:          #EAB308   (VIP, legendary, special badges)
GOLD_BG:               rgba(234,179,8,0.08)
GOLD_BORDER:           rgba(234,179,8,0.22)
```

### Industry Theme Colors
```
FAST_FOOD:    #F97316   (orange, warm, energetic)
TECH:         #6366F1   (indigo, modern, digital)
FASHION:      #EC4899   (pink, trendy, stylish)
HEALTHCARE:   #10B981   (emerald green, clean, trusted)
ENTERTAINMENT:#A855F7   (purple, vibrant, creative)
```

### Semantic Colors
```
MONEY_POSITIVE:  GREEN_DEFAULT    (earning, revenue)
MONEY_NEGATIVE:  RED_DEFAULT      (spending, loss)
MORALE_HIGH:     #22C55E          (60-100)
MORALE_MID:      #F59E0B          (30-59)
MORALE_LOW:      #EF4444          (0-29)
QUALITY_HIGH:    #22C55E          (70-100)
QUALITY_MID:     #F59E0B          (40-69)
QUALITY_LOW:     #EF4444          (0-39)
```

## Typography

### Font Stack
```
PRIMARY_FONT:   "Inter", "SF Pro Display", system-ui, -apple-system, sans-serif
MONO_FONT:      "JetBrains Mono", "Fira Code", "Courier New", monospace
NUMBER_FEATURES: font-variant-numeric: tabular-nums (all numbers, for clean alignment)
```

### Type Scale
```
DISPLAY_XL:   32px / weight 700 / tracking -0.03em  (Breaking News headline)
DISPLAY_LG:   24px / weight 700 / tracking -0.02em  (Tab headers, major values)
HEADING_MD:   18px / weight 600 / tracking -0.01em  (Section headers in tabs)
HEADING_SM:   15px / weight 600 / tracking 0        (Card titles)
BODY_MD:      14px / weight 400 / line-height 1.6   (Main body text)
BODY_SM:      13px / weight 400 / line-height 1.55  (Descriptions, labels)
CAPTION:      11px / weight 500 / tracking 0.04em   (Badges, meta)
LABEL:        10px / weight 700 / tracking 0.08em   (Category labels, uppercase)
MONO_MD:      13px / mono font                      (Code, IDs, data)
MONO_SM:      11px / mono font                      (Small data values)
```

## Spacing System
```
Base unit: 4px
XS:   4px
SM:   8px
MD:   12px
LG:   16px
XL:   20px
2XL:  24px
3XL:  32px
4XL:  40px
5XL:  52px
```

## Border Radius
```
XS:  4px   (tags, badges, small chips)
SM:  6px   (buttons, inputs)
MD:  8px   (small cards)
LG:  10px  (cards, panels)
XL:  12px  (large cards, modals)
2XL: 16px  (floating panels)
FULL: 9999px (pills, avatars, toggles)
```

## Layout Structure
```
SCREEN_WIDTH:       100vw
TOP_BAR_HEIGHT:     52px (fixed, always visible)
BOTTOM_NAV_HEIGHT:  60px (fixed, always visible)
CONTENT_AREA:       screen height - 112px (scrollable)
MAX_CONTENT_WIDTH:  520px (centered on wide screens, mobile-first design)
SIDE_PADDING:       16px (left/right on content)
CARD_GAP:           10px (between cards in grid)
SECTION_GAP:        20px (between sections within a tab)
```

## Icon System (Tabler Icons — all line style, 1.5px stroke)
Tabler Icons is used throughout. All icons are line variants, never filled.
Icon size defaults: 16px (inline), 18px (button), 20px (card header), 24px (tab nav).

### Navigation Icons
```
Dashboard:       icon-layout-dashboard
Branches:        icon-building-store
Staff:           icon-users-group
Executives:      icon-tie
Research:        icon-flask
Stock Market:    icon-chart-candle
Board:           icon-clipboard-list
Leaderboard:     icon-trophy
Shop:            icon-shopping-cart
Settings:        icon-settings
```

### Action Icons
```
Buy / Purchase:  icon-shopping-cart-plus
Upgrade:         icon-arrow-up-circle
Hire:            icon-user-plus
Fire:            icon-user-minus
Promote:         icon-medal
Transfer:        icon-arrows-exchange
Renovate:        icon-paint
Relocate:        icon-map-pin
Close Branch:    icon-building-off
Start Research:  icon-player-play
Complete:        icon-check-circle
Cancel:          icon-x
Back:            icon-arrow-left
Expand:          icon-chevron-down
Collapse:        icon-chevron-up
```

### Status Icons
```
Save Saving:     icon-loader (spinning)
Save Done:       icon-check
Save Error:      icon-alert-triangle
Notification:    icon-bell
Morale High:     icon-mood-happy
Morale Mid:      icon-mood-neutral
Morale Low:      icon-mood-sad
Crisis:          icon-alert-octagon
Opportunity:     icon-sparkles
Locked:          icon-lock
Unlocked:        icon-lock-open
VIP:             icon-crown
Boost Active:    icon-bolt
Offline:         icon-moon
Online:          icon-wifi
```

### Data Icons
```
Money / Cash:    icon-coin
Revenue:         icon-trending-up
Net Worth:       icon-building-bank
Brand Score:     icon-star
Quality:         icon-award
Morale:          icon-heart
Staff Slot:      icon-user
Level:           icon-layers
Country:         icon-world
City:            icon-map-pin
Research Timer:  icon-clock
Stock Up:        icon-trending-up
Stock Down:      icon-trending-down
Season Timer:    icon-calendar-event
Legacy:          icon-history
IPO:             icon-rocket
Corp:            icon-users
Takeover:        icon-sword
Dossier:         icon-id-badge
News:            icon-news
```

### Industry Icons
```
Fast Food:       icon-burger
Tech:            icon-cpu
Fashion:         icon-shirt
Healthcare:      icon-heart-rate-monitor
Entertainment:   icon-movie
```

### Country Tier Icons
```
Tier 1:          icon-map (unlocked at start)
Tier 2:          icon-map-2
Tier 3:          icon-globe
Tier 4:          icon-world
Tier 5:          icon-planet
Tier 6:          icon-universe
```

## UI Component Specifications

### Cards
```
Standard Card:
  background: BACKGROUND_SECONDARY
  border: 1px solid BORDER_DEFAULT
  border-radius: LG (10px)
  padding: 14px 16px
  shadow: none (flat design)

Elevated Card (modals, important info):
  background: BACKGROUND_TERTIARY
  border: 1px solid BORDER_STRONG
  border-radius: XL (12px)
  padding: 18px 20px

Highlight Card (success, active boost):
  background: GREEN_BG
  border: 1px solid GREEN_BORDER
  border-radius: LG

Warning Card:
  background: AMBER_BG
  border: 1px solid AMBER_BORDER

Danger Card:
  background: RED_BG
  border: 1px solid RED_BORDER
```

### Buttons
```
Primary Button:
  background: GREEN_DEFAULT (#22C55E)
  text: TEXT_INVERSE
  border-radius: SM (6px)
  padding: 9px 16px
  font: BODY_SM, weight 600
  hover: brightness 1.1
  disabled: opacity 0.4

Secondary Button:
  background: BACKGROUND_TERTIARY
  border: 1px solid BORDER_STRONG
  text: TEXT_PRIMARY
  same sizing as Primary

Danger Button:
  background: RED_DEFAULT
  text: white

Ghost Button:
  background: transparent
  border: 1px solid BORDER_DEFAULT
  text: TEXT_SECONDARY
  hover: BACKGROUND_HOVER

Icon Button:
  width: 32px, height: 32px
  border-radius: SM
  center-aligned icon
```

### Progress Bars
```
Standard Bar:
  height: 6px
  border-radius: FULL
  background track: BORDER_DEFAULT
  fill: varies by type (green=morale/quality/brand, teal=research, purple=season XP)

Tall Bar (main metrics):
  height: 8px
  with label showing value above
```

### Tags / Badges
```
Standard Tag:
  font: LABEL (10px uppercase)
  padding: 2px 8px
  border-radius: XS (4px)
  border: 1px solid matching BORDER color
  
Pill Badge (numbers, counts):
  min-width: 18px, height: 18px
  border-radius: FULL
  font: 10px weight 700
  background: RED_DEFAULT (notification)
  text: white
```

### Animations
```
Card hover:         translateY(-1px), 150ms ease
Modal open:         scale 0.95 → 1.0 + opacity 0 → 1, 200ms ease-out
Modal close:        scale 1.0 → 0.95 + opacity 1 → 0, 150ms ease-in
Tab switch:         opacity 0 → 1, 120ms ease
Number tick:        smooth counter animation, 400ms
Toast slide-in:     translateX(120%) → 0, 200ms ease-out
Toast slide-out:    translateX(0) → 120%, 150ms ease-in
Breaking News:      translateY(40px) → 0 + opacity 0 → 1, 350ms ease-out
Pulse (alert):      scale 1 → 1.05 → 1, 800ms infinite
Spin (loading):     rotate 0 → 360deg, 1000ms linear infinite
Bar fill:           width animated, 600ms ease-out
```

---

# SECTION 3: INDUSTRY SYSTEM

At the start of every new game (or after an IPO), the player picks their industry.
This changes UI theme colors, upgrade/staff naming, country demand multipliers,
crisis pools, and R&D project names. It does NOT change the core mechanics —
only the flavor and which countries are most profitable.

---

## INDUSTRY: FAST FOOD

```
ID:              fast_food
THEME_COLOR:     #F97316
ICON:            icon-burger
BRANCH_NAME:     Restaurant
STAFF_TITLE:     Team Member
PRODUCT_NAME:    Menu Item
HQ_NAME:         Corporate Kitchen
EXEC_FLAVOR:     Operations focus, supply chain, food quality

STRENGTHS:
  - Highest base volume (customers per hour)
  - Lowest branch cost
  - Fastest expansion
  - Strong in high-population, lower-income countries

WEAKNESSES:
  - Lowest margin per customer
  - Health inspection crises frequent
  - Premium path less effective (lower luxury appeal)

BEST COUNTRIES:   India, Brazil, Indonesia, Mexico, Nigeria, Philippines, Bangladesh
WORST COUNTRIES:  Switzerland, Norway, Luxembourg (low fast food demand / high costs)

UPGRADE NAMES (Volume Path):    "Combo Deals", "Express Line", "Drive-Through", "Kiosk Stations", "Meal Bundles"
UPGRADE NAMES (Premium Path):   "Gourmet Menu", "Table Service", "Chef Partnership", "Premium Ingredients", "VIP Dining"
UPGRADE NAMES (Seasonal Path):  "Holiday Special", "Summer Sale", "Festive Meal Box", "Limited Edition Burger", "Anniversary Deal"

CRISIS TYPES:
  health_inspection_failure, supply_chain_shortage, food_contamination_scare,
  staff_walkout, competitor_price_war, delivery_delay, equipment_breakdown,
  bad_review_viral, ingredient_price_spike, health_department_audit

EXCLUSIVE R&D:
  Recipe Innovation:      +20% income all branches, 60 min
  Drive-Through AI:       +25% Volume path throughput, 90 min
  Nutrition Partnership:  +10 brand score + immune to health inspection, 75 min
  Franchise Training Kit: +20% all staff specialty bonuses, 60 min
```

---

## INDUSTRY: TECH

```
ID:              tech
THEME_COLOR:     #6366F1
ICON:            icon-cpu
BRANCH_NAME:     Office
STAFF_TITLE:     Engineer
PRODUCT_NAME:    Software Suite
HQ_NAME:         Innovation Campus
EXEC_FLAVOR:     R&D focus, CTO extremely valuable

STRENGTHS:
  - Highest income ceiling
  - R&D bonuses are doubled
  - Premium path most effective
  - Best late-game country multipliers

WEAKNESSES:
  - Slowest early game (expensive branches)
  - High sensitivity to crises (data breaches = huge brand hit)
  - Needs more executives to reach potential

BEST COUNTRIES:   USA, Japan, South Korea, Germany, Israel, Singapore, Netherlands, Sweden, Finland
WORST COUNTRIES:  Nigeria, Bangladesh, Myanmar (low tech demand)

UPGRADE NAMES (Volume Path):    "Open Workspace", "Agile Sprint", "Dev Tools Upgrade", "CI/CD Pipeline", "Cloud Scaling"
UPGRADE NAMES (Premium Path):   "Enterprise Suite", "Custom API", "White-Glove Onboarding", "Dedicated Support", "Executive Dashboard"
UPGRADE NAMES (Seasonal Path):  "Product Launch", "Hackathon Event", "Beta Access Drop", "Conference Keynote", "Year-End Release"

CRISIS TYPES:
  server_outage, data_breach, security_vulnerability, key_engineer_quit,
  product_launch_delay, competitor_feature_copy, regulatory_investigation,
  bad_app_review, patent_dispute, AI_ethics_controversy

EXCLUSIVE R&D:
  Platform Launch:        +30% income, 120 min
  AI Integration:         +20% all income permanently, 150 min
  Security Fortress:      Immune to data breach crises, 90 min
  Developer Relations:    +20% staff specialty bonuses, 75 min
```

---

## INDUSTRY: FASHION

```
ID:              fashion
THEME_COLOR:     #EC4899
ICON:            icon-shirt
BRANCH_NAME:     Boutique
STAFF_TITLE:     Stylist
PRODUCT_NAME:    Collection
HQ_NAME:         Design Atelier
EXEC_FLAVOR:     CMO extremely valuable, brand score crucial

STRENGTHS:
  - Highest brand score multiplier
  - Very strong in luxury/rich countries
  - Seasonal path most powerful of all industries
  - Premium path gives highest per-customer margin

WEAKNESSES:
  - Very volatile (trends change fast)
  - Low demand in developing countries
  - Brand score damage from crises is severe

BEST COUNTRIES:   France, Italy, UAE, UK, Japan, South Korea, Switzerland, USA, Spain, Australia
WORST COUNTRIES:  Bangladesh, Pakistan, Ethiopia, Myanmar (very low luxury demand)

UPGRADE NAMES (Volume Path):    "Fast Fashion Line", "Pop-Up Event", "Flash Sale", "Outlet Store", "Capsule Collection"
UPGRADE NAMES (Premium Path):   "Designer Collab", "Exclusive Members", "Runway Show", "Couture Line", "Personal Shopper"
UPGRADE NAMES (Seasonal Path):  "Summer Collection", "Winter Gala", "Fashion Week", "Holiday Edition", "Trend Drop"

CRISIS TYPES:
  knockoff_scandal, influencer_fallout, trend_miss, fabric_shortage,
  sweatshop_accusation, celebrity_disassociation, fashion_week_disaster,
  viral_bad_review, return_rate_spike, copyright_infringement

EXCLUSIVE R&D:
  Signature Collection:   +25% income, 75 min
  Influencer Network:     +15 brand score + prevents influencer crisis, 90 min
  Sustainability Push:    +12 brand score + cost -10%, 60 min
  Virtual Fitting Room:   +20% Premium path income, 90 min
```

---

## INDUSTRY: HEALTHCARE

```
ID:              healthcare
THEME_COLOR:     #10B981
ICON:            icon-heart-rate-monitor
BRANCH_NAME:     Clinic
STAFF_TITLE:     Specialist
PRODUCT_NAME:    Treatment Package
HQ_NAME:         Medical Center
EXEC_FLAVOR:     CFO crucial (high overhead), COO important for compliance

STRENGTHS:
  - Most recession-proof (demand stable in all economies)
  - Regulatory crises often manageable
  - High per-customer margin
  - Best CEO Pass synergy (CFO + offline cap)

WEAKNESSES:
  - Most expensive to expand
  - Slowest volume growth
  - Many government regulatory crises
  - Staff morale issues common (high-stress environment)

BEST COUNTRIES:   Germany, USA, Australia, Switzerland, Canada, Sweden, Japan, UK, Denmark, Austria
WORST COUNTRIES:  Nigeria, Ethiopia, Bangladesh, Myanmar (underdeveloped healthcare markets)

UPGRADE NAMES (Volume Path):    "Walk-In Clinic", "Telemedicine Line", "Insurance Partnership", "Screening Program", "Community Outreach"
UPGRADE NAMES (Premium Path):   "Private Suite", "Specialist Referral", "Executive Health Plan", "Concierge Medicine", "Research Trial"
UPGRADE NAMES (Seasonal Path):  "Flu Season Campaign", "Annual Check-Up Drive", "Mental Health Month", "Summer Wellness", "New Year Health"

CRISIS TYPES:
  malpractice_claim, regulatory_audit, supply_drug_shortage, staff_burnout_mass,
  insurance_dispute, health_scandal, data_privacy_breach, inspection_failure,
  staff_union_strike, competitor_undercutting

EXCLUSIVE R&D:
  Clinical Excellence Protocol: +25% income, 90 min
  Digital Health Platform:      +20% volume throughput, 75 min
  Compliance Shield:            -60% regulatory crisis damage, 60 min
  Specialist Recruitment:       +25% staff specialty bonuses, 90 min
```

---

## INDUSTRY: ENTERTAINMENT

```
ID:              entertainment
THEME_COLOR:     #A855F7
ICON:            icon-movie
BRANCH_NAME:     Studio / Venue
STAFF_TITLE:     Creator
PRODUCT_NAME:    Experience
HQ_NAME:         Creative Hub
EXEC_FLAVOR:     CMO and CTO equally important, highest variance industry

STRENGTHS:
  - Highest income ceiling with Seasonal path
  - Viral opportunity events are most frequent
  - Seasonal events give biggest multiplier (4x vs 3x other industries)
  - Most social sharing potential (Breaking News feels most fun)

WEAKNESSES:
  - Most volatile income (boom/bust)
  - Flop events can tank income significantly
  - High crisis frequency
  - Needs consistent active management

BEST COUNTRIES:   USA, China, South Korea, Japan, UK, Brazil, India, Nigeria, Australia, Mexico
WORST COUNTRIES:  Switzerland, Norway, Germany (conservative entertainment markets)

UPGRADE NAMES (Volume Path):    "Streaming Rights", "Syndication Deal", "Box Office Boost", "Fan Club", "Merchandise Line"
UPGRADE NAMES (Premium Path):   "Exclusive Premiere", "VIP Experience", "Director's Cut", "Private Screening", "Brand Collaboration"
UPGRADE NAMES (Seasonal Path):  "Summer Blockbuster", "Holiday Special", "Award Season Push", "Viral Campaign", "World Tour"

CRISIS TYPES:
  box_office_flop, streaming_rights_lost, celebrity_scandal, bad_critic_review,
  production_delay, copyright_lawsuit, audience_boycott, technical_failure,
  talent_dispute, piracy_surge

EXCLUSIVE R&D:
  Blockbuster Engine:     +35% Seasonal path income, 90 min
  Fan Engagement Platform: +20% all income + viral events 2x more frequent, 120 min
  IP Portfolio:           Immune to copyright crisis, 75 min
  Creator Network:        +25% staff specialty bonuses, 60 min
```

---

# SECTION 4: COUNTRY DATABASE

Format per country:
  TIER | UNLOCK_REQ (cumulative revenue) | UNLOCK_COST | WEALTH_MULT
  Demand multipliers: FF=Fast Food, TC=Tech, FS=Fashion, HC=Healthcare, EN=Entertainment
  CITIES: name (city type) — types: Airport, Mall, Downtown, Industrial, Luxury, University, Harbor, Resort

Demand scale: 0.5=very low, 0.8=low, 1.0=average, 1.2=good, 1.5=strong, 1.8=very strong, 2.0=exceptional

---

## TIER 1 — STARTER (Unlocked by default, no cost)

### USA
```
TIER: 1 | UNLOCK: default | COST: free | WEALTH: 1.6
DEMAND: FF=1.3 TC=1.8 FS=1.4 HC=1.5 EN=1.8
CITIES:
  New York City (Downtown), Los Angeles (Entertainment District),
  Chicago (Industrial), Houston (Airport), Miami (Luxury),
  San Francisco (Tech Campus), Seattle (Harbor)
CRISIS_FLAVOR: FDA investigations, FTC antitrust, union strikes
NOTES: Best all-round starting country. Tech and Entertainment excel here.
```

---

## TIER 2 — EARLY ($500K milestone | $100K-$200K unlock cost)

### United Kingdom
```
TIER: 2 | UNLOCK: $500K | COST: $100K | WEALTH: 1.4
DEMAND: FF=1.1 TC=1.4 FS=1.5 HC=1.6 EN=1.4
CITIES: London (Luxury), Manchester (Industrial), Edinburgh (Downtown), Birmingham (Mall), Bristol (University)
CRISIS_FLAVOR: GDPR violations, media scrutiny, NHS competition
NOTES: Fashion and Healthcare strongest. London Luxury is the best slot.
```

### Germany
```
TIER: 2 | UNLOCK: $500K | COST: $120K | WEALTH: 1.5
DEMAND: FF=0.9 TC=1.5 FS=1.1 HC=1.7 EN=0.9
CITIES: Berlin (Tech Campus), Munich (Luxury), Hamburg (Harbor), Frankfurt (Airport), Cologne (Mall)
CRISIS_FLAVOR: Labor union strikes, strict regulatory audits, environmental compliance
NOTES: Healthcare powerhouse. Frankfurt Airport is highest-earning slot.
```

### France
```
TIER: 2 | UNLOCK: $500K | COST: $130K | WEALTH: 1.5
DEMAND: FF=1.0 TC=1.2 FS=2.0 HC=1.3 EN=1.3
CITIES: Paris (Luxury), Lyon (Downtown), Marseille (Harbor), Bordeaux (Resort), Toulouse (University)
CRISIS_FLAVOR: Fashion knockoff lawsuits, labor strikes, trade disputes
NOTES: Fashion capital. Paris Luxury gives exceptional Fashion multiplier. 2.0 demand.
```

### Japan
```
TIER: 2 | UNLOCK: $500K | COST: $150K | WEALTH: 1.6
DEMAND: FF=1.1 TC=1.8 FS=1.7 HC=1.4 EN=1.6
CITIES: Tokyo (Luxury), Osaka (Mall), Kyoto (Resort), Yokohama (Harbor), Sapporo (Downtown)
CRISIS_FLAVOR: Earthquake disruptions, strict quality audits, cultural sensitivity issues
NOTES: Excellent across Tech, Fashion, Entertainment. Tokyo is one of the best cities in the game.
```

### Canada
```
TIER: 2 | UNLOCK: $750K | COST: $150K | WEALTH: 1.4
DEMAND: FF=1.2 TC=1.3 FS=1.1 HC=1.7 EN=1.1
CITIES: Toronto (Downtown), Vancouver (Resort), Montreal (University), Calgary (Industrial), Ottawa (Airport)
CRISIS_FLAVOR: Supply freeze, healthcare regulation, environmental protests
NOTES: Healthcare specialist. Vancouver Resort is a hidden gem for Healthcare.
```

### Australia
```
TIER: 2 | UNLOCK: $750K | COST: $160K | WEALTH: 1.4
DEMAND: FF=1.3 TC=1.2 FS=1.2 HC=1.5 EN=1.4
CITIES: Sydney (Harbor), Melbourne (Downtown), Brisbane (Mall), Perth (Industrial), Gold Coast (Resort)
CRISIS_FLAVOR: Environmental activist protests, strict food standards, mining disputes
NOTES: Gold Coast Resort excellent for Entertainment Seasonal path.
```

### South Korea
```
TIER: 2 | UNLOCK: $1M | COST: $180K | WEALTH: 1.3
DEMAND: FF=1.2 TC=1.7 FS=1.8 HC=1.3 EN=1.8
CITIES: Seoul (Luxury), Busan (Harbor), Incheon (Airport), Daegu (Mall), Jeju (Resort)
CRISIS_FLAVOR: Chaebol competition, media controversies, tech patent disputes
NOTES: K-pop/K-beauty effect: Fashion and Entertainment very strong. Seoul Luxury is excellent.
```

### Netherlands
```
TIER: 2 | UNLOCK: $1M | COST: $170K | WEALTH: 1.5
DEMAND: FF=0.9 TC=1.6 FS=1.2 HC=1.4 EN=1.2
CITIES: Amsterdam (Harbor), Rotterdam (Industrial), The Hague (Downtown), Eindhoven (Tech Campus), Utrecht (University)
CRISIS_FLAVOR: GDPR enforcement, financial regulation, cycling logistics disruption
NOTES: Tech hub in Europe. Eindhoven Tech Campus has unique R&D bonus (+10% research speed).
```

---

## TIER 3 — MID ($3M milestone | $400K-$700K unlock cost)

### Brazil
```
TIER: 3 | UNLOCK: $3M | COST: $400K | WEALTH: 0.9
DEMAND: FF=1.6 TC=1.0 FS=1.1 HC=1.1 EN=1.5
CITIES: Sao Paulo (Mall), Rio de Janeiro (Resort), Brasilia (Downtown), Salvador (Harbor), Curitiba (Industrial)
CRISIS_FLAVOR: Currency devaluation, political instability, infrastructure failure
NOTES: Fast Food goldmine. High population volume. Rio Resort for Entertainment.
```

### India
```
TIER: 3 | UNLOCK: $3M | COST: $450K | WEALTH: 0.7
DEMAND: FF=1.8 TC=1.3 FS=0.8 HC=1.5 EN=1.2
CITIES: Mumbai (Mall), Delhi (Downtown), Bangalore (Tech Campus), Chennai (Harbor), Hyderabad (Industrial), Kolkata (Airport)
CRISIS_FLAVOR: Infrastructure disruption, regulatory complexity, political protests
NOTES: Highest Fast Food demand in the game (1.8). Bangalore Tech Campus strong for Tech.
```

### China
```
TIER: 3 | UNLOCK: $5M | COST: $600K | WEALTH: 1.1
DEMAND: FF=1.5 TC=1.6 FS=1.3 HC=1.2 EN=1.7
CITIES: Shanghai (Mall), Beijing (Downtown), Shenzhen (Tech Campus), Guangzhou (Industrial), Chengdu (Airport), Hangzhou (Luxury)
CRISIS_FLAVOR: Regulatory crackdown, trade restrictions, censorship compliance
NOTES: Huge market. High risk of government regulation crises but excellent income when stable.
```

### Spain
```
TIER: 3 | UNLOCK: $3M | COST: $380K | WEALTH: 1.2
DEMAND: FF=1.1 TC=1.1 FS=1.4 HC=1.3 EN=1.5
CITIES: Madrid (Downtown), Barcelona (Resort), Valencia (Harbor), Seville (Airport), Bilbao (University)
CRISIS_FLAVOR: Tourism seasonality, labor strikes, regional political tension
NOTES: Barcelona Resort excellent for Fashion Seasonal path.
```

### Italy
```
TIER: 3 | UNLOCK: $3M | COST: $400K | WEALTH: 1.3
DEMAND: FF=1.0 TC=1.1 FS=1.9 HC=1.4 EN=1.3
CITIES: Milan (Luxury), Rome (Downtown), Florence (Resort), Naples (Harbor), Turin (Industrial)
CRISIS_FLAVOR: Fashion knockoffs, regulatory bureaucracy, political instability
NOTES: Milan Luxury is the second-best Fashion slot in the game after Paris.
```

### Mexico
```
TIER: 3 | UNLOCK: $3M | COST: $350K | WEALTH: 0.8
DEMAND: FF=1.7 TC=0.9 FS=1.0 HC=1.0 EN=1.4
CITIES: Mexico City (Mall), Guadalajara (Industrial), Monterrey (Downtown), Cancun (Resort), Tijuana (Airport)
CRISIS_FLAVOR: Logistics disruption, crime impact on staff morale, customs delays
NOTES: Fast Food second-best after India. Cancun Resort for Entertainment.
```

### Singapore
```
TIER: 3 | UNLOCK: $4M | COST: $500K | WEALTH: 1.8
DEMAND: FF=1.1 TC=1.7 FS=1.6 HC=1.5 EN=1.3
CITIES: Marina Bay (Luxury), Orchard Road (Mall), Changi (Airport), Jurong (Industrial), Sentosa (Resort)
CRISIS_FLAVOR: Strict regulatory fines, competitive tech market, expat staff turnover
NOTES: Small but incredibly wealthy. Changi Airport gives unique logistics bonus (+5% offline income).
```

### Sweden
```
TIER: 3 | UNLOCK: $4M | COST: $480K | WEALTH: 1.5
DEMAND: FF=0.8 TC=1.6 FS=1.2 HC=1.6 EN=1.1
CITIES: Stockholm (Downtown), Gothenburg (Harbor), Malmo (University), Uppsala (Tech Campus), Kiruna (Industrial)
CRISIS_FLAVOR: High labor costs, environmental scrutiny, work-life balance disputes
NOTES: Excellent Tech + Healthcare combo. Lowest crisis frequency of any country.
```

### Switzerland
```
TIER: 3 | UNLOCK: $5M | COST: $600K | WEALTH: 2.0
DEMAND: FF=0.6 TC=1.4 FS=1.5 HC=2.0 EN=0.9
CITIES: Zurich (Luxury), Geneva (Downtown), Basel (University), Bern (Airport), Lausanne (Resort)
CRISIS_FLAVOR: Strict privacy laws, expensive compliance, currency volatility
NOTES: Highest wealth multiplier (2.0). Healthcare demand exceptional (2.0). Very expensive but worth it.
```

### Turkey
```
TIER: 3 | UNLOCK: $3M | COST: $360K | WEALTH: 0.9
DEMAND: FF=1.4 TC=1.0 FS=1.3 HC=1.1 EN=1.2
CITIES: Istanbul (Mall), Ankara (Downtown), Izmir (Harbor), Antalya (Resort), Bursa (Industrial)
CRISIS_FLAVOR: Currency inflation, political pressure, tourism volatility
NOTES: Istanbul Mall is very high traffic for Fast Food. Antalya Resort good for Fashion Seasonal.
```

### Poland
```
TIER: 3 | UNLOCK: $3M | COST: $340K | WEALTH: 1.0
DEMAND: FF=1.2 TC=1.3 FS=1.0 HC=1.2 EN=1.1
CITIES: Warsaw (Downtown), Krakow (University), Gdansk (Harbor), Wroclaw (Tech Campus), Poznan (Industrial)
CRISIS_FLAVOR: EU regulatory compliance, labor market tightness, logistics disruption
NOTES: Solid all-rounder. Wroclaw Tech Campus gives same R&D bonus as Eindhoven.
```

### Israel
```
TIER: 3 | UNLOCK: $4M | COST: $500K | WEALTH: 1.4
DEMAND: FF=1.0 TC=2.0 FS=1.1 HC=1.5 EN=1.2
CITIES: Tel Aviv (Tech Campus), Jerusalem (Downtown), Haifa (Harbor), Eilat (Resort), Beer Sheva (University)
CRISIS_FLAVOR: Geopolitical tension, security concerns, startup competition
NOTES: Highest Tech demand (2.0) in the game tied with USA. Tel Aviv Tech Campus is a gem.
```

---

## TIER 4 — ADVANCED ($15M milestone | $1.5M-$3M unlock cost)

### UAE
```
TIER: 4 | UNLOCK: $15M | COST: $1.5M | WEALTH: 1.9
DEMAND: FF=1.0 TC=1.4 FS=1.9 HC=1.3 EN=1.7
CITIES: Dubai (Luxury), Abu Dhabi (Downtown), Sharjah (Mall), Ras Al Khaimah (Resort), Fujairah (Harbor)
CRISIS_FLAVOR: Cultural sensitivity violations, labor disputes, regulatory surprises
NOTES: Dubai Luxury is third best Fashion slot. Massive wealth multiplier (1.9).
```

### Saudi Arabia
```
TIER: 4 | UNLOCK: $15M | COST: $2M | WEALTH: 1.8
DEMAND: FF=1.2 TC=1.2 FS=1.0 HC=1.6 EN=1.3
CITIES: Riyadh (Downtown), Jeddah (Mall), Mecca (Airport), NEOM (Tech Campus), Dammam (Industrial)
CRISIS_FLAVOR: Regulatory restrictions, cultural compliance costs, political instability
NOTES: NEOM Tech Campus is a unique futuristic slot with extra Tech bonus (+15%).
```

### Indonesia
```
TIER: 4 | UNLOCK: $15M | COST: $1.5M | WEALTH: 0.7
DEMAND: FF=1.8 TC=1.1 FS=0.9 HC=1.0 EN=1.3
CITIES: Jakarta (Mall), Surabaya (Industrial), Bali (Resort), Medan (Downtown), Bandung (University)
CRISIS_FLAVOR: Logistics failure, monsoon disruption, labor regulation
NOTES: Second-highest Fast Food demand tied with Brazil (1.8). Bali Resort for Entertainment.
```

### Argentina
```
TIER: 4 | UNLOCK: $15M | COST: $1.6M | WEALTH: 0.8
DEMAND: FF=1.5 TC=1.0 FS=1.1 HC=1.1 EN=1.3
CITIES: Buenos Aires (Downtown), Cordoba (University), Rosario (Industrial), Mendoza (Resort), Mar del Plata (Harbor)
CRISIS_FLAVOR: Currency devaluation (severe), inflation events, political crisis
NOTES: High crisis rate from currency events but strong Fast Food income when stable.
```

### South Africa
```
TIER: 4 | UNLOCK: $15M | COST: $1.8M | WEALTH: 0.9
DEMAND: FF=1.3 TC=1.0 FS=1.1 HC=1.2 EN=1.4
CITIES: Johannesburg (Downtown), Cape Town (Resort), Durban (Harbor), Pretoria (Airport), Port Elizabeth (Industrial)
CRISIS_FLAVOR: Power outages, political protests, infrastructure failures
NOTES: Cape Town Resort excellent for Entertainment. Unique "Load Shedding" crisis type.
```

### Nigeria
```
TIER: 4 | UNLOCK: $20M | COST: $2M | WEALTH: 0.6
DEMAND: FF=1.7 TC=0.8 FS=0.9 HC=0.9 EN=1.5
CITIES: Lagos (Mall), Abuja (Downtown), Kano (Industrial), Ibadan (University), Port Harcourt (Harbor)
CRISIS_FLAVOR: Infrastructure failure, political instability, logistics breakdown
NOTES: Very high Fast Food demand. High risk but strong reward. Lagos Mall is massive volume.
```

### Russia
```
TIER: 4 | UNLOCK: $20M | COST: $2.5M | WEALTH: 1.0
DEMAND: FF=1.1 TC=1.2 FS=1.1 HC=1.3 EN=1.1
CITIES: Moscow (Downtown), St. Petersburg (Luxury), Novosibirsk (Industrial), Kazan (Mall), Sochi (Resort)
CRISIS_FLAVOR: Sanctions complications, regulatory pressure, political instability
NOTES: High crisis frequency. Sochi Resort has skiing-seasonal bonus for Entertainment.
```

### Vietnam
```
TIER: 4 | UNLOCK: $15M | COST: $1.5M | WEALTH: 0.6
DEMAND: FF=1.6 TC=1.3 FS=1.0 HC=0.9 EN=1.1
CITIES: Ho Chi Minh City (Mall), Hanoi (Downtown), Da Nang (Resort), Hai Phong (Harbor), Binh Duong (Industrial)
CRISIS_FLAVOR: Supply chain delays, regulatory changes, rapid market shifts
NOTES: Emerging market. Ho Chi Minh Mall has excellent Fast Food throughput.
```

### Thailand
```
TIER: 4 | UNLOCK: $15M | COST: $1.5M | WEALTH: 0.8
DEMAND: FF=1.4 TC=1.1 FS=1.3 HC=1.1 EN=1.6
CITIES: Bangkok (Mall), Phuket (Resort), Chiang Mai (Downtown), Pattaya (Resort), Chonburi (Industrial)
CRISIS_FLAVOR: Tourism volatility, political protests, flooding events
NOTES: Two Resort slots. Phuket Resort is top Entertainment Seasonal earner in Tier 4.
```

### Malaysia
```
TIER: 4 | UNLOCK: $12M | COST: $1.4M | WEALTH: 0.9
DEMAND: FF=1.5 TC=1.3 FS=1.1 HC=1.2 EN=1.2
CITIES: Kuala Lumpur (Downtown), Petaling Jaya (Mall), Penang (Harbor), Johor Bahru (Industrial), Kota Kinabalu (Resort)
CRISIS_FLAVOR: Political uncertainty, currency weakness, logistics delays
NOTES: Solid mid-tier country with no outstanding weaknesses.
```

---

## TIER 5 — EXPERT ($75M milestone | $6M-$12M unlock cost)

### Egypt
```
TIER: 5 | UNLOCK: $75M | COST: $6M | WEALTH: 0.6
DEMAND: FF=1.5 TC=0.9 FS=1.2 HC=1.0 EN=1.4
CITIES: Cairo (Mall), Alexandria (Harbor), Sharm El-Sheikh (Resort), Luxor (Downtown), Giza (Airport)
CRISIS_FLAVOR: Political instability, tourism disruption, currency crisis
NOTES: Giza Airport gives unique "Ancient Market" bonus (+8% Fashion income).
```

### Kenya
```
TIER: 5 | UNLOCK: $75M | COST: $6M | WEALTH: 0.5
DEMAND: FF=1.5 TC=1.0 FS=0.9 HC=1.1 EN=1.3
CITIES: Nairobi (Downtown), Mombasa (Harbor), Kisumu (Mall), Nakuru (Industrial), Eldoret (Airport)
CRISIS_FLAVOR: Infrastructure gaps, climate events, political protests
NOTES: Nairobi growing fast. Mobile tech adoption makes this a surprise Tech opportunity.
```

### Morocco
```
TIER: 5 | UNLOCK: $75M | COST: $7M | WEALTH: 0.7
DEMAND: FF=1.2 TC=0.9 FS=1.6 HC=1.0 EN=1.3
CITIES: Casablanca (Downtown), Marrakech (Resort), Rabat (Airport), Tangier (Harbor), Fes (University)
CRISIS_FLAVOR: Tourism disruption, political tension, supply chain issues
NOTES: Marrakech Resort is surprisingly strong for Fashion. Unique "Medina Market" bonus.
```

### Colombia
```
TIER: 5 | UNLOCK: $75M | COST: $7M | WEALTH: 0.7
DEMAND: FF=1.4 TC=1.0 FS=1.1 HC=1.1 EN=1.4
CITIES: Bogota (Downtown), Medellin (University), Cali (Mall), Cartagena (Resort), Barranquilla (Harbor)
CRISIS_FLAVOR: Security concerns, political instability, logistics disruption
NOTES: Medellin has "Tech Innovation" bonus (+10% Tech income) from city's transformation story.
```

### Chile
```
TIER: 5 | UNLOCK: $75M | COST: $8M | WEALTH: 1.0
DEMAND: FF=1.3 TC=1.2 FS=1.1 HC=1.3 EN=1.2
CITIES: Santiago (Downtown), Valparaiso (Harbor), Concepcion (University), Antofagasta (Industrial), Vina del Mar (Resort)
CRISIS_FLAVOR: Earthquake events, political protests, copper market impact
NOTES: Most stable South American country. Lowest crisis frequency in Tier 5.
```

### Philippines
```
TIER: 5 | UNLOCK: $75M | COST: $6.5M | WEALTH: 0.6
DEMAND: FF=1.7 TC=1.1 FS=0.9 HC=1.0 EN=1.5
CITIES: Manila (Mall), Cebu (Harbor), Davao (Downtown), Quezon City (University), Boracay (Resort)
CRISIS_FLAVOR: Typhoon events, political volatility, infrastructure failure
NOTES: Third-highest Fast Food demand (1.7). Boracay Resort for Entertainment.
```

### Pakistan
```
TIER: 5 | UNLOCK: $75M | COST: $6M | WEALTH: 0.5
DEMAND: FF=1.7 TC=0.8 FS=0.8 HC=0.9 EN=1.0
CITIES: Karachi (Industrial), Lahore (Mall), Islamabad (Downtown), Faisalabad (University), Rawalpindi (Airport)
CRISIS_FLAVOR: Political instability, power outages, currency crisis, security concerns
NOTES: Very high Fast Food volume despite low wealth. Cheap unlock, high risk, decent reward.
```

### Bangladesh
```
TIER: 5 | UNLOCK: $75M | COST: $5.5M | WEALTH: 0.4
DEMAND: FF=1.8 TC=0.7 FS=1.3 HC=0.8 EN=0.9
CITIES: Dhaka (Industrial), Chittagong (Harbor), Sylhet (Downtown), Rajshahi (Mall), Khulna (University)
CRISIS_FLAVOR: Flooding events, labor unrest, infrastructure failure, supply chain breakdown
NOTES: Cheapest Tier 5 unlock. Highest Fast Food demand alongside India (1.8). Very high risk.
```

### Denmark
```
TIER: 5 | UNLOCK: $80M | COST: $9M | WEALTH: 1.6
DEMAND: FF=0.8 TC=1.5 FS=1.2 HC=1.8 EN=1.0
CITIES: Copenhagen (Downtown), Aarhus (University), Odense (Industrial), Aalborg (Harbor), Esbjerg (Airport)
CRISIS_FLAVOR: Labor cost spikes, strict environmental compliance, regulatory changes
NOTES: Very high Healthcare demand. Copenhagen one of the best Healthcare cities in the game.
```

### Finland
```
TIER: 5 | UNLOCK: $80M | COST: $9M | WEALTH: 1.5
DEMAND: FF=0.7 TC=1.8 FS=1.0 HC=1.6 EN=0.9
CITIES: Helsinki (Tech Campus), Espoo (University), Tampere (Industrial), Turku (Harbor), Oulu (Downtown)
CRISIS_FLAVOR: Extreme weather disruption, high labor costs, small market saturation
NOTES: Helsinki Tech Campus is the strongest R&D bonus city in the game (+20% research speed).
```

### Norway
```
TIER: 5 | UNLOCK: $80M | COST: $10M | WEALTH: 1.8
DEMAND: FF=0.7 TC=1.4 FS=1.1 HC=1.9 EN=0.9
CITIES: Oslo (Downtown), Bergen (Harbor), Stavanger (Industrial), Trondheim (University), Tromso (Resort)
CRISIS_FLAVOR: Oil price sensitivity, environmental protests, extreme weather
NOTES: Highest Healthcare demand of all Tier 5 countries. Very expensive but massive margin.
```

### Austria
```
TIER: 5 | UNLOCK: $80M | COST: $9.5M | WEALTH: 1.5
DEMAND: FF=0.9 TC=1.3 FS=1.5 HC=1.7 EN=1.2
CITIES: Vienna (Luxury), Graz (University), Linz (Industrial), Salzburg (Resort), Innsbruck (Downtown)
CRISIS_FLAVOR: Regulatory compliance, labor disputes, high overhead
NOTES: Vienna Luxury top tier for Fashion. Salzburg Resort for Entertainment.
```

### Belgium
```
TIER: 5 | UNLOCK: $80M | COST: $9M | WEALTH: 1.4
DEMAND: FF=1.0 TC=1.4 FS=1.4 HC=1.5 EN=1.1
CITIES: Brussels (Downtown), Antwerp (Harbor), Ghent (University), Bruges (Resort), Liege (Industrial)
CRISIS_FLAVOR: EU regulatory changes, political complexity, logistics disruption
NOTES: EU headquarters means unique "Policy Windfall" opportunity events more frequent.
```

### Portugal
```
TIER: 5 | UNLOCK: $75M | COST: $8M | WEALTH: 1.1
DEMAND: FF=1.0 TC=1.3 FS=1.3 HC=1.3 EN=1.4
CITIES: Lisbon (Downtown), Porto (Harbor), Algarve (Resort), Braga (University), Setubal (Industrial)
CRISIS_FLAVOR: Tourism volatility, brain drain crisis, infrastructure aging
NOTES: Algarve Resort strong for Fashion + Entertainment Seasonal. Growing tech scene.
```

---

## TIER 6 — ENDGAME ($500M milestone | $30M-$60M unlock cost)

### Ethiopia
```
TIER: 6 | UNLOCK: $500M | COST: $30M | WEALTH: 0.4
DEMAND: FF=1.6 TC=0.6 FS=0.7 HC=0.8 EN=0.8
CITIES: Addis Ababa (Mall), Dire Dawa (Industrial), Bahir Dar (Downtown), Hawassa (University), Adama (Airport)
CRISIS_FLAVOR: Infrastructure failure, political instability, drought events, supply breakdown
NOTES: Massive population, very low wealth. Fast Food at high volume but thin margins.
```

### Peru
```
TIER: 6 | UNLOCK: $500M | COST: $32M | WEALTH: 0.7
DEMAND: FF=1.4 TC=0.9 FS=1.2 HC=1.1 EN=1.3
CITIES: Lima (Downtown), Cusco (Resort), Arequipa (Industrial), Trujillo (Mall), Piura (Harbor)
CRISIS_FLAVOR: Political instability, mining strikes, infrastructure gaps
NOTES: Cusco Resort has "Machu Picchu Tourism Boost" for Entertainment Seasonal (+20%).
```

### New Zealand
```
TIER: 6 | UNLOCK: $500M | COST: $40M | WEALTH: 1.4
DEMAND: FF=1.2 TC=1.3 FS=1.1 HC=1.6 EN=1.4
CITIES: Auckland (Harbor), Wellington (Downtown), Christchurch (Mall), Queenstown (Resort), Hamilton (University)
CRISIS_FLAVOR: Earthquake events, isolation logistics, environmental protests
NOTES: Queenstown Resort has the highest base quality retention in the game (quality decays 50% slower).
```

### Greece
```
TIER: 6 | UNLOCK: $500M | COST: $35M | WEALTH: 1.0
DEMAND: FF=1.1 TC=1.0 FS=1.3 HC=1.2 EN=1.6
CITIES: Athens (Downtown), Thessaloniki (Harbor), Crete (Resort), Mykonos (Luxury), Patras (Industrial)
CRISIS_FLAVOR: Economic volatility, political protests, tourism seasonality
NOTES: Mykonos Luxury gives highest seasonal bonus in the game for Fashion (+30% during seasonal events).
```

### Romania
```
TIER: 6 | UNLOCK: $500M | COST: $30M | WEALTH: 0.8
DEMAND: FF=1.3 TC=1.4 FS=1.0 HC=1.2 EN=1.0
CITIES: Bucharest (Downtown), Cluj-Napoca (Tech Campus), Timisoara (Industrial), Iasi (University), Constanta (Harbor)
CRISIS_FLAVOR: Political uncertainty, infrastructure gaps, EU compliance costs
NOTES: Cluj-Napoca Tech Campus growing tech hub. Hidden gem for Tech in Tier 6.
```

### Czech Republic
```
TIER: 6 | UNLOCK: $500M | COST: $32M | WEALTH: 1.1
DEMAND: FF=1.2 TC=1.4 FS=1.1 HC=1.3 EN=1.2
CITIES: Prague (Downtown), Brno (University), Ostrava (Industrial), Plzen (Mall), Liberec (Airport)
CRISIS_FLAVOR: Regulatory compliance, labor cost increases, supply chain disruption
NOTES: Prague Downtown has tourism bonus for Entertainment. Good all-rounder in Tier 6.
```

### Ukraine
```
TIER: 6 | UNLOCK: $500M | COST: $28M | WEALTH: 0.6
DEMAND: FF=1.3 TC=1.5 FS=0.9 HC=1.1 EN=1.0
CITIES: Kyiv (Downtown), Lviv (University), Odessa (Harbor), Kharkiv (Tech Campus), Dnipro (Industrial)
CRISIS_FLAVOR: Geopolitical instability (high frequency), infrastructure damage, logistics breakdown
NOTES: High risk. Kharkiv Tech Campus strong for Tech. Cheapest Tier 6 unlock.
```

### Kazakhstan
```
TIER: 6 | UNLOCK: $500M | COST: $35M | WEALTH: 0.8
DEMAND: FF=1.4 TC=1.0 FS=0.9 HC=1.1 EN=1.0
CITIES: Almaty (Downtown), Nur-Sultan (Airport), Shymkent (Mall), Aktau (Harbor), Karaganda (Industrial)
CRISIS_FLAVOR: Political instability, oil price impact, infrastructure gaps
NOTES: Nur-Sultan Airport has unique "Silk Road Hub" bonus (+10% all income logistics bonus).
```

### Sri Lanka
```
TIER: 6 | UNLOCK: $500M | COST: $30M | WEALTH: 0.5
DEMAND: FF=1.3 TC=0.9 FS=1.4 HC=1.0 EN=1.3
CITIES: Colombo (Harbor), Kandy (Resort), Negombo (Mall), Jaffna (Downtown), Galle (University)
CRISIS_FLAVOR: Economic crisis, political instability, tourism disruption
NOTES: Fashion higher than expected due to textile manufacturing heritage.
```

### Myanmar
```
TIER: 6 | UNLOCK: $500M | COST: $28M | WEALTH: 0.4
DEMAND: FF=1.5 TC=0.6 FS=1.1 HC=0.7 EN=0.8
CITIES: Yangon (Mall), Mandalay (Downtown), Naypyidaw (Airport), Bago (Industrial), Mawlamyine (Harbor)
CRISIS_FLAVOR: Political instability (very high), sanctions risk, infrastructure failure, supply breakdown
NOTES: Cheapest + highest risk Tier 6 country. Fast Food volume significant if crises managed.
```

---

# SECTION 5: BRANCH SYSTEM

## Branch Data Structure
```
Each branch contains:
  id:           GUID (auto-generated)
  cityId:       string (city config reference)
  countryId:    string (country config reference)
  level:        integer 1-10
  path:         string ("volume" | "premium" | "seasonal" | nil)
  pathTier:     integer 1-5 (sub-upgrades within path)
  quality:      integer 0-100
  staffSlots:   integer (base 2, increases with upgrades)
  openedAt:     Unix timestamp
  renovatedAt:  Unix timestamp
```

## Branch Opening Costs by Industry and Tier

```
TIER 1-2 COUNTRIES:
  Fast Food:     $15,000 base
  Tech:          $35,000 base
  Fashion:       $22,000 base
  Healthcare:    $45,000 base
  Entertainment: $55,000 base

TIER 3 COUNTRIES:      multiply base × 3
TIER 4 COUNTRIES:      multiply base × 8
TIER 5 COUNTRIES:      multiply base × 25
TIER 6 COUNTRIES:      multiply base × 80
```

## Branch Level Upgrade Costs (multiplier on base open cost)

```
LEVEL  | COST MULTIPLIER | INCOME MULT | STAFF SLOTS | NOTES
  1    |   1.0× (open)   |    1.00×    |     2       | Starting state
  2    |   0.8×          |    1.25×    |     2       | First upgrade
  3    |   1.2×          |    1.55×    |     3       | Staff slot unlocked
  4    |   1.8×          |    1.90×    |     3       |
  5    |   2.7×          |    2.30×    |     4       | Staff slot unlocked
  6    |   4.0×          |    2.80×    |     4       |
  7    |   6.0×          |    3.40×    |     5       | Staff slot unlocked
  8    |   9.0×          |    4.10×    |     5       |
  9    |   13.5×         |    4.95×    |     6       | Staff slot unlocked
  10   |   20.0×         |    6.00×    |     6       | Maximum level
```

## Upgrade Paths

### VOLUME PATH
```
Focus:     Maximum customers, lower margin per customer
Bonus:     +15% income per staff assigned to this branch (stacks)
Best for:  Countries with high demand multiplier (India, Indonesia, Brazil, etc.)
           Fast Food and Healthcare industries

SUB-UPGRADES (one chosen per tier unlock, 5 tiers):
  Tier 1 — Choose one of:
    Express Queue:         +8% volume throughput
    Combo Deal Boards:     +6% revenue per customer
    Self-Service Station:  Remove 1 required staff slot

  Tier 2 — Choose one of:
    Drive-Through Lane:    +12% throughput (Fast Food only: +18%)
    Bulk Purchase Deals:   -8% overhead cost
    Extended Hours:        +10% income (offline hours count extra)

  Tier 3 — Choose one of:
    Digital Order System:  +15% volume, -5% staff morale decay
    Loyalty Card Program:  +10% revenue, +5 brand score
    Second Location Wing:  +20% income but +1 required staff slot

  Tier 4 — Choose one of:
    Automated Checkout:    -2 required staff slots (min 1)
    Regional Supply Hub:   -15% branch overhead cost
    Flash Sale System:     Income × 1.5 for 10 min every 2 hours

  Tier 5 — Choose one of:
    Full Automation Suite: -1 required staff slot, +5% income
    Volume Leader Bonus:   If this is top-earning branch, +25% income
    Franchise Licensing:   This branch generates passive passive franchise fee income equal to 5% of its base income (stackable across all Volume branches)
```

### PREMIUM PATH
```
Focus:     Fewer customers, much higher margin per customer
Bonus:     +0.4× income multiplier per executive tier owned (COO/CMO/CFO/CTO each count)
Best for:  Wealthy countries (Switzerland, UAE, Norway, Singapore)
           Fashion and Tech industries, Premium city locations (Luxury, Resort)

SUB-UPGRADES (5 tiers):
  Tier 1 — Choose one of:
    VIP Lounge:            +20% revenue per customer
    Concierge Service:     +15% customer satisfaction (quality decays 20% slower)
    Members-Only Entry:    +10% income, +3 brand score/month

  Tier 2 — Choose one of:
    Private Consultation:  +18% margin (Healthcare: +25%)
    Premium Packaging:     +12% revenue, +5 brand score (Fashion: +20%)
    Curated Experience:    +15% income, -20% crisis chance

  Tier 3 — Choose one of:
    Exclusive Membership Club: +25% income from repeat customers
    Bespoke Service Line:      +22% margin, requires 1 extra staff slot
    Executive Partnership:     +30% income but only if COO or CMO is hired

  Tier 4 — Choose one of:
    Personal Shopper / Advisor: +30% margin (Fashion/Healthcare)
    White Glove Delivery:      +20% income + immune to quality-based crisis
    Ultra Luxury Rebrand:       +40% income but brand score must stay above 70

  Tier 5 — Choose one of:
    Invitation-Only Tier:  +50% income from top 10% customers (simulated)
    Celebrity Ambassador:  +35% income + +10 brand score (CMO required)
    Flagship Status:       This branch grants +2% income to all other Premium branches
```

### SEASONAL PATH
```
Focus:     Low baseline, massive spikes during seasonal events
Bonus:     ×3.0 income during active seasonal events (×4.0 for Entertainment)
Best for:  Resort city slots, Entertainment industry, Fashion seasonal events

SUB-UPGRADES (5 tiers):
  Tier 1 — Choose one of:
    Holiday Decoration:     +30% during events, -5% baseline
    Event-Ready Layout:     -20% setup cost for next event upgrade tier
    Pop-Up Flexibility:     Can switch between event types without upgrade cost

  Tier 2 — Choose one of:
    Limited Edition Products:  +40% revenue during events
    Event Staffing Contract:   No morale decay during event periods
    Advance Ticketing System:  Income starts 2 hours before event officially begins

  Tier 3 — Choose one of:
    Seasonal Brand Identity:  +50% during events + +5 brand score per event
    Cross-Season Strategy:    Baseline income is 0.8× instead of 0.5× (safer floor)
    Flash Collab Drop:        One random opportunity event fires per season (extra income spike)

  Tier 4 — Choose one of:
    Event Anchor Status:       This branch gets the highest event multiplier on the server (×3.5 base instead of ×3)
    Multi-Season Package Deal: Income spikes last 50% longer
    Viral Moment Machine:      15% chance each event creates a "Breaking News" level viral spike

  Tier 5 — Choose one of:
    Year-Round Festival:   Branch generates 1.2× income even outside events
    Legendary Seasonal:    ×5.0 multiplier during events (max in game)
    Event Empire Network:  If 3+ Seasonal branches active globally, all get +20% event bonus
```

## City Slot Types and Bonuses

```
AIRPORT:
  Bonus: +8% all income (high foot traffic, diverse customers)
  Special: +5% offline income (operates while you sleep)
  Best for: All industries equally

MALL:
  Bonus: +6% volume income, +3% all income
  Special: -10% staff morale decay (pleasant working environment)
  Best for: Fast Food, Fashion, Entertainment

DOWNTOWN:
  Bonus: +5% all income (central business district)
  Special: +5% brand score gain rate
  Best for: Tech, Healthcare

LUXURY DISTRICT:
  Bonus: +25% Premium path income
  Special: Immune to quality-based reputation damage
  Best for: Fashion, Healthcare Premium path

RESORT:
  Bonus: +50% Seasonal path event multiplier
  Special: +10% Entertainment income always
  Best for: Entertainment, Fashion Seasonal, Healthcare Premium

INDUSTRIAL:
  Bonus: -15% branch overhead cost
  Special: +10% Volume path income
  Best for: Fast Food Volume, Healthcare (cost savings)

UNIVERSITY:
  Bonus: -15% staff hire cost
  Special: +10% R&D research speed (per University slot owned)
  Best for: Tech, Healthcare

TECH CAMPUS:
  Bonus: +20% Tech industry income
  Special: +15% R&D research speed
  Best for: Tech only (massive bonus)

HARBOR:
  Bonus: +10% offline income, +5% all income
  Special: -10% supply chain crisis chance
  Best for: Fast Food, Healthcare (supply chain sensitive)

ENTERTAINMENT DISTRICT:
  Bonus: +20% Entertainment income, +10% Seasonal multiplier
  Special: Viral opportunity events 25% more frequent
  Best for: Entertainment only
```

## Branch Quality System

```
Starting quality:  75
Quality cap:       100
Quality floor:     0

DECAY RATE:
  Base:            -1 per real hour
  COO T1 hired:    -0.7 per hour
  COO T2 hired:    -0.5 per hour
  COO T3 hired:    -0.3 per hour
  Research: Predictive Maintenance completed: further -0.2/hr

INCOME MULTIPLIER FROM QUALITY:
  Quality 90-100:  ×1.20
  Quality 70-89:   ×1.10
  Quality 50-69:   ×1.00
  Quality 30-49:   ×0.85
  Quality 10-29:   ×0.70
  Quality 0-9:     ×0.50

RENOVATION:
  Cost:     30% of branch market value
  Effect:   Quality instantly reset to 100
  Cooldown: None

QUALITY EFFECTS ON BRAND SCORE:
  Average quality below 50: -1 brand score per day
  Average quality above 80: +0.5 brand score per day
```

---

# SECTION 6: STAFF SYSTEM

## Staff Data Structure
```
Each staff member:
  id:           GUID
  name:         string (from name pool, see below)
  specialty:    string (from specialty list)
  level:        integer 1-4
  morale:       integer 0-100
  branchId:     GUID or array of GUIDs (Regional VP can have 3)
  hiredAt:      Unix timestamp
  transferredAt: Unix timestamp (cooldown tracker)
  quitTimer:    Unix timestamp or nil
```

## Staff Name Pool (150 names across genders/cultures)
```
WESTERN:
  Emma, Liam, Sophia, Noah, Olivia, James, Ava, William, Isabella, Oliver,
  Mia, Benjamin, Charlotte, Elijah, Amelia, Lucas, Harper, Mason, Evelyn,
  Logan, Abigail, Ethan, Emily, Aiden, Elizabeth, Jackson, Sofia, Sebastian,
  Avery, Mateo, Ella, Jack, Madison, Owen, Scarlett, Theodore, Victoria,
  Luke, Aria, Jayden, Grace, Dylan, Chloe, Grayson, Penelope, Levi, Riley

LATIN:
  Carlos, Maria, Jose, Ana, Luis, Rosa, Miguel, Carmen, Pedro, Elena,
  Diego, Gabriela, Rafael, Isabella, Fernando, Valentina, Alejandro, Camila,
  Juan, Sofia, Ricardo, Lucia, Eduardo, Paula, Andres, Natalia

ASIAN:
  Wei, Yuki, Raj, Priya, Jin, Mei, Arjun, Sakura, Chen, Aiko, Vikram, Yuna,
  Sanjay, Hana, Akira, Preethi, Kento, Ananya, Takeshi, Divya, Hiroshi, Mio,
  Ravi, Yuna, Kenji, Pooja, Haruto, Nisha, Daichi, Kavya

AFRICAN:
  Amara, Kofi, Nadia, Kwame, Zara, Chukwu, Fatima, Obinna, Aisha, Seun,
  Ngozi, Emeka, Adaeze, Yusuf, Kemi, Tunde, Bisi, Chidi, Funmi, Wale

MIDDLE EASTERN:
  Omar, Layla, Hassan, Nour, Ali, Yasmine, Karim, Dina, Tariq, Rania,
  Samir, Lina, Fadi, Mona, Ziad, Hala

EASTERN EUROPEAN:
  Alexei, Katya, Dmitri, Natasha, Pavel, Oksana, Ivan, Olga, Mikhail, Svetlana
```

## All Staff Specialties (15 types)

```
SPECIALTY 1 — Sales Expert
  Unlock Level:  1
  Drop Weight:   High (most common)
  L1 Bonus:      +12% branch revenue
  L2 Bonus:      +18% branch revenue
  L3 Bonus:      +25% branch revenue
  L4 Bonus:      +35% branch revenue (all 3 branches if Regional VP)
  Synergy:       Volume path (more customers to sell to)

SPECIALTY 2 — Cost Cutter
  Unlock Level:  1
  Drop Weight:   High
  L1 Bonus:      -10% branch overhead (net +10% effective income)
  L2 Bonus:      -15% overhead
  L3 Bonus:      -22% overhead
  L4 Bonus:      -30% overhead
  Synergy:       Any path, especially Healthcare (high overhead)

SPECIALTY 3 — Morale Booster
  Unlock Level:  1
  Drop Weight:   Medium
  L1 Bonus:      Halves morale decay for all staff in same branch
  L2 Bonus:      Stops morale decay entirely for branch (no decay while assigned)
  L3 Bonus:      Stops decay + restores 1 morale/hour to all branch staff
  L4 Bonus:      Restores 2 morale/hour + applies to 2 branches if Regional VP
  Synergy:       Any branch with high staff count

SPECIALTY 4 — Speed Demon
  Unlock Level:  1
  Drop Weight:   Medium
  L1 Bonus:      +15% Volume path throughput
  L2 Bonus:      +22% throughput
  L3 Bonus:      +30% throughput
  L4 Bonus:      +40% throughput
  Note:          No bonus on Premium or Seasonal paths
  Synergy:       Volume path + Airport/Mall locations

SPECIALTY 5 — Recruiter
  Unlock Level:  1
  Drop Weight:   Medium
  L1 Bonus:      -20% hire cost for new staff at same branch
  L2 Bonus:      -30% hire cost
  L3 Bonus:      -40% hire cost
  L4 Bonus:      -50% hire cost + -10% fire severance globally
  Synergy:       Branches you plan to build out fast

SPECIALTY 6 — Quality Inspector
  Unlock Level:  1
  Drop Weight:   Medium
  L1 Bonus:      Quality decays 30% slower in this branch
  L2 Bonus:      Quality decays 50% slower
  L3 Bonus:      Quality decays 70% slower + slow passive quality recovery (+0.3/hr)
  L4 Bonus:      Quality decays 80% slower + passive recovery +0.5/hr
  Synergy:       Premium path (quality crucial), Luxury/Resort locations

SPECIALTY 7 — Trainer
  Unlock Level:  2 (slightly rarer, unlocks at $5M)
  Drop Weight:   Low
  L1 Bonus:      -25% promotion cost for all staff in same branch
  L2 Bonus:      -35% promotion cost
  L3 Bonus:      -50% promotion cost
  L4 Bonus:      -50% cost + L4 Trainer enables other L4 promotions in branch to be instant
  Synergy:       Branches where you are actively leveling up your team

SPECIALTY 8 — Negotiator
  Unlock Level:  2
  Drop Weight:   Low
  L1 Bonus:      -15% cost to open new branches in same country
  L2 Bonus:      -20% country opening cost
  L3 Bonus:      -20% cost + -10% country unlock cost for one country
  L4 Bonus:      -25% all expansion costs while assigned
  Synergy:       Countries you are expanding heavily in

SPECIALTY 9 — Crisis Manager
  Unlock Level:  2
  Drop Weight:   Low
  L1 Bonus:      -25% damage from any crisis affecting this branch
  L2 Bonus:      -40% crisis damage
  L3 Bonus:      -50% crisis damage + extends crisis response window by 2 min
  L4 Bonus:      -60% crisis damage (stacks with Crisis Protocol R&D)
  Synergy:       High-crisis countries (Nigeria, Russia, Bangladesh, Argentina)

SPECIALTY 10 — Data Analyst
  Unlock Level:  3 (rare, unlocks at $25M)
  Drop Weight:   Low
  L1 Bonus:      +8% all income for this branch
  L2 Bonus:      +12% all income
  L3 Bonus:      +15% all income + reveals next board decision type in advance
  L4 Bonus:      +20% all income + 10% faster contract completion rate
  Synergy:       Any branch, especially Tech industry

SPECIALTY 11 — Social Media Manager
  Unlock Level:  2
  Drop Weight:   Low-Medium
  L1 Bonus:      +3 brand score per month passively
  L2 Bonus:      +5 brand score per month
  L3 Bonus:      +7 brand score per month + PR crisis chance -30%
  L4 Bonus:      +10 brand score per month (assigned branch acts as global SMM)
  Synergy:       Fashion and Entertainment industries

SPECIALTY 12 — Logistics Expert
  Unlock Level:  2
  Drop Weight:   Low-Medium
  L1 Bonus:      +15% offline income for this branch
  L2 Bonus:      +22% offline income
  L3 Bonus:      +30% offline income
  L4 Bonus:      +40% offline income (applies across all branches if Regional VP)
  Synergy:       Players who log in infrequently

SPECIALTY 13 — Customer Relations
  Unlock Level:  2
  Drop Weight:   Low-Medium
  L1 Bonus:      +10% investor contract reward value
  L2 Bonus:      +18% contract rewards
  L3 Bonus:      +25% contract rewards + generates 1 extra contract slot passively (every 2 days)
  L4 Bonus:      +35% contract rewards
  Synergy:       Contract-focused playstyle

SPECIALTY 14 — Finance Wizard
  Unlock Level:  3
  Drop Weight:   Very Low
  L1 Bonus:      +12% stock dividend income
  L2 Bonus:      +20% dividends + -5% stock purchase cost
  L3 Bonus:      +30% dividends + crash warnings appear 8 min before instead of 5
  L4 Bonus:      +40% dividends + immune to one stock crash per season
  Synergy:       Stock market-focused players

SPECIALTY 15 — Innovation Lead
  Unlock Level:  3
  Drop Weight:   Very Low (rarest specialty)
  L1 Bonus:      One extra R&D idea revealed in the R&D pool (not a slot, just an extra visible option)
  L2 Bonus:      -15% R&D research time
  L3 Bonus:      -25% R&D research time + can preview R&D bonus before starting research
  L4 Bonus:      -35% research time + all completed R&D bonuses are +10% stronger
  Synergy:       R&D-heavy strategy, pairs with CTO executive
```

## Promotion Tree

```
LEVEL 1 — Entry Level (base)
  Title:        [Industry-specific] (Team Member / Engineer / Stylist / Specialist / Creator)
  Cost:         Base (no cost, starting level)
  Specialty:    1× multiplier

LEVEL 2 — Shift Manager
  Cost:         $5,000
  Title:        Shift Manager / Senior Engineer / Lead Stylist / Senior Specialist / Lead Creator
  Specialty:    ×1.3 multiplier
  New Ability:  Can cover 2 branches (not just 1) when transferred

LEVEL 3 — Store Manager / Department Lead
  Cost:         $25,000
  Title:        Store Manager / Department Lead / Creative Director / Clinical Lead / Production Lead
  Specialty:    ×1.6 multiplier
  New Ability:  Morale never drops below 20 (personal floor)

LEVEL 4 — Regional VP
  Cost:         $100,000
  Title:        Regional VP / Principal Engineer / Regional Director / Medical Director / Executive Producer
  Specialty:    ×2.0 multiplier
  New Ability:  Oversees up to 3 branches simultaneously (bonus applies to all 3)
  Special:      Quitting protection — Regional VPs cannot quit, only be fired
```

## Morale System Details

```
STARTING MORALE:   80 (on hire)
MAXIMUM MORALE:    100

DECAY TRIGGERS (per 10 real minutes):
  Base decay:                   -2
  Branch quality < 50:          -1 extra
  Country in active crisis:     -1 extra
  Unresolved crisis > 30 min:   -2 extra
  No Morale Booster in branch:  base applies
  Morale Booster L1 present:    base halved (-1)
  Morale Booster L2 present:    no decay (0)
  Research: Loyalty App done:   all decay rates -30%
  Research: Employee Wellness:  quit risk eliminated (morale can hit 0 but no quit)

RECOVERY TRIGGERS:
  Pay Branch Bonus ($500 × staff count): All branch staff → 100 morale
  Morale Package dev product:            All staff globally → 100 morale
  Morale Booster L3/L4:                 +1/+2 morale per hour (passive recovery)
  Successful board decision "Team Day":  +20 morale all staff, 24h
  Opportunity event "Great Review":      +15 morale all staff in affected branch

QUIT SEQUENCE:
  Morale hits 0:                 10-minute grace timer starts
  Client notified at morale 10:  "Warning: [Name] is about to quit!"
  Client notified at morale 0:   "Crisis: [Name] is on the verge of quitting!"
  Timer expires at morale 0:     Staff removed, branch slot freed, -3 brand score
  Exception:                     Regional VP (L4) cannot quit
  Exception:                     Employee Wellness R&D: quit is blocked, morale floors at 1
```

## Staff Hire Costs by Level

```
Fresh hire (always Level 1):
  Base cost:     $2,000
  Recruiter L1:  $1,600
  Recruiter L2:  $1,400
  Recruiter L3:  $1,200
  Recruiter L4:  $1,000

Promotion costs:
  To Level 2:    $5,000  (×0.75 with Trainer L1, ×0.65 with Trainer L2)
  To Level 3:    $25,000
  To Level 4:    $100,000

Fire severance (cost to fire):
  Level 1:       $1,000
  Level 2:       $2,500
  Level 3:       $8,000
  Level 4:       $25,000

Transfer cooldown:   5 minutes (bonus halved during cooldown)
```

---

# SECTION 7: EXECUTIVE SYSTEM

All executives apply company-wide bonuses.
You have 4 slots: COO, CMO, CFO, CTO. Each must be hired separately.
Can only have one exec per role at a time.
Replacing costs new hire cost + 20% severance of old hire cost.

## COO — Chief Operating Officer

```
FOCUS: Operations, quality, overhead reduction

TIER 1 — Junior COO
  Cost:     $50,000
  Bonuses:
    - All branch overhead: -10% (net income +10%)
    - Quality decay rate:  -30% slower
    - Branch renovation:   -10% cost
  Unlocks:  Nothing new

TIER 2 — Senior COO
  Cost:     $200,000
  Bonuses:
    - All branch overhead: -18% (net income +18%)
    - Quality decay rate:  -50% slower
    - Branch renovation:   -20% cost
    - Branch opening cost: -10%
  Unlocks:  "Operational Excellence" board decision option

TIER 3 — Elite COO
  Cost:     $1,000,000
  Bonuses:
    - All branch overhead: -28% (net income +28%)
    - Quality decay rate:  -70% slower
    - Branch renovation:   -35% cost + branch renovation restores to 110 quality (temporary cap)
    - Branch opening cost: -20%
    - Staff quit chance:   -25%
  Unlocks:  "Zero Defect Protocol" (branches immune to quality-based crises for 48h, weekly use)
```

## CMO — Chief Marketing Officer

```
FOCUS: Brand, marketing, demand amplification

TIER 1 — Junior CMO
  Cost:     $50,000
  Bonuses:
    - Brand score cap:        raised to 110
    - Brand score on hire:    +5 immediate
    - All country demand:     +8% multiplier
    - PR Campaign cooldown:   48h → 36h
  Unlocks:  PR Campaign board action

TIER 2 — Senior CMO
  Cost:     $200,000
  Bonuses:
    - Brand score cap:        raised to 120
    - Brand score on hire:    +8 immediate
    - All country demand:     +15% multiplier
    - PR Campaign cooldown:   36h → 24h
    - PR Campaign cost:       $500k → $350k
    - Celebrity opportunity:  30% more frequent
  Unlocks:  "Market Domination" board decision option

TIER 3 — Elite CMO
  Cost:     $1,000,000
  Bonuses:
    - Brand score cap:        raised to 130 (income bonus for 101-130 score)
    - Brand score on hire:    +12 immediate
    - All country demand:     +25% multiplier
    - PR Campaign cooldown:   24h → 16h
    - PR Campaign cost:       $500k → $200k
    - Brand score gain rate:  +50% faster from all sources
    - Viral events:           50% more frequent
  Unlocks:  "Brand Legend" status (company name shown in gold on leaderboard)
```

## CFO — Chief Financial Officer

```
FOCUS: Offline income, contracts, financial stability

TIER 1 — Junior CFO
  Cost:     $50,000
  Bonuses:
    - Offline earnings cap:          8h → 12h
    - Investor contract rewards:     +20%
    - Stock purchase commission:     -10%
    - Market crash impact on cash:   -10%
  Unlocks:  "Financial Hedge" board decision option

TIER 2 — Senior CFO
  Cost:     $200,000
  Bonuses:
    - Offline earnings cap:          8h → 18h
    - Investor contract rewards:     +35%
    - Stock purchase commission:     -20%
    - Market crash impact on cash:   -20%
    - Active contract slots:         3 → 4
  Unlocks:  "Debt Leverage" board action (borrow $500k against future earnings)

TIER 3 — Elite CFO
  Cost:     $1,000,000
  Bonuses:
    - Offline earnings cap:          8h → 24h
    - Investor contract rewards:     +50%
    - Stock purchase commission:     -35%
    - Market crash impact on cash:   -40%
    - Active contract slots:         3 → 5
    - Dividend income:               +25%
  Unlocks:  "IPO Advantage" (IPO legacy multiplier increased from +0.10 to +0.15 per IPO)
```

## CTO — Chief Technology Officer

```
FOCUS: Research & Development speed, tech-related income

TIER 1 — Junior CTO
  Cost:     $50,000
  Bonuses:
    - R&D research speed:     +25% faster
    - R&D startup cost:       -15%
    - Tech industry income:   +10%
  Unlocks:  Nothing extra (base CTO)

TIER 2 — Senior CTO
  Cost:     $200,000
  Bonuses:
    - R&D research speed:     +50% faster
    - R&D startup cost:       -25%
    - Tech industry income:   +20%
    - University slot bonus:  +10% R&D speed per University city owned
  Unlocks:  Extra R&D slot (3 concurrent research slots)

TIER 3 — Elite CTO
  Cost:     $1,000,000
  Bonuses:
    - R&D research speed:     +75% faster
    - R&D startup cost:       -40%
    - Tech industry income:   +30%
    - University slot bonus:  +15% R&D speed per University city owned
    - R&D bonus strength:     All research bonuses are 20% stronger
  Unlocks:
    - 4th concurrent R&D slot (stacks with Extra R&D Slot gamepass)
    - "R&D Breakthrough" — once per season, complete any research project instantly
```

---

# SECTION 8: RESEARCH & DEVELOPMENT

## System Rules
```
Base concurrent slots:       2
With Extra R&D Slot pass:    3
With CTO T2:                 3 (stacks to 4 with pass)
With CTO T3 + pass:          4 (maximum)

Each project can only be completed ONCE per season.
Projects reset after IPO.
Offline completion: checked on login.
University city slots: each one you own adds R&D speed bonus.
```

## All R&D Projects (25 total)

```
PROJECT 1 — Signature Product / Service
  Available:    All industries (name changes)
  Fast Food:    "Secret Recipe Formula"
  Tech:         "Core Platform V2"
  Fashion:      "Iconic Signature Line"
  Healthcare:   "Proprietary Treatment Protocol"
  Entertainment:"Flagship IP Launch"
  Cost:         $25,000
  Duration:     60 min (45 with CTO T1, 30 with CTO T2, 15 with CTO T3)
  Effect:       +20% income all branches, permanent for season
  Category:     Income

PROJECT 2 — Loyalty App
  Available:    All industries
  Cost:         $35,000
  Duration:     75 min
  Effect:       -30% staff morale decay rate globally, permanent
  Category:     Staff

PROJECT 3 — Automation Suite
  Available:    All industries
  Cost:         $80,000
  Duration:     120 min
  Effect:       -1 required staff slot per branch (branches with 0 requirement still run fine)
  Category:     Operations

PROJECT 4 — Market Intelligence
  Available:    All industries
  Cost:         $15,000
  Duration:     30 min
  Effect:       Reveals all locked country demand multipliers before you unlock them
               (permanent, shown as hidden values revealed on world map)
  Category:     Strategy

PROJECT 5 — Crisis Response Protocol
  Available:    All industries
  Cost:         $45,000
  Duration:     75 min
  Effect:       -40% damage from all crisis events (cash penalty, brand penalty, income penalty)
  Category:     Defense

PROJECT 6 — Supply Chain Optimization
  Available:    All industries
  Cost:         $30,000
  Duration:     60 min
  Effect:       -15% branch opening cost globally, permanent
  Category:     Expansion

PROJECT 7 — Premium Experience Design
  Available:    All industries
  Cost:         $55,000
  Duration:     90 min
  Effect:       All Premium path branches: +0.30× additional income multiplier
  Category:     Income (Premium)

PROJECT 8 — Viral Marketing Campaign
  Available:    All industries
  Cost:         $20,000
  Duration:     45 min
  Effect:       One-time +25 brand score immediately on completion
  Category:     Brand

PROJECT 9 — AI Analytics Platform
  Available:    All industries
  Cost:         $100,000
  Duration:     150 min
  Effect:       +18% all income, permanent for season
  Note:         Cannot be started in same season as Signature Product
  Category:     Income

PROJECT 10 — Employee Wellness Program
  Available:    All industries
  Cost:         $40,000
  Duration:     90 min
  Effect:       Staff morale can never reach 0 (floors at 1). No staff can quit.
  Category:     Staff

PROJECT 11 — Green Initiative
  Available:    All industries
  Cost:         $35,000
  Duration:     75 min
  Effect:       +12 brand score immediately + government contract bonus (+20% contract reward)
  Category:     Brand + Contracts

PROJECT 12 — Mobile Application
  Available:    All industries
  Cost:         $50,000
  Duration:     90 min
  Effect:       +10% all income + offline earnings cap +2 hours
  Category:     Income + Offline

PROJECT 13 — Predictive Maintenance System
  Available:    All industries
  Cost:         $30,000
  Duration:     60 min
  Effect:       All branch quality restoration passive: +0.3 quality/hour all branches
               (replaces normal zero-recovery with slight passive recovery)
  Category:     Quality

PROJECT 14 — International Trade Deal
  Available:    All industries
  Cost:         $120,000
  Duration:     180 min
  Effect:       -30% unlock cost for all Tier 4 and Tier 5 countries
  Category:     Expansion

PROJECT 15 — Customer Satisfaction Score System
  Available:    All industries
  Cost:         $25,000
  Duration:     45 min
  Effect:       +20% investor contract reward value (stacks with CFO bonus)
  Category:     Contracts

PROJECT 16 — Franchise Training Kit
  Available:    All industries
  Cost:         $60,000
  Duration:     90 min
  Effect:       All staff specialty bonuses at all levels +20% stronger
  Category:     Staff

PROJECT 17 — Hostile Takeover Preparation
  Available:    All industries
  Cost:         $40,000
  Duration:     60 min
  Effect:       +15% takeover success rate + takeover response window extended to 8 min
  Category:     PvP

PROJECT 18 — Brand Refresh Campaign
  Available:    All industries
  Cost:         $20,000
  Duration:     40 min
  Effect:       +20 brand score immediately + brand score decay rate -50% for 7 days
  Category:     Brand

PROJECT 19 — Recipe Innovation (Fast Food exclusive)
  Available:    Fast Food only
  Cost:         $30,000
  Duration:     60 min
  Effect:       +20% Fast Food income on top of all other bonuses
  Category:     Income (Industry)

PROJECT 20 — Platform Launch (Tech exclusive)
  Available:    Tech only
  Cost:         $75,000
  Duration:     120 min
  Effect:       +30% Tech income on top of all other bonuses
  Category:     Income (Industry)

PROJECT 21 — Signature Collection (Fashion exclusive)
  Available:    Fashion only
  Cost:         $45,000
  Duration:     80 min
  Effect:       +25% Fashion income + Seasonal path event bonus +0.5× for Fashion branches
  Category:     Income (Industry)

PROJECT 22 — Clinical Excellence Protocol (Healthcare exclusive)
  Available:    Healthcare only
  Cost:         $80,000
  Duration:     100 min
  Effect:       +25% Healthcare income + immune to malpractice crises
  Category:     Income (Industry)

PROJECT 23 — Blockbuster Engine (Entertainment exclusive)
  Available:    Entertainment only
  Cost:         $60,000
  Duration:     90 min
  Effect:       +35% Seasonal path event bonus for Entertainment
               Seasonal events last 20% longer
  Category:     Income (Industry)

PROJECT 24 — Security Fortress (Tech exclusive / Universal crisis defense)
  Available:    All industries (effect varies)
  Cost:         $55,000
  Duration:     90 min
  Effect (Tech):     Immune to data breach and server outage crises permanently
  Effect (others):   -25% digital/regulatory crisis chance
  Category:     Defense

PROJECT 25 — Global Partnership Network
  Available:    All industries (unlocks at $100M cumulative revenue)
  Cost:         $200,000
  Duration:     240 min
  Effect:       -20% unlock cost for ALL remaining locked countries
               +5% income multiplier per Tier 5+ country you own a branch in
  Category:     Expansion + Income
```

---

# SECTION 9: BRAND REPUTATION SYSTEM

## Brand Score Overview
```
Range:      0 to 100 (110 with CMO T1, 120 with CMO T2, 130 with CMO T3)
Starting:   50
Display:    Progress bar in top bar + number on Dashboard
Effect:     Income multiplier 0.5× at 0, 1.2× at 100, up to 1.5× at 130 (CMO prestige)
Formula:    multiplier = 0.5 + (min(score, 100) / 100) × 0.7
            Above 100 (CMO prestige): each extra point adds +0.005 multiplier
```

## Events That RAISE Brand Score
```
Investor contract completed:          +5
Successful board decision:            +2 (most decisions)
Revenue milestone hit:                +3 ($1M), +5 ($10M), +8 ($100M), +12 ($1B)
Successful crisis response:           +8
Viral Marketing R&D completed:        +25 (one-time)
Brand Refresh R&D completed:          +20 (one-time)
Green Initiative R&D completed:       +12 (one-time)
PR Campaign board action:             +15 (48h cooldown)
Hiring CMO:                           +5 (T1), +8 (T2), +12 (T3)
Viral opportunity event:              +10 to +20 (varies)
Celebrity endorsement event accepted: +12
Social Media Manager L4 (monthly):    +10
Average branch quality > 80:          +0.5/day passive
Branch renovation completed:          +1 per renovation
Successful hostile takeover:          +5
Completing an IPO:                    +10 (reset at start of next season to 50)
Season pass holder weekly bonus:      +2/week
```

## Events That LOWER Brand Score
```
Average branch quality < 50:          -1/day passive
Staff member quits:                   -3 per quit
Stock crash (if you hold shares):     -5 per major crash
Failed crisis response:               -10 (mild) to -25 (severe)
Ignoring a crisis:                    same as failed + secondary crisis chance
Target of successful hostile takeover:-15
Second crisis triggered by ignoring:  -8
Knockoff scandal (Fashion crisis):    -18
Data breach (Tech crisis):            -15
Malpractice claim (Healthcare):       -20
Celebrity scandal (Entertainment):    -18
Food contamination scare (FF):        -22 (highest single event penalty)
Board decision — wrong choice:        -3 to -8 (depends on decision)
```

## Brand Score Tiers
```
130:   "Global Icon" — legendary status, gold name, unique breaking news variants
110-129: "Market Leader" — CMO prestige zone
90-109: "Trusted Brand" — above average multiplier
70-89:  "Reputable" — solid multiplier, most players operate here
50-69:  "Building" — average, starting zone
30-49:  "Struggling" — below average, crises more likely
10-29:  "At Risk" — significantly reduced income, hostile takeover vulnerable
0-9:    "Damaged" — minimum income floor, crisis magnet
```

---

# SECTION 10: STOCK MARKET SYSTEM

## Market Structure
```
5 Industry Indexes:
  FFIDX — Fast Food Industry Index
  TCIDX — Tech Industry Index
  FSIDX — Fashion Industry Index
  HCIDX — Healthcare Industry Index
  ENIDX — Entertainment Industry Index

Each index:
  Starting price:  $100 (all indexes start equal)
  Price history:   24h of 60-second candles stored
  Drift range:     ±2% per 60-second tick
  Momentum:        If 3 consecutive up ticks, +0.5% extra. If 3 down, -0.5%.
  Player pressure: Sell volume > 20% in 5 min = -2% modifier
  Crash modifier:  Applied during crash events

Player Company Stocks:
  Any player who lists their company appears in the "Companies" sub-tab
  Starting price:  netWorth / 1,000
  Updates:         Every 5 minutes based on revenue performance
  Dividend:        2% of listed player's income shared to shareholders proportionally
  Max shares out:  30% of company can be held by others (income floor protection)
```

## Crash Event Types
```
MINOR CRASH:
  Frequency:    Every 20-50 minutes (random)
  Affected:     1 index
  Severity:     -15% to -25% over 3 ticks
  Warning:      5 minutes before (standard)
  Recovery:     +1-2% positive drift for 10 ticks after

MODERATE CRASH:
  Frequency:    Every 60-90 minutes
  Affected:     1-2 indexes
  Severity:     -30% to -45% over 4 ticks
  Warning:      5 minutes before
  Recovery:     +1.5% drift for 15 ticks

MAJOR CRASH:
  Frequency:    Once per 3-4 hours
  Affected:     2-3 indexes
  Severity:     -50% to -65% over 5 ticks
  Warning:      5 minutes before (unless "sudden" variant, 10% chance)
  Recovery:     Slow, 20 ticks of +1% drift

INDUSTRY EVENT CRASH (triggered by in-game crises):
  Triggered by: Severe industry-wide crisis event (rare, 5% chance on severe crisis)
  Affected:     The industry matching the crisis type
  Severity:     -20% to -40%
  Warning:      Fires as part of the crisis news ticker (no separate warning)

CORRECTION:
  Frequency:    After 10+ consecutive up ticks on any index
  Type:         Natural market correction, not a "crash"
  Severity:     -5% to -15%
  No warning:   Natural price action, no news ticker entry
```

## Player Trading Rules
```
Buy stocks:       Fire "RequestBuyStock" { ticker, quantity }
                  Cost = currentPrice × quantity
                  Server deducts cash, adds to profile.stock.holdings

Sell stocks:      Fire "RequestSellStock" { ticker, quantity }
                  Revenue = currentPrice × quantity
                  Server removes from holdings, adds to cash

Portfolio view:   Shows quantity held, average buy price, current value, P&L (green/red)

Tax (optional feature):  0% in-game tax (no tax mechanic — keep it simple)

Stock limit per player:  Max 1,000 units of any single stock (prevents corner-the-market)

Listing your company:
  Requirement:  Net worth > $500,000
  Effect:       Your company appears in "Companies" sub-tab
  Other players can buy up to 30% of your company shares
  You receive upfront listing fee: 5% of initial market cap
  Downside: Shareholders receive 2% of your income distributed proportionally
  Delist option: Pay back shareholders at current price + 10% premium
```

---

# SECTION 11: BOARD DECISIONS (65 Types)

Each day, 3 decisions are randomly selected from this pool (4 with Season Pass).
Decisions are seeded by playerID + date for consistency across sessions.
Format: DECISION NAME | Option A | Option B | Option C

---

## CATEGORY: Market Expansion (12 decisions)

```
1. ACCELERATED ENTRY
   "A new market is available ahead of schedule."
   A) Enter now at 2× normal unlock cost (gain market early)
   B) Wait 3 days for normal price (save cash)
   C) Skip this market entirely, focus resources elsewhere

2. REGIONAL DISTRIBUTION DEAL
   "A logistics firm offers a distribution partnership."
   A) Accept: -10% opening cost in one country for 30 days (+$20K fee)
   B) Negotiate: -5% cost but no fee (weaker deal, guaranteed)
   C) Decline

3. COMPETITOR TERRITORY
   "A rival is dominating a new country. Do you enter?"
   A) Enter aggressively — open 2 branches immediately (double cost, double speed)
   B) Enter cautiously — 1 branch at normal cost, observe rival
   C) Let rival keep it, focus on existing markets

4. CITY SLOT PREMIUM
   "A premium city slot is available at auction."
   A) Bid high: secure the Luxury slot at 2.5× normal price
   B) Bid moderate: 50% chance at 1.5× price, 50% miss
   C) Don't bid, let someone else have it

5. JOINT VENTURE
   "A local company offers a joint venture in [Country]."
   A) Accept: -40% opening cost but share 20% of that branch's income
   B) Decline: pay full price, keep 100% of income
   C) Counter-offer: -20% cost, share 10% income

6. FAST EXPANSION LOAN
   "A bank offers a $500K expansion loan."
   A) Accept: receive $500K cash now, repay $600K over 14 days (auto-deducted)
   B) Decline
   C) Partial: take $250K now, repay $295K over 7 days

7. MARKET RESEARCH OFFER
   "A consulting firm will reveal hidden demand data."
   A) Hire them ($15K): reveals demand multipliers for 5 random unchecked countries
   B) DIY: spend 2 board decision slots this week on research (free but slower)
   C) Skip research, expand based on intuition

8. FRANCHISE ZONE LICENSE
   "Government offers a special economic zone in [Country]."
   A) Buy license ($80K): all branches in that country get +15% income for 60 days
   B) Ignore
   C) Buy license + lobby ($120K): extend to 90 days

9. CITY RENOVATION DISTRICT
   "A city is undergoing renovation — slots temporarily cheaper."
   A) Open 2 branches now at -30% discount before renovation ends
   B) Open 1 branch at -30%
   C) Wait until renovation completes — slot type upgrades to better tier afterward

10. SATELLITE OFFICE CHAIN
    "Open 3 small satellite branches at reduced income for big discounts."
    A) Accept: 3 branches at 60% income but only 50% cost each
    B) Open 1 premium branch instead at full cost/income
    C) Decline

11. INTERNATIONAL TRADE BLOC
    "Joining a trade bloc reduces expansion costs in member countries."
    A) Join ($50K membership): -20% all expansion cost in 5 specific countries
    B) Negotiate: -10% in all countries for free (smaller benefit)
    C) Don't join, remain independent

12. STRATEGIC WITHDRAWAL
    "One of your low-performing branches is bleeding money in a crisis zone."
    A) Sell it for 30% market value now (clean exit)
    B) Invest $30K to stabilize and hold
    C) Redirect staff to another branch, close it for free (lose all value)
```

---

## CATEGORY: Staff & HR (12 decisions)

```
13. TALENT ACQUISITION
    "A headhunter has found an exceptional engineer / manager."
    A) Poach them ($25K): hire a Level 3 specialist of your choice of specialty
    B) Offer standard role: hire them at Level 2 for $8K
    C) Decline, rely on internal promotions

14. UNION DEMAND
    "Your staff union is making demands."
    A) Agree to all: morale +20 all staff, costs +$50K/month for 30 days
    B) Partial agreement: morale +8, costs +$20K/month for 15 days
    C) Refuse: morale -15, 30% chance of staff strike (2 staff quit immediately)

15. TEAM BUILDING DAY
    "A team retreat is available."
    A) Full retreat ($30K): all staff morale → 90 + 5-day morale decay pause
    B) Lunch event ($8K): all staff morale +20
    C) Virtual event ($2K): all staff morale +8, online format

16. STAR EMPLOYEE PROMOTION
    "Your top performer is due for a raise."
    A) Promote immediately + $5K bonus: morale +30 for them, +10 for whole team
    B) Promise promotion next month: morale +15 for them
    C) Ignore: morale -20 for them, 50% quit risk for that staff member

17. EXTERNAL TRAINING PROGRAM
    "A training institute offers company-wide upskilling."
    A) Full program ($40K): all staff specialty bonuses +15% for 30 days
    B) Partial ($15K): one branch's staff get +25% bonuses for 30 days
    C) Internal training instead: free but takes 7 days, +8% bonuses

18. STAFF REFERRAL SCHEME
    "Launch a referral program for new hires."
    A) Launch ($10K): next 5 hires get a free Specialty reroll (guaranteed non-common)
    B) Micro-referral ($3K): next 2 hires get reroll
    C) Decline

19. TALENT POACHING (by rival)
    "A rival company is trying to poach your best employee."
    A) Counter-offer ($20K raise for target): they stay, morale +25 for team
    B) Let them go: lose employee, gain $5K exit bonus from rival (they pay)
    C) Block poaching (legal threat): -$5K legal cost, 80% chance they stay

20. OVERTIME REQUEST
    "Your managers ask to approve overtime for a major push."
    A) Approve premium overtime (+50% cost): income +30% for 24h, morale -15
    B) Approve standard overtime (+20% cost): income +15% for 24h, morale -5
    C) Decline: no change

21. RESTRUCTURE PROPOSAL
    "A consultant suggests restructuring your staff hierarchy."
    A) Full restructure ($25K): reduces required staff slots by 1 globally for 30 days
    B) Partial ($10K): one country's branches need 1 fewer staff
    C) Decline

22. WELLNESS INITIATIVE
    "A wellness provider offers staff health programs."
    A) Full program ($15K): morale decay -20% for all staff for 30 days
    B) Meditation app only ($3K): morale decay -8% for 30 days
    C) Decline

23. PERFORMANCE REVIEW CYCLE
    "Annual review time — reward or rank-and-yank?"
    A) Reward top performers ($20K bonuses): morale +25 all, brand +3
    B) Rank-and-yank (fire bottom 10%): income efficiency +5% but morale -30
    C) Skip review: no change (opportunity cost)

24. REMOTE WORK POLICY
    "Staff push for remote / hybrid work options."
    A) Full remote: morale +15, income -5% (less in-person service quality)
    B) Hybrid 3/2: morale +8, no income change
    C) Office-first: morale -10, income +3% (forced productivity)
```

---

## CATEGORY: Financial Decisions (10 decisions)

```
25. DIVIDEND PAYOUT
    "Pay a company dividend to boost brand reputation."
    A) Large payout ($100K): brand score +8, attracts more investors to your stock
    B) Small payout ($30K): brand score +3
    C) No payout: save cash

26. DEBT RESTRUCTURING
    "Your CFO recommends restructuring debt for future expansion."
    A) Restructure (costs $10K): unlock ability to borrow $1M at 15% interest
    B) Minor restructure ($5K): $500K at 18% interest
    C) Decline: stay debt-free

27. EMERGENCY RESERVE FUND
    "Establish a reserve fund for crisis protection."
    A) Create $50K reserve: automatically absorbs next 2 crisis cash penalties
    B) Create $20K micro-reserve: absorbs next 1 crisis
    C) No reserve: invest all cash into expansion

28. REVENUE REINVESTMENT
    "Choose how to allocate this quarter's profits."
    A) Expansion fund: next 3 branch openings -20% cost
    B) Staff fund: next 10 hires -25% cost
    C) Operations fund: all renovations -30% for 14 days

29. TAX OPTIMIZATION
    "An accountant offers aggressive tax optimization."
    A) Full optimization ($15K fee): income +8% for 30 days, small crisis risk
    B) Standard optimization ($5K): income +3% for 30 days
    C) Decline: too much regulatory risk

30. SHARE BUYBACK
    "Buy back shares from public investors."
    A) Full buyback (at current price + 10%): end dividend drain, regain full income
    B) Partial buyback (50% of shares): reduce dividend by 50%
    C) Decline

31. EMERGENCY CAPITAL RAISE
    "Raise emergency capital by issuing bonds."
    A) Issue bonds: +$200K now, -2% income for 30 days (interest)
    B) Small issue: +$75K now, -0.5% income for 30 days
    C) Decline

32. COST AUDIT
    "A cost audit identifies inefficiencies."
    A) Act on all findings ($20K consultant fee): overhead -12% all branches for 60 days
    B) Act on some findings ($8K): overhead -5% for 30 days
    C) Ignore findings

33. INSURANCE PACKAGE
    "Business insurance offer for crisis protection."
    A) Full package ($25K/month): next crisis cash penalty zeroed out (covers one)
    B) Basic package ($8K/month): next crisis penalty -50%
    C) Self-insure: no cost, full crisis exposure

34. STRATEGIC INVESTMENT
    "Invest in a new market sector."
    A) $50K investment: +$75K return in 7 days (1.5× return, medium risk)
    B) $20K conservative: +$24K return in 7 days (1.2× return, low risk)
    C) Decline

```

---

## CATEGORY: Brand & Marketing (10 decisions)

```
35. CELEBRITY ENDORSEMENT
    "A celebrity wants to endorse your brand."
    A) Major deal ($80K): brand score +15, income +12% for 30 days, then possible scandal risk
    B) Micro-influencer ($15K): brand score +5, income +4% for 14 days, low risk
    C) Decline: save money

36. PR CAMPAIGN
    "Launch a targeted PR campaign." (Available only with CMO hired)
    A) National campaign ($200K): brand score +15 now, reaches all countries you're in
    B) Regional ($80K): brand score +8, applies to one region (e.g. Europe)
    C) Social media push ($20K): brand score +4, low cost

37. REBRANDING
    "Consider rebranding your company image."
    A) Full rebrand ($50K): lose 5 brand score short-term, gain 20 after 3 days
    B) Refresh ($20K): neutral short-term, +10 brand after 2 days
    C) Decline

38. CHARITY PARTNERSHIP
    "Partner with a charity for CSR benefit."
    A) Major commitment ($30K donation): brand score +10, +5 weekly for 4 weeks
    B) Small donation ($8K): brand score +3
    C) Decline

39. AWARDS CAMPAIGN
    "Campaign for an industry award."
    A) Major campaign ($25K): 70% chance of winning (+12 brand), 30% lose (-3 brand)
    B) Small campaign ($8K): 40% chance (+6 brand), 60% no change
    C) Let it happen organically: 15% chance (+4 brand) for free

40. CRISIS COMMUNICATIONS
    "You have an opportunity to get ahead of a potential scandal."
    A) Proactive statement ($10K PR): if scandal hits, damage -50%
    B) Prepare response ($3K): damage -20% if it hits
    C) Ignore: full damage if scandal fires

41. BRAND AMBASSADOR PROGRAM
    "Train your best staff as brand ambassadors."
    A) Full program ($20K): Social Media Manager bonus +50% for 30 days
    B) Lite program ($8K): +25% for 14 days
    C) Decline

42. COMPETITOR DEFAMATION DEFENSE
    "A rival is spreading negative press about your brand."
    A) Legal action ($15K): brand damage stopped, rival's brand score -10
    B) PR counter-response ($8K): brand damage halved
    C) Ignore and outperform: no immediate cost but brand -5 from the attack

43. VIRAL CONTENT PUSH
    "Your marketing team pitches a viral content strategy."
    A) Go all in ($25K): 60% chance of viral success (+18 brand, income +15% 48h), 40% flop (-3 brand)
    B) Safe push ($10K): 85% chance moderate success (+7 brand), 15% nothing
    C) Skip

44. SPONSORSHIP OPPORTUNITY
    "Sponsor a major global event."
    A) Title sponsor ($60K): brand score +12, +8% income for 7 days
    B) Supporting sponsor ($20K): brand score +5, +3% income for 7 days
    C) Decline
```

---

## CATEGORY: Operations (11 decisions)

```
45. QUALITY OVERHAUL
    "A quality improvement program is available."
    A) Company-wide ($40K): all branches +30 quality immediately
    B) Priority branches ($15K): top 3 branches by income +40 quality
    C) Renovate cheapest branches only ($8K): bottom 3 branches +50 quality

46. TECH UPGRADE
    "New operational technology is available."
    A) Full upgrade ($30K): branch income recalc speed improves, +5% all income
    B) Partial upgrade ($12K): +2% all income
    C) Decline

47. SUPPLY CHAIN REVIEW
    "Your supply chain is flagged for inefficiency."
    A) Full review + fix ($25K): supply chain crises -60% for 30 days
    B) Partial fix ($10K): -30% for 14 days
    C) Ignore: risk remains

48. ENERGY EFFICIENCY PROGRAM
    "Reduce energy consumption across branches."
    A) Install ($35K): overhead -8% permanently
    B) Partial install ($15K): overhead -3% permanently
    C) Decline

49. STANDARDIZATION INITIATIVE
    "Standardize processes across all branches."
    A) Full standard ($20K): quality floor raised to 30 (can't drop below 30)
    B) Partial: quality floor raised to 15
    C) Decline

50. EMERGENCY PROTOCOL UPDATE
    "Update crisis response procedures."
    A) Full update ($15K): all future crisis response windows +3 minutes
    B) Quick update ($5K): +1 minute
    C) Decline

51. BRANCH AUDIT
    "Order a full audit of your branches."
    A) Full audit ($10K): reveals which branch has the highest hidden inefficiency + fixes it
    B) Quick scan ($3K): reveals data only, no fix
    C) Decline

52. LOGISTICS PARTNERSHIP
    "A delivery company offers a partnership deal."
    A) Full deal ($20K/month): offline income +15% for 30 days
    B) Trial ($5K): offline income +5% for 7 days
    C) Decline

53. RENOVATION ROUND
    "Mass-renovate for a quality boost."
    A) All branches ($30K + 10K per branch): reset quality to 100 everywhere
    B) Top 5 branches only (scaled cost): reset top earners to 100
    C) One branch only (normal renovation cost)

54. PROCESS AUTOMATION PILOT
    "Pilot automation at one branch."
    A) Run pilot (free): branch income +10% for 14 days, if successful unlocks full automation choice
    B) Skip to full automation ($60K): all branches -1 required staff slot
    C) Decline

55. OPENING HOURS EXPANSION
    "Expand branch operating hours."
    A) 24/7 all branches ($25K): +15% income, staff morale -8
    B) Extended hours top 3 branches ($10K): +12% for those branches
    C) Current hours fine: no change
```

---

## CATEGORY: Competitive & Events (10 decisions)

```
56. HOSTILE TAKEOVER TARGET
    "You've identified a vulnerable rival."
    A) Launch takeover (costs 15% net worth, 40-70% success chance)
    B) Wait and observe: free, take action next opportunity
    C) Decline

57. DEFEND AGAINST TAKEOVER
    "A rival is attempting to acquire one of your branches."
    A) Hire legal defense ($30K): 80% chance attack fails
    B) PR counterattack ($15K): 50% defense, brand score +5 if successful
    C) Accept buyout: lose branch but receive 150% market value

58. PARTNERSHIP OFFER (from real player)
    "Another company has requested a merger discussion."
    A) Explore merger (leads to Corporation Mode prompt)
    B) Counter-offer: strategic alliance only (revenue sharing deal, 5%)
    C) Decline

59. INDUSTRY AWARD NOMINATION
    "Your company has been nominated for a prestigious award."
    A) Campaign hard ($20K): 70% win → +15 brand, news ticker
    B) Accept nomination only: 30% win → +8 brand, no campaign cost
    C) Withdraw nomination

60. MARKET DISRUPTION RESPONSE
    "A new competitor is disrupting your best market."
    A) Price war: reduce margin temporarily, income -10% for 14 days, rival slowed
    B) Quality push: invest $20K in quality upgrades, income +5% after 3 days
    C) Ignore and let market stabilize

61. INDUSTRY CONFERENCE SPONSORSHIP
    "Sponsor the Global [Industry] Conference."
    A) Title sponsor ($50K): +10 brand, +5% income for 7 days, networking bonus
    B) Exhibitor ($15K): +4 brand
    C) Attend only ($5K): +1 brand, intel on rival strategies

62. SEASONAL CAMPAIGN PLANNING
    "Plan your upcoming seasonal campaign."
    A) Max budget ($40K): Seasonal event multiplier +0.5× for next event
    B) Standard ($15K): +0.2× for next event
    C) No campaign: use base multiplier

63. MARKET CRASH RESPONSE
    "Markets are volatile. How do you respond?"
    A) Buy the dip ($100K into stocks): position for recovery profit
    B) Hold cash: safe, no action
    C) Diversify: sell 50% stock holdings, spread risk

64. COMPETITIVE INTELLIGENCE
    "Buy intel on your top rival."
    A) Full intel ($10K): see rival's brand score, top country, estimated net worth for 7 days
    B) Basic scan ($3K): see rival's brand score only
    C) Decline

65. CRISIS SIMULATION DRILL
    "Run a preparedness drill for potential crises."
    A) Full drill ($8K): next crisis response window +5 minutes + damage -15%
    B) Quick drill ($2K): +2 minute window only
    C) Decline
```

---

# SECTION 12: EVENTS & NEWS SYSTEM

## News Ticker Priorities
```
NORMAL (white text):    Routine business updates, minor events
WARNING (amber text):   Market volatility, morale warnings, approaching deadlines
BREAKING (red + pulse): Major crises, milestone hits, takeover attempts, market crashes
```

## All Crisis Event Types (45 total)

### Fast Food Crises
```
FF-1:  health_inspection_failure
       "Health inspection failed at [branch]."
       Mild: income -20% branch 48h, brand -5
       Severe: income -40% branch 72h, brand -15, $30K fine

FF-2:  supply_chain_shortage
       "[Ingredient] shortage affects [country] restaurants."
       Mild: income -15% all branches in country 24h
       Severe: income -30% 48h, branch renovation forced

FF-3:  food_contamination_scare
       "Food safety scare hits your brand in [country]."
       Mild: brand -10, income -20% 48h
       Severe: brand -22, income -35% 72h, $50K fine

FF-4:  staff_walkout
       "Staff at [branch] stage a walkout."
       Mild: branch offline for 30 min, morale -20 for that branch
       Severe: 3 staff quit, morale -30, income -0 (branch locked) for 2 hours

FF-5:  competitor_price_war
       "A rival launches aggressive pricing in [country]."
       Mild: demand multiplier -10% in country for 48h
       Severe: -20% for 72h + forces board decision to respond

FF-6:  equipment_breakdown
       "Critical equipment failure at [branch]."
       Mild: income -25% for 24h, $10K repair
       Severe: income -50% for 48h, $25K repair

FF-7:  delivery_delay
       "Logistics failure delays supply to [country] branches."
       Mild: income -10% all country branches 24h
       Severe: -25% 48h + offline income halved for 24h

FF-8:  bad_review_viral
       "A viral negative review is spreading about [branch]."
       Mild: brand -8, income -15% 24h
       Severe: brand -18, income -30% 48h

FF-9:  ingredient_price_spike
       "Key ingredient costs surge 40%."
       Mild: overhead +15% all branches 48h
       Severe: overhead +30% 72h, board decision forces response

FF-10: health_department_audit
       "Surprise audit by health authority."
       Mild: income -10% all branches during audit (6 hours)
       Severe: $40K compliance cost + branch closed for 4 hours
```

### Tech Crises
```
TC-1:  server_outage
       "Major server outage disrupts service."
       Mild: Tech income -35% 48h, brand -8
       Severe: Tech income -0% (shutdown) 4 hours, brand -15

TC-2:  data_breach
       "Customer data breach detected."
       Mild: brand -15, $30K fine, income -20% 72h
       Severe: brand -25, $80K fine, income -40% 72h + regulatory investigation trigger

TC-3:  security_vulnerability
       "Critical security flaw found in your system."
       Mild: $15K emergency patch cost, income -10% 24h
       Severe: $40K patch + 30% chance of data breach escalation

TC-4:  key_engineer_quit
       "Top engineer leaves for a competitor."
       Mild: income -10% one branch, lose one assigned staff member
       Severe: Regional VP quits (bypasses quit protection), income -20% 48h

TC-5:  product_launch_delay
       "Product launch delayed by technical issues."
       Mild: Seasonal event for Tech delayed 24h for your company
       Severe: Seasonal multiplier halved for next event

TC-6:  competitor_feature_copy
       "Rival copies your flagship feature."
       Mild: Tech demand -8% in 2 countries for 48h
       Severe: Tech demand -15% globally 72h + board decision forced

TC-7:  regulatory_investigation
       "Government investigating your tech practices."
       Mild: $25K legal fees, income -10% 48h
       Severe: $75K + 30-day income -15% + brand -10

TC-8:  bad_app_review
       "Flood of negative user reviews."
       Mild: brand -8, Tech income -15% 48h
       Severe: brand -18, -30% 72h

TC-9:  patent_dispute
       "Competitor files patent infringement suit."
       Mild: $20K settlement, no income impact
       Severe: $60K settlement + income -5% 30 days pending resolution

TC-10: AI_ethics_controversy
       "Media criticizes your AI practices."
       Mild: brand -10, income -10% 24h
       Severe: brand -20, CMO effectiveness halved for 7 days
```

### Fashion Crises
```
FS-1:  knockoff_scandal
FS-2:  influencer_fallout
FS-3:  trend_miss
FS-4:  fabric_shortage
FS-5:  sweatshop_accusation
FS-6:  celebrity_disassociation
FS-7:  fashion_week_disaster
FS-8:  viral_bad_review
FS-9:  return_rate_spike
FS-10: copyright_infringement
[Each follows same mild/severe format as above — same mechanical structure, different flavor text]
```

### Healthcare Crises
```
HC-1:  malpractice_claim
HC-2:  regulatory_audit
HC-3:  drug_supply_shortage
HC-4:  staff_burnout_mass
HC-5:  insurance_dispute
HC-6:  health_scandal
HC-7:  data_privacy_breach
HC-8:  inspection_failure
HC-9:  staff_union_strike
HC-10: competitor_undercutting
```

### Entertainment Crises
```
EN-1:  box_office_flop
EN-2:  streaming_rights_lost
EN-3:  celebrity_scandal
EN-4:  bad_critic_review
EN-5:  production_delay
EN-6:  copyright_lawsuit
EN-7:  audience_boycott
EN-8:  technical_failure_live
EN-9:  talent_dispute
EN-10: piracy_surge
```

### Universal/Country-Flavor Crises
```
UNI-1: natural_disaster (earthquakes, typhoons, floods — country-specific)
UNI-2: political_instability (election, coup, protest)
UNI-3: currency_devaluation (emerging markets)
UNI-4: power_outage (developing country logistics)
UNI-5: logistics_breakdown (supply chain, global)
```

## Crisis Response Options (all crises follow this structure)
```
OPTION A — PAY TO RESOLVE:
  Cost:    Scales with crisis severity ($5K-$80K)
  Effect:  Crisis ends immediately, brand score damage halved, income restored now
  Result:  Best outcome, costs money

OPTION B — RIDE IT OUT:
  Cost:    $0
  Effect:  Accept all damage for the stated duration
  Result:  Free but takes the full hit

OPTION C — IGNORE (only available for first 2 minutes of response window):
  Cost:    $0
  Effect:  Same as ride it out PLUS 50% chance of secondary crisis firing
  Result:  High risk, use only if cash is critical

CRISIS PROTOCOL R&D reduces all damage types by 40%.
CRISIS MANAGER staff specialty further reduces damage for affected branch.
```

## All Opportunity Event Types (20 types)
```
OPP-1:  viral_moment            Income +30% 20 min, brand +10
OPP-2:  celebrity_endorsement    Brand +12, income +8% 48h (cost $0 — they came to you)
OPP-3:  government_contract      Cash bonus equal to 30% monthly income, brand +5
OPP-4:  media_feature            Brand +15, income +5% 24h
OPP-5:  investor_windfall        $100K-$500K cash injection from investor
OPP-6:  competitor_bankruptcy    Demand in one country +20% for 72h
OPP-7:  trade_deal_bonus         Unlock cost of one country -50% for 24h
OPP-8:  staff_talent_walk-in     Free Level 2 specialist hire available (rare specialty)
OPP-9:  industry_event_spike     Seasonal path income +0.5× for next event
OPP-10: quality_award            Brand +8, quality all branches +10
OPP-11: research_breakthrough    One R&D project completes instantly
OPP-12: market_expansion_tip     Reveal best-performing country for your industry (hidden rank)
OPP-13: merger_interest          Another player approaches for Corporation Mode
OPP-14: patent_success           $50K cash + brand +5 (industry-specific)
OPP-15: community_recognition    Brand +10, local branch income +20% 48h
OPP-16: supply_deal              Branch opening cost -20% in one country for 7 days
OPP-17: talent_conference        Next 3 hires have guaranteed rare specialty
OPP-18: viral_product_launch     Entertainment/Fashion seasonal: immediate mini-event spike
OPP-19: regulatory_approval      Healthcare: new branch slot opens in restricted country
OPP-20: funding_round            Tech: $200K cash, no strings attached (simulates VC funding)
```

## Seasonal Events (12 global events per year in rotation)
```
EVENT 1:  HOLIDAY RUSH (December)
  Duration:  48 hours
  Effect:    Fast Food ×2.5, Entertainment ×3.5, all others ×1.5
  Seasonal path bonus: as listed × its multiplier

EVENT 2:  SUMMER SALE (July-August)
  Duration:  36 hours
  Effect:    Fashion ×2.5, Entertainment ×2.0, Fast Food ×1.8

EVENT 3:  TECH SUMMIT (March)
  Duration:  24 hours
  Effect:    Tech ×3.0, all others ×1.2

EVENT 4:  FASHION WEEK (February, September)
  Duration:  24 hours (fires twice per year)
  Effect:    Fashion ×3.5, Entertainment ×1.5

EVENT 5:  HEALTH AWARENESS MONTH (October)
  Duration:  72 hours
  Effect:    Healthcare ×2.0, all others ×1.1

EVENT 6:  GLOBAL ENTERTAINMENT AWARDS (April)
  Duration:  24 hours
  Effect:    Entertainment ×3.0, Fashion ×1.5

EVENT 7:  NEW YEAR LAUNCH (January 1)
  Duration:  24 hours
  Effect:    All industries ×1.8 (unique: universal event)

EVENT 8:  BACK TO SCHOOL (August)
  Duration:  24 hours
  Effect:    Fast Food ×1.6, Tech ×1.8

EVENT 9:  VALENTINES PUSH (February 14)
  Duration:  12 hours
  Effect:    Fashion ×2.0, Entertainment ×2.0, Fast Food ×1.5

EVENT 10: BLACK FRIDAY (November)
  Duration:  24 hours
  Effect:    Fast Food ×2.0, Fashion ×2.5, Entertainment ×1.8

EVENT 11: WORLD CUP / MAJOR SPORT EVENT (varies)
  Duration:  48 hours
  Effect:    Fast Food ×2.5, Entertainment ×3.0, all others ×1.3

EVENT 12: INNOVATION SHOWCASE (May)
  Duration:  24 hours
  Effect:    Tech ×2.5, Healthcare ×1.5
```

---

# SECTION 13: INVESTOR CONTRACTS

## Contract Slot Rules
```
Default slots:       3 active contracts
CFO T2 hired:        4 slots
CFO T3 hired:        5 slots
Refresh:             New contract generated when slot empties
Duration:            72 hours per contract (deadline from generation)
Auto-complete:       Yes (checked on login and every 5 minutes)
Scaling:             Requirements scale to 1.5× current revenue level
```

## All Contract Types (25 types)

```
CONTRACT 1:  REVENUE MILESTONE
  Requirement: Reach $X in cumulative revenue this session
  Reward:      30% of X as cash + brand +5
  Example:     "Reach $500K revenue" → $150K reward

CONTRACT 2:  BRANCH EXPANSION
  Requirement: Open X branches total
  Reward:      $X,000 × branch count + brand +3

CONTRACT 3:  GLOBAL REACH
  Requirement: Have active branches in X different countries
  Reward:      Large cash payout + brand +8

CONTRACT 4:  STAFF MILESTONE
  Requirement: Have X total staff employed
  Reward:      Cash + brand +4

CONTRACT 5:  QUALITY STANDARD
  Requirement: Maintain average branch quality above X for 24 hours
  Reward:      Cash + brand +6

CONTRACT 6:  BRAND TARGET
  Requirement: Reach brand score of X
  Reward:      Cash + unlock one extra PR Campaign charge

CONTRACT 7:  INCOME PER HOUR
  Requirement: Achieve $X income per hour
  Reward:      Cash + contract auto-activates 1 new slot for 24h

CONTRACT 8:  COUNTRY DOMINATION
  Requirement: Have X branches in a single country
  Reward:      +15% income in that country for 7 days + cash

CONTRACT 9:  EXECUTIVE HIRE
  Requirement: Hire any executive
  Reward:      Cash + executive hire cost partially refunded (20%)

CONTRACT 10: RESEARCH COMPLETE
  Requirement: Complete any 2 R&D projects
  Reward:      Cash + 1 free R&D slot for 48h

CONTRACT 11: SEASONAL PERFORMANCE
  Requirement: Earn $X during the next seasonal event
  Reward:      Large cash + Seasonal path bonus +0.5× permanent

CONTRACT 12: NET WORTH THRESHOLD
  Requirement: Reach net worth of $X
  Reward:      30% of threshold as cash

CONTRACT 13: STOCK INVESTMENT
  Requirement: Hold $X in total stock value
  Reward:      Cash + 1 crash immunity token

CONTRACT 14: MORALE STANDARD
  Requirement: Keep all staff above 50 morale for 12 hours
  Reward:      Cash + 3 days morale decay paused

CONTRACT 15: PREMIUM BRANCH MILESTONE
  Requirement: Have X branches on Premium path
  Reward:      Cash + all Premium branches +10% for 48h

CONTRACT 16: RENOVATION ROUND
  Requirement: Renovate X branches
  Reward:      Cash + 2 free renovations (waived cost)

CONTRACT 17: TAKEOVER SUCCESS
  Requirement: Successfully complete 1 hostile takeover
  Reward:      Large cash + brand +10

CONTRACT 18: CONTINENT COVERAGE
  Requirement: Have branches on 3 different continents
  Reward:      Very large cash + unlock "Global Mogul" dossier badge

CONTRACT 19: LUXURY SECTOR
  Requirement: Have X branches in Luxury District or Resort slots
  Reward:      Cash + Luxury slot income +15% for 7 days

CONTRACT 20: DAILY ENGAGEMENT
  Requirement: Log in for 5 consecutive days
  Reward:      Cash + brand +5

CONTRACT 21: CRISIS SURVIVAL
  Requirement: Survive X crises without letting brand score drop below 40
  Reward:      Cash + crisis damage -15% for 7 days

CONTRACT 22: INVESTOR CONFIDENCE
  Requirement: Complete 10 contracts this season
  Reward:      Permanent +5% contract reward boost for rest of season

CONTRACT 23: REGIONAL VP MILESTONE
  Requirement: Promote X staff to Regional VP (Level 4)
  Reward:      Cash + future promotion costs -20% for 30 days

CONTRACT 24: SEASONAL BRANCH
  Requirement: Have X branches on Seasonal path before next event
  Reward:      Cash + next seasonal event starts 2 hours early for you

CONTRACT 25: CORPORATION MILESTONE
  Requirement: (Corp Mode only) Corp net worth reaches $X
  Reward:      Both corp members receive cash + exclusive Corp Badge
```

---

# SECTION 14: SEASONAL & PRESTIGE SYSTEM

## Season Duration
```
Length:      30 real-world days per season
Timer:       Server-wide, same for all players (shared DataStore)
Countdown:   Shown in Leaderboard tab
End:         Season snapshot taken, leaderboard archived, new season begins
```

## IPO System
```
Requirement:    Cumulative revenue this season >= $500,000,000
Timing:         Can IPO at any point after requirement met (season still active)
Process:        Player chooses to IPO (voluntary, not forced at season end)
                Full-screen "IPO" animation (Breaking News style)
Resets:         cash → $250,000
                branches → empty
                staff → empty
                executives → empty
                research → empty (bonuses wiped)
                brand score → 50
                upgrades → all cleared
Preserved:      company name, logo, colors
                season.legacyMultiplier (increases per IPO)
                season.ipoCount (total IPOs across all seasons)
                season.badges (permanent collection)
                gamepass benefits
                Corp membership
```

## Legacy Multiplier
```
Starting value:    1.0× (no IPO)
Per IPO:           +0.10× added
CFO T3 bonus:      +0.15× per IPO instead of +0.10×

EXAMPLES:
  0 IPOs:    1.0×  (base game)
  1 IPO:     1.1×
  3 IPOs:    1.3×
  5 IPOs:    1.5×
  10 IPOs:   2.0×  (income doubled from the start of each run)
  20 IPOs:   3.0×  (endgame veterans — very fast runners)

Applied:    In IncomeService.Recalculate() as the first multiplier
```

## Season Pass Reward Track (20 tiers)
```
XP Sources:
  Contract completed:     +10 XP
  Board decision made:    +5 XP
  Revenue milestone:      +50 XP
  Crisis survived:        +8 XP
  Seasonal event active:  +15 XP
  Daily login:            +3 XP

TIER  | XP REQUIRED | REWARD
  1   |     25      | Exclusive branch name prefix "[Season 1]"
  2   |     60      | PR Campaign cost -10% for this season
  3   |     100     | 1 additional board decision per day for 7 days
  4   |     150     | Exclusive logo frame (season badge style)
  5   |     200     | Free branch renovation (1 use)
  6   |     275     | +5% all income for 48 hours
  7   |     350     | Exclusive branch skin (UI color theme for your branches)
  8   |     450     | Crisis response window +2 minutes for remainder of season
  9   |     550     | Free Regional VP promotion (1 use)
  10  |     700     | Exclusive company dossier background
  11  |     850     | +10 brand score immediate
  12  |    1000     | 1 free country unlock (any Tier 2 or 3 country)
  13  |    1200     | Staff morale decay paused for 72 hours
  14  |    1400     | 1 R&D project completed instantly
  15  |    1600     | Exclusive "Season [N] Champion" badge on dossier
  16  |    1900     | Income +15% for 7 days
  17  |    2200     | Free hostile takeover (covers cash cost, 1 use)
  18  |    2600     | Exclusive animated logo (season-unique animation style)
  19  |    3000     | Legacy multiplier bonus: +0.02× extra this IPO
  20  |    4000     | Exclusive "Season MVP" dossier title + golden leaderboard name
```

## Season End Rewards
```
Rank 1:    "Global Mogul" badge + 1000 XP next season + exclusive animated frame
Rank 2:    "Empire Builder" badge + 500 XP next season
Rank 3:    "Tycoon" badge + 250 XP next season
Ranks 4-10: "Top 10" seasonal badge
IPO Club:  "IPO [N]×" badge for completing N IPOs in a single season
```

---

# SECTION 15: SOCIAL FEATURES

## Corporation Mode

```
Max members:     2 players
Corp DataStore:  Separate from both players' personal profiles
Shared data:     economy, branches, staff, executives (corp-level only)
Solo data:       Each player keeps their personal profile unchanged

CREATE CORP:
  Player A fires "RequestCreateCorp" { name }
  Name is text-filtered
  CorpID generated (GUID)
  Stored in shared DataStore "Corporations"
  A gets role: "founder"

JOIN CORP:
  Player B gets the CorpID from Player A (shared out-of-game)
  B fires "RequestJoinCorp" { corpId }
  Server validates: corp has < 2 members, B has no existing corp
  B gets role: "partner"
  Corp immediately visible to both in Leaderboard → Corp tab

CORP ACTIONS:
  Both players can: open branches, hire staff, make board decisions, buy stock
  Race condition protection: 1-second session lock on Corp DataStore write
  Last-write-wins for simultaneous edits

LEAVING CORP:
  Either player can leave (founder or partner)
  On leave: that player's contributed assets stay with corp (don't transfer back)
  Remaining member becomes sole operator of corp
  Can recruit a new partner after 24-hour cooldown

CORP LEADERBOARD:
  Separate tab from Solo leaderboard
  Ranked by combined net worth: Member A net worth + Member B net worth + Corp assets
  Resets each season
  Corp badges awarded to both members for top 10 finishes
```

## Company Dossier

```
Visible to:   Any player who clicks another on the leaderboard
Contains:
  - Company name + logo + brand colors
  - Industry icon + industry name
  - Founded date (season + date)
  - Current brand score (with bar)
  - Total revenue all-time (across all seasons)
  - IPO count + legacy multiplier
  - All badges (permanent collection displayed as icons)
  - Recent 5 events (news ticker history, last 5 items)
  - Net worth (current season)
  - Corp membership (if in one)
  - Season rank (current)

VIP Dossier gamepass additions:
  - Animated logo (shimmer effect)
  - Gold animated border frame
  - Extended badge display (all-time)
  - "VIP" tag on dossier header
```

## Player Business Marketplace

```
Listing:
  Player selects a branch from their roster
  Sets asking price (50%-300% of market value allowed)
  Branch removed from their profile immediately (held in escrow)
  Listing expires after 72 hours if unsold (branch returned, no penalty)

Buying:
  Browse "Marketplace" section in Branches tab
  Listed branches shown with: country, city, level, path, quality, asking price
  Buy fires "RequestBuyBranch" { listingId }
  Cash deducted, branch added to buyer's roster
  Seller receives cash (minus 10% marketplace fee) even if offline

Branch escrow:
  The branch exists in the marketplace DataStore during listing
  Neither player nor marketplace can modify it during listing
  Returned if unsold after 72h

Rules:
  Max 3 branches listed per player at once
  Cannot list branches currently in crisis
  Price min: 50% market value (prevents spam listings)
  Price max: 300% market value (prevents price gouging)
```

## Leaderboard Details

```
SOLO LEADERBOARD:
  Ranked by:    Net worth (cash + branch values + stock portfolio)
  Updated:      Every 5 minutes via OrderedDataStore
  Display:      Top 10 real players + NPC rivals to fill gaps
  Your row:     Always shown (pinned at bottom if outside top 10, shows actual rank)
  Season:       Resets each season. Archive available for past 3 seasons.

CORP LEADERBOARD:
  Ranked by:    Combined corp net worth (both members + corp assets)
  Updated:      Every 5 minutes
  Display:      Top 10 active corps
  Separate tab: "Corp" tab next to "Solo" tab in Leaderboard screen

SEASON ARCHIVE:
  Button in Leaderboard tab: "Past Seasons ▾"
  Dropdown shows last 3 seasons
  Each shows snapshot of top 50 at season end
  Names are links to player dossiers (if available)
```

---

# SECTION 16: UNIQUE FEATURES

## Breaking News Moments

```
TRIGGERS (in order of game progression):
  $100K milestone:     "Your company has crossed $100 Thousand in revenue!"
  $500K milestone:     "Mogul Inc. is growing fast — $500K reached!"
  $1M milestone:       "BREAKING: [Company] crosses the million dollar mark."
  $5M milestone:       "Business is booming at [Company] — $5 Million!"
  $10M milestone:      "[Company] hits $10 Million revenue."
  $50M milestone:      "[Company] is now a $50 Million enterprise."
  $100M milestone:     "BREAKING: [Company] crosses $100 Million."
  $500M milestone:     "IPO threshold reached — [Company] valued at $500M+!"
  $1B milestone:       "BREAKING: [Company] is officially a Billionaire."
  $5B milestone:       "[Company] now worth $5 Billion."
  $10B milestone:      "BREAKING: [Company] crosses $10 Billion."
  $100B milestone:     "[Company] joins the global elite — $100 Billion!"
  $1T milestone:       "HISTORIC: [Company] reaches $1 Trillion. The world takes notice."
  First IPO:           "BREAKING: [Company] goes public. A new era begins."
  Each subsequent IPO: "Season [N] IPO complete. Legacy continues."
  First hostile takeover success: "BREAKING: [Company] acquires rival."
  First hostile takeover defense: "BREAKING: [Company] repels hostile bid."
  Corp formation:      "[Corp Name] Corporation is founded. Two giants unite."
  Rank #1 on leaderboard: "[Company] reaches #1. The top of the world."

VISUAL STYLE:
  Full-screen dark overlay (rgba 0,0,0,0.85)
  Centered card: 380px wide, dark navy background, sharp white border
  "BREAKING NEWS" red banner at top (uppercase, bold, red background)
  Company logo (your custom logo) displayed prominently
  Headline text: 22px bold white
  Sub-headline: 14px muted
  Industry icon shown
  Animated line sweep across bottom
  Auto-dismisses after 5 seconds with animated countdown bar
  Can be dismissed instantly by clicking anywhere
  Sound: none (Roblox audio restrictions) — rely on visual impact
```

## Login Summary Screen

```
TRIGGERS:    Shown if offline >= 5 minutes
SKIPPED:     First-ever login (tutorial replaces it)
             Offline < 5 minutes

CONTENT (lines appear one by one, 0.3s apart):
  Line 1:  "You were away for [Xh Ym]"                  (always shown)
  Line 2:  "💰 $X earned while you slept"               (if > $0)
  Line 3:  "🏢 X branches auto-opened"                  (if Regional Manager active)
  Line 4:  "✅ X contracts completed"                    (if any)
  Line 5:  "🔬 X research projects finished"             (if any)
  Line 6:  "⚡ X crises weathered (auto-responded)"      (if any)
  Line 7:  "📉 Staff morale dropped — check your team"  (if any staff below 40)
  Line 8:  "🏗️ Branch quality has decayed — renovate soon" (if avg quality < 60)
  Line 9:  "📈 Brand score changed: [±N]"               (if changed > 5 points)
  Line 10: "🏆 Your rank: #X this season"               (always shown)

VISUAL STYLE:
  Full-screen dark overlay
  Centered panel: clean card, max 360px wide
  Title: "Welcome back, [name]" in large text
  Lines: each slides in from left (translateX -20px → 0, opacity 0 → 1)
  After all lines: "Let's Go →" button pulses
  Background: subtle animated gradient (very slow color shift)
```

## Hostile Takeover System (Full Detail)

```
TARGETING:
  Can target: NPC rivals (always available)
               Listed players (those with brand score < 60 are highlighted as "vulnerable")

COST:
  Base cost:  15% of attacker's net worth
  With Takeover Token: 7.5% of net worth (halved)
  With Takeover Prep R&D: no cost reduction, but success rate +15%

SUCCESS CHANCE:
  Base:                  40%
  Target brand 0-20:     +25% (very vulnerable)
  Target brand 21-40:    +15%
  Target brand 41-60:    +5%
  Target brand 61-80:    -5%
  Target brand 81-100:   -15% (well-defended)
  Attacker brand > 80:   +5% (reputation gives credibility)
  R&D: Takeover Prep:    +15%
  Defender legal action: -30% (if defender chose "Legal Defense" in board decision)

SUCCESS OUTCOME:
  Attacker receives: defender's highest-income branch transferred to attacker
  Defender:          loses branch + brand score -15
  Attacker:          brand score +5
  News ticker:       "[Attacker] has acquired [branch] from [Defender]!"
  Breaking News:     fires for attacker (first takeover only)

FAILURE OUTCOME:
  Attacker:          loses the cash cost (not refunded)
  Defender:          brand score +3 (survived attack)
  Attacker:          brand score -2 (embarrassing failure)
  News ticker:       "Hostile takeover attempt by [Attacker] was repelled."

AGAINST AI RIVALS:
  Success chance:    60% (fixed, higher than player PvP)
  Success outcome:   AI revenue -20%, attacker gains cash bonus (10% of AI revenue)
  No branch transfer (AI doesn't have real branches)
  AI "recovers" over 30 minutes

COOLDOWN:
  24 hours between takeover attempts (per attacker)
  24 hours vulnerability window (defenders can see they were attacked in dossier for 24h)
```

---

# SECTION 17: UI SCREEN LAYOUTS

## TOP BAR (52px fixed, always visible)

```
LEFT SIDE (company identity):
  [Logo: 32×32px] [Company Name: 15px bold] [Industry icon: 16px]

CENTER-LEFT (financial):
  [Cash: green, large mono font] / [Revenue/hr: smaller, muted]
  Updates every 5 seconds via smooth counter animation

CENTER (brand):
  [Brand Score progress bar: 120px wide, 6px tall]
  [Score number above bar]
  Color: green >70, amber 40-70, red <40

CENTER-RIGHT (news ticker):
  [Scrolling text area: max 220px]
  [TweenService horizontal scroll]

RIGHT (utilities):
  [Save status icon + text: 11px]
  [Notification bell with badge count]
  [Shop button: icon-shopping-cart]
  [Settings button: icon-settings]
```

## BOTTOM NAVIGATION (60px fixed)

```
8 tabs, equal width, icon + label:
  [icon-layout-dashboard]  Dashboard
  [icon-building-store]    Branches
  [icon-users-group]       Staff
  [icon-tie]               Execs
  [icon-flask]             Research
  [icon-chart-candle]      Market
  [icon-clipboard-list]    Board
  [icon-trophy]            Rankings

Active tab: highlighted with industry theme color
Notification badge (red dot, white number) on:
  - Board: count of unresolved decisions
  - Staff: count of staff below 20 morale or about to quit
  - Research: count of completed research waiting to be viewed
  - Market: if a crash is imminent (warning)
```

## DASHBOARD TAB

```
LAYOUT (top to bottom):
  [Section: Overview cards — 2×2 grid]
    Card 1: Net Worth (large number, trend arrow vs last hour)
    Card 2: Revenue per Hour (with bar showing % of max possible)
    Card 3: Brand Score (progress bar + history sparkline)
    Card 4: Season Rank (rank number + name + days left in season)

  [Section: Top Branches]
    Header: "Top Earning Branches"
    3 mini cards: branch name, flag, city type, income/hr, quality bar
    "View all →" link to Branches tab

  [Section: Active Buffs]
    Scrollable horizontal list of active temporary effects
    Each shows: effect name, magnitude, time remaining countdown
    Empty state: "No active boosts" in muted text

  [Section: Recent Activity]
    Last 5 events from combined history (news, crises, board, contracts)
    Each item: icon, description, time ago
    "View all" → expands inline or opens full history modal
```

## BRANCHES TAB

```
LAYOUT:
  [Sub-tab: World Map | List View]

WORLD MAP VIEW:
  Large 2D illustrated world map (static ImageLabel background)
  Country nodes positioned at geographic locations
  Node states:
    Unlocked + branches: Filled circle, industry color, branch count badge
    Unlocked + no branches: Outlined circle, neutral
    Locked: Grayed circle with [icon-lock] icon
    Active crisis: Warning triangle overlay, amber pulse
  Clicking unlocked country: Opens City Slots panel (slide up from bottom)
  Clicking locked country: Opens Unlock Info panel

CITY SLOTS PANEL (slide-up modal):
  Country name + flag + wealth multiplier
  Grid of city slots (3-7 per country depending on country)
  Each slot card:
    [Slot icon: type] [City name] [City type badge]
    If empty: [Open Branch] button + cost shown
    If occupied: [Branch name] [Level badge] [Income/hr] [Manage →]
  Close button at top

LIST VIEW:
  All owned branches in scrollable list, grouped by country
  Sort options: Income (high→low), Country, Level, Quality
  Quick actions per row: Upgrade, Renovate, Manage

BRANCH DETAIL MODAL:
  Branch name (editable — player can name their branches)
  Country + city + type
  Current level [X/10] + Upgrade button with cost
  Upgrade path: if nil → "Choose Path" button opens path picker
                if set → show path name + sub-upgrade tier + next upgrade button
  Quality bar (color-coded) + Renovate button
  Staff assigned: list of names + specialty icons + morale bars
  Income contribution: $X/hr (this branch)
  Actions: [Upgrade] [Renovate] [Relocate] [Close Branch]
```

## STAFF TAB

```
LAYOUT:
  [Hire Summary bar at top: total staff, total slots, % filled]
  [Grouped by branch / country toggle]
  [Sort: by Morale (default, ascending to show at-risk first) / Level / Specialty]

STAFF LIST (grouped by branch):
  Branch header: [Branch name] [Country flag] [path icon] [Hire button if slots open]
  Staff row: [Name] [Specialty icon] [Level badge L1-L4] [Morale bar] [Promote] [Transfer] [Fire]
  Morale bar colors: green (60+), amber (30-59), red (0-29)
  "About to quit" state: red glow on row, warning text

HIRE POPUP:
  "Hiring for: [Branch Name]"
  Preview card: Random name + rolled specialty (with rarity label)
  Specialty probabilities shown as percentage bars
  [Reroll Preview] button (free, client-side only)
  [Hire for $2,000] button
  Note: actual specialty rolled on server (client preview is estimate only)

PROMOTE POPUP:
  Shows current level → next level
  Lists: specialty bonus increase (current → new)
  Cost shown clearly
  [Promote] [Cancel]

TRANSFER POPUP:
  Dropdown of available target branches (showing open slot count)
  5-minute settling cooldown warning shown
  [Transfer] [Cancel]
```

## EXECUTIVES TAB

```
LAYOUT: 2×2 grid of role cards

EACH CARD:
  Role name (COO / CMO / CFO / CTO) [VACANT or HIRED badge]
  If hired: Tier badge (T1/T2/T3), hired date, active bonuses list
  If vacant: "No executive" muted text, list of what hiring would unlock
  Action button: [Hire] or [Replace]
  
  Lock state: CTO locked until $5M revenue (shows progress bar to unlock)

HIRE MODAL:
  Role name header
  3 tier options as cards:
    Card: Tier label + cost + full bonus breakdown + "Hire" button
  Side-by-side comparison: clearly shows what each tier adds
  Replacing: shows severance cost prominently

BONUS DISPLAY:
  Each bonus shown as: [icon] [description] [value, highlighted in industry color]
  Live value shown where applicable: "COO T2: overhead -18% = +$X,XXX/hr currently"
```

## RESEARCH TAB

```
LAYOUT (3 sections):

ACTIVE RESEARCH:
  Header: "Researching (X/Y slots used)"
  Progress cards for each active project:
    [Project name] [Category badge]
    [Progress bar: animates from current % to new % on render]
    [Time remaining: countdown in H:MM:SS, client-side]
    [Complete Instantly — R&D Accelerator] button (prompts purchase if no accelerator)
    [Cancel Research] button (refunds 50% of startup cost)

AVAILABLE PROJECTS:
  Grid of project cards (2 columns):
    [Project name] [Duration] [Cost]
    [Short effect description]
    [Industry-exclusive badge if applicable]
    [Start Research] button (grayed if no slot, shows slot count)
    [Completed ✓] state if already done this season
  Filter buttons: All / Income / Staff / Brand / Defense / Industry

COMPLETED:
  Collapsible list of all completed research this season
  Each item: project name + bonus applied indicator
```

## STOCK MARKET TAB

```
LAYOUT (3 sub-tabs):

INDEXES:
  5 cards in a grid (2 columns, 1 full-width at bottom):
    Industry name + icon
    Current price (large mono font)
    24h change % (green/red with arrow)
    Mini sparkline chart (24h price history as bar heights)
    [Buy X units] input + [Buy] button
    Your holdings in this index (if any)

PORTFOLIO:
  Summary row: Total portfolio value, total P&L (green/red)
  List of holdings:
    Ticker + name | Quantity | Avg buy price | Current value | P&L
    [Sell] button per holding (opens quantity input)
  
  Listed company holding section:
    If you own shares in other players' companies, shown here
    Dividend income shown: "+$X/hr passive"

COMPANIES:
  Listed player companies (those who chose to list):
    Company name + logo | Industry | Current share price | Your holdings
    [Buy] button
  NPC rivals section (below):
    NPC name + industry | Simulated stock price | [Buy] button
```

## BOARD TAB

```
LAYOUT (3 sections):

TODAY'S DECISIONS:
  Decision card (one per active decision):
    [Decision title] [Category badge: Expansion / HR / Financial / Brand / Operations / Competitive]
    Description text (2-3 lines)
    [Option A] [Option B] [Option C] buttons (2-3 per decision)
    Each option shows: label + short consequence preview on hover/long-press
    Resolved decisions: chosen option shown in grayed card with result text
  Header shows: "3 decisions • Refreshes in Xh Ym"

ACTIVE CONTRACTS:
  Contract card (one per active contract):
    [Contract title] [Progress bar] [Deadline countdown]
    Current value vs requirement (e.g. "Revenue: $2.1M / $3.0M")
    Reward shown: "Reward: $900K + brand +5"
    [Complete] button shown when requirement met

BOARD HISTORY:
  Scrollable list of past 20 decisions
  Each: date + decision title + option chosen + result (positive/negative)
  Collapsible (collapsed by default)
```

## LEADERBOARD TAB

```
LAYOUT:
  [Sub-tabs: Solo | Corp]
  [Past Seasons dropdown]
  [Season Timer: "Season ends in Xd Xh"]

SOLO VIEW:
  Top 10 rows:
    Rank # | [Logo] Company Name | [Industry icon] | Net Worth | [Badges: 3 max shown]
    Special styling: #1 gold, #2 silver, #3 bronze
    NPC rivals: faded style + "(AI)" label in muted text
    Your row: highlighted with your brand primary color, always visible
    Clickable: opens company dossier popup

CORP VIEW:
  Same layout for top 10 corps
  Shows: Corp name | Both member names | Combined net worth

DOSSIER POPUP (opens on click):
  Company logo (full size) + colors
  Company name + industry + founded
  Brand score bar
  IPO count + legacy multiplier
  All badges (icon grid)
  Recent 5 events (activity feed)
  Net worth
  [Close] button
```

---

# SECTION 18: MONETIZATION

## Developer Products (Repeatable Purchases)

### Revenue Boost — 49 Robux
```
Effect:      2× income multiplier for 2 hours
Stacking:    Multiple purchases add time (not extra multiplier)
Max stack:   24 hours of boost time
Display:     Top bar shows "2× BOOST — Xh Xm" while active
Best used:   Before a seasonal event, after opening many new branches
```

### Morale Package — 39 Robux
```
Effect:      All staff globally → 100 morale immediately
             Cancels all pending quit timers
Best used:   When many staff are low morale or about to quit
Warning:     Client shows staff morale summary before prompting purchase
             If all staff are above 80, suggests "Your staff look fine — still buy?"
```

### R&D Accelerator — 59 Robux
```
Effect:      All active research projects complete instantly
             Bonuses applied immediately
             Slots become available for new research
Best used:   When 2-3 projects are near completion and you want the bonuses now
Warning:     Client warns if no active research ("Nothing to accelerate")
```

### Takeover Token — 99 Robux
```
Effect:      Halves the cash cost of your next hostile takeover attempt
             Consumed even if takeover fails
Limit:       Max 1 token held at once
Display:     "1 Token Active" indicator in Leaderboard tab when held
Best used:   Before attacking a player with very high net worth
```

### Quick Renovation — 19 Robux
```
Effect:      Instantly renovates the currently selected branch (quality → 100)
             No cash cost (replaces the in-game cash cost)
When shown:  Only appears as an option in the Branch Detail popup
Best used:   When cash is tight but a branch is performing badly due to quality
```

### Branch Slot Unlock — 79 Robux
```
Effect:      Instantly adds +1 staff slot to the currently selected branch
             Permanent (doesn't reset)
Limit:       Max 3 extra slots purchased per branch (hard cap: 9 total slots)
When shown:  In Branch Detail popup when branch is at current slot cap
```

---

## Game Passes (Permanent, One-Time)

### CEO Pass — 349 Robux
```
Permanent effects:
  - Offline earnings cap: 24 hours (vs 8 hour base)
  - Stacks with CFO: takes whichever is higher
  - Exclusive "CEO" title before your company name on leaderboard
  - Unique CEO banner displayed on company dossier card
  - Branch detail popup shows your CEO badge on the branch header
```

### Expansion License — 199 Robux
```
Permanent effects:
  - Choose any 3 countries to unlock at 50% of their normal unlock cost
  - Choices made in Branches tab via "Use License" button on locked country nodes
  - Choices are permanent (can't be reselected)
  - Works across all seasons (doesn't reset on IPO)
```

### Extra R&D Slot — 249 Robux
```
Permanent effects:
  - +1 concurrent research slot (3 total base, 4 with CTO T3 as well)
  - Applies across all seasons (doesn't reset)
  - Visible in R&D tab as extra progress bar slot
```

### VIP Dossier — 149 Robux
```
Permanent cosmetic effects:
  - 4 extra animated logo options (shimmer animation via UIGradient tween)
  - Full color picker for brand colors (any Color3 value vs 16 presets)
  - Animated gold frame on company dossier card
  - "[VIP]" tag on leaderboard row (styled in gold)
  - Golden news ticker text for your company's events
  - Other players see all VIP cosmetics when viewing your dossier
```

### Starter Bundle — 129 Robux (one-time, first game only)
```
Effects applied on first game start only:
  - Starting cash: $750,000 instead of $250,000
  - 1 instant R&D completion token (use any time in first season)
  - Exclusive "Founder's Edition" branch skin for all branches opened in first 30 minutes
  - Exclusive "Founder" badge on company dossier (permanent, all seasons)
Note:
  Game pass can be purchased at any time but effects only activate if
  profile.meta.isNewPlayer is true (first ever login, no branches opened yet)
  If purchased after playing, no cash benefit — badge still awarded
```

### Season Pass — 199 Robux per season
```
Season-specific (new pass ID each season, must repurchase):
  - +1 daily board decision (4 per day instead of 3)
  - 1 free board decision refresh per day
  - Exclusive season branch skin (UI theme color for branches this season)
  - +10% season XP gain (rewards track faster)
  - "Season [N] Pass" badge on dossier (shows all seasons you've held pass)
  - Access to Season Pass reward track (20 tiers of rewards)
Previous season pass owners get "Veteran" indicator on dossier header.
```

---

# SECTION 19: TECHNICAL ARCHITECTURE

## Data Persistence: ProfileStore

```
MODULE:      ProfileStore by Madwork (ServerScriptService)
STORE NAME:  "MogulInc_v1" (bump version on schema changes)
SESSION:     Started on PlayerAdded, ended on PlayerRemoving
AUTO-SAVE:   ProfileStore internal scheduler (every 60 seconds)
SAVE ON LEAVE: EndSession() in PlayerRemoving + BindToClose() for all players
BACKUP:      ProfileStore handles session locking (prevents dual-server data conflicts)

DATA SCHEMA (defaultProfile):
  company:
    name:            string  ("")
    industry:        string  (nil)
    logoId:          number  (1)
    colorPrimary:    string  ("#22C55E")
    colorAccent:     string  ("#3B82F6")

  economy:
    cash:            number  (250000)
    totalRevenue:    number  (0)
    incomePerHour:   number  (0)
    boostActive:     table   (nil)
    takeoverToken:   boolean (false)
    rdAcceleratorToken: boolean (false)

  branches:          array   ([])
  staff:             array   ([])
  executives:        table   ({coo=nil,cmo=nil,cfo=nil,cto=nil})
  research:
    active:          array   ([])
    completed:       array   ([])
    bonuses:         table   ({})

  brand:
    score:           number  (50)
    history:         array   ([])
    lastCampaignAt:  number  (0)

  stock:
    holdings:        table   ({})
    listed:          boolean (false)
    sharePrice:      number  (0)

  contracts:
    active:          array   ([])
    completed:       array   ([])
    expired:         array   ([])

  board:
    decisions:       array   ([])
    lastRefreshDate: string  ("")
    history:         array   ([])
    activeEffects:   array   ([])

  events:
    activeConsequences: array ([])
    history:         array   ([])

  season:
    legacyMultiplier: number (1.0)
    ipoCount:        number  (0)
    badges:          array   ([])
    milestoneRewards: array  ([])
    passXP:          number  (0)
    passRewardsClaimed: array ([])

  corp:
    id:              string  (nil)
    role:            string  (nil)

  meta:
    lastSeen:        number  (os.time())
    hasCompletedTutorial: boolean (false)
    isNewPlayer:     boolean (true)
    totalPlaytime:   number  (0)
    createdAt:       number  (os.time())

  gamepasses:
    ceo:             boolean (false)
    expansionLicense: boolean (false)
    extraRdSlot:     boolean (false)
    vipDossier:      boolean (false)
    starterBundle:   boolean (false)
    licensedCountries: array ([])

  unlockedCountries: array   (["usa"])
  branchSlots:       table   ({})
```

## Server Architecture

```
ServerScriptService/
  GameServer.Script         (main, requires all services)
  Services/
    PlayerService           (profile load/unload, offline calc, summary)
    IncomeService           (recalculate, tick loop)
    BranchService           (open, upgrade, path, renovate, relocate, close)
    StaffService            (hire, fire, promote, transfer, morale)
    ExecService             (hire, replace, bonus application)
    ResearchService         (start, complete, offline check)
    BrandService            (add/subtract score, PR campaign)
    StockService            (tick, crash, buy, sell, dividends)
    BoardService            (generate, decision, history)
    EventService            (crisis, opportunity, seasonal, news ticker)
    ContractService         (generate, check, complete)
    SeasonService           (timer, IPO, badge award)
    TakeoverService         (initiate, resolve, defend)
    CorpService             (create, join, leave, sync)
    MarketplaceHandler      (ProcessReceipt, gamepass checks)
    MilestoneTracker        (Breaking News triggers)
    RateLimiter             (anti-exploit, per-player per-event)
  Config/
    IndustryConfig          (in ReplicatedStorage — shared)
    CountryConfig           (in ReplicatedStorage — shared)
    BranchConfig            (in ReplicatedStorage — shared)
    StaffConfig             (in ReplicatedStorage — shared)
    ExecConfig              (in ReplicatedStorage — shared)
    ResearchConfig          (in ReplicatedStorage — shared)
    BoardConfig             (server only — don't expose decision pool to client)
    EventConfig             (server only)
    ContractConfig          (server only)
    GameConfig              (product IDs, pass IDs, server constants)

ReplicatedStorage/
  Remotes/                  (all RemoteEvents and RemoteFunctions)
  Config/                   (IndustryConfig, CountryConfig, BranchConfig, StaffConfig, ExecConfig, ResearchConfig)
  DefaultProfile            (ModuleScript — schema reference)

StarterPlayerScripts/
  UIController              (tab switching, animation)
  DashboardClient
  BranchesClient
  StaffClient
  ExecsClient
  ResearchClient
  MarketClient
  BoardClient
  LeaderboardClient
  ShopClient
  OverlayManager            (Breaking News, Login Summary, Crisis Alert, Notifications)
  NumberFormatter           (format $1,234,567 as "$1.2M", etc.)
```

## RemoteEvent Reference

```
SERVER → CLIENT (FireClient):
  SyncEconomy          { cash, incomePerHour, netWorth, boostActive }
  SyncBranches         { branches[] }
  SyncStaff            { staff[] }
  SyncResearch         { active[], completed[], bonuses{} }
  SyncBoard            { decisions[], activeEffects[] }
  SyncContracts        { active[] }
  SaveStatus           { status: "saving" | "saved" | "error" }
  PushNewsItem         { message, priority }
  BreakingNews         { headline, companyName, milestone }
  ShowLoginSummary     { summaryData{} }
  CrisisAlert          { crisisId, type, severity, description, expiresAt }
  ContractCompleted    { contractId, reward }
  Toast                { message, type }
  TakeoverAlert        { attackerId, attackerName, success }

CLIENT → SERVER (FireServer):
  RequestOpenBranch    { cityId, countryId }
  RequestUpgradeBranch { branchId }
  RequestSetPath       { branchId, path }
  RequestSetPathUpgrade{ branchId, tier, optionIndex }
  RequestRenovateBranch{ branchId }
  RequestRelocateBranch{ branchId, newCityId, newCountryId }
  RequestCloseBranch   { branchId }
  RequestHireStaff     { branchId }
  RequestFireStaff     { staffId }
  RequestPromoteStaff  { staffId }
  RequestTransferStaff { staffId, targetBranchId }
  RequestMoraleBoost   { branchId }
  RequestHireExec      { role, tier }
  RequestStartResearch { projectId }
  MakeBoardDecision    { decisionId, optionIndex }
  RespondToCrisis      { crisisId, response }
  RequestBuyStock      { ticker, quantity }
  RequestSellStock     { ticker, quantity }
  RequestListCompany   { sharePrice }
  RequestDelistCompany { }
  RequestTakeover      { targetId }
  RequestUnlockCountry { countryId }
  RequestIPO           { }
  RequestCreateCorp    { name }
  RequestJoinCorp      { corpId }
  RequestLeaveCorp     { }
  RequestListBranch    { branchId, price }
  RequestBuyBranch     { listingId }
  RequestSetCompanyName{ name }
  RequestSetLogo       { logoId }
  RequestSetColors     { primary, accent }
  RequestSetIndustry   { industry }

CLIENT → SERVER (InvokeServer — RemoteFunctions):
  GetDashboardData     → { overview, topBranches, activeBuffs, recentActivity }
  GetStockData         → { indexes[], portfolio[], companies[] }
  GetLeaderboard       { type }  → { entries[] }
  GetDossier           { userId }  → { dossierData{} }
  GetResearchData      → { active[], available[], completed[] }
```

## Anti-Exploit Rules

```
NEVER trust client for:
  - Cash values or income amounts
  - Branch/staff/exec data (always read from server profile)
  - Upgrade costs (always read from Config, never from client request)
  - Research durations (server timestamps only)
  - Brand score (server calculated only)

Rate limiting thresholds:
  Action events (RequestOpenBranch, etc.):  max 5 per second
  Query events (GetDashboardData, etc.):    max 10 per second
  Board/Crisis responses:                   max 2 per second
  Takeover requests:                        max 1 per 30 seconds
  On exceed: kick player, log to admin output

Sanity checks on every server handler:
  1. Check player exists and has loaded profile
  2. Check arguments are correct types (typecheck all)
  3. Check business logic (sufficient cash, entity exists, not at cap, etc.)
  4. Act. Never act before all checks pass.

Cash delta check:
  Server tracks expectedCash every 30 seconds
  If actual cash > expectedCash × 1.1 (10% tolerance for timing):
    Flag account for admin review
    Don't kick immediately (could be legitimate timing edge case)
```

## Offline Calculation Order (on PlayerJoin)

```
1.  Calculate offlineSeconds = os.time() - profile.meta.lastSeen
2.  Calculate cappedSeconds = min(offlineSeconds, offlineCap)
    offlineCap = 8h base, +CFO bonus, +CEO Pass if owned
3.  Apply offline income: cash += (cappedSeconds / 3600) × incomePerHour
4.  Apply morale decay: for each staff, calculate hours offline × decay rate
5.  Apply quality decay: for each branch, calculate hours offline × decay rate
6.  Check R&D completions: for each active research, if elapsed >= duration: complete it
7.  Apply board active effects expiry: remove expired effects
8.  Check contract completions: for each contract, evaluate requirements
9.  Check contract expiry: remove expired contracts, generate replacements
10. Apply crisis auto-response: for any crises that fired offline, apply "Ride it out" outcome
11. Update Regional Manager auto-opens: if eligible, open branches in cheapest city slots
12. Recalculate income per hour (after all changes)
13. Build summaryData table
14. Update profile.meta.lastSeen = os.time()
15. Fire "ShowLoginSummary" to client with summaryData
16. Fire initial sync events (SyncEconomy, SyncBranches, SyncStaff, etc.)
```

---

# SECTION 20: ALL PLAYER CHOICES — MASTER LIST

This section lists every single decision point a player can make in the game.

## A. Industry & Company Setup Choices

```
1.  Choose industry: Fast Food / Tech / Fashion / Healthcare / Entertainment
2.  Name your company (text input, 2-20 characters)
3.  Choose company logo (1-20 standard, 21-24 with VIP Dossier pass)
4.  Choose primary brand color (16 presets or full picker with VIP)
5.  Choose accent brand color (16 presets or full picker with VIP)
6.  Re-pick industry on each IPO (or keep the same)
```

## B. Branch Decisions

```
7.   Choose which country to unlock next (from locked countries)
8.   Choose which city slot to open a branch in (Airport / Mall / Downtown / etc.)
9.   Choose branch upgrade path: Volume / Premium / Seasonal (irreversible without relocation)
10.  Choose Volume sub-upgrade per tier (1-5): one of 2-3 options each = 10-15 choices per branch
11.  Choose Premium sub-upgrade per tier (1-5): one of 2-3 options each
12.  Choose Seasonal sub-upgrade per tier (1-5): one of 2-3 options each
13.  Upgrade branch level (1-10): when to spend and on which branch
14.  Renovate branch: spend now vs wait
15.  Relocate branch: which city and country to move to
16.  Close branch: yes/no + confirms which to close
17.  Name individual branches (optional, player can name each)
```

## C. Staff Decisions

```
18.  Hire staff for which branch (allocate limited cash)
19.  Accept random specialty or reroll preview (cosmetic choice, real roll on server)
20.  Promote staff (Level 1→2, 2→3, 3→4): when to invest
21.  Transfer staff: which staff to which branch
22.  Fire staff: when to cut costs
23.  Assign Regional VP to up to 3 branches: choose which 3
24.  Pay morale bonus (for specific branch) vs buy Morale Package (global)
25.  Prioritize which staff to promote vs hire new
```

## D. Executive Decisions

```
26.  Which executive to hire first (COO / CMO / CFO / CTO)
27.  Which tier to hire (T1 = cheap, T3 = expensive but best)
28.  Replace current exec with higher tier: when to invest
29.  Fill all 4 slots vs specialize (e.g. focus on COO + CMO before CFO + CTO)
```

## E. R&D Decisions

```
30.  Which project to start (from pool of available projects)
31.  Which project slot to use for which project (slot allocation)
32.  Whether to buy R&D Accelerator to finish instantly
33.  Whether to cancel an active project (refund 50%)
34.  Order of completion: which bonuses to unlock first matters for early vs late strategy
35.  Industry-exclusive R&D: which industry-specific project to do
```

## F. Brand Score Decisions

```
36.  Whether to run PR Campaign now (spend $200K-$500K) vs wait
38.  How to respond to crises (Pay / Ride out / Ignore)
39.  Board decision choices that affect brand score
40.  Whether to hire CMO to raise brand cap
41.  How to prioritize brand vs income (Premium path needs high brand; Volume does not)
```

## G. Stock Market Decisions

```
42.  Buy stocks: which index/company and how much
43.  Sell stocks: when to take profit or cut losses
44.  List your company: yes/no (share income for upfront capital)
45.  Delist your company: buy back shares at premium
46.  How to respond to crash warnings (sell / hold / buy more)
47.  Use Finance Wizard staff's crash immunity
```

## H. Board Decision Choices

```
48-112. For each of the 65 board decision types, choose Option A / B / C
        65 decision types × 2-3 options each = ~180 distinct option choices
        Players see 3-4 per day, so they encounter all types over multiple sessions
```

## I. Event Responses

```
113. Crisis response: Pay to resolve / Ride it out / Ignore
     (45 crisis types × 3 responses = 135 possible interactions)
114. Opportunity event: Accept / Decline (20 opportunity types)
115. Hostile takeover defense: Legal / PR / Accept buyout
```

## J. Investor Contracts

```
116. Which contracts to prioritize (when 5 slots, can choose focus)
117. Whether to complete early (if possible before deadline) or let them auto-complete
```

## K. Seasonal System

```
118. Whether to IPO (voluntary, done at $500M threshold)
119. What industry to pick for next run (after IPO)
120. Whether to buy Season Pass
121. Season Pass reward choices (if any rewards have options — future feature)
122. How to use seasonal events (which branches to activate for max Seasonal path income)
```

## L. Social Decisions

```
123. Create a Corporation vs play solo
124. Who to invite to Corporation (external to game)
125. Whether to leave Corporation
126. Who to target for hostile takeover (NPC rivals vs player companies)
127. Whether to list branches on marketplace
128. Listing price for branches (50%-300% of market value)
129. Whether to buy another player's branch from marketplace
130. Whether to invest in another player's company stock
```

## M. Monetization Choices

```
131. Buy Revenue Boost (49 R$): timing matters — buy before events
132. Buy Morale Package (39 R$): reactive purchase when staff at risk
133. Buy R&D Accelerator (59 R$): impulsive vs planned
134. Buy Takeover Token (99 R$): before a specific takeover attempt
135. Buy CEO Pass (349 R$): long-term offline earnings improvement
136. Buy Expansion License (199 R$): choose which 3 countries to discount
137. Buy Extra R&D Slot (249 R$): R&D-focused playstyle
138. Buy VIP Dossier (149 R$): cosmetic/social flex
139. Buy Season Pass (199 R$): seasonal value player
140. Buy Starter Bundle (129 R$): best on very first game
141. Buy Quick Renovation (19 R$): reactive when branch quality low
142. Buy Branch Slot Unlock (79 R$): per-branch, chosen per branch
```

## N. UI & Display Choices

```
143. Choose world map view vs list view in Branches tab
144. Sort staff by morale / level / specialty
145. Choose which "Past Season" to view in leaderboard archive
146. View another player's dossier vs move on
147. Close Branch Detail popup via outside click or X button
148. Expand vs collapse Board History
149. Filter R&D available projects by category
150. Choose Corp sub-tab vs Solo sub-tab in leaderboard
```

---

# SECTION 21: IMPLEMENTATION NOTES

## Development Priority Order

```
PHASE 1 — MVP (4-6 weeks):
  - ProfileStore setup (correct from day one — no shortcuts)
  - Income tick system + cash display
  - Branch system (open, level, path choosing, income formula)
  - Staff system (hire, morale, fire)
  - USA + UK + Germany only (3 countries to test with)
  - Fast Food industry only
  - Login summary screen
  - Basic Dashboard tab + Branches tab
  - Monetization: Revenue Boost + CEO Pass only
  → Soft launch as alpha, collect feedback

PHASE 2 — v1.0 (4-6 more weeks):
  - All 5 industries
  - All 10 Tier 1-3 countries
  - Executive system
  - R&D system
  - Brand reputation
  - Board decisions (30 types minimum)
  - Crisis/events system (all crisis types)
  - Investor contracts
  - Full UI (all tabs)
  - All monetization items
  → Official release

PHASE 3 — v1.5 (ongoing):
  - Stock market
  - Hostile takeovers
  - Corporation Mode
  - Player marketplace
  - Seasonal system (IPO + prestige)
  - Remaining countries (Tier 4+)
  - Season pass

PHASE 4 — Live Service:
  - Monthly seasons
  - Seasonal events calendar
  - New R&D projects
  - New board decisions
  - Leaderboard badges
  - Community events
```

## Critical "Don't Make These Mistakes" Notes

```
1. SAVE SYSTEM: Use ProfileStore. Not raw DataStore. Not DataStore2.
   ProfileStore's session locking is non-negotiable. Franchise Empire's
   broken saves are entirely from poor DataStore management.

2. NEVER TRUST CLIENT: All cash calculations are server-side.
   Never accept a "cost" value from a RemoteEvent argument.
   Always read cost from server Config.

3. INCOME TICK: Don't fire a RemoteEvent every single second.
   Batch UI updates every 5 seconds. The server still ticks every second
   for accuracy, but the client display updates less frequently.

4. OFFLINE CALCULATION: Must run as a single synchronous block on join,
   BEFORE any sync events fire. Player should never see their pre-offline
   state on screen — they should always load into the post-offline state.

5. TEXT FILTER: Every single player-entered string (company name, corp name)
   must pass through TextService:FilterStringAsync. No exceptions.
   Roblox will moderate the game if player-generated content bypasses this.

6. MOBILE FIRST: All UI must be tap-friendly. Minimum touch target: 44×44px.
   Test every screen with Roblox's mobile emulator before shipping.

7. LOADING STATES: Every async operation (DataStore, RemoteFunction) needs
   a loading state in the UI. Players who see blank screens assume the game broke.

8. RATE LIMITING: Implement from day one. Exploit scripts are common in Roblox.
   Having no rate limiting means griefers can spam fire events and crash the server.
```

## Key Config Values to Balance

```
These numbers should be tunable without code changes:
  INCOME_TICK_RATE:          1 second
  CLIENT_SYNC_RATE:          5 seconds
  AUTO_SAVE_INTERVAL:        60 seconds
  MORALE_DECAY_INTERVAL:     10 minutes
  QUALITY_DECAY_RATE:        1 per hour
  OFFLINE_CAP_DEFAULT:       8 hours
  STOCK_TICK_RATE:           60 seconds
  CRASH_MIN_INTERVAL:        20 minutes
  CRASH_MAX_INTERVAL:        50 minutes
  CRISIS_MIN_INTERVAL:       30 minutes
  CRISIS_MAX_INTERVAL:       90 minutes
  OPPORTUNITY_MIN_INTERVAL:  60 minutes
  LEADERBOARD_UPDATE_RATE:   5 minutes
  CONTRACT_DURATION:         72 hours
  BOARD_REFRESH_HOUR:        0 (midnight UTC)
  TAKEOVER_COOLDOWN:         24 hours
  SEASON_DURATION_DAYS:      30
  IPO_REVENUE_THRESHOLD:     500000000
  LEGACY_MULTIPLIER_PER_IPO: 0.10
```

---

END OF DOCUMENT
Mogul Inc. Complete Game Specification — Version 1.0
Total: 55 countries, 15 staff specialties, 25 R&D projects, 65 board decisions,
45 crisis types, 20 opportunity types, 12 seasonal events, 157 game elements,
150+ player choices documented.
