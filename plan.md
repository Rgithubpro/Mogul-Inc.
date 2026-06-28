# MOGUL INC. — COMPLETE GAME SPECIFICATION
## Version 2.0 | Roblox UI-Only Business Empire Game

---

# TABLE OF CONTENTS

1.  Game Overview
2.  Visual Design System
3.  Industry System (15)
4.  Country Database (55)
5.  Branch System
6.  Staff System
7.  Executive System
8.  Research & Development
9.  Brand Reputation
10. Stock Market System
11. Board Decisions (65)
12. Events & News System
13. Investor Contracts
14. Seasonal & Prestige
15. Social features
16. Unique features
17. UI screen layouts
18. Monetization
19. Technical architecture
20. All player choises - Master list
21. Implementation notes

---

# SECTION 1: GAME OVERVIEW

## Concept
Mogul Inc. is a 100% UI-based Roblox idle tycoon game. No 3D world, no avatars running around.
Players build a global franchise empire, expanding across 55 countries, managing staff, executives,
research, stock markets, and rival companies — all through clean menus and panels.
Directly inspired by "Franchise Empire" on Roblox but rebuilt with working saves and more depth.

## Key Pillars
- Every upgrade decision has a real tradeoff (no "obviously correct" choices)
- Offline income that matters (players come back to a satisfying catch-up)
- Social flex layer (leaderboard, dossier, Breaking News moments)
- Long-term retention via seasonal IPO resets and legacy multipliers
- Works on mobile and desktop equally well

## Starting Conditions
- Cash: $250,000 (or $750,000 with Starter Bundle gamepass)
- Country: USA (always unlocked) | Branches: 0 | Staff: 0 | Brand Score: 50

---

# SECTION 2: VISUAL DESIGN SYSTEM

All colors are hex strings for readability. In Luau: Color3.fromHex("#RRGGBB").
Transparency: Roblox 0-1 range (0=opaque, 1=transparent).

## Color Palette

### Base Colors
```
BACKGROUND_PRIMARY:   #09090E   Color3.fromHex("#09090E")  -- very dark navy-black
BACKGROUND_SECONDARY: #111118   Color3.fromHex("#111118")  -- surface, cards
BACKGROUND_TERTIARY:  #1A1A24   Color3.fromHex("#1A1A24")  -- elevated, modals
BACKGROUND_HOVER:     #222230   Color3.fromHex("#222230")  -- MouseEnter tween target

BORDER_SUBTLE:   Color3.fromRGB(255,255,255)  UIStroke.Transparency = 0.94
BORDER_DEFAULT:  Color3.fromRGB(255,255,255)  UIStroke.Transparency = 0.90
BORDER_STRONG:   Color3.fromRGB(255,255,255)  UIStroke.Transparency = 0.82

TEXT_PRIMARY:    #EEEEF5   TEXT_SECONDARY: #8A8A9A
TEXT_MUTED:      #4A4A60   TEXT_INVERSE:   #09090E
```

### Accent Colors
```
GREEN_DEFAULT:  #22C55E  | GREEN_BG:  BackgroundTransparency=0.92 | GREEN_BORDER: UIStroke.Transparency=0.78
AMBER_DEFAULT:  #F59E0B  | AMBER_BG:  BackgroundTransparency=0.92 | AMBER_BORDER: UIStroke.Transparency=0.78
RED_DEFAULT:    #EF4444  | RED_BG:    BackgroundTransparency=0.92 | RED_BORDER:   UIStroke.Transparency=0.78
BLUE_DEFAULT:   #3B82F6  | BLUE_BG:   BackgroundTransparency=0.92 | BLUE_BORDER:  UIStroke.Transparency=0.78
PURPLE_DEFAULT: #8B5CF6  | PURPLE_BG: BackgroundTransparency=0.92 | PURPLE_BORDER:UIStroke.Transparency=0.78
TEAL_DEFAULT:   #14B8A6  | TEAL_BG:   BackgroundTransparency=0.92 | TEAL_BORDER:  UIStroke.Transparency=0.78
PINK_DEFAULT:   #EC4899  | PINK_BG:   BackgroundTransparency=0.92 | PINK_BORDER:  UIStroke.Transparency=0.78
GOLD_DEFAULT:   #EAB308  | GOLD_BG:   BackgroundTransparency=0.92 | GOLD_BORDER:  UIStroke.Transparency=0.78
```

### Industry Theme Colors (all 15)
```
FAST_FOOD:    #F97316  | TECH:        #6366F1  | FASHION:     #EC4899
HEALTHCARE:   #10B981  | ENTERTAINMENT:#A855F7 | CAFE:        #78350F
FITNESS:      #06B6D4  | HOTEL:       #D97706  | RETAIL:      #BE123C
SPORTS:       #65A30D  | AUTOMOTIVE:  #DC2626  | REAL_ESTATE: #64748B
MUSIC:        #C026D3  | SOCIAL_MEDIA:#0EA5E9  | AEROSPACE:   #1E3A5F
```

### Semantic Colors
```
MONEY_POSITIVE: GREEN_DEFAULT | MONEY_NEGATIVE: RED_DEFAULT
MORALE_HIGH: #22C55E (60-100) | MORALE_MID: #F59E0B (30-59) | MORALE_LOW: #EF4444 (0-29)
QUALITY_HIGH:#22C55E (70-100) | QUALITY_MID:#F59E0B (40-69) | QUALITY_LOW:#EF4444 (0-39)
```

## Typography (Roblox Fonts)

```
PRIMARY_FONT:  Enum.Font.GothamMedium
               Font.new("rbxasset://fonts/families/GothamSSm.json", Enum.FontWeight.Medium)
BOLD_FONT:     Enum.Font.GothamBold
SEMIBOLD_FONT: Enum.Font.GothamSemibold
MONO_FONT:     Enum.Font.RobotoMono    -- use for all numbers (naturally fixed-width)
               Font.new("rbxasset://fonts/families/RobotoMono.json")

NOTE: Roblox TextLabels do not support letter-spacing or line-height directly.
      Use separate labels for fine spacing. TextSize = pixel size.
```

### Type Scale
```
DISPLAY_XL: TextSize=32, GothamBold     -- Breaking News headline
DISPLAY_LG: TextSize=24, GothamBold     -- Tab headers, major values
HEADING_MD: TextSize=18, GothamSemibold -- Section headers
HEADING_SM: TextSize=15, GothamSemibold -- Card titles
BODY_MD:    TextSize=14, GothamMedium   -- Main body text
BODY_SM:    TextSize=13, GothamMedium   -- Descriptions, labels
CAPTION:    TextSize=11, GothamBold     -- Badges, meta
LABEL:      TextSize=10, GothamBold     -- Category labels (string.upper())
MONO_MD:    TextSize=13, RobotoMono     -- Data values, IDs
MONO_SM:    TextSize=11, RobotoMono     -- Small data values
```

## Spacing System (UDim Offset values)
```
XS=4  SM=8  MD=12  LG=16  XL=20  2XL=24  3XL=32  4XL=40  5XL=52
Example: UIPadding.PaddingLeft = UDim.new(0, 16)  -- LG padding
```

## Border Radius (UICorner.CornerRadius)
```
XS: UDim.new(0,4)   SM: UDim.new(0,6)   MD: UDim.new(0,8)
LG: UDim.new(0,10)  XL: UDim.new(0,12)  2XL: UDim.new(0,16)
FULL: UDim.new(1,0) -- pills, circles
```

## Layout Structure (Roblox UDim2 values)
```
SCREEN_WIDTH:      UDim2.new(1,0,0,0)      -- full screen width
TOP_BAR_HEIGHT:    UDim2.new(1,0,0,52)     -- fixed 52px
BOTTOM_NAV:        UDim2.new(1,0,0,60)     -- fixed 60px
CONTENT_AREA:      UDim2.new(1,0,1,-112)   -- full screen minus both bars
MAX_CONTENT_WIDTH: 520 offset, AnchorPoint=Vector2.new(0.5,0), centered
SIDE_PADDING:      UIPadding PaddingLeft/Right = UDim.new(0,16)
CARD_GAP:          UIListLayout.Padding = UDim.new(0,10)
```

## Icon System (Roblox ImageLabel-based)

All icons are PNG assets uploaded to Roblox as Decals (white-on-transparent).
Stored in: ReplicatedStorage/Config/IconConfig ModuleScript (key=name, value=assetId).
Tint at runtime: imageLabel.ImageColor3 = Color3.fromHex("#22C55E")
Emoji shown as quick-reference / prototyping fallback only.

Icon sizes: 16x16 (inline), 18x18 (button), 20x20 (card header), 24x24 (tab nav)

```
Navigation:  Dashboard=layout-dashboard  Branches=building-store  Staff=users-group
             Executives=tie  Research=flask  Market=chart-candle  Board=clipboard-list
             Rankings=trophy  Shop=shopping-cart  Settings=settings

Status:      Saving=loader(spin)  Saved=check  Crisis=alert-octagon  Opportunity=sparkles
             MoraleHigh=mood-happy  MoraleMid=mood-neutral  MoraleLow=mood-sad
             VIP=crown  Boost=bolt  Locked=lock  Unlocked=lock-open

Data:        Cash=coin  Revenue=trending-up  BrandScore=star  Quality=award
             Morale=heart  Country=world  ResearchTimer=clock  IPO=rocket

Industry icons: FastFood=burger  Tech=cpu  Fashion=shirt  Healthcare=heart-rate-monitor
                Entertainment=movie  Cafe=coffee  Fitness=dumbbell  Hotel=building
                Retail=shopping-bag  Sports=trophy  Automotive=car  RealEstate=building-2
                Music=music  SocialMedia=device-mobile  Aerospace=rocket-2
```

## UI Component Specifications

### Cards
```
Standard Card:
  BackgroundColor3 = BACKGROUND_SECONDARY
  UIStroke: Color3=white, Transparency=0.90, Thickness=1, ApplyStrokeMode=Border
  UICorner: CornerRadius=UDim.new(0,10)
  UIPadding: Top/Bottom=UDim.new(0,14), Left/Right=UDim.new(0,16)
  -- No drop shadow (not natively supported in Roblox 2D GUI)

Elevated Card (modals):
  BackgroundColor3=BACKGROUND_TERTIARY, UICorner=UDim.new(0,12)
  UIStroke Transparency=0.82, UIPadding Top/Bottom=UDim.new(0,18)

Highlight/Warning/Danger Cards:
  BackgroundColor3 = matching color, BackgroundTransparency = 0.92
  UIStroke: matching color, Transparency = 0.78
```

### Buttons
```
Primary (TextButton):
  BackgroundColor3=Color3.fromHex("#22C55E"), TextColor3=Color3.fromHex("#09090E")
  UICorner=UDim.new(0,6), UIPadding Top/Bottom=UDim.new(0,9) Left/Right=UDim.new(0,16)
  TextSize=13, Font=GothamSemibold
  Hover: MouseEnter -> TweenService BackgroundColor3 to lighter green
  Disabled: Active=false, BackgroundTransparency=0.6, TextTransparency=0.6

Secondary: BackgroundColor3=BACKGROUND_TERTIARY, UIStroke=BORDER_STRONG
Danger:    BackgroundColor3=Color3.fromHex("#EF4444")
Ghost:     BackgroundTransparency=1, UIStroke=BORDER_DEFAULT
           Hover: TweenService BackgroundColor3->BACKGROUND_HOVER, Transparency->0
Icon Button: Size=UDim2.new(0,32,0,32), UICorner=UDim.new(0,6)
```

### Progress Bars
```
Track Frame: Size=UDim2.new(1,0,0,6), BackgroundColor3=BORDER_DEFAULT color
             UICorner=UDim.new(1,0), ClipsDescendants=true
Fill Frame (child):
  Size=UDim2.new(fillPercent,0,1,0)
  BackgroundColor3: morale/quality/brand->GREEN/AMBER/RED, research->TEAL, XP->PURPLE
  UICorner=UDim.new(1,0)
  Animate: TweenService Size to new UDim2.new(newPercent,0,1,0), 0.6s Quad EaseOut
Tall Bar: same pattern with height=8 offset
```

### Tags / Badges
```
Tag: TextLabel, TextSize=10, Font=GothamBold, Text=string.upper(tagText)
     UIPadding Top/Bottom=UDim.new(0,2) Left/Right=UDim.new(0,8)
     UICorner=UDim.new(0,4), UIStroke matching color Transparency=0.78

Pill (notification count):
  Frame Size min UDim2.new(0,18,0,18), BackgroundColor3=RED_DEFAULT
  UICorner=UDim.new(1,0) -- FULL radius
  TextLabel inside: TextSize=10, GothamBold, white
```

### Animations (TweenService)
```
Card hover:    TweenInfo.new(0.15, Quad, Out) -> Position -1 offset (lift)
               MouseLeave -> tween back
Modal open:    UIScale.Scale 0.95->1.0 + GroupTransparency 1->0, 0.2s Back EaseOut
Modal close:   UIScale.Scale 1.0->0.95 + GroupTransparency 0->1, 0.15s Quad EaseIn
Tab fade:      GroupTransparency 1->0, 0.12s Quad EaseOut
Toast slide:   Position from UDim2.new(1,20,y,0) to UDim2.new(1,-width-16,y,0), 0.2s
Breaking News: Position from UDim2.new(0.5,-190,0.5,40) to UDim2.new(0.5,-190,0.5,-100)
               + BackgroundTransparency 1->0, 0.35s Back EaseOut
Pulse:         TweenInfo.new(0.4,Sine,Out,-1,true) UIScale.Scale 1->1.05 (infinite)
Spinner:       RunService.Heartbeat: imageLabel.Rotation += 360 * dt
Bar fill:      TweenService Size to UDim2.new(targetPercent,0,1,0), 0.6s Quad EaseOut
Number tick:   RunService.Heartbeat lerp toward target value, ~400ms convergence
```

---

# SECTION 3: INDUSTRY SYSTEM

At game start (or after IPO), player picks from 15 industries.
Changes: UI theme color, branch/staff naming, country demand multipliers,
crisis pool, R&D project names. Core mechanics unchanged.
Space & Aerospace locked until first IPO completed.

---

## INDUSTRY: FAST FOOD
```
ID: fast_food | THEME: #F97316 | BRANCH: Restaurant | STAFF: Team Member | HQ: Corporate Kitchen
STRENGTHS: Highest volume, lowest branch cost, fastest expansion, strong in high-population countries
WEAKNESSES: Lowest margin/customer, health inspection crises frequent, Premium path weaker
BEST: India, Brazil, Indonesia, Mexico, Nigeria, Philippines, Bangladesh
WORST: Switzerland, Norway, Luxembourg

UPGRADES Volume:   "Combo Deals","Express Line","Drive-Through","Kiosk Stations","Meal Bundles"
UPGRADES Premium:  "Gourmet Menu","Table Service","Chef Partnership","Premium Ingredients","VIP Dining"
UPGRADES Seasonal: "Holiday Special","Summer Sale","Festive Meal Box","Limited Burger","Anniversary Deal"

CRISES: health_inspection_failure, supply_chain_shortage, food_contamination_scare, staff_walkout,
        competitor_price_war, delivery_delay, equipment_breakdown, bad_review_viral,
        ingredient_price_spike, health_department_audit

EXCLUSIVE R&D:
  Recipe Innovation:       +20% income all branches, 60 min
  Drive-Through AI:        +25% Volume path throughput, 90 min
  Nutrition Partnership:   +10 brand score + immune to health inspection, 75 min
  Franchise Training Kit:  +20% all staff specialty bonuses, 60 min
```

---

## INDUSTRY: TECH
```
ID: tech | THEME: #6366F1 | BRANCH: Office | STAFF: Engineer | HQ: Innovation Campus
STRENGTHS: Highest income ceiling, R&D bonuses doubled, Premium path most effective
WEAKNESSES: Slowest early game (expensive), data breaches = huge brand hit, exec-dependent
BEST: USA, Japan, South Korea, Germany, Israel, Singapore, Netherlands, Sweden, Finland
WORST: Nigeria, Bangladesh, Myanmar

UPGRADES Volume:   "Open Workspace","Agile Sprint","Dev Tools Upgrade","CI/CD Pipeline","Cloud Scaling"
UPGRADES Premium:  "Enterprise Suite","Custom API","White-Glove Onboarding","Dedicated Support","Executive Dashboard"
UPGRADES Seasonal: "Product Launch","Hackathon Event","Beta Access Drop","Conference Keynote","Year-End Release"

CRISES: server_outage, data_breach, security_vulnerability, key_engineer_quit,
        product_launch_delay, competitor_feature_copy, regulatory_investigation,
        bad_app_review, patent_dispute, AI_ethics_controversy

EXCLUSIVE R&D:
  Platform Launch:     +30% income, 120 min
  AI Integration:      +20% all income permanently, 150 min
  Security Fortress:   Immune to data breach crises, 90 min
  Developer Relations: +20% staff specialty bonuses, 75 min
```

---

## INDUSTRY: FASHION
```
ID: fashion | THEME: #EC4899 | BRANCH: Boutique | STAFF: Stylist | HQ: Design Atelier
STRENGTHS: Highest brand score multiplier, very strong luxury/rich countries, Seasonal most powerful
WEAKNESSES: Volatile (trends), low demand developing countries, brand crises severe
BEST: France, Italy, UAE, UK, Japan, South Korea, Switzerland, USA, Spain, Australia
WORST: Bangladesh, Pakistan, Ethiopia, Myanmar

UPGRADES Volume:   "Fast Fashion Line","Pop-Up Event","Flash Sale","Outlet Store","Capsule Collection"
UPGRADES Premium:  "Designer Collab","Exclusive Members","Runway Show","Couture Line","Personal Shopper"
UPGRADES Seasonal: "Summer Collection","Winter Gala","Fashion Week","Holiday Edition","Trend Drop"

CRISES: knockoff_scandal, influencer_fallout, trend_miss, fabric_shortage, sweatshop_accusation,
        celebrity_disassociation, fashion_week_disaster, viral_bad_review,
        return_rate_spike, copyright_infringement

EXCLUSIVE R&D:
  Signature Collection:  +25% income, 75 min
  Influencer Network:    +15 brand score + prevents influencer crisis, 90 min
  Sustainability Push:   +12 brand score + cost -10%, 60 min
  Virtual Fitting Room:  +20% Premium path income, 90 min
```

---

## INDUSTRY: HEALTHCARE
```
ID: healthcare | THEME: #10B981 | BRANCH: Clinic | STAFF: Specialist | HQ: Medical Center
STRENGTHS: Most recession-proof, stable demand, high per-customer margin, CFO+offline synergy
WEAKNESSES: Most expensive expansion, slowest volume, many regulatory crises, staff burnout
BEST: Germany, USA, Australia, Switzerland, Canada, Sweden, Japan, UK, Denmark, Austria
WORST: Nigeria, Ethiopia, Bangladesh, Myanmar

UPGRADES Volume:   "Walk-In Clinic","Telemedicine Line","Insurance Partnership","Screening Program","Community Outreach"
UPGRADES Premium:  "Private Suite","Specialist Referral","Executive Health Plan","Concierge Medicine","Research Trial"
UPGRADES Seasonal: "Flu Season Campaign","Annual Check-Up Drive","Mental Health Month","Summer Wellness","New Year Health"

CRISES: malpractice_claim, regulatory_audit, supply_drug_shortage, staff_burnout_mass,
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
ID: entertainment | THEME: #A855F7 | BRANCH: Studio/Venue | STAFF: Creator | HQ: Creative Hub
STRENGTHS: Highest ceiling with Seasonal, viral events frequent, Seasonal 4x (vs 3x), Breaking News fun
WEAKNESSES: Most volatile (boom/bust), flop events severe, high crisis frequency, needs active play
BEST: USA, China, South Korea, Japan, UK, Brazil, India, Nigeria, Australia, Mexico
WORST: Switzerland, Norway, Germany

UPGRADES Volume:   "Streaming Rights","Syndication Deal","Box Office Boost","Fan Club","Merchandise Line"
UPGRADES Premium:  "Exclusive Premiere","VIP Experience","Director's Cut","Private Screening","Brand Collaboration"
UPGRADES Seasonal: "Summer Blockbuster","Holiday Special","Award Season Push","Viral Campaign","World Tour"

CRISES: box_office_flop, streaming_rights_lost, celebrity_scandal, bad_critic_review,
        production_delay, copyright_lawsuit, audience_boycott, technical_failure,
        talent_dispute, piracy_surge

EXCLUSIVE R&D:
  Blockbuster Engine:      +35% Seasonal path income, 90 min
  Fan Engagement Platform: +20% all income + viral events 2x more frequent, 120 min
  IP Portfolio:            Immune to copyright crisis, 75 min
  Creator Network:         +25% staff specialty bonuses, 60 min
```

---

## INDUSTRY: COFFEE & CAFE
```
ID: cafe | THEME: #78350F | BRANCH: Cafe | STAFF: Barista | HQ: Roastery HQ
STRENGTHS: Cheapest branch cost in game, very high customer frequency, low crisis rate,
           strong in University/Downtown/Airport, steady offline income
WEAKNESSES: Lowest income ceiling per customer, competitive market, Premium path weaker
BEST: USA, UK, Australia, Canada, Sweden, Finland, Germany, Netherlands, New Zealand, South Korea
WORST: India, Bangladesh, Pakistan (tea-dominant cultures)

UPGRADES Volume:   "Drive-Through Lane","Express Counter","App Ordering","24/7 Service","Loyalty Stamp Card"
UPGRADES Premium:  "Reserve Bar","Single Origin Menu","Barista Championship","Cupping Room","Private Label Roast"
UPGRADES Seasonal: "Pumpkin Spice Season","Iced Summer Menu","Holiday Cups","Limited Reserve Drop","Anniversary Blend"

CRISES: coffee_bean_shortage, barista_walkout, bad_health_inspection, competitor_price_war,
        equipment_breakdown, viral_bad_review, sustainability_controversy, franchise_dispute,
        supply_chain_delay, gentrification_protest

EXCLUSIVE R&D:
  Cold Brew Innovation:  +20% income all cafes, 60 min
  Subscription App:      -30% morale decay + +15% offline income, 90 min
  Bean-to-Cup Brand:     +15 brand score + immune to sustainability crisis, 75 min
  Barista Academy:       +25% all staff specialty bonuses, 60 min

NOTES: Cheapest entry point. Great first industry for new players. University city slots +20%.
       Airport slots are top performers. Pairs well with CFO offline strategy.
```

---

## INDUSTRY: FITNESS & WELLNESS
```
ID: fitness | THEME: #06B6D4 | BRANCH: Gym/Studio | STAFF: Trainer | HQ: Wellness Campus
STRENGTHS: Recurring membership model (stable income floor), Premium path very effective,
           strong offline income (memberships don't stop), less severe staff morale crises
WEAKNESSES: High branch opening cost (equipment), seasonal dips (summer), high overhead
BEST: USA, UK, Australia, UAE, Sweden, Norway, Germany, Japan, Canada, Switzerland
WORST: Ethiopia, Bangladesh, Myanmar, Pakistan

UPGRADES Volume:   "Group Classes","24/7 Access Cards","Online Membership","Corporate Packages","Multi-Site Pass"
UPGRADES Premium:  "Personal Training Suite","VIP Locker Room","Recovery Center","Spa & Sauna","Performance Lab"
UPGRADES Seasonal: "New Year Challenge","Summer Body Push","Marathon Season Drive","Holiday Fitness Package","Resolution Sale"

CRISES: equipment_injury_claim, trainer_walkout, overcrowding_complaint, hygiene_inspection_failure,
        competitor_price_war, membership_cancellation_wave, star_trainer_poached,
        viral_negative_review, regulatory_safety_audit, class_scheduling_disaster

EXCLUSIVE R&D:
  Smart Gym Technology:       +25% all income + -10% equipment overhead, 90 min
  Wellness App Platform:      +20% member retention -> offline income +20%, 75 min
  Injury Prevention Protocol: Immune to equipment_injury_claim crisis, 60 min
  Certified Trainer Network:  +25% all staff specialty bonuses, 75 min

NOTES: Income floor never drops below 60% even during crises (membership model).
       COO T3 is essential (quality decay). Pairs extremely well with COO.
```

---

## INDUSTRY: LUXURY HOTELS & HOSPITALITY
```
ID: hotel | THEME: #D97706 | BRANCH: Hotel | STAFF: Concierge | HQ: Grand Headquarters
STRENGTHS: Highest single-branch income, Resort slots extraordinary, best offline income,
           Premium path most impactful, wealth-multiplier countries are gold mines
WEAKNESSES: Most expensive to open, very vulnerable to tourism crises, fastest quality decay (-2/hr),
            needs frequent renovation
BEST: UAE, France, Italy, Switzerland, Japan, Thailand, Greece, Spain, Australia, Singapore
WORST: Nigeria, Bangladesh, Ethiopia, Pakistan

UPGRADES Volume:   "Budget Suite Expansion","Online Booking Platform","Conference Center","Tour Package Deals","Airport Shuttle"
UPGRADES Premium:  "Presidential Suite","Butler Service","Michelin Star Dining","Rooftop Bar","Spa Penthouse"
UPGRADES Seasonal: "Summer Escape Package","New Year Gala","Holiday Retreat","Fashion Week Hosting","Award Season Package"

CRISES: bad_review_viral, guest_injury_claim, health_inspection_failure, staff_strike,
        tourism_disruption, overbooking_disaster, food_safety_incident, maintenance_failure,
        celebrity_guest_scandal, competitor_undercutting

EXCLUSIVE R&D:
  White Glove Protocol:    +25% Premium income + quality decays 40% slower, 90 min
  Dynamic Pricing AI:      +20% all revenue, 75 min
  Tourism Partnership:     +15 brand score + immune to tourism_disruption, 90 min
  Hospitality Academy:     +25% staff specialty bonuses, 60 min

NOTES: Unique offline mechanic — base offline cap is 12h (guests continue checking in).
       CEO Pass raises to 36h. Quality decay is -2/hr (double normal). COO is essential.
```

---

## INDUSTRY: RETAIL & E-COMMERCE
```
ID: retail | THEME: #BE123C | BRANCH: Store/Warehouse | STAFF: Sales Associate | HQ: Distribution Hub
STRENGTHS: Mall slots peak bonus, Black Friday x5.0 on Seasonal (unique max), broad global demand,
           lower crisis frequency, Volume path scales well in high-population countries
WEAKNESSES: Relies heavily on Mall slots, low per-customer margin, e-commerce logistics crises
BEST: USA, UK, China, Germany, Japan, South Korea, Australia, France, Canada, Brazil
WORST: Ethiopia, Myanmar, Bangladesh, Pakistan

UPGRADES Volume:   "Self-Checkout Stations","Flash Sale System","Bulk Buy Deals","Extended Store Hours","Loyalty Points Program"
UPGRADES Premium:  "Personal Shopper","Members Club","Exclusive Product Lines","VIP After-Hours Shopping","Concierge Returns"
UPGRADES Seasonal: "Black Friday Setup","Holiday Gifting Hub","Back-to-School Drive","Summer Clearance","Mega Sale Campaign"

CRISES: stock_shortage, bad_review_viral, shoplifting_surge, returns_avalanche, competitor_sale_war,
        logistics_breakdown, counterfeit_goods_scandal, staff_theft_incident, data_breach, supplier_dispute

EXCLUSIVE R&D:
  Inventory AI System:      -20% overhead + +15% all income, 75 min
  Omnichannel Platform:     +20% all income + +20% offline income, 90 min
  Anti-Counterfeit Shield:  Immune to counterfeit crisis + brand +10, 60 min
  Customer Experience Lab:  +25% staff specialty bonuses, 75 min

NOTES: Black Friday event (Section 12) gives x5.0 on Seasonal path — unique, highest in game.
       Mall city slots give +6% volume income AND -10% morale decay. Stack multiple Mall slots.
```

---

## INDUSTRY: SPORTS & RECREATION
```
ID: sports | THEME: #65A30D | BRANCH: Venue/Arena | STAFF: Coach | HQ: Sports Complex
STRENGTHS: Tied with Entertainment for highest Seasonal multiplier (x4.0), frequent viral events,
           great in large-population/sports-passionate nations, World Cup is best event
WEAKNESSES: Very volatile (event-dependent), low baseline between events, staff drama high,
            performance crises can tank income overnight
BEST: Brazil, USA, UK, Germany, Spain, France, Argentina, China, India, Australia, South Korea, Nigeria
WORST: Switzerland, Luxembourg, Norway

UPGRADES Volume:   "Season Ticket Drive","Community Programs","Youth Academy","Merchandise Shop","Multi-Sport Offering"
UPGRADES Premium:  "VIP Box Seats","Premium Hospitality Lounge","Corporate Boxes","Meet & Greet Package","Exclusive Club"
UPGRADES Seasonal: "World Cup Campaign","Championship Push","All-Star Weekend","Play-Off Season Blitz","Opening Day Event"

CRISES: match_fixing_scandal, player_injury, crowd_safety_incident, broadcast_deal_lost,
        performance_slump, doping_controversy, stadium_maintenance_failure, ticket_fraud,
        rival_team_domination, weather_cancellation

EXCLUSIVE R&D:
  Performance Analytics:   +25% all income + viral events 30% more frequent, 90 min
  Fan Engagement App:      +20% income + events last 25% longer, 75 min
  Injury Prevention System:Immune to player_injury crisis, 60 min
  Elite Coaching Network:  +25% staff specialty bonuses, 75 min

NOTES: World Cup/Major Sport Event (Section 12) gives x4.5 to Sports industry specifically.
       Venues only valid in Downtown, Mall, Resort, or Industrial city slots.
```

---

## INDUSTRY: AUTOMOTIVE
```
ID: automotive | THEME: #DC2626 | BRANCH: Dealership/Showroom | STAFF: Sales Consultant | HQ: Corporate Showroom
STRENGTHS: Highest per-transaction value, Premium path extremely lucrative in wealthy countries,
           Luxury/Downtown slots ideal, strong in tech-forward countries (EV)
WEAKNESSES: Slowest transaction volume, sensitive to economic downturns, high overhead,
            recall crises devastating across multiple branches
BEST: Germany, USA, Japan, UAE, Switzerland, South Korea, UK, China, Sweden, Italy
WORST: Ethiopia, Bangladesh, Myanmar, Nigeria

UPGRADES Volume:   "Fleet Sales Program","Test Drive Incentive","Financing Partnership","Trade-In Program","Volume Dealer Status"
UPGRADES Premium:  "Luxury Brand Partnership","Bespoke Configuration","VIP Delivery Experience","Chauffeur Demo Service","Celebrity Collection"
UPGRADES Seasonal: "Motor Show Season","Year-End Sales Push","New Model Launch Event","Summer Drive Campaign","EV Awareness Month"

CRISES: vehicle_recall, safety_defect_discovered, competitor_price_war, supply_chain_shortage,
        economic_downturn_impact, star_consultant_poached, bad_review_viral, regulatory_emission_audit,
        financing_scandal, test_drive_accident

EXCLUSIVE R&D:
  EV Transition Program:     +20% income + immune to emission audit crisis, 90 min
  Digital Showroom Platform: +15% all income + +25% offline income, 75 min
  Safety Excellence Award:   +15 brand score + recall crisis damage -60%, 60 min
  Expert Sales Training:     +25% all staff specialty bonuses, 75 min
```

---

## INDUSTRY: REAL ESTATE
```
ID: realestate | THEME: #64748B | BRANCH: Development Office | STAFF: Agent | HQ: Portfolio HQ
STRENGTHS: Best offline income in game (properties earn passively), income scales with level,
           very resistant to standard crises, CFO synergy unmatched
WEAKNESSES: Slowest early game (very expensive), market crash crises severe/long, slow startup,
            expansion very expensive
BEST: USA, UK, UAE, Singapore, Australia, Canada, Germany, Switzerland, Netherlands, France
WORST: Ethiopia, Bangladesh, Myanmar, Pakistan

UPGRADES Volume:   "Rental Unit Block","Co-Working Space","Student Housing Complex","Buy-to-Let Portfolio","Serviced Apartments"
UPGRADES Premium:  "Luxury Penthouse Floor","Private Villa Estate","Branded Residences","Concierge Property","Ultra-Prime Portfolio"
UPGRADES Seasonal: "Spring Market Push","Year-End Tax Sale","Investment Showcase","New Development Launch","Q4 Portfolio Drive"

CRISES: market_crash, planning_permission_denied, tenant_dispute, construction_overrun,
        regulatory_compliance_failure, neighbor_protest, environmental_audit, property_damage,
        agent_misconduct, interest_rate_shock

EXCLUSIVE R&D:
  PropTech Platform:          +20% offline income + +15% all income, 90 min
  Green Building Cert:        +15 brand score + branch cost -10%, 60 min
  Market Intelligence System: -30% market crash crisis damage, 75 min
  Elite Agent Training:       +25% all staff specialty bonuses, 75 min

NOTES: Unique passive — Real Estate branches generate +30% offline income bonus inherently.
       Stacks with CFO and CEO Pass. Undisputed #1 industry for offline players.
```

---

## INDUSTRY: MUSIC & RECORD LABEL
```
ID: music | THEME: #C026D3 | BRANCH: Label/Recording Studio | STAFF: Producer | HQ: Creative HQ
STRENGTHS: Most frequent viral events, award season massive impact, celebrity events 2x impact,
           Social Media Manager staff most effective, easiest brand score momentum
WEAKNESSES: Most volatile income (larger boom AND bust than Entertainment), flop crises longer,
            celebrity crises most damaging, income near-zero without active management
BEST: USA, UK, South Korea, Nigeria, Brazil, Sweden, Australia, Japan, France, India
WORST: Kazakhstan, Myanmar, Bangladesh, Pakistan

UPGRADES Volume:   "Digital Distribution Deal","Playlist Placement","Sync Licensing Program","Merch Line","Streaming Royalty Push"
UPGRADES Premium:  "Exclusive Club Residency","Limited Edition Vinyl","VIP Fan Experience","Major Artist Partnership","Label Flagship"
UPGRADES Seasonal: "Award Season Push","Summer Festival Tour","Holiday Album Drop","New Year Release Blitz","Chart Attack Campaign"

CRISES: artist_beef_scandal, album_flop, copyright_lawsuit, streaming_deal_lost, artist_quit,
        bad_critical_review, social_media_backlash, tour_cancellation,
        ghostwriting_accusation, sample_clearance_dispute

EXCLUSIVE R&D:
  Algorithm Domination:       +25% streaming income + viral events 2x more frequent, 90 min
  Artist Development Program: +20% income + immune to artist_quit crisis, 75 min
  Global Label Network:       Unlock 2 extra countries at -50% cost (unique to Music), 90 min
  Producer Academy:           +25% staff specialty bonuses, 60 min

NOTES: Ignoring a crisis has 75% secondary crisis chance (vs standard 50%). High risk, high reward.
```

---

## INDUSTRY: SOCIAL MEDIA & APPS
```
ID: socialmedia | THEME: #0EA5E9 | BRANCH: Platform Hub | STAFF: Growth Engineer | HQ: Innovation Campus
STRENGTHS: Fastest income growth rate, viral events most impactful, R&D doubles effectiveness,
           Data Analyst staff most effective, each R&D completion gives +5% permanent income (unique)
WEAKNESSES: Most vulnerable to regulatory crises (GDPR, antitrust), data breach catastrophic,
            needs constant R&D, very brand-sensitive, Premium path weak
BEST: USA, China, India, Brazil, Indonesia, UK, Japan, South Korea, Nigeria, Philippines
WORST: Norway, Finland, Denmark (strict regulation)

UPGRADES Volume:   "User Acquisition Push","Algorithm Optimization","Creator Partner Program","Free Tier Expansion","Ad Network Integration"
UPGRADES Premium:  "Premium Subscription","Business Analytics Suite","Brand Partnership Portal","Verified Creator Tools","Enterprise API Access"
UPGRADES Seasonal: "Viral Challenge Campaign","Trending Topic Blitz","Platform Awards Event","Year in Review","New Feature Global Launch"

CRISES: data_breach_catastrophic, antitrust_investigation, algorithm_manipulation_accusation,
        moderator_revolt, viral_misinformation_wave, platform_outage, government_ban_threat,
        content_creator_exodus, ad_boycott_campaign, privacy_law_violation

EXCLUSIVE R&D:
  AI Recommendation Engine:   +30% all income permanently (highest R&D income boost), 150 min
  Privacy Shield Compliance:  Immune to privacy/data crisis permanently, 90 min
  Creator Monetization Hub:   +25% all Premium path income, 75 min
  Community Growth Engine:    +25% staff specialty bonuses, 75 min

NOTES: Each completed R&D gives +5% permanent income stack. CTO + R&D heavy is dominant.
       Recommended for experienced players. Most complex industry to play well.
```

---

## INDUSTRY: SPACE & AEROSPACE (PRESTIGE UNLOCK)
```
ID: aerospace | THEME: #1E3A5F | BRANCH: Facility/Launch Site | STAFF: Scientist | HQ: Mission Control
UNLOCK CONDITION: Must have completed at least 1 IPO in a previous season.

STRENGTHS: Highest income ceiling of any industry, R&D bonuses 3x stronger (unique),
           rare crises (most events are opportunities), brand score gains 50% faster,
           designed for veterans with high Legacy Multiplier
WEAKNESSES: 5x standard branch opening cost, very slow startup, limited city slots
            (only Tech Campus, Industrial, Airport), crises when they happen are catastrophic
BEST: USA, Russia, China, Japan, Israel, UAE, France, Germany, India, UK
WORST: Ethiopia, Bangladesh, Myanmar, Nigeria, Pakistan

UPGRADES Volume:   "Satellite Constellation","Reusable Rocket Program","Launch Schedule Optimization","Small Sat Platform","Rideshare Program"
UPGRADES Premium:  "Crewed Mission Contract","Deep Space Probe","Government Defense Contract","Space Tourism Package","Classified Payload"
UPGRADES Seasonal: "Annual Launch Window","Space Race Event","ISS Resupply Season","Orbital Tourism Push","New Frontier Campaign"

CRISES: launch_failure, satellite_malfunction, regulatory_approval_delay, key_scientist_quit,
        competitor_launch_success, component_supply_disruption, government_contract_cancelled,
        environmental_protest, technical_fault_discovered, funding_cut_announcement

EXCLUSIVE R&D:
  Reusable Launch Vehicle:     +35% all income + supply crisis immunity, 120 min
  AI Mission Control:          R&D speed x3 all projects (this industry), 150 min
  Space Tourism Certification: Unlocks extra Premium sub-upgrade tier (unique), 90 min
  Elite Engineering Academy:   +35% staff specialty bonuses (highest in game), 90 min

NOTES: Branch income 5x higher than standard once established. Branch cost 5x higher.
       Only Tech Campus, Industrial, Airport city slots valid for Aerospace branches.
       Prestige industry for veteran players. Not viable early even in the same season.
```

---

# SECTION 4: COUNTRY DATABASE

All 55 countries. Demand multipliers shown for original 5 industries:
FF=Fast Food, TC=Tech, FS=Fashion, HC=Healthcare, EN=Entertainment
New industry demand follows the same 0.5-2.0 scale — key pairings documented per
industry in Section 3. Full tables to be filled during development.
CITIES: name (type) | Types: Airport, Mall, Downtown, Industrial, Luxury, University, Harbor, Resort, Tech Campus, Entertainment District
Demand: 0.5=very low, 0.8=low, 1.0=avg, 1.2=good, 1.5=strong, 1.8=very strong, 2.0=exceptional

---

## TIER 1 — STARTER (Unlocked by default)

### USA
```
TIER:1 | UNLOCK:default | COST:free | WEALTH:1.6
DEMAND: FF=1.3 TC=1.8 FS=1.4 HC=1.5 EN=1.8
CITIES: New York City(Downtown), Los Angeles(Entertainment District), Chicago(Industrial),
        Houston(Airport), Miami(Luxury), San Francisco(Tech Campus), Seattle(Harbor)
NOTES: Best all-round starting country. Tech and Entertainment excel. Tech demand tied highest.
```

## TIER 2 — EARLY ($500K milestone | $100K-$200K unlock cost)

### United Kingdom
```
TIER:2 | UNLOCK:$500K | COST:$100K | WEALTH:1.4
DEMAND: FF=1.1 TC=1.4 FS=1.5 HC=1.6 EN=1.4
CITIES: London(Luxury), Manchester(Industrial), Edinburgh(Downtown), Birmingham(Mall), Bristol(University)
NOTES: Fashion and Healthcare strongest. London Luxury is the best slot.
```
### Germany
```
TIER:2 | UNLOCK:$500K | COST:$120K | WEALTH:1.5
DEMAND: FF=0.9 TC=1.5 FS=1.1 HC=1.7 EN=0.9
CITIES: Berlin(Tech Campus), Munich(Luxury), Hamburg(Harbor), Frankfurt(Airport), Cologne(Mall)
NOTES: Healthcare powerhouse. Frankfurt Airport highest-earning slot.
```
### France
```
TIER:2 | UNLOCK:$500K | COST:$130K | WEALTH:1.5
DEMAND: FF=1.0 TC=1.2 FS=2.0 HC=1.3 EN=1.3
CITIES: Paris(Luxury), Lyon(Downtown), Marseille(Harbor), Bordeaux(Resort), Toulouse(University)
NOTES: Fashion capital. Paris Luxury exceptional (2.0 Fashion demand).
```
### Japan
```
TIER:2 | UNLOCK:$500K | COST:$150K | WEALTH:1.6
DEMAND: FF=1.1 TC=1.8 FS=1.7 HC=1.4 EN=1.6
CITIES: Tokyo(Luxury), Osaka(Mall), Kyoto(Resort), Yokohama(Harbor), Sapporo(Downtown)
NOTES: Excellent across Tech, Fashion, Entertainment. Tokyo one of best cities in game.
```
### Canada
```
TIER:2 | UNLOCK:$750K | COST:$150K | WEALTH:1.4
DEMAND: FF=1.2 TC=1.3 FS=1.1 HC=1.7 EN=1.1
CITIES: Toronto(Downtown), Vancouver(Resort), Montreal(University), Calgary(Industrial), Ottawa(Airport)
NOTES: Healthcare specialist. Vancouver Resort hidden gem for Healthcare.
```
### Australia
```
TIER:2 | UNLOCK:$750K | COST:$160K | WEALTH:1.4
DEMAND: FF=1.3 TC=1.2 FS=1.2 HC=1.5 EN=1.4
CITIES: Sydney(Harbor), Melbourne(Downtown), Brisbane(Mall), Perth(Industrial), Gold Coast(Resort)
NOTES: Gold Coast Resort excellent for Entertainment Seasonal path.
```
### South Korea
```
TIER:2 | UNLOCK:$1M | COST:$180K | WEALTH:1.3
DEMAND: FF=1.2 TC=1.7 FS=1.8 HC=1.3 EN=1.8
CITIES: Seoul(Luxury), Busan(Harbor), Incheon(Airport), Daegu(Mall), Jeju(Resort)
NOTES: K-pop/K-beauty: Fashion and Entertainment very strong. Seoul Luxury excellent.
```
### Netherlands
```
TIER:2 | UNLOCK:$1M | COST:$170K | WEALTH:1.5
DEMAND: FF=0.9 TC=1.6 FS=1.2 HC=1.4 EN=1.2
CITIES: Amsterdam(Harbor), Rotterdam(Industrial), The Hague(Downtown), Eindhoven(Tech Campus), Utrecht(University)
NOTES: Tech hub. Eindhoven Tech Campus +10% research speed bonus.
```

## TIER 3 — MID ($3M milestone | $400K-$700K unlock cost)

### Brazil
```
TIER:3 | UNLOCK:$3M | COST:$400K | WEALTH:0.9
DEMAND: FF=1.6 TC=1.0 FS=1.1 HC=1.1 EN=1.5
CITIES: Sao Paulo(Mall), Rio de Janeiro(Resort), Brasilia(Downtown), Salvador(Harbor), Curitiba(Industrial)
NOTES: Fast Food goldmine. Rio Resort for Entertainment.
```
### India
```
TIER:3 | UNLOCK:$3M | COST:$450K | WEALTH:0.7
DEMAND: FF=1.8 TC=1.3 FS=0.8 HC=1.5 EN=1.2
CITIES: Mumbai(Mall), Delhi(Downtown), Bangalore(Tech Campus), Chennai(Harbor), Hyderabad(Industrial), Kolkata(Airport)
NOTES: Highest Fast Food demand in game (1.8). Bangalore Tech Campus strong for Tech.
```
### China
```
TIER:3 | UNLOCK:$5M | COST:$600K | WEALTH:1.1
DEMAND: FF=1.5 TC=1.6 FS=1.3 HC=1.2 EN=1.7
CITIES: Shanghai(Mall), Beijing(Downtown), Shenzhen(Tech Campus), Guangzhou(Industrial), Chengdu(Airport), Hangzhou(Luxury)
NOTES: Huge market. High regulatory crisis risk but excellent income when stable.
```
### Spain
```
TIER:3 | UNLOCK:$3M | COST:$380K | WEALTH:1.2
DEMAND: FF=1.1 TC=1.1 FS=1.4 HC=1.3 EN=1.5
CITIES: Madrid(Downtown), Barcelona(Resort), Valencia(Harbor), Seville(Airport), Bilbao(University)
NOTES: Barcelona Resort excellent for Fashion Seasonal path.
```
### Italy
```
TIER:3 | UNLOCK:$3M | COST:$400K | WEALTH:1.3
DEMAND: FF=1.0 TC=1.1 FS=1.9 HC=1.4 EN=1.3
CITIES: Milan(Luxury), Rome(Downtown), Florence(Resort), Naples(Harbor), Turin(Industrial)
NOTES: Milan Luxury second-best Fashion slot after Paris.
```
### Mexico
```
TIER:3 | UNLOCK:$3M | COST:$350K | WEALTH:0.8
DEMAND: FF=1.7 TC=0.9 FS=1.0 HC=1.0 EN=1.4
CITIES: Mexico City(Mall), Guadalajara(Industrial), Monterrey(Downtown), Cancun(Resort), Tijuana(Airport)
NOTES: Fast Food second-best after India. Cancun Resort for Entertainment.
```
### Singapore
```
TIER:3 | UNLOCK:$4M | COST:$500K | WEALTH:1.8
DEMAND: FF=1.1 TC=1.7 FS=1.6 HC=1.5 EN=1.3
CITIES: Marina Bay(Luxury), Orchard Road(Mall), Changi(Airport), Jurong(Industrial), Sentosa(Resort)
NOTES: Small but incredibly wealthy. Changi Airport +5% offline income bonus.
```
### Sweden
```
TIER:3 | UNLOCK:$4M | COST:$480K | WEALTH:1.5
DEMAND: FF=0.8 TC=1.6 FS=1.2 HC=1.6 EN=1.1
CITIES: Stockholm(Downtown), Gothenburg(Harbor), Malmo(University), Uppsala(Tech Campus), Kiruna(Industrial)
NOTES: Excellent Tech+Healthcare combo. Lowest crisis frequency of any country.
```
### Switzerland
```
TIER:3 | UNLOCK:$5M | COST:$600K | WEALTH:2.0
DEMAND: FF=0.6 TC=1.4 FS=1.5 HC=2.0 EN=0.9
CITIES: Zurich(Luxury), Geneva(Downtown), Basel(University), Bern(Airport), Lausanne(Resort)
NOTES: Highest wealth multiplier (2.0). Healthcare demand exceptional (2.0).
```
### Turkey
```
TIER:3 | UNLOCK:$3M | COST:$360K | WEALTH:0.9
DEMAND: FF=1.4 TC=1.0 FS=1.3 HC=1.1 EN=1.2
CITIES: Istanbul(Mall), Ankara(Downtown), Izmir(Harbor), Antalya(Resort), Bursa(Industrial)
NOTES: Istanbul Mall very high traffic for Fast Food. Antalya Resort for Fashion Seasonal.
```
### Poland
```
TIER:3 | UNLOCK:$3M | COST:$340K | WEALTH:1.0
DEMAND: FF=1.2 TC=1.3 FS=1.0 HC=1.2 EN=1.1
CITIES: Warsaw(Downtown), Krakow(University), Gdansk(Harbor), Wroclaw(Tech Campus), Poznan(Industrial)
NOTES: Solid all-rounder. Wroclaw Tech Campus same R&D bonus as Eindhoven.
```
### Israel
```
TIER:3 | UNLOCK:$4M | COST:$500K | WEALTH:1.4
DEMAND: FF=1.0 TC=2.0 FS=1.1 HC=1.5 EN=1.2
CITIES: Tel Aviv(Tech Campus), Jerusalem(Downtown), Haifa(Harbor), Eilat(Resort), Beer Sheva(University)
NOTES: Highest Tech demand (2.0) tied with USA. Tel Aviv Tech Campus is a gem.
```

## TIER 4 — ADVANCED ($15M milestone | $1.5M-$3M unlock cost)

### UAE
```
TIER:4 | UNLOCK:$15M | COST:$1.5M | WEALTH:1.9
DEMAND: FF=1.0 TC=1.4 FS=1.9 HC=1.3 EN=1.7
CITIES: Dubai(Luxury), Abu Dhabi(Downtown), Sharjah(Mall), Ras Al Khaimah(Resort), Fujairah(Harbor)
NOTES: Dubai Luxury third-best Fashion slot. Wealth mult 1.9.
```
### Saudi Arabia
```
TIER:4 | UNLOCK:$15M | COST:$2M | WEALTH:1.8
DEMAND: FF=1.2 TC=1.2 FS=1.0 HC=1.6 EN=1.3
CITIES: Riyadh(Downtown), Jeddah(Mall), Mecca(Airport), NEOM(Tech Campus), Dammam(Industrial)
NOTES: NEOM Tech Campus unique futuristic slot +15% Tech bonus.
```
### Indonesia
```
TIER:4 | UNLOCK:$15M | COST:$1.5M | WEALTH:0.7
DEMAND: FF=1.8 TC=1.1 FS=0.9 HC=1.0 EN=1.3
CITIES: Jakarta(Mall), Surabaya(Industrial), Bali(Resort), Medan(Downtown), Bandung(University)
NOTES: Second-highest Fast Food demand tied with Brazil. Bali Resort for Entertainment.
```
### Argentina
```
TIER:4 | UNLOCK:$15M | COST:$1.6M | WEALTH:0.8
DEMAND: FF=1.5 TC=1.0 FS=1.1 HC=1.1 EN=1.3
CITIES: Buenos Aires(Downtown), Cordoba(University), Rosario(Industrial), Mendoza(Resort), Mar del Plata(Harbor)
NOTES: High currency crisis rate but strong Fast Food when stable.
```
### South Africa
```
TIER:4 | UNLOCK:$15M | COST:$1.8M | WEALTH:0.9
DEMAND: FF=1.3 TC=1.0 FS=1.1 HC=1.2 EN=1.4
CITIES: Johannesburg(Downtown), Cape Town(Resort), Durban(Harbor), Pretoria(Airport), Port Elizabeth(Industrial)
NOTES: Cape Town Resort excellent for Entertainment. Unique "Load Shedding" crisis type.
```
### Nigeria
```
TIER:4 | UNLOCK:$20M | COST:$2M | WEALTH:0.6
DEMAND: FF=1.7 TC=0.8 FS=0.9 HC=0.9 EN=1.5
CITIES: Lagos(Mall), Abuja(Downtown), Kano(Industrial), Ibadan(University), Port Harcourt(Harbor)
NOTES: High Fast Food demand. High risk high reward. Lagos Mall massive volume.
```
### Russia
```
TIER:4 | UNLOCK:$20M | COST:$2.5M | WEALTH:1.0
DEMAND: FF=1.1 TC=1.2 FS=1.1 HC=1.3 EN=1.1
CITIES: Moscow(Downtown), St. Petersburg(Luxury), Novosibirsk(Industrial), Kazan(Mall), Sochi(Resort)
NOTES: High crisis frequency. Sochi Resort skiing-seasonal bonus for Entertainment.
```
### Vietnam
```
TIER:4 | UNLOCK:$15M | COST:$1.5M | WEALTH:0.6
DEMAND: FF=1.6 TC=1.3 FS=1.0 HC=0.9 EN=1.1
CITIES: Ho Chi Minh City(Mall), Hanoi(Downtown), Da Nang(Resort), Hai Phong(Harbor), Binh Duong(Industrial)
NOTES: Emerging market. Ho Chi Minh Mall excellent Fast Food throughput.
```
### Thailand
```
TIER:4 | UNLOCK:$15M | COST:$1.5M | WEALTH:0.8
DEMAND: FF=1.4 TC=1.1 FS=1.3 HC=1.1 EN=1.6
CITIES: Bangkok(Mall), Phuket(Resort), Chiang Mai(Downtown), Pattaya(Resort), Chonburi(Industrial)
NOTES: Two Resort slots! Phuket Resort top Entertainment Seasonal earner in Tier 4.
```
### Malaysia
```
TIER:4 | UNLOCK:$12M | COST:$1.4M | WEALTH:0.9
DEMAND: FF=1.5 TC=1.3 FS=1.1 HC=1.2 EN=1.2
CITIES: Kuala Lumpur(Downtown), Petaling Jaya(Mall), Penang(Harbor), Johor Bahru(Industrial), Kota Kinabalu(Resort)
NOTES: Solid mid-tier country with no outstanding weaknesses.
```

## TIER 5 — EXPERT ($75M milestone | $6M-$12M unlock cost)

### Egypt
```
TIER:5 | UNLOCK:$75M | COST:$6M | WEALTH:0.6
DEMAND: FF=1.5 TC=0.9 FS=1.2 HC=1.0 EN=1.4
CITIES: Cairo(Mall), Alexandria(Harbor), Sharm El-Sheikh(Resort), Luxor(Downtown), Giza(Airport)
NOTES: Giza Airport "Ancient Market" bonus +8% Fashion income.
```
### Kenya
```
TIER:5 | UNLOCK:$75M | COST:$6M | WEALTH:0.5
DEMAND: FF=1.5 TC=1.0 FS=0.9 HC=1.1 EN=1.3
CITIES: Nairobi(Downtown), Mombasa(Harbor), Kisumu(Mall), Nakuru(Industrial), Eldoret(Airport)
NOTES: Mobile tech adoption makes this a surprise Tech opportunity.
```
### Morocco
```
TIER:5 | UNLOCK:$75M | COST:$7M | WEALTH:0.7
DEMAND: FF=1.2 TC=0.9 FS=1.6 HC=1.0 EN=1.3
CITIES: Casablanca(Downtown), Marrakech(Resort), Rabat(Airport), Tangier(Harbor), Fes(University)
NOTES: Marrakech Resort strong for Fashion. "Medina Market" bonus.
```
### Colombia
```
TIER:5 | UNLOCK:$75M | COST:$7M | WEALTH:0.7
DEMAND: FF=1.4 TC=1.0 FS=1.1 HC=1.1 EN=1.4
CITIES: Bogota(Downtown), Medellin(University), Cali(Mall), Cartagena(Resort), Barranquilla(Harbor)
NOTES: Medellin "Tech Innovation" bonus +10% Tech income.
```
### Chile
```
TIER:5 | UNLOCK:$75M | COST:$8M | WEALTH:1.0
DEMAND: FF=1.3 TC=1.2 FS=1.1 HC=1.3 EN=1.2
CITIES: Santiago(Downtown), Valparaiso(Harbor), Concepcion(University), Antofagasta(Industrial), Vina del Mar(Resort)
NOTES: Most stable South American country. Lowest crisis frequency in Tier 5.
```
### Philippines
```
TIER:5 | UNLOCK:$75M | COST:$6.5M | WEALTH:0.6
DEMAND: FF=1.7 TC=1.1 FS=0.9 HC=1.0 EN=1.5
CITIES: Manila(Mall), Cebu(Harbor), Davao(Downtown), Quezon City(University), Boracay(Resort)
NOTES: Third-highest Fast Food demand (1.7). Boracay Resort for Entertainment.
```
### Pakistan
```
TIER:5 | UNLOCK:$75M | COST:$6M | WEALTH:0.5
DEMAND: FF=1.7 TC=0.8 FS=0.8 HC=0.9 EN=1.0
CITIES: Karachi(Industrial), Lahore(Mall), Islamabad(Downtown), Faisalabad(University), Rawalpindi(Airport)
NOTES: Very high Fast Food volume despite low wealth. Cheap unlock, high risk.
```
### Bangladesh
```
TIER:5 | UNLOCK:$75M | COST:$5.5M | WEALTH:0.4
DEMAND: FF=1.8 TC=0.7 FS=1.3 HC=0.8 EN=0.9
CITIES: Dhaka(Industrial), Chittagong(Harbor), Sylhet(Downtown), Rajshahi(Mall), Khulna(University)
NOTES: Cheapest Tier 5 unlock. Highest FF demand alongside India (1.8). Very high risk.
```
### Denmark
```
TIER:5 | UNLOCK:$80M | COST:$9M | WEALTH:1.6
DEMAND: FF=0.8 TC=1.5 FS=1.2 HC=1.8 EN=1.0
CITIES: Copenhagen(Downtown), Aarhus(University), Odense(Industrial), Aalborg(Harbor), Esbjerg(Airport)
NOTES: Very high Healthcare demand. Copenhagen one of best Healthcare cities.
```
### Finland
```
TIER:5 | UNLOCK:$80M | COST:$9M | WEALTH:1.5
DEMAND: FF=0.7 TC=1.8 FS=1.0 HC=1.6 EN=0.9
CITIES: Helsinki(Tech Campus), Espoo(University), Tampere(Industrial), Turku(Harbor), Oulu(Downtown)
NOTES: Helsinki Tech Campus strongest R&D bonus city in game (+20% research speed).
```
### Norway
```
TIER:5 | UNLOCK:$80M | COST:$10M | WEALTH:1.8
DEMAND: FF=0.7 TC=1.4 FS=1.1 HC=1.9 EN=0.9
CITIES: Oslo(Downtown), Bergen(Harbor), Stavanger(Industrial), Trondheim(University), Tromso(Resort)
NOTES: Highest Healthcare demand of Tier 5 countries. Very expensive, massive margin.
```
### Austria
```
TIER:5 | UNLOCK:$80M | COST:$9.5M | WEALTH:1.5
DEMAND: FF=0.9 TC=1.3 FS=1.5 HC=1.7 EN=1.2
CITIES: Vienna(Luxury), Graz(University), Linz(Industrial), Salzburg(Resort), Innsbruck(Downtown)
NOTES: Vienna Luxury top tier for Fashion. Salzburg Resort for Entertainment.
```
### Belgium
```
TIER:5 | UNLOCK:$80M | COST:$9M | WEALTH:1.4
DEMAND: FF=1.0 TC=1.4 FS=1.4 HC=1.5 EN=1.1
CITIES: Brussels(Downtown), Antwerp(Harbor), Ghent(University), Bruges(Resort), Liege(Industrial)
NOTES: EU HQ — "Policy Windfall" opportunity events more frequent.
```
### Portugal
```
TIER:5 | UNLOCK:$75M | COST:$8M | WEALTH:1.1
DEMAND: FF=1.0 TC=1.3 FS=1.3 HC=1.3 EN=1.4
CITIES: Lisbon(Downtown), Porto(Harbor), Algarve(Resort), Braga(University), Setubal(Industrial)
NOTES: Algarve Resort strong for Fashion+Entertainment Seasonal.
```

## TIER 6 — ENDGAME ($500M milestone | $28M-$60M unlock cost)

### Ethiopia
```
TIER:6 | UNLOCK:$500M | COST:$30M | WEALTH:0.4
DEMAND: FF=1.6 TC=0.6 FS=0.7 HC=0.8 EN=0.8
CITIES: Addis Ababa(Mall), Dire Dawa(Industrial), Bahir Dar(Downtown), Hawassa(University), Adama(Airport)
NOTES: Massive population, very low wealth. FF at high volume but thin margins.
```
### Peru
```
TIER:6 | UNLOCK:$500M | COST:$32M | WEALTH:0.7
DEMAND: FF=1.4 TC=0.9 FS=1.2 HC=1.1 EN=1.3
CITIES: Lima(Downtown), Cusco(Resort), Arequipa(Industrial), Trujillo(Mall), Piura(Harbor)
NOTES: Cusco Resort "Machu Picchu Tourism Boost" for Entertainment Seasonal (+20%).
```
### New Zealand
```
TIER:6 | UNLOCK:$500M | COST:$40M | WEALTH:1.4
DEMAND: FF=1.2 TC=1.3 FS=1.1 HC=1.6 EN=1.4
CITIES: Auckland(Harbor), Wellington(Downtown), Christchurch(Mall), Queenstown(Resort), Hamilton(University)
NOTES: Queenstown Resort highest base quality retention — quality decays 50% slower.
```
### Greece
```
TIER:6 | UNLOCK:$500M | COST:$35M | WEALTH:1.0
DEMAND: FF=1.1 TC=1.0 FS=1.3 HC=1.2 EN=1.6
CITIES: Athens(Downtown), Thessaloniki(Harbor), Crete(Resort), Mykonos(Luxury), Patras(Industrial)
NOTES: Mykonos Luxury: highest seasonal bonus in game for Fashion (+30% during events).
```
### Romania
```
TIER:6 | UNLOCK:$500M | COST:$30M | WEALTH:0.8
DEMAND: FF=1.3 TC=1.4 FS=1.0 HC=1.2 EN=1.0
CITIES: Bucharest(Downtown), Cluj-Napoca(Tech Campus), Timisoara(Industrial), Iasi(University), Constanta(Harbor)
NOTES: Cluj-Napoca Tech Campus — hidden gem for Tech in Tier 6.
```
### Czech Republic
```
TIER:6 | UNLOCK:$500M | COST:$32M | WEALTH:1.1
DEMAND: FF=1.2 TC=1.4 FS=1.1 HC=1.3 EN=1.2
CITIES: Prague(Downtown), Brno(University), Ostrava(Industrial), Plzen(Mall), Liberec(Airport)
NOTES: Prague Downtown tourism bonus for Entertainment. Good all-rounder.
```
### Ukraine
```
TIER:6 | UNLOCK:$500M | COST:$28M | WEALTH:0.6
DEMAND: FF=1.3 TC=1.5 FS=0.9 HC=1.1 EN=1.0
CITIES: Kyiv(Downtown), Lviv(University), Odessa(Harbor), Kharkiv(Tech Campus), Dnipro(Industrial)
NOTES: High risk. Kharkiv Tech Campus strong for Tech. Cheapest Tier 6 unlock.
```
### Kazakhstan
```
TIER:6 | UNLOCK:$500M | COST:$35M | WEALTH:0.8
DEMAND: FF=1.4 TC=1.0 FS=0.9 HC=1.1 EN=1.0
CITIES: Almaty(Downtown), Nur-Sultan(Airport), Shymkent(Mall), Aktau(Harbor), Karaganda(Industrial)
NOTES: Nur-Sultan Airport "Silk Road Hub" bonus +10% all income.
```
### Sri Lanka
```
TIER:6 | UNLOCK:$500M | COST:$30M | WEALTH:0.5
DEMAND: FF=1.3 TC=0.9 FS=1.4 HC=1.0 EN=1.3
CITIES: Colombo(Harbor), Kandy(Resort), Negombo(Mall), Jaffna(Downtown), Galle(University)
NOTES: Fashion higher than expected (textile manufacturing heritage).
```
### Myanmar
```
TIER:6 | UNLOCK:$500M | COST:$28M | WEALTH:0.4
DEMAND: FF=1.5 TC=0.6 FS=1.1 HC=0.7 EN=0.8
CITIES: Yangon(Mall), Mandalay(Downtown), Naypyidaw(Airport), Bago(Industrial), Mawlamyine(Harbor)
NOTES: Cheapest + highest risk Tier 6 country. FF volume significant if crises managed.
```

---

# SECTION 5: BRANCH SYSTEM

## Branch Data Structure (Luau)
```lua
local branch = {
    id          = HttpService:GenerateGUID(false),
    cityId      = "new_york_city",   -- references CityConfig
    countryId   = "usa",             -- references CountryConfig
    level       = 1,                 -- 1-10
    path        = nil,               -- "volume"|"premium"|"seasonal"|nil
    pathTier    = 0,                 -- 0-5 (upgrades chosen within path)
    quality     = 75,                -- 0-100
    staffSlots  = 2,                 -- base 2, increases at levels 3,5,7,9
    openedAt    = os.time(),
    renovatedAt = 0,
    name        = nil,               -- optional player-given branch name
}
```

## Branch Opening Costs by Industry and Tier
```
Tier 1-2 base costs:
  Fast Food:$15K  Tech:$35K  Fashion:$22K  Healthcare:$45K  Entertainment:$55K
  Cafe:$8K  Fitness:$40K  Hotel:$60K  Retail:$18K  Sports:$50K
  Automotive:$70K  Real Estate:$80K  Music:$30K  Social Media:$35K  Aerospace:$200K

Tier multipliers: Tier 3 x3 | Tier 4 x8 | Tier 5 x25 | Tier 6 x80
```

## Branch Level Upgrade Costs
```
LVL | COST MULT | INCOME MULT | STAFF SLOTS
 1  |  1.0x     |  1.00x      |  2  (opening cost)
 2  |  0.8x     |  1.25x      |  2
 3  |  1.2x     |  1.55x      |  3  (slot unlocked)
 4  |  1.8x     |  1.90x      |  3
 5  |  2.7x     |  2.30x      |  4  (slot unlocked)
 6  |  4.0x     |  2.80x      |  4
 7  |  6.0x     |  3.40x      |  5  (slot unlocked)
 8  |  9.0x     |  4.10x      |  5
 9  |  13.5x    |  4.95x      |  6  (slot unlocked)
10  |  20.0x    |  6.00x      |  6  (maximum)
```

## Upgrade Paths

### VOLUME PATH
```
Focus: Maximum customers, lower margin/customer
Bonus: +15% income per staff assigned to branch (stacks)
Best for: High-population countries, Fast Food, Cafe, Retail, Sports

Sub-upgrades (5 tiers, pick one option per tier):
Tier 1: Express Queue(+8% throughput) | Combo Deal Boards(+6% revenue/customer) | Self-Service(-1 staff req)
Tier 2: Drive-Through Lane(+12% throughput, FF/Cafe +18%) | Bulk Purchase(-8% overhead) | Extended Hours(+10% + offline bonus)
Tier 3: Digital Order System(+15% volume) | Loyalty Card(+10% revenue, +5 brand) | Second Wing(+20% income, +1 staff req)
Tier 4: Automated Checkout(-2 staff req, min 1) | Regional Supply Hub(-15% overhead) | Flash Sale(x1.5 income 10min/2hrs)
Tier 5: Full Automation(-1 staff, +5% income) | Volume Leader Bonus(+25% if top-earning branch) | Franchise Licensing(+5% passive income)
```

### PREMIUM PATH
```
Focus: Fewer customers, much higher margin/customer
Bonus: +0.4x income multiplier per executive tier owned (all 4 execs each count)
Best for: Wealthy countries, Fashion/Tech/Hotel/Auto/Fitness, Luxury/Resort slots

Sub-upgrades (5 tiers):
Tier 1: VIP Lounge(+20% revenue/customer) | Concierge Service(+15% quality decay slower) | Members-Only(+10% income, +3 brand/mo)
Tier 2: Private Consultation(+18% margin, HC/FT +25%) | Premium Packaging(+12%, +5 brand, FS +20%) | Curated Experience(+15%, -20% crisis)
Tier 3: Exclusive Membership Club(+25% repeat) | Bespoke Service(+22%, +1 staff req) | Executive Partnership(+30% if COO/CMO hired)
Tier 4: Personal Advisor(+30% margin) | White Glove Delivery(+20%, immune quality crisis) | Ultra Luxury Rebrand(+40%, brand must stay >70)
Tier 5: Invitation-Only(+50% top 10%) | Celebrity Ambassador(+35%, +10 brand, CMO req) | Flagship Status(+2% to all other Premium branches)
```

### SEASONAL PATH
```
Focus: Low baseline, massive spikes during seasonal events
Bonus: x3.0 during events (x4.0 for Entertainment/Sports, x5.0 Retail on Black Friday)
Best for: Resort slots, Entertainment/Sports/Retail/Music industries

Sub-upgrades (5 tiers):
Tier 1: Holiday Decoration(+30% events, -5% baseline) | Event-Ready Layout(-20% next upgrade cost) | Pop-Up Flexibility(free event type switch)
Tier 2: Limited Edition Products(+40% events) | Event Staffing Contract(no morale decay during events) | Advance Ticketing(income starts 2hr early)
Tier 3: Seasonal Brand Identity(+50% events, +5 brand/event) | Cross-Season Strategy(baseline 0.8x not 0.5x) | Flash Collab Drop(1 random opp/season)
Tier 4: Event Anchor Status(highest multiplier on server) | Multi-Season Package(spikes last 50% longer) | Viral Moment Machine(15% chance Breaking News spike)
Tier 5: Year-Round Festival(1.2x even outside events) | Legendary Seasonal(x5.0 multiplier max) | Event Empire Network(3+ Seasonal branches: all +20% event)
```

## City Slot Types and Bonuses
```
AIRPORT:     +8% all income, +5% offline income. Valid: all industries
MALL:        +6% volume income, +3% all, -10% morale decay. Valid: all except Aerospace, Sports
DOWNTOWN:    +5% all income, +5% brand gain rate. Valid: all
LUXURY:      +25% Premium income, immune quality reputation damage. Valid: all except Aerospace, Sports
RESORT:      +50% Seasonal multiplier, +10% Entertainment/Sports/Hotel always. Valid: all except Aerospace
INDUSTRIAL:  -15% overhead, +10% Volume income. Valid: all
UNIVERSITY:  -15% hire cost, +10% R&D speed per owned. Valid: all except Aerospace
TECH CAMPUS: +20% Tech/Social/Aerospace income, +15% R&D speed. Valid: Tech, Social, Aerospace, Fitness, Real Estate
HARBOR:      +10% offline, +5% all, -10% supply chain crisis. Valid: all except Aerospace, Sports
ENTERTAINMENT DISTRICT: +20% Entertainment/Music income, +10% Seasonal, viral events +25%. Valid: Entertainment, Music only
```

## Branch Quality System
```lua
local QualityConfig = {
    STARTING_QUALITY     = 75,
    BASE_DECAY_PER_HOUR  = 1,   -- standard: -1/hr
    HOTEL_DECAY_PER_HOUR = 2,   -- hotel industry: -2/hr
    -- COO T1: x0.7 decay | COO T2: x0.5 | COO T3: x0.3 | +Predictive Maint: -0.2/hr
    INCOME_MULTIPLIERS = {
        {min=90, max=100, mult=1.20}, {min=70, max=89, mult=1.10},
        {min=50, max=69, mult=1.00},  {min=30, max=49, mult=0.85},
        {min=10, max=29, mult=0.70},  {min=0,  max=9,  mult=0.50},
    },
}
-- Renovation: 30% of branch market value -> quality = 100 instantly
-- Brand effects: avg quality <50 -> -1 brand/day | avg quality >80 -> +0.5 brand/day
```

---

# SECTION 6: STAFF SYSTEM

## Staff Data Structure (Luau)
```lua
local staffMember = {
    id            = HttpService:GenerateGUID(false),
    name          = "Emma",        -- from 150-name pool
    specialty     = "sales_expert",-- one of 15 specialties
    level         = 1,             -- 1-4
    morale        = 80,            -- 0-100
    branchId      = nil,           -- string GUID (L4 can be array of up to 3)
    hiredAt       = os.time(),
    transferredAt = 0,             -- for 300s cooldown
    quitTimer     = nil,           -- os.time()+600 when triggered
}
```

## Staff Name Pool (150 names)
```
Western: Emma,Liam,Sophia,Noah,Olivia,James,Ava,William,Isabella,Oliver,Mia,Benjamin,
         Charlotte,Elijah,Amelia,Lucas,Harper,Mason,Evelyn,Logan,Abigail,Ethan,Emily,
         Aiden,Elizabeth,Jackson,Sofia,Sebastian,Avery,Mateo,Ella,Jack,Madison,Owen,
         Scarlett,Theodore,Victoria,Luke,Aria,Jayden,Grace,Dylan,Chloe,Grayson,Penelope,Levi,Riley
Latin:   Carlos,Maria,Jose,Ana,Luis,Rosa,Miguel,Carmen,Pedro,Elena,Diego,Gabriela,
         Rafael,Isabella,Fernando,Valentina,Alejandro,Camila,Juan,Sofia,Ricardo,
         Lucia,Eduardo,Paula,Andres,Natalia
Asian:   Wei,Yuki,Raj,Priya,Jin,Mei,Arjun,Sakura,Chen,Aiko,Vikram,Yuna,Sanjay,Hana,
         Akira,Preethi,Kento,Ananya,Takeshi,Divya,Hiroshi,Mio,Ravi,Kenji,Pooja,
         Haruto,Nisha,Daichi,Kavya
African: Amara,Kofi,Nadia,Kwame,Zara,Chukwu,Fatima,Obinna,Aisha,Seun,Ngozi,Emeka,
         Adaeze,Yusuf,Kemi,Tunde,Bisi,Chidi,Funmi,Wale
Middle East: Omar,Layla,Hassan,Nour,Ali,Yasmine,Karim,Dina,Tariq,Rania,Samir,Lina,Fadi,Mona,Ziad,Hala
E. European: Alexei,Katya,Dmitri,Natasha,Pavel,Oksana,Ivan,Olga,Mikhail,Svetlana
```

## All Staff Specialties (15 types)
```
1. Sales Expert      L1:+12% rev L2:+18% L3:+25% L4:+35%  (High drop weight)
2. Cost Cutter       L1:-10% overhead L2:-15% L3:-22% L4:-30%  (High)
3. Morale Booster    L1:halve decay L2:stop decay L3:stop+restore 1/hr L4:restore 2/hr  (Medium)
4. Speed Demon       L1:+15% Volume L2:+22% L3:+30% L4:+40%  (Volume only, no Premium/Seasonal)  (Medium)
5. Recruiter         L1:-20% hire cost L2:-30% L3:-40% L4:-50% + -10% severance  (Medium)
6. Quality Inspector L1:decay-30% slower L2:-50% L3:-70%+0.3 regen/hr L4:-80%+0.5 regen/hr  (Medium)
7. Trainer           L1:-25% promo cost L2:-35% L3:-50% L4:-50%+L4 promos instant  (Low — unlocks $5M)
8. Negotiator        L1:-15% branch cost in country L2:-20% L3:-20%+-10% unlock cost L4:-25% all expansion  (Low)
9. Crisis Manager    L1:-25% crisis damage L2:-40% L3:-50%+2min window L4:-60%  (Low)
10. Data Analyst     L1:+8% income L2:+12% L3:+15%+reveals next board decision L4:+20%+10% contract speed  (Low — unlocks $25M)
11. Social Media Mgr L1:+3 brand/mo L2:+5 L3:+7+-30% PR crisis L4:+10 global SMM  (Low-Med)
12. Logistics Expert L1:+15% offline L2:+22% L3:+30% L4:+40% (Regional VP: all branches)  (Low-Med)
13. Customer Relations L1:+10% contract rewards L2:+18% L3:+25%+1 extra contract slot L4:+35%  (Low-Med)
14. Finance Wizard   L1:+12% dividends L2:+20%+-5% buy cost L3:+30%+crash warn 8min L4:+40%+1 crash immunity  (Very Low)
15. Innovation Lead  L1:+1 R&D visible option L2:-15% research time L3:-25%+preview bonuses L4:-35%+bonuses +10% stronger  (Very Low)
```

## Promotion Tree
```
L1 Entry Level      | Base salary | Specialty x1.0
L2 Shift Manager    | $5,000 cost | Specialty x1.3 | Can cover 2 branches
L3 Store/Dept Lead  | $25,000     | Specialty x1.6 | Morale never below 20
L4 Regional VP      | $100,000    | Specialty x2.0 | Oversees 3 branches | Cannot quit
```

## Morale System
```lua
-- Decay: every 600 seconds (10 min)
-- Base: -2 | Branch quality <50: -1 extra | Active crisis: -1 extra | Unresolved 30min+: -2 extra
-- Recovery: Pay Branch Bonus $500 x staff count -> all 100 | Morale Booster L3/L4: passive regen
-- Quit: morale=0 -> quitTimer=os.time()+600 | Regional VP (L4) cannot quit
-- Employee Wellness R&D: morale floors at 1, quit blocked
-- Warn client at morale=10 (quitWarning=true in SyncStaff)
```

## Costs
```
Fresh hire: $2,000 base (Recruiter L1:$1,600 L2:$1,400 L3:$1,200 L4:$1,000)
Promotions: L2=$5K | L3=$25K | L4=$100K
Severance:  L1=$1K | L2=$2.5K | L3=$8K | L4=$25K
Transfer cooldown: 300 seconds (bonus halved during cooldown)
```

---

# SECTION 7: EXECUTIVE SYSTEM

4 slots: COO, CMO, CFO, CTO. One exec per role. Company-wide bonuses.
Replacing: new hire cost + 20% severance of replaced exec.

```
COO — Chief Operating Officer (quality, overhead, operations)
  T1 $50K:  overhead -10%, quality decay -30% slower, renovation -10% cost
  T2 $200K: overhead -18%, decay -50%, renovation -20%, branch open -10%
             Unlocks: "Operational Excellence" board option
  T3 $1M:   overhead -28%, decay -70%, renovation -35% (restores to 110 quality),
             branch open -20%, staff quit -25%
             Unlocks: "Zero Defect Protocol" (quality crisis immunity 48h, weekly)

CMO — Chief Marketing Officer (brand, demand, marketing)
  T1 $50K:  brand cap -> 110, +5 brand on hire, demand +8%, PR campaign CD 48h->36h
             Unlocks: PR Campaign board action
  T2 $200K: brand cap -> 120, +8 brand, demand +15%, campaign CD->24h cost->$350K,
             celebrity events +30% more frequent
             Unlocks: "Market Domination" board option
  T3 $1M:   brand cap -> 130, +12 brand, demand +25%, campaign CD->16h cost->$200K,
             brand gain +50% faster, viral events +50% more frequent
             Unlocks: "Brand Legend" (gold name on leaderboard)

CFO — Chief Financial Officer (offline, contracts, financial)
  T1 $50K:  offline cap 8h->12h, contracts +20%, stock commission -10%, crash impact -10%
             Unlocks: "Financial Hedge" board option
  T2 $200K: offline 8h->18h, contracts +35%, commission -20%, crash -20%, slots 3->4
             Unlocks: "Debt Leverage" board action
  T3 $1M:   offline 8h->24h, contracts +50%, commission -35%, crash -40%, slots 3->5,
             dividend income +25%
             Unlocks: "IPO Advantage" (legacy mult +0.15/IPO instead of +0.10)

CTO — Chief Technology Officer (R&D speed, tech/digital income)
  T1 $50K:  R&D speed +25%, R&D cost -15%, Tech/Social income +10%
  T2 $200K: R&D speed +50%, cost -25%, income +20%, University slot +10% R&D speed
             Unlocks: Extra R&D slot (3 concurrent)
  T3 $1M:   R&D speed +75%, cost -40%, income +30%, University slot +15% R&D speed,
             all R&D bonus strength +20%
             Unlocks: 4th R&D slot, "R&D Breakthrough" (once/season: complete any project instantly)
```

---

# SECTION 8: RESEARCH & DEVELOPMENT

## System Rules
```lua
-- Slot count: 2 base + 1 (Extra R&D Slot pass) + 1 (CTO T2) + 1 (CTO T3 + pass) = max 4
-- Each project once per season. Reset on IPO.
-- Social Media industry: each completed R&D gives +5% permanent income (stacks)
-- Aerospace industry: all R&D bonus strength is 3x
```

## All 25 R&D Projects
```
 1. Signature Product/Service  All | $25K | 60min | +20% income all branches
 2. Loyalty App                All | $35K | 75min | -30% staff morale decay globally
 3. Automation Suite           All | $80K | 120min| -1 required staff slot per branch
 4. Market Intelligence        All | $15K | 30min | Reveals all locked country demand multipliers
 5. Crisis Response Protocol   All | $45K | 75min | -40% damage from all crises
 6. Supply Chain Optimization  All | $30K | 60min | -15% branch opening cost globally
 7. Premium Experience Design  All | $55K | 90min | All Premium branches +0.30x income mult
 8. Viral Marketing Campaign   All | $20K | 45min | One-time +25 brand score
 9. AI Analytics Platform      All | $100K| 150min| +18% all income (can't stack with #1)
10. Employee Wellness Program  All | $40K | 90min | Staff morale floors at 1, no quits
11. Green Initiative           All | $35K | 75min | +12 brand score + gov contracts +20%
12. Mobile Application         All | $50K | 90min | +10% income + offline cap +2h
13. Predictive Maintenance     All | $30K | 60min | +0.3 quality/hour passive all branches
14. International Trade Deal   All | $120K| 180min| -30% unlock cost Tier 4+5 countries
15. Customer Satisfaction Score All | $25K | 45min | +20% investor contract rewards
16. Franchise Training Kit     All | $60K | 90min | All staff specialty bonuses +20% stronger
17. Hostile Takeover Prep      All | $40K | 60min | +15% takeover success + response window 8min
18. Brand Refresh Campaign     All | $20K | 40min | +20 brand score + decay -50% for 7 days
19. Recipe Innovation          Fast Food,Cafe only | $30K | 60min | +20% FF/Cafe income
20. Platform Launch            Tech,Social Media only | $75K | 120min| +30% income
21. Signature Collection       Fashion only | $45K | 80min | +25% income + Seasonal +0.5x
22. Clinical Excellence        Healthcare only | $80K | 100min| +25% income + immune malpractice
23. Blockbuster Engine         Entertainment,Sports | $60K | 90min | +35% Seasonal + events last 20% longer
24. Security Fortress          All | $55K | 90min | Tech/Social: immune data/server crises; Others: -25% digital crisis
25. Global Partnership Network All ($100M req) | $200K | 240min| -20% all remaining country costs + 5% per Tier5+ country
```

---

# SECTION 9: BRAND REPUTATION SYSTEM

```lua
-- Brand income multiplier:
local function getBrandMult(score) -- 0.5x at 0, 1.2x at 100, up to 1.5x at 130 (CMO prestige)
    local base = 0.5 + (math.min(score,100)/100) * 0.7
    if score > 100 then base = base + (score-100) * 0.005 end
    return base
end
-- Range: 0-100 (110 with CMO T1, 120 T2, 130 T3). Starting: 50.
```

## Score Raises
```
Contract completed:+5 | Board success:+2 | Revenue milestone:+3/+5/+8/+12
Crisis resolved:+8 | Viral Marketing R&D:+25 | Brand Refresh R&D:+20 | Green Initiative:+12
PR Campaign:+15 | Hiring CMO: T1+5, T2+8, T3+12 | Viral event:+10-20
Quality avg >80:+0.5/day | Renovation:+1 | IPO:+10 | Season Pass weekly:+2
```

## Score Lowers
```
Quality avg <50:-1/day | Staff quits:-3 | Major stock crash:-5
Failed crisis:-10 to -25 | Ignored crisis: same + secondary crisis 50% chance
Food contamination scare (worst single): -22 | Celebrity scandal (Music/Entertainment): -18
Data breach (Tech/Social): -15 to -20 | Wrong board decision: -3 to -8
```

## Brand Score Tiers
```
130: "Global Icon" — legendary, gold name, unique Breaking News variants
110-129: "Market Leader" — CMO prestige zone
90-109:  "Trusted Brand"
70-89:   "Reputable" — most players operate here
50-69:   "Building" — starting zone
30-49:   "Struggling" — below average, crises more likely
10-29:   "At Risk" — low income, takeover vulnerable
0-9:     "Damaged" — minimum income, crisis magnet
```

---

# SECTION 10: STOCK MARKET SYSTEM

```
5 original Industry Indexes: FFIDX, TCIDX, FSIDX, HCIDX, ENIDX
Extended indexes added when 5+ players use each new industry:
CFIDX, FTIDX, HTIDX, RTIDX, SPIDX, ATIDX, REIDX, MUIDX, SMIDX
(Aerospace not indexed — too few players)

Each index: Starting $100, ±2% per 60-second tick, momentum modifier,
24h candle history stored in DataStore, sell pressure -2% modifier

Crash types: Minor(-15-25% 1 index), Moderate(-30-45% 1-2), Major(-50-65% 2-3),
             Industry Event(-20-40% triggered by crisis), Correction(-5-15% natural)
All crashes except Correction: 5-minute warning in news ticker

Player trading: Buy/Sell via RemoteEvents | Max 1,000 units any single stock
Listing: Net worth >$500K | 5% listing fee upfront | 2% of income as dividends
         Max 30% of company shares outstanding | Delist: buy back at price +10%
```

---

# SECTION 11: BOARD DECISIONS (65 Types)

3 per day (4 with Season Pass). Seeded by playerID + date. Options A/B/C.

## CATEGORY: Market Expansion (12)
```
1.  ACCELERATED ENTRY:       A)Enter 2x cost early B)Wait normal price C)Skip market
2.  REGIONAL DISTRIBUTION:   A)Accept deal -10% cost +$20K B)Negotiate -5% free C)Decline
3.  COMPETITOR TERRITORY:    A)Enter aggressively (2 branches) B)Enter cautiously C)Let rival keep it
4.  CITY SLOT PREMIUM:       A)Bid high 2.5x for Luxury B)Bid moderate 50% chance C)Don't bid
5.  JOINT VENTURE:           A)Accept -40% cost share 20% income B)Full price 100% C)Counter -20% share 10%
6.  FAST EXPANSION LOAN:     A)$500K now repay $600K/14days B)Decline C)$250K repay $295K/7days
7.  MARKET RESEARCH:         A)Hire $15K reveal 5 countries B)DIY slower C)Intuition
8.  FRANCHISE ZONE LICENSE:  A)Buy $80K +15% income 60days B)Ignore C)Buy+lobby $120K 90days
9.  CITY RENOVATION:         A)Open 2 branches -30% discount B)Open 1 C)Wait for slot upgrade
10. SATELLITE OFFICE CHAIN:  A)3 branches 60% income 50% cost B)1 premium branch C)Decline
11. INTERNATIONAL TRADE BLOC:A)Join $50K -20% in 5 countries B)-10% all free C)Stay independent
12. STRATEGIC WITHDRAWAL:    A)Sell 30% market value B)Invest $30K stabilize C)Redirect staff close free
```

## CATEGORY: Staff & HR (12)
```
13. TALENT ACQUISITION:     A)Poach $25K L3 staff B)Hire L2 $8K C)Internal promotions
14. UNION DEMAND:           A)Agree all morale+20 cost+$50K/mo B)Partial morale+8 C)Refuse morale-15 30% strike
15. TEAM BUILDING DAY:      A)Full retreat $30K morale->90 5day pause B)Lunch $8K +20 C)Virtual $2K +8
16. STAR EMPLOYEE PROMO:    A)Promote+$5K bonus morale+30/+10 B)Promise morale+15 C)Ignore morale-20 50% quit
17. EXTERNAL TRAINING:      A)Full $40K +15% bonuses 30d B)Partial $15K one branch +25% C)Internal free 7d +8%
18. STAFF REFERRAL:         A)Launch $10K next 5 hires reroll B)Micro $3K 2 hires C)Decline
19. TALENT POACHING (rival): A)Counter-offer $20K morale+25 B)Let go +$5K exit C)Block legal -$5K 80% stays
20. OVERTIME REQUEST:        A)Premium +50% cost income+30% 24h morale-15 B)Standard +20% +15% morale-5 C)Decline
21. RESTRUCTURE PROPOSAL:    A)Full $25K -1 staff slot 30d B)Partial $10K one country C)Decline
22. WELLNESS INITIATIVE:     A)Full $15K decay-20% 30d B)App $3K -8% 30d C)Decline
23. PERFORMANCE REVIEW:      A)Reward $20K morale+25 brand+3 B)Rank-and-yank eff+5% morale-30 C)Skip
24. REMOTE WORK POLICY:      A)Full remote morale+15 income-5% B)Hybrid morale+8 C)Office morale-10 income+3%
```

## CATEGORY: Financial Decisions (10)
```
25. DIVIDEND PAYOUT:      A)Large $100K brand+8 B)Small $30K brand+3 C)No payout save cash
26. DEBT RESTRUCTURING:   A)Restructure $10K unlock $1M@15% B)Minor $5K $500K@18% C)Decline
27. EMERGENCY RESERVE:    A)$50K fund absorbs next 2 crises B)$20K absorbs 1 C)No reserve
28. REVENUE REINVESTMENT: A)Expansion fund -20% next 3 opens B)Staff fund -25% next 10 hires C)Ops -30% renos 14d
29. TAX OPTIMIZATION:     A)Full $15K income+8% 30d small risk B)Standard $5K +3% C)Decline
30. SHARE BUYBACK:        A)Full buyback end dividend B)Partial 50% C)Decline
31. EMERGENCY CAPITAL:    A)Issue bonds +$200K -2% income 30d B)Small +$75K -0.5% C)Decline
32. COST AUDIT:           A)Act all $20K overhead-12% 60d B)Some $8K -5% 30d C)Ignore
33. INSURANCE PACKAGE:    A)Full $25K/mo next crisis zeroed B)Basic $8K -50% C)Self-insure
34. STRATEGIC INVESTMENT: A)$50K->$75K in 7d B)$20K->$24K 7d low risk C)Decline
```

## CATEGORY: Brand & Marketing (10)
```
35. CELEBRITY ENDORSEMENT: A)Major $80K brand+15 income+12% 30d B)Micro $15K brand+5 +4% 14d C)Decline
36. PR CAMPAIGN:           A)National $200K brand+15 all countries B)Regional $80K brand+8 one region C)Social $20K brand+4
37. REBRANDING:            A)Full $50K -5 brand then +20 after 3d B)Refresh $20K +10 after 2d C)Decline
38. CHARITY PARTNERSHIP:   A)Major $30K brand+10 +5/wk 4wks B)Small $8K brand+3 C)Decline
39. AWARDS CAMPAIGN:       A)Major $25K 70% chance +12 brand B)Small $8K 40% chance +6 C)Organic 15% chance +4 free
40. CRISIS COMMUNICATIONS: A)Proactive $10K scandal damage -50% B)Prepare $3K damage -20% C)Ignore full damage
41. BRAND AMBASSADOR:      A)Full $20K SMM bonus +50% 30d B)Lite $8K +25% 14d C)Decline
42. DEFAMATION DEFENSE:    A)Legal $15K damage stopped rival-10 B)PR $8K damage halved C)Ignore brand-5
43. VIRAL CONTENT PUSH:    A)All in $25K 60% viral +18 brand +15% 48h B)Safe $10K 85% +7 brand C)Skip
44. SPONSORSHIP:           A)Title $60K brand+12 income+8% 7d B)Supporting $20K brand+5 +3% C)Decline
```

## CATEGORY: Operations (11)
```
45. QUALITY OVERHAUL:       A)Company $40K all branches +30 quality B)Priority $15K top 3 +40 C)Cheap $8K bottom 3 +50
46. TECH UPGRADE:           A)Full $30K +5% all income B)Partial $12K +2% C)Decline
47. SUPPLY CHAIN REVIEW:    A)Full $25K supply crises -60% 30d B)Partial $10K -30% 14d C)Ignore
48. ENERGY EFFICIENCY:      A)Install $35K overhead -8% permanent B)Partial $15K -3% permanent C)Decline
49. STANDARDIZATION:        A)Full $20K quality floor raised to 30 B)Partial floor to 15 C)Decline
50. EMERGENCY PROTOCOL:     A)Full $15K crisis response windows +3min B)Quick $5K +1min C)Decline
51. BRANCH AUDIT:           A)Full $10K reveals+fixes worst inefficiency B)Scan $3K reveals only C)Decline
52. LOGISTICS PARTNERSHIP:  A)Full $20K/mo offline+15% 30d B)Trial $5K +5% 7d C)Decline
53. RENOVATION ROUND:       A)All branches $30K+$10K each quality->100 B)Top 5 scaled C)One normal cost
54. PROCESS AUTOMATION:     A)Pilot free +10% 14d (if success unlock full) B)Full $60K -1 staff all branches C)Decline
55. OPENING HOURS:          A)24/7 all $25K +15% income morale-8 B)Extended top 3 $10K +12% C)Current fine
```

## CATEGORY: Competitive & Events (10)
```
56. HOSTILE TAKEOVER TARGET: A)Launch 15% net worth 40-70% success B)Wait observe C)Decline
57. DEFEND TAKEOVER:         A)Legal $30K 80% defense B)PR $15K 50% defense brand+5 C)Accept 150% market value
58. PARTNERSHIP OFFER:       A)Explore merger (Corporation Mode prompt) B)Strategic alliance 5% revenue share C)Decline
59. INDUSTRY AWARD:          A)Campaign $20K 70% chance +15 brand ticker B)Accept nomination 30% chance +8 C)Withdraw
60. MARKET DISRUPTION:       A)Price war -10% income 14d rival slowed B)Quality push $20K +5% after 3d C)Ignore
61. CONFERENCE SPONSORSHIP:  A)Title $50K brand+10 +5% 7d networking B)Exhibitor $15K brand+4 C)Attend $5K brand+1
62. SEASONAL CAMPAIGN:       A)Max budget $40K seasonal mult +0.5x next event B)Standard $15K +0.2x C)No campaign base mult
63. MARKET CRASH RESPONSE:   A)Buy dip $100K stocks B)Hold cash C)Diversify sell 50% holdings
64. COMPETITIVE INTEL:       A)Full $10K see rival brand/country/net worth 7d B)Basic $3K brand only C)Decline
65. CRISIS SIMULATION:       A)Full drill $8K next crisis +5min +damage-15% B)Quick $2K +2min only C)Decline
```

---

# SECTION 12: EVENTS & NEWS SYSTEM

## News Ticker (Top Bar ScrollingFrame)
```lua
-- Priority levels set TextColor3:
-- "normal"   -> TEXT_PRIMARY color
-- "warning"  -> AMBER_DEFAULT color
-- "breaking" -> RED_DEFAULT color + pulse UIScale animation on ticker area
-- Implementation: inner TextLabel with all items concat, TweenService on CanvasPosition.X
```

## Crisis Events (45 total — 10 per industry + 5 universal)

```
Fast Food (10): health_inspection_failure, supply_chain_shortage, food_contamination_scare,
                staff_walkout, competitor_price_war, delivery_delay, equipment_breakdown,
                bad_review_viral, ingredient_price_spike, health_department_audit

Tech (10):      server_outage, data_breach, security_vulnerability, key_engineer_quit,
                product_launch_delay, competitor_feature_copy, regulatory_investigation,
                bad_app_review, patent_dispute, AI_ethics_controversy

Fashion (10):   knockoff_scandal, influencer_fallout, trend_miss, fabric_shortage,
                sweatshop_accusation, celebrity_disassociation, fashion_week_disaster,
                viral_bad_review, return_rate_spike, copyright_infringement

Healthcare (10):malpractice_claim, regulatory_audit, supply_drug_shortage, staff_burnout_mass,
                insurance_dispute, health_scandal, data_privacy_breach, inspection_failure,
                staff_union_strike, competitor_undercutting

Entertainment(10):box_office_flop, streaming_rights_lost, celebrity_scandal, bad_critic_review,
                production_delay, copyright_lawsuit, audience_boycott, technical_failure_live,
                talent_dispute, piracy_surge

Universal (5):  natural_disaster, political_instability, currency_devaluation, power_outage, logistics_breakdown

(New industries each have 10 crises as defined in Section 3 — see each industry entry)
```

## Crisis Response Options (all crises)
```
A) Pay to resolve: cost scales $5K-$80K by severity | crisis ends now | damage halved
B) Ride it out:    $0 cost | accept full damage for stated duration
C) Ignore:         $0 | full damage + 50% chance secondary crisis (75% for Music industry)
   Only available first 120 seconds of response window
Crisis Manager specialty and Crisis Response Protocol R&D reduce damage further.
```

## Opportunity Events (20 types)
```
OPP-1:  viral_moment              income+30% 20min, brand+10
OPP-2:  celebrity_endorsement     brand+12, income+8% 48h (free)
OPP-3:  government_contract       cash = 30% monthly income, brand+5
OPP-4:  media_feature             brand+15, income+5% 24h
OPP-5:  investor_windfall         $100K-$500K cash
OPP-6:  competitor_bankruptcy     demand in one country +20% 72h
OPP-7:  trade_deal_bonus          one country unlock -50% cost for 24h
OPP-8:  staff_talent_walkin       free L2 specialist available
OPP-9:  industry_event_spike      Seasonal path income +0.5x next event
OPP-10: quality_award             brand+8, all branch quality+10
OPP-11: research_breakthrough     one R&D project completes instantly
OPP-12: market_expansion_tip      reveals best-performing country for your industry
OPP-13: merger_interest           Corporation Mode prompt
OPP-14: patent_success            $50K cash + brand+5
OPP-15: community_recognition     brand+10, local branch income+20% 48h
OPP-16: supply_deal               branch open cost -20% one country 7 days
OPP-17: talent_conference         next 3 hires guaranteed rare specialty
OPP-18: viral_product_launch      Entertainment/Fashion/Music/Retail: immediate mini-event spike
OPP-19: regulatory_approval       Healthcare: new branch slot opens in restricted country
OPP-20: funding_round             Tech/Social Media: $200K cash (simulates VC)
```

## Seasonal Events (12 per year)
```
EVENT                    | DURATION | KEY MULTIPLIERS
1. HOLIDAY RUSH (Dec)    | 48h      | FF:2.5 EN:3.5 RT:3.0 SP:2.5 others:1.5
2. SUMMER SALE (Jul-Aug) | 36h      | FS:2.5 EN:2.0 RT:2.0 CF:2.0 FF:1.8
3. TECH SUMMIT (Mar)     | 24h      | TC:3.0 SM:3.0 AE:2.5 others:1.2
4. FASHION WEEK (Feb,Sep)| 24h      | FS:3.5 MU:2.0 HT:1.8 EN:1.5 (fires twice/year)
5. HEALTH MONTH (Oct)    | 72h      | HC:2.0 FT:2.5 others:1.1
6. ENTERTAINMENT AWARDS  | 24h      | EN:3.0 MU:3.5 SP:2.0 FS:1.5
7. NEW YEAR LAUNCH (Jan1)| 24h      | ALL:1.8 (universal — only event affecting every industry)
8. BACK TO SCHOOL (Aug)  | 24h      | FF:1.6 CF:2.0 TC:1.8 RT:1.6
9. VALENTINES (Feb 14)   | 12h      | FS:2.0 EN:2.0 MU:2.5 FF:1.5 HT:2.0
10.BLACK FRIDAY (Nov)    | 24h      | RT:5.0 FF:2.0 FS:2.5 EN:1.8 (RT unique max)
11.WORLD CUP/SPORT EVENT | 48h      | SP:4.5 FF:2.5 EN:3.0 others:1.3
12.INNOVATION SHOWCASE   | 24h      | TC:2.5 SM:3.0 HC:1.5 AE:3.0

Seasonal path bonus stacks MULTIPLICATIVELY with these event multipliers.
Resort city slot stacks +50% further on Seasonal multiplier.
```

---

# SECTION 13: INVESTOR CONTRACTS

```lua
-- Slot count: 3 base, +1 with CFO T2, +1 with CFO T3 (max 5)
-- Each contract: 72-hour deadline from generation
-- Auto-complete checked on login and every 300 seconds
-- Requirements scale to ~1.5x player's current revenue level
```

## All 25 Contract Types
```
 1. Revenue Milestone:    Reach $X cumulative this session -> 30% of X cash + brand+5
 2. Branch Expansion:     Open X total branches -> $X,000 x count + brand+3
 3. Global Reach:         Branches in X countries -> large cash + brand+8
 4. Staff Milestone:      X total staff employed -> cash + brand+4
 5. Quality Standard:     Avg quality >X for 24h -> cash + brand+6
 6. Brand Target:         Reach brand score X -> cash + extra PR Campaign charge
 7. Income Per Hour:      Achieve $X/hr -> cash + 24h extra contract slot
 8. Country Domination:   X branches in one country -> +15% income that country 7d + cash
 9. Executive Hire:       Hire any executive -> cash + 20% of hire cost refunded
10. Research Complete:    Complete 2 R&D projects -> cash + free R&D slot 48h
11. Seasonal Performance: Earn $X during next event -> large cash + Seasonal +0.5x permanent
12. Net Worth Threshold:  Reach net worth $X -> 30% of X cash
13. Stock Investment:     Hold $X total stock value -> cash + 1 crash immunity token
14. Morale Standard:      All staff above 50 morale 12h -> cash + 3d morale decay paused
15. Premium Branch:       X branches on Premium path -> cash + all Premium +10% 48h
16. Renovation Round:     Renovate X branches -> cash + 2 free renovations
17. Takeover Success:     Complete 1 hostile takeover -> large cash + brand+10
18. Continent Coverage:   Branches on 3 continents -> very large cash + "Global Mogul" badge
19. Luxury Sector:        X Luxury or Resort slot branches -> cash + Luxury +15% 7d
20. Daily Engagement:     Log in 5 consecutive days -> cash + brand+5
21. Crisis Survival:      Survive X crises without brand dropping below 40 -> cash + crisis damage -15% 7d
22. Investor Confidence:  Complete 10 contracts this season -> permanent +5% contract rewards this season
23. Regional VP Milestone:Promote X to L4 -> cash + promotion costs -20% 30d
24. Seasonal Branch:      X branches on Seasonal before next event -> cash + next event starts 2h early
25. Corporation Milestone:(Corp Mode) Corp net worth $X -> both members cash + exclusive Corp Badge
```

---

# SECTION 14: SEASONAL & PRESTIGE SYSTEM

## Season Duration
```lua
-- Server-wide timer in DataStore "MogulInc_Season_v1"
-- All players share the same season end time
local SEASON_DURATION_DAYS = 30  -- 30 real-world days
```

## IPO System
```
Requirement: Cumulative revenue this season >= $500,000,000
Voluntary: Player fires RequestIPO RemoteEvent (not forced at season end)
Animation: Full-screen Breaking News style overlay
Resets: cash($250K), branches, staff, executives, research, brand(50), upgrades
Preserved: company name/logo/colors, legacyMultiplier, ipoCount, badges, gamepasses, Corp membership
```

## Legacy Multiplier
```lua
-- Applied in IncomeService.Recalculate() as first multiplier
-- profile.season.legacyMultiplier starts at 1.0
-- Each IPO: += 0.10 (or += 0.15 with CFO T3 hired at IPO time)
-- Examples: 0 IPOs=1.0x | 1=1.1x | 5=1.5x | 10=2.0x | 20=3.0x
```

## Season Pass Reward Track (20 tiers)
```
XP Sources: Contract+10 | Board decision+5 | Revenue milestone+50 | Crisis survived+8 | Event active+15 | Daily login+3

TIER | XP  | REWARD
  1  |  25 | Exclusive branch name prefix "[Season N]"
  2  |  60 | PR Campaign cost -10% this season
  3  | 100 | +1 board decision/day for 7 days
  4  | 150 | Exclusive logo frame
  5  | 200 | Free branch renovation (1 use)
  6  | 275 | +5% all income for 48 hours
  7  | 350 | Exclusive branch skin (UIColorTheme for your branches)
  8  | 450 | Crisis response window +2 minutes (rest of season)
  9  | 550 | Free Regional VP promotion (1 use)
 10  | 700 | Exclusive company dossier background
 11  | 850 | +10 brand score immediate
 12  |1000 | 1 free country unlock (any Tier 2 or 3)
 13  |1200 | Staff morale decay paused 72 hours
 14  |1400 | 1 R&D project completed instantly
 15  |1600 | Exclusive "Season [N] Champion" badge
 16  |1900 | Income +15% for 7 days
 17  |2200 | Free hostile takeover (covers cash cost, 1 use)
 18  |2600 | Exclusive animated logo (UIGradient TweenService shimmer animation)
 19  |3000 | Legacy multiplier bonus: +0.02x extra this IPO
 20  |4000 | Exclusive "Season MVP" dossier title + golden leaderboard name

Season End Rewards:
  Rank 1: "Global Mogul" badge + 1000 XP next season + exclusive animated frame
  Rank 2: "Empire Builder" badge + 500 XP | Rank 3: "Tycoon" badge + 250 XP
  Ranks 4-10: "Top 10" seasonal badge | IPO Club: "IPO Nx" badge per IPO count
```

---
ier background
  11  |  850   | +10 brand score immediate
  12  | 1000   | 1 free country unlock (any Tier 2 or 3 country)
  13  | 1200   | Staff morale decay paused for 72 hours
  14  | 1400   | 1 R&D project completed instantly
  15  | 1600   | Exclusive "Season [N] Champion" badge on dossier
  16  | 1900   | Income +15% for 7 days
  17  | 2200   | Free hostile takeover (covers cash cost, 1 use)
  18  | 2600   | Exclusive animated logo (season-unique UIGradient animation style)
  19  | 3000   | Legacy multiplier bonus: +0.02× extra this IPO
  20  | 4000   | Exclusive "Season MVP" dossier title + golden leaderboard name
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

```lua
-- CorpService manages corps via a separate DataStore
-- DataStore name: "MogulInc_Corps_v1"
-- Race condition protection: use UpdateAsync with a 1-second session lock flag

local CorpSchema = {
    id        = "",         -- GUID
    name      = "",         -- text-filtered
    members   = {},         -- array of {userId, role} — max 2 members
    economy   = {cash = 0, totalRevenue = 0},
    branches  = {},
    staff     = {},
    executives = {},
    createdAt = 0,
}
```

```
CREATE CORP:
  Player A fires RequestCreateCorp { name }
  Name passes TextService:FilterStringAsync — reject if failed
  CorpID = HttpService:GenerateGUID(false)
  Stored in DataStore "MogulInc_Corps_v1" with key = CorpID
  A gets role: "founder"

JOIN CORP:
  Player B fires RequestJoinCorp { corpId }
  Server validates: corp exists, corp.members count < 2, B has no existing corp
  B gets role: "partner"

CORP ACTIONS:
  Both players can: open branches, hire staff, make board decisions, buy stock
  Race condition: UpdateAsync with pcall retry on DataStore lock
  Last-write-wins for simultaneous edits (acceptable for non-critical data)

LEAVING CORP:
  Either player can leave — contributed assets stay with corp
  Remaining member becomes sole operator
  24-hour cooldown before recruiting a new partner

CORP LEADERBOARD:
  Ranked by combined net worth: Member A netWorth + Member B netWorth + Corp assets
  Separate "Corp" sub-tab in Leaderboard screen
  Resets each season
```

## Company Dossier

```
Visible to:  Any player who clicks another on the leaderboard
Data source: RemoteFunction GetDossier { userId } → dossierData

Contains:
  - Company name + logo (ImageLabel) + brand colors
  - Industry name + industry icon
  - Founded date (season number + os.date string)
  - Current brand score (progress bar)
  - All-time total revenue (across all seasons)
  - IPO count + legacy multiplier
  - All badges (ImageLabel grid, permanent collection)
  - Recent 5 events (last 5 news ticker entries)
  - Current net worth
  - Corp membership (if in one)
  - Current season rank

VIP Dossier gamepass additions:
  - UIGradient-animated logo (shimmer effect via TweenService on UIGradient Offset)
  - Gold UIStroke animated border frame (Color3 tweens between gold variants)
  - "VIP" gold TextLabel badge on dossier header
  - Extended badge display (all-time history)
```

## Player Business Marketplace

```lua
-- Marketplace stored in DataStore "MogulInc_Market_v1"
-- Listings expire after 72 hours (checked on listing retrieval and login)

local ListingSchema = {
    id         = "",           -- GUID
    sellerId   = 0,            -- UserId
    branchData = {},           -- full branch snapshot
    askPrice   = 0,
    listedAt   = 0,            -- os.time()
    expiresAt  = 0,            -- listedAt + (72 * 3600)
}
```

```
Listing:
  Max 3 branches listed per player at once
  Cannot list branches currently in active crisis
  Price range: 50% to 300% of branch market value
  Branch held in Marketplace DataStore during listing (removed from player profile)
  Returns to seller if unsold after 72h

Buying:
  Browse in Branches tab → "Marketplace" sub-tab
  Buy fires RequestBuyBranch { listingId }
  10% marketplace fee deducted from seller's payout
  Cash transfers even if seller is offline
```

## Leaderboard Details

```lua
-- Solo leaderboard via OrderedDataStore
-- Key: userId, Value: math.floor(netWorth)
-- Updated every 300 seconds via a server loop in SeasonService
-- GetSortedAsync(false, 10) gets top 10

-- Corp leaderboard: separate OrderedDataStore
-- Key: corpId, Value: math.floor(combinedNetWorth)
```

```
SOLO LEADERBOARD:
  Ranked by:    Net worth (cash + branch values + stock portfolio)
  Updated:      Every 5 minutes
  Display:      Top 10 real players + NPC rivals to fill gaps (styled with faded rows + "(AI)" tag)
  Your row:     Always visible — pinned at bottom if outside top 10, shows actual rank
  Season:       Resets each season. Archive available for past 3 seasons.

SEASON ARCHIVE:
  "Past Seasons ▾" dropdown in Leaderboard tab
  Shows last 3 seasons — each is a snapshot of top 50 at season end
  Clicking a name opens that player's dossier popup
```

---

# SECTION 16: UNIQUE FEATURES

## Breaking News Moments

```
TRIGGERS:
  $100K, $500K, $1M, $5M, $10M, $50M, $100M, $500M, $1B, $5B, $10B, $100B, $1T milestones
  First IPO, each subsequent IPO
  First hostile takeover success / defense
  Corp formation
  Rank #1 on leaderboard

VISUAL IMPLEMENTATION:
  -- In OverlayManager LocalScript:
  -- 1. Create a full-screen Frame: Size = UDim2.new(1,0,1,0), BackgroundColor3 = Color3.new(0,0,0)
  --    BackgroundTransparency starts at 1, tweens to 0.15 (dark overlay)
  -- 2. Centered card Frame: Size = UDim2.new(0,380,0,220), AnchorPoint = Vector2.new(0.5,0.5)
  --    Position = UDim2.new(0.5,0,0.5,0), BackgroundColor3 = BACKGROUND_TERTIARY
  --    UICorner CornerRadius = UDim.new(0,12), UIStroke Color = Color3.new(1,1,1)
  -- 3. "BREAKING NEWS" red banner TextLabel at top of card
  --    BackgroundColor3 = RED_DEFAULT, TextColor3 = Color3.new(1,1,1)
  --    TextSize = 11, Font = GothamBold, Text = "BREAKING NEWS"
  -- 4. Company logo ImageLabel (player's custom logo asset)
  -- 5. Headline TextLabel: TextSize = 22, Font = GothamBold
  -- 6. Animated sweep line at bottom: Frame tweened in Size from UDim2.new(0,0,0,2)
  --    to UDim2.new(1,0,0,2) using TweenService
  -- 7. Countdown bar: Frame child of card, width tweens from full to 0 over 5 seconds
  -- 8. UserInputService.InputBegan → dismiss on any click/tap

  Auto-dismisses after 5 seconds
  Can be dismissed by any tap/click (UserInputService.InputBegan)
  No sound (Roblox audio restrictions for UI games — rely on visual impact)
```

## Login Summary Screen

```
TRIGGERS: Shown if (os.time() - profile.meta.lastSeen) >= 300 seconds (5 minutes offline)
SKIPPED:  First-ever login (tutorial replaces it)

IMPLEMENTATION:
  -- OverlayManager builds a ScreenGui with a centered panel
  -- Frame: Size = UDim2.new(0,360,0,0) with AutomaticSize = Enum.AutomaticSize.Y
  --        AnchorPoint = Vector2.new(0.5,0.5), Position = UDim2.new(0.5,0,0.5,0)
  --        BackgroundColor3 = BACKGROUND_SECONDARY, UICorner = UDim.new(0,12)
  -- Lines appear sequentially: each TextLabel tweens Position from
  --   UDim2.new(0,-20,0,yPos) to UDim2.new(0,0,0,yPos) AND BackgroundTransparency 1→0
  --   with 0.3s delay between each line using task.delay()

CONTENT (lines appear one by one, 0.3s apart):
  "You were away for [Xh Ym]"
  "$X earned while you slept"          (if > $0)
  "X contracts completed"              (if any)
  "X research projects finished"       (if any)
  "X crises weathered (auto-responded)" (if any)
  "Staff morale dropped — check team"  (if any staff below 40)
  "Branch quality decaying — renovate soon" (if avg quality < 60)
  "Brand score changed: [±N]"          (if changed > 5 points)
  "Your rank: #X this season"          (always shown)

  After all lines: "Let's Go →" TextButton pulses with UIScale tween
```

## Hostile Takeover System

```lua
-- TakeoverService on server handles all takeover logic
-- Costs 15% of attacker's current net worth (cash deducted immediately)

local function getSuccessChance(attacker, defender)
    local chance = 0.40  -- base 40%
    -- defender vulnerability (by brand score)
    if defender.brand.score <= 20 then chance += 0.25
    elseif defender.brand.score <= 40 then chance += 0.15
    elseif defender.brand.score <= 60 then chance += 0.05
    elseif defender.brand.score <= 80 then chance -= 0.05
    else chance -= 0.15 end
    -- attacker bonuses
    if attacker.brand.score > 80 then chance += 0.05 end
    if attacker.research.completed["takeover_prep"] then chance += 0.15 end
    -- defender chose "legal defense" board decision
    if defender.board.activeEffects["legal_defense"] then chance -= 0.30 end
    return math.clamp(chance, 0.05, 0.90)
end
```

```
VS AI RIVALS:
  Success chance:  60% fixed
  Success outcome: AI revenue -20%, attacker gains cash bonus (10% of AI revenue)
  No branch transfer for AI (AI doesn't have real branch objects)

COOLDOWN:
  24-hour cooldown between attempts (per attacker) stored in profile
  Defender can see they were attacked in dossier for 24h
```

---

# SECTION 17: UI SCREEN LAYOUTS

All UI is Roblox GuiObjects parented to ScreenGui instances in PlayerGui.
StarterGui contains template ScreenGuis. UIController LocalScript manages visibility.

## TOP BAR (52px fixed height, always visible ScreenGui)

```lua
-- TopBarGui: ScreenGui, ResetOnSpawn = false, DisplayOrder = 10
-- Main Frame: Size = UDim2.new(1,0,0,52), BackgroundColor3 = BACKGROUND_SECONDARY
-- UIStroke on bottom edge: requires a child Frame as border line

Layout (left to right inside top bar Frame, using UIListLayout FillDirection.Horizontal):

LEFT SIDE (company identity):
  [Logo: ImageLabel 32×32 offset] [Company Name: TextLabel 15px GothamBold] [Industry Icon: ImageLabel 16×16]

CENTER-LEFT (financial):
  [Cash: TextLabel, GREEN_DEFAULT, TextSize=20, Font=RobotoMono (MONO font for numbers)]
  [Revenue/hr: TextLabel below cash, TEXT_SECONDARY, TextSize=11]
  Updates every 5 seconds via SyncEconomy RemoteEvent → NumberFormatter module

CENTER (brand score):
  [Brand Score progress bar: Frame 120×6 offset — track + fill child pattern]
  [Score TextLabel above bar, TextSize=11]
  Bar fill color: GREEN_DEFAULT if >70, AMBER_DEFAULT if 40-70, RED_DEFAULT if <40

CENTER-RIGHT (news ticker):
  [ScrollingFrame: Size=UDim2.new(0,220,1,0), ScrollingDirection=X, ScrollBarThickness=0]
  [Inner TextLabel with all news items concatenated — TweenService tweens CanvasPosition.X]

RIGHT (utilities):
  [Save status: ImageLabel icon + TextLabel TextSize=11]
  [Notification bell: ImageButton 32×32, with pill badge (Frame child) showing count]
  [Shop button: ImageButton 32×32]
  [Settings button: ImageButton 32×32]
```

## BOTTOM NAVIGATION (60px fixed height)

```lua
-- BottomNavGui: ScreenGui, DisplayOrder = 10
-- Main Frame: Size = UDim2.new(1,0,0,60), Position = UDim2.new(0,0,1,-60)
-- BackgroundColor3 = BACKGROUND_SECONDARY
-- UIListLayout FillDirection.Horizontal, HorizontalAlignment.Center

8 tab buttons, equal width (each ~12.5% of screen width):
  Icon ImageLabel (24×24) + TextLabel below (TextSize=10, Font=GothamMedium)

  Dashboard | Branches | Staff | Execs | Research | Market | Board | Rankings

Active tab: BackgroundColor3 set to industry THEME_COLOR at BackgroundTransparency = 0.85
            Icon ImageColor3 = industry THEME_COLOR
            TextColor3 = TEXT_PRIMARY

Notification badges (red pill Frame with count TextLabel):
  Board:    count of unresolved decisions today
  Staff:    count of staff below morale 20 or in quit grace period
  Research: count of completed research not yet viewed
  Market:   amber dot only if crash imminent (no number)
```

## DASHBOARD TAB

```
Layout (UIListLayout FillDirection.Vertical inside a ScrollingFrame):

[Section: Overview — UIGridLayout 2 columns, CellSize UDim2.new(0.5,-5,0,90)]
  Card 1: Net Worth — large number (NumberFormatter), trend arrow vs last hour
  Card 2: Revenue per Hour — with tall bar showing % of estimated maximum
  Card 3: Brand Score — progress bar + tiny sparkline (5 Frame bars of varying heights)
  Card 4: Season Rank — rank number + "#1" style badge + days remaining TextLabel

[Section: Top Branches — header TextLabel + UIListLayout of 3 mini cards]
  Each mini card: branch name, flag ImageLabel, city type badge tag, income/hr, quality bar
  "View all →" TextButton navigates to Branches tab

[Section: Active Buffs — horizontal ScrollingFrame]
  Each buff chip: Frame with UIListLayout, effect name + magnitude + countdown TextLabel
  Countdown updates every 1 second via RunService.Heartbeat
  Empty state: muted TextLabel "No active boosts"

[Section: Recent Activity — UIListLayout of 5 activity rows]
  Each row: icon ImageLabel + description TextLabel + "Xm ago" TextLabel
  Tap row: expands inline or opens a modal with full history
```

## BRANCHES TAB

```lua
-- BranchesClient LocalScript manages this tab
-- Sub-tabs: TextButton array, active tab shows content Frame

Sub-tabs:
  [World Map View] [List View] [Marketplace]

WORLD MAP VIEW:
  ImageLabel background: 2D illustrated world map asset (uploaded to Roblox as a Decal)
  Size = UDim2.new(1,0,1,0), ScaleType = Enum.ScaleType.Fit
  Country nodes = small circular Frames positioned absolutely using Position UDim2

  Node states (set via Lua, not CSS):
    Unlocked + branches:  BackgroundColor3 = THEME_COLOR, TextLabel shows branch count
    Unlocked + no branch: BackgroundTransparency = 0.5, outlined via UIStroke
    Locked:               BackgroundColor3 = TEXT_MUTED, lock icon ImageLabel child
    Active crisis:        UIStroke Color = AMBER_DEFAULT + pulse UIScale tween

  Clicking a country node (ImageButton.Activated event):
    → Opens City Slots panel (Frame slides up from bottom via TweenService Position)
    → City Slots panel Position tweens from UDim2.new(0,0,1,0) to UDim2.new(0,0,0.35,0)

CITY SLOTS PANEL (slide-up Frame, not a new ScreenGui):
  Country name TextLabel + flag ImageLabel + wealth multiplier badge
  UIGridLayout of city slot cards (CellSize responsive to count)
  Each slot card:
    [Slot icon ImageLabel] [City name TextLabel] [City type badge tag]
    If empty:    "Open Branch" TextButton with cost TextLabel
    If occupied: branch name, Level badge, income/hr, "Manage →" TextButton

LIST VIEW:
  ScrollingFrame with UIListLayout
  Sort buttons (TextButtons above list): Income | Country | Level | Quality
  Each branch row: quick-tap shows Branch Detail Modal

BRANCH DETAIL MODAL:
  Elevated Card Frame (modal style) overlaid on top with dark background overlay
  BackgroundColor3 = Color3.new(0,0,0), BackgroundTransparency = 0.5 on overlay Frame
  Branch card:
    Editable branch name (TextBox, text-filtered on submit)
    Country + city + type TextLabels
    Level badge + "Upgrade $X" TextButton
    Path display: if nil → "Choose Path" TextButton
                  if set → path name tag + sub-upgrade tier + "Next Upgrade" TextButton
    Quality bar (color-coded fill) + "Renovate $X" TextButton
    Staff list: UIListLayout of assigned staff rows (name, specialty icon, level badge, morale bar)
    Income TextLabel: "$X / hr from this branch"
    Action buttons row: [Upgrade] [Renovate] [Relocate] [Close Branch]
  Dismiss: clicking overlay Frame or X button → reverse slide tween
```

## STAFF TAB

```
Layout (ScrollingFrame, UIListLayout Vertical):

[Hire Summary bar — top]:
  TextLabels showing: total staff, total slots used, % filled
  BackgroundColor3 = BACKGROUND_SECONDARY, full width

[Group by branch / by country toggle]:
  Two TextButtons acting as a toggle — active one has THEME_COLOR background

[Sort buttons]: by Morale (default) | Level | Specialty

STAFF LIST (grouped by branch):
  Branch header row:
    Branch name TextLabel | Country flag ImageLabel | path icon ImageLabel
    "Hire" TextButton (only visible if branch has open slots)

  Staff row (per staff member):
    [Name TextLabel] [Specialty icon ImageLabel] [Level badge: "L1"/"L2"/"L3"/"L4"]
    [Morale bar: Frame 60px wide, fill color changes by value]
    [Promote TextButton] [Transfer TextButton] [Fire TextButton]
    Morale bar colors: fill BackgroundColor3:
      GREEN_DEFAULT if morale >= 60, AMBER_DEFAULT if 30-59, RED_DEFAULT if 0-29
    "About to quit" state:
      Row BackgroundColor3 = RED_BG, UIStroke = RED_BORDER (pulsing via UIScale tween)

HIRE POPUP (modal):
  Shows random name TextLabel + rolled specialty + rarity TextLabel
  Specialty probability bars (Frame fill per specialty weight)
  [Reroll Preview] TextButton (free, client-side preview only — real roll on server)
  [Hire for $2,000] TextButton
  Fine print TextLabel: "Actual specialty determined on hire"

PROMOTE POPUP:
  Current level → next level arrow display
  Before/after specialty bonus TextLabels (TextColor3 = GREEN_TEXT for the improvement)
  Cost TextLabel + [Promote] TextButton + [Cancel] TextButton

TRANSFER POPUP:
  TextScrollingList (ScrollingFrame) of available target branches + open slot count
  Cooldown warning TextLabel: "5-minute settling period after transfer"
  [Transfer] TextButton + [Cancel] TextButton
```

## EXECUTIVES TAB

```lua
-- ExecsClient LocalScript
-- 2×2 UIGridLayout of role cards
-- CellSize = UDim2.new(0.5, -5, 0, 180)

Each exec card (Frame with UIListLayout Vertical):
  Role name TextLabel (COO / CMO / CFO / CTO) + "VACANT"/"HIRED" badge tag
  If HIRED: Tier badge tag ("T1"/"T2"/"T3"), hired date TextLabel, active bonuses list
  If VACANT: muted TextLabel "No executive", preview of what hiring unlocks
  [Hire TextButton] or [Replace TextButton]

Note: CTO card shows locked state (lock icon + TextLabel "Unlocks at $5M revenue")
      with a mini progress bar showing progress to $5M until requirement met

HIRE MODAL (Elevated Card Frame overlay):
  Role name header TextLabel
  3 tier option cards side by side (UIListLayout Horizontal):
    Tier label tag + cost TextLabel + full bonus breakdown (UIListLayout of bonus rows)
    [Hire TextButton] per tier
  Replacing note: TextLabel in RED_DEFAULT showing severance cost
  Bonus rows: Icon ImageLabel + description TextLabel + value TextLabel (THEME_COLOR)
  Live impact shown: "COO T2: +18% overhead savings = +$X/hr currently"
  — Calculated from current income and updated each time modal opens
```

## RESEARCH TAB

```lua
-- ResearchClient LocalScript
-- Layout: 3 sections via UIListLayout Vertical in ScrollingFrame

SECTION 1 — ACTIVE RESEARCH:
  Header TextLabel: "Researching (X/Y slots)"
  Per active project — progress card (Standard Card):
    Project name TextLabel + category badge tag
    Progress bar (fill width tweens on render, not continuously)
    Time remaining TextLabel updated every second via RunService.Heartbeat
    [Complete Instantly — R&D Accelerator] TextButton (grayed + tooltip if no accelerator)
    [Cancel Research] TextButton (shows "Refunds 50%" note)

SECTION 2 — AVAILABLE PROJECTS:
  Filter TextButtons row: All | Income | Staff | Brand | Defense | Industry
  UIGridLayout 2-column, CellSize = UDim2.new(0.5,-5, 0,140)
  Per project card:
    Project name TextLabel + duration TextLabel + cost TextLabel
    Short effect description TextLabel (TEXT_SECONDARY)
    Industry-exclusive badge tag (if applicable, GOLD color)
    [Start Research] TextButton — grayed out with "No slots available" if at cap
    ✓ checkmark badge + "Completed" if already done this season

SECTION 3 — COMPLETED (collapsible):
  Collapsed by default — TextButton header "Completed This Season (X)"
  On expand: UIListLayout of completed project name rows
             Each shows project name + green ✓ icon + effect summary
```

## STOCK MARKET TAB

```
Sub-tabs: [Indexes] [Portfolio] [Companies]

INDEXES SUB-TAB:
  UIGridLayout 2-column (1 card full-width at bottom for last index)
  Per index card:
    Industry name + icon ImageLabel
    Current price: TextLabel, TextSize=20, Font=RobotoMono, color changes vs previous tick
    24h change %: TextLabel with ▲▼ arrow prefix, GREEN/RED_DEFAULT
    Mini sparkline: UIListLayout Horizontal of 24 small Frames, heights proportional to price
    [Buy] TextButton — opens quantity TextBox inline
    Holdings TextLabel: "You own: X units" (muted if 0)

PORTFOLIO SUB-TAB:
  Summary row: total portfolio value + total P&L (GREEN/RED_DEFAULT)
  UIListLayout of holdings rows:
    Ticker TextLabel | Quantity | Avg buy price | Current value | P&L TextLabel
    [Sell] TextButton per row → opens quantity input popup
  Listed company section (if holding other players' shares):
    Similar row format + "Dividend: +$X/hr" green TextLabel

COMPANIES SUB-TAB:
  Listed player companies (ScrollingFrame):
    Company logo ImageLabel + name TextLabel | Industry tag | Share price | Holdings
    [Buy] TextButton
  NPC rivals section below with same format
  Note TextLabel at top: "Shares in other players pay 2% of their income as dividends"
```

## BOARD TAB

```
Layout (UIListLayout Vertical in ScrollingFrame):

TODAY'S DECISIONS:
  Header TextLabel: "X decisions • Refreshes in Xh Ym" (countdown updated every 60s)
  Per decision (Standard Card or Resolved Card):
    Unresolved: Decision title TextLabel + category badge + description TextLabel (2-3 lines)
    3 option TextButtons in UIListLayout Horizontal
    Each button: SHORT option label (1-3 words) + longer description in smaller TextLabel below
    Long-press / hover (mobile: 0.5s hold) → shows full consequence preview in a tooltip Frame

    Resolved (grayed card): BackgroundTransparency = 0.5, chosen option highlighted
    Result TextLabel in GREEN/RED_DEFAULT showing outcome

ACTIVE CONTRACTS:
  Header TextLabel: "Active Contracts (X/Y slots)"
  Per contract (Standard Card):
    Contract title + progress bar (fill = current/requirement)
    Deadline countdown TextLabel: "Expires in Xh Ym"
    Current vs requirement TextLabel: "$2.1M / $3.0M"
    Reward TextLabel: "Reward: $900K + brand +5"
    [Complete] TextButton — only active/green when requirement met

BOARD HISTORY (collapsible):
  Header TextButton "Past Decisions ▾"
  On expand: UIListLayout of last 20 decisions (compact rows)
  Each row: date string + decision title + chosen option + outcome icon (✓/✗)
```

## LEADERBOARD TAB

```lua
-- LeaderboardClient LocalScript
-- GetDossier RemoteFunction returns dossierData when clicking a player row

Sub-tab bar: [Solo] [Corp]
Season timer TextLabel: "Season ends in Xd Xh" (updated every 60s via server sync)
Past Seasons dropdown: TextButton "Past Seasons ▾" → shows 3 past season options

SOLO VIEW (UIListLayout Vertical):
  Top 10 player rows (each is a TextButton for dossier popup):
    Rank #: TextLabel (GOLD_DEFAULT for #1, silver-ish for #2, bronze-ish for #3)
    Logo ImageLabel (32×32) + Company Name TextLabel + Industry icon (16×16)
    Net Worth TextLabel (right-aligned, RobotoMono)
    Badges: up to 3 ImageLabel icons
    NPC rivals: BackgroundTransparency = 0.6, "(AI)" muted TextLabel
    Your row: BackgroundColor3 = THEME_COLOR at BackgroundTransparency = 0.88

CORP VIEW: Same layout for top 10 corps
  Corp name + both member names TextLabel + combined net worth

DOSSIER POPUP (Frame overlay, Elevated Card style):
  Company logo ImageLabel (full size, 64×64)
  Company name TextLabel (large) + industry TextLabel
  Founded TextLabel
  Brand score progress bar
  IPO count + legacy multiplier TextLabels
  Badge grid: UIGridLayout of ImageLabel badge icons (3 per row)
  Recent 5 events: UIListLayout of short TextLabel activity rows
  Net worth TextLabel
  [Close] TextButton
```

---

# SECTION 18: MONETIZATION

## Developer Products (Repeatable Purchases via MarketplaceService)

```lua
-- MarketplaceHandler Script in ServerScriptService
-- All product IDs stored in GameConfig ModuleScript
-- MarketplaceService.ProcessReceipt callback handles all purchases
-- IMPORTANT: ProcessReceipt must return Enum.ProductPurchaseDecision.PurchaseGranted
--            only AFTER the effect is applied AND profile is saved

local DevProducts = {
    REVENUE_BOOST   = 123456001,  -- 49 Robux
    MORALE_PACKAGE  = 123456002,  -- 39 Robux
    RD_ACCELERATOR  = 123456003,  -- 59 Robux
    TAKEOVER_TOKEN  = 123456004,  -- 99 Robux
    QUICK_RENO      = 123456005,  -- 19 Robux
    BRANCH_SLOT     = 123456006,  -- 79 Robux
}
```

### Revenue Boost — 49 Robux
```
Effect:      2× income multiplier for 2 hours
Stacking:    Multiple purchases add time (not extra multiplier), max 24h stack
Display:     Top bar shows "2× BOOST — Xh Xm" TextLabel while active
Best used:   Before a seasonal event or after opening many new branches
```

### Morale Package — 39 Robux
```
Effect:      All staff globally → 100 morale, cancels all pending quit timers
Warning:     If all staff above 80, show prompt: "Your staff look fine — still buy?"
Best used:   When many staff low morale or multiple staff about to quit
```

### R&D Accelerator — 59 Robux
```
Effect:      All active research projects complete instantly, slots free immediately
Warning:     If no active research, show: "Nothing to accelerate"
Best used:   When 2-3 projects near completion and you want bonuses now
```

### Takeover Token — 99 Robux
```
Effect:      Halves cash cost of next hostile takeover attempt (consumed even if failed)
Limit:       Max 1 token held at once
Display:     "1 Token Active" indicator in Leaderboard tab (gold badge)
```

### Quick Renovation — 19 Robux
```
Effect:      Instantly renovates selected branch (quality → 100), no cash cost
When shown:  Only visible in Branch Detail popup, not in shop
Best used:   When cash is tight but branch quality severely hurting income
```

### Branch Slot Unlock — 79 Robux
```
Effect:      +1 permanent staff slot to currently selected branch
Limit:       Max 3 extra slots per branch (total max 9 slots per branch)
When shown:  Only visible in Branch Detail popup when at current slot cap
```

---

## Game Passes (Permanent via MarketplaceService:UserOwnsGamePassAsync)

```lua
-- Check on PlayerAdded:
local GamePasses = {
    CEO_PASS          = 234567001,  -- 349 Robux
    EXPANSION_LICENSE = 234567002,  -- 199 Robux
    EXTRA_RD_SLOT     = 234567003,  -- 249 Robux
    VIP_DOSSIER       = 234567004,  -- 149 Robux
    STARTER_BUNDLE    = 234567005,  -- 129 Robux
    SEASON_PASS       = 234567006,  -- 199 Robux (new ID each season)
}

-- In PlayerService on join:
for passName, passId in pairs(GamePasses) do
    local owned = MarketplaceService:UserOwnsGamePassAsync(player.UserId, passId)
    profile.gamepasses[string.lower(passName)] = owned
end
```

### CEO Pass — 349 Robux
```
Offline earnings cap:  24 hours (stacks with CFO — takes whichever is higher)
Leaderboard display:   "CEO" TextLabel prefix before company name
Dossier:               CEO banner Frame with unique styling
```

### Expansion License — 199 Robux
```
Effect:    Choose any 3 countries to unlock at 50% cost
Usage:     "Use License" TextButton on locked country nodes in World Map view
Choices:   Permanent (stored in profile.gamepasses.licensedCountries array)
Resets:    Does NOT reset on IPO
```

### Extra R&D Slot — 249 Robux
```
Effect:    +1 concurrent research slot (3 total; 4 with CTO T3 simultaneously)
Display:   Extra progress bar slot visible in Research tab
Resets:    Does NOT reset on IPO
```

### VIP Dossier — 149 Robux
```
Effects:
  4 extra animated logo options (UIGradient TweenService shimmer)
  Full Color3 color picker (any Color3 value vs 16 presets)
  Animated gold UIStroke frame on dossier
  "[VIP]" gold TextLabel badge on leaderboard row
  Golden TextColor3 for your company's news ticker entries
  Other players see all VIP cosmetics when viewing your dossier
```

### Starter Bundle — 129 Robux (first game only)
```
Effects applied on first game start ONLY (profile.meta.isNewPlayer must be true):
  Starting cash: $750,000 instead of $250,000
  1 instant R&D completion token (use any time in first season)
  Exclusive "Founder's Edition" branch skin for first 30 minutes of branches opened
  Permanent "Founder" badge on dossier (all seasons)
Note:
  Can be purchased any time, but cash bonus only applies if isNewPlayer == true
  "Founder" badge always awarded regardless of timing
```

### Season Pass — 199 Robux per season
```
Season-specific (new GamePass ID each season, must repurchase):
  +1 daily board decision (4 per day instead of 3)
  1 free board decision refresh per day
  Exclusive season branch skin
  +10% season XP gain (reward track levels faster)
  "Season [N] Pass" badge on dossier
  Access to Season Pass 20-tier reward track (Section 14)
```

---

# SECTION 19: TECHNICAL ARCHITECTURE

## Data Persistence: ProfileStore

```lua
-- ProfileStore by Madwork — install via Roblox model package
-- ServerScriptService/ProfileStore (ModuleScript)
-- DO NOT use raw DataStoreService. ProfileStore handles session locking.

-- In PlayerService Script:
local ProfileStore = require(ServerScriptService.ProfileStore)
local GameProfiles = ProfileStore.GetProfileStore("MogulInc_v1", DefaultProfile)

local function onPlayerAdded(player)
    local profile = GameProfiles:LoadProfileAsync("Player_" .. player.UserId)
    if profile == nil then
        -- LoadProfileAsync returns nil if session lock can't be acquired
        player:Kick("Failed to load profile. Please rejoin.")
        return
    end
    profile:AddUserId(player.UserId)  -- GDPR compliance
    profile:Reconcile()               -- fill in any missing keys from DefaultProfile
    PlayerService.ActiveProfiles[player.UserId] = profile
    -- run offline calculation block (Section 19 Offline Calc Order) BEFORE any sync
    PlayerService.RunOfflineCalculation(player, profile)
    -- then fire all initial sync RemoteEvents to client
    PlayerService.SyncAll(player, profile)
end

local function onPlayerRemoving(player)
    local profile = PlayerService.ActiveProfiles[player.UserId]
    if profile then
        profile:Release()
        PlayerService.ActiveProfiles[player.UserId] = nil
    end
end

game:BindToClose(function()
    for _, profile in pairs(PlayerService.ActiveProfiles) do
        profile:Release()
    end
end)
```

## Data Schema (DefaultProfile ModuleScript)

```lua
-- ReplicatedStorage/DefaultProfile (ModuleScript)
-- This is the canonical schema — ProfileStore.Reconcile() fills missing keys on load

local DefaultProfile = {
    company = {
        name         = "",
        industry     = nil,              -- string id like "fast_food" | "cafe" etc.
        logoId       = 1,
        colorPrimary = "#22C55E",        -- stored as hex string
        colorAccent  = "#3B82F6",
    },
    economy = {
        cash            = 250000,
        totalRevenue    = 0,
        incomePerHour   = 0,
        boostActive     = nil,           -- { multiplier=2, expiresAt=os.time()+7200 }
        takeoverToken   = false,
        rdAcceleratorToken = false,
    },
    branches  = {},                      -- array of branch tables (Section 5)
    staff     = {},                      -- array of staff tables (Section 6)
    executives = {coo=nil, cmo=nil, cfo=nil, cto=nil},
    research = {
        active    = {},                  -- { projectId, startedAt, duration }
        completed = {},                  -- array of completed projectIds this season
        bonuses   = {},                  -- { ["signature_product"] = true, ... }
    },
    brand = {
        score       = 50,
        history     = {},                -- last 24h hourly snapshots
        lastCampaignAt = 0,
    },
    stock = {
        holdings = {},                   -- { ["FFIDX"] = {quantity=0, avgBuyPrice=0} }
        listed   = false,
        sharePrice = 0,
    },
    contracts = {
        active    = {},
        completed = {},
        expired   = {},
    },
    board = {
        decisions      = {},
        lastRefreshDate = "",            -- os.date("%Y-%m-%d")
        history        = {},
        activeEffects  = {},             -- temporary bonuses from board decisions
    },
    events = {
        activeConsequences = {},
        history            = {},
    },
    season = {
        legacyMultiplier  = 1.0,
        ipoCount          = 0,
        badges            = {},
        milestoneRewards  = {},          -- which Breaking News milestones triggered
        passXP            = 0,
        passRewardsClaimed = {},
    },
    corp = {
        id   = nil,
        role = nil,
    },
    meta = {
        lastSeen              = 0,       -- os.time() on each session end
        hasCompletedTutorial  = false,
        isNewPlayer           = true,
        totalPlaytime         = 0,
        createdAt             = 0,
    },
    gamepasses = {
        ceo              = false,
        expansionLicense = false,
        extraRdSlot      = false,
        vipDossier       = false,
        starterBundle    = false,
        seasonPass       = false,
        licensedCountries = {},          -- array of countryIds unlocked with license
    },
    unlockedCountries = {"usa"},
    branchSlots       = {},              -- { [branchId] = extraSlotsCount }
}

return DefaultProfile
```

## Server Architecture

```
ServerScriptService/
  GameServer (Script — server root, requires all services on startup)
  Services/
    PlayerService     (Script — profile load/unload, offline calc, sync dispatch)
    IncomeService     (Script — recalculate income, 1s tick loop)
    BranchService     (Script — open, upgrade, path, renovate, relocate, close)
    StaffService      (Script — hire, fire, promote, transfer, morale tick)
    ExecService       (Script — hire, replace, bonus application)
    ResearchService   (Script — start, complete, offline completion check)
    BrandService      (Script — score add/subtract, PR campaign, decay)
    StockService      (Script — 60s tick, crash events, buy/sell, dividends)
    BoardService      (Script — generate daily decisions, handle choices, history)
    EventService      (Script — crisis spawn, opportunity, seasonal, news ticker)
    ContractService   (Script — generate, check completion, expiry, reward)
    SeasonService     (Script — season timer, IPO handling, badge awards)
    TakeoverService   (Script — initiate, resolve, defend, cooldown)
    CorpService       (Script — create, join, leave, sync corp DataStore)
    MarketplaceHandler(Script — MarketplaceService.ProcessReceipt, gamepass checks)
    MilestoneTracker  (Script — Breaking News triggers, milestone history)
    RateLimiter       (ModuleScript — per-player per-action rate limiting)
  Config/
    GameConfig        (ModuleScript — product IDs, pass IDs, server constants, tunable values)
    BoardConfig       (ModuleScript — server-only, full 65 decision pool)
    EventConfig       (ModuleScript — server-only, crisis + opportunity definitions)
    ContractConfig    (ModuleScript — server-only, 25 contract type definitions)

ReplicatedStorage/
  Remotes/
    Events/           (all RemoteEvent instances)
    Functions/        (all RemoteFunction instances)
  Config/
    IndustryConfig    (ModuleScript — 15 industry definitions, shared with client)
    CountryConfig     (ModuleScript — 55 country definitions, shared with client)
    BranchConfig      (ModuleScript — upgrade costs, path definitions)
    StaffConfig       (ModuleScript — specialty definitions, promotion costs)
    ExecConfig        (ModuleScript — 4 executive role definitions)
    ResearchConfig    (ModuleScript — 25 R&D project definitions)
    IconConfig        (ModuleScript — all icon asset IDs keyed by name)
  DefaultProfile      (ModuleScript — schema reference, used by ProfileStore)

StarterPlayerScripts/
  UIController        (LocalScript — tab switching, overlay manager, animations)
  DashboardClient     (LocalScript)
  BranchesClient      (LocalScript)
  StaffClient         (LocalScript)
  ExecsClient         (LocalScript)
  ResearchClient      (LocalScript)
  MarketClient        (LocalScript)
  BoardClient         (LocalScript)
  LeaderboardClient   (LocalScript)
  ShopClient          (LocalScript)
  OverlayManager      (LocalScript — Breaking News, Login Summary, Crisis Alert, Toasts)
  NumberFormatter     (ModuleScript — formats numbers: $1,234,567 → "$1.2M")
  
NOTE: All files in StarterPlayerScripts that process game logic are LocalScripts.
      All files in ServerScriptService are Scripts (server-side only).
      ModuleScripts are required by their parent Scripts/LocalScripts as needed.
```

## RemoteEvent / RemoteFunction Reference

```lua
-- All Remotes parented to ReplicatedStorage/Remotes/Events/ and /Functions/
-- Accessed via: ReplicatedStorage.Remotes.Events.SyncEconomy etc.

-- SERVER → CLIENT (RemoteEvent:FireClient)
SyncEconomy       -- { cash, incomePerHour, netWorth, boostActive }
SyncBranches      -- { branches[] }
SyncStaff         -- { staff[] }
SyncResearch      -- { active[], completed[], bonuses{} }
SyncBoard         -- { decisions[], activeEffects[] }
SyncContracts     -- { active[] }
SaveStatus        -- { status: "saving" | "saved" | "error" }
PushNewsItem      -- { message: string, priority: "normal"|"warning"|"breaking" }
BreakingNews      -- { headline, companyName, milestone }
ShowLoginSummary  -- { summaryData{} }
CrisisAlert       -- { crisisId, type, severity, description, expiresAt }
ContractCompleted -- { contractId, reward{} }
Toast             -- { message, type: "success"|"error"|"info" }
TakeoverAlert     -- { attackerId, attackerName, success: bool }

-- CLIENT → SERVER (RemoteEvent:FireServer — no return value)
RequestOpenBranch      -- { cityId, countryId }
RequestUpgradeBranch   -- { branchId }
RequestSetPath         -- { branchId, path }
RequestSetPathUpgrade  -- { branchId, tier, optionIndex }
RequestRenovateBranch  -- { branchId }
RequestRelocateBranch  -- { branchId, newCityId, newCountryId }
RequestCloseBranch     -- { branchId }
RequestHireStaff       -- { branchId }
RequestFireStaff       -- { staffId }
RequestPromoteStaff    -- { staffId }
RequestTransferStaff   -- { staffId, targetBranchId }
RequestMoraleBoost     -- { branchId }
RequestHireExec        -- { role, tier }
RequestStartResearch   -- { projectId }
MakeBoardDecision      -- { decisionId, optionIndex }
RespondToCrisis        -- { crisisId, response }
RequestBuyStock        -- { ticker, quantity }
RequestSellStock       -- { ticker, quantity }
RequestListCompany     -- { sharePrice }
RequestDelistCompany   -- {}
RequestTakeover        -- { targetId }
RequestUnlockCountry   -- { countryId }
RequestIPO             -- {}
RequestCreateCorp      -- { name }
RequestJoinCorp        -- { corpId }
RequestLeaveCorp       -- {}
RequestListBranch      -- { branchId, price }
RequestBuyBranch       -- { listingId }
RequestSetCompanyName  -- { name }
RequestSetLogo         -- { logoId }
RequestSetColors       -- { primary, accent }
RequestSetIndustry     -- { industry }

-- CLIENT → SERVER (RemoteFunction:InvokeServer — returns data)
GetDashboardData  -- {} → { overview{}, topBranches[], activeBuffs[], recentActivity[] }
GetStockData      -- {} → { indexes[], portfolio[], companies[] }
GetLeaderboard    -- { type: "solo"|"corp" } → { entries[] }
GetDossier        -- { userId } → { dossierData{} }
GetResearchData   -- {} → { active[], available[], completed[] }
```

## Anti-Exploit Rules

```lua
-- RateLimiter ModuleScript tracks per-player request counts
-- Exceeding limits: kick player + log to output

local RateLimits = {
    action  = { max = 5,  window = 1  },   -- RequestOpenBranch etc.: 5/second
    query   = { max = 10, window = 1  },   -- GetDashboardData etc.: 10/second
    board   = { max = 2,  window = 1  },   -- MakeBoardDecision etc.
    takeover= { max = 1,  window = 30 },   -- RequestTakeover: 1 per 30 seconds
}

-- Every server handler (in every Service) follows this pattern:
local function handleRequest(player, data)
    -- 1. Verify player exists and profile is loaded
    local profile = PlayerService.ActiveProfiles[player.UserId]
    if not profile then return end

    -- 2. Type-check ALL arguments (never trust client data types)
    assert(type(data.branchId) == "string", "Invalid branchId type")

    -- 3. Business logic validation (sufficient cash, entity exists, not at cap, etc.)
    local branch = findBranch(profile, data.branchId)
    assert(branch ~= nil, "Branch not found")
    assert(profile.economy.cash >= upgradeCost, "Insufficient cash")

    -- 4. Apply change AFTER all checks pass
    applyChange(profile, branch)
end

-- NEVER:
--   Read cost/price values from RemoteEvent data (always recalculate server-side)
--   Trust client-provided entity IDs without verifying ownership
--   Apply changes before all validations pass

-- Cash sanity check (runs every 30 seconds in IncomeService):
-- If profile.economy.cash > expectedCash * 1.10 → flag for review (don't kick immediately)
```

## Offline Calculation Order (PlayerService.RunOfflineCalculation)

```lua
local function RunOfflineCalculation(player, profile)
    local now = os.time()
    local offlineSeconds = now - profile.meta.lastSeen
    if offlineSeconds <= 0 then return end

    -- 1. Clamp to offline cap
    local offlineCap = 8 * 3600  -- 8h base
    if profile.gamepasses.ceo then offlineCap = math.max(offlineCap, 24 * 3600) end
    if profile.executives.cfo then
        local cfoCaps = {12 * 3600, 18 * 3600, 24 * 3600}
        offlineCap = math.max(offlineCap, cfoCaps[profile.executives.cfo.tier])
    end
    -- Hotel industry inherent base: 12h
    if profile.company.industry == "hotel" then
        offlineCap = math.max(offlineCap, 12 * 3600)
    end
    local cappedSeconds = math.min(offlineSeconds, offlineCap)

    -- 2. Apply offline income
    local offlineIncome = (cappedSeconds / 3600) * profile.economy.incomePerHour
    profile.economy.cash += offlineIncome
    profile.economy.totalRevenue += offlineIncome

    -- 3. Apply morale decay (per staff member)
    local moraleDecayHours = cappedSeconds / 3600
    for _, staffMember in ipairs(profile.staff) do
        local decay = calculateMoraleDecay(staffMember, profile, moraleDecayHours)
        staffMember.morale = math.max(0, staffMember.morale - decay)
        if staffMember.morale == 0 and staffMember.level < 4 then
            -- auto-quit after grace period (treat as quit during offline)
            removeStaff(profile, staffMember.id)
            profile.brand.score = math.max(0, profile.brand.score - 3)
        end
    end

    -- 4. Apply quality decay (per branch)
    local qualityDecayHours = cappedSeconds / 3600
    for _, branch in ipairs(profile.branches) do
        local decayRate = getQualityDecayRate(branch, profile)
        branch.quality = math.max(0, branch.quality - (decayRate * qualityDecayHours))
    end

    -- 5. Complete finished R&D projects
    for i, activeResearch in ipairs(profile.research.active) do
        if now >= activeResearch.startedAt + activeResearch.duration then
            ResearchService.CompleteProject(profile, activeResearch.projectId)
            table.remove(profile.research.active, i)
        end
    end

    -- 6. Expire board active effects
    for i, effect in ipairs(profile.board.activeEffects) do
        if now >= effect.expiresAt then
            table.remove(profile.board.activeEffects, i)
        end
    end

    -- 7. Complete/expire contracts
    ContractService.CheckAllContracts(profile, now)

    -- 8. Auto-respond to any crises that fired offline (ride_out outcome)
    for _, crisis in ipairs(profile.events.activeConsequences) do
        if now >= crisis.expiresAt then
            EventService.ApplyCrisisOutcome(profile, crisis, "ride_out")
        end
    end

    -- 9. Refresh board decisions if date has changed
    BoardService.CheckRefresh(profile, now)

    -- 10. Recalculate income per hour (after all changes)
    profile.economy.incomePerHour = IncomeService.Recalculate(profile)

    -- 11. Build summary data for Login Summary Screen
    local summaryData = {
        offlineTime    = offlineSeconds,
        earned         = offlineIncome,
        contractsDone  = 0,   -- filled above in ContractService.CheckAllContracts
        researchDone   = 0,   -- filled above
        crisisesWeathered = 0,
        moraleWarning  = false,
        qualityWarning = false,
        brandChange    = 0,
        rank           = SeasonService.GetRank(player.UserId),
    }

    -- 12. Update lastSeen
    profile.meta.lastSeen = now

    -- 13. Fire Login Summary to client (after all sync events)
    -- (Sync events fire in PlayerService.SyncAll AFTER this function returns)
    PlayerService.PendingLoginSummary[player.UserId] = summaryData
end
```

## Key Config Values (all in GameConfig ModuleScript — tunable without code changes)

```lua
local GameConfig = {
    -- Tick rates
    INCOME_TICK_RATE         = 1,       -- seconds between income accumulation
    CLIENT_SYNC_RATE         = 5,       -- seconds between SyncEconomy to client
    AUTO_SAVE_INTERVAL       = 60,      -- ProfileStore saves every 60s automatically

    -- Decay rates
    MORALE_DECAY_INTERVAL    = 600,     -- 10 minutes between morale decay checks
    QUALITY_DECAY_RATE       = 1,       -- quality points lost per real hour (base)
    HOTEL_QUALITY_DECAY_RATE = 2,       -- hotel industry quality decay rate

    -- Offline caps
    OFFLINE_CAP_DEFAULT      = 8 * 3600,   -- 8 hours
    OFFLINE_CAP_CEO          = 24 * 3600,  -- CEO Pass cap
    OFFLINE_CAP_HOTEL_BASE   = 12 * 3600, -- Hotel industry base cap

    -- Stock market
    STOCK_TICK_RATE          = 60,      -- seconds between stock price updates
    CRASH_MIN_INTERVAL       = 1200,    -- 20 minutes minimum between minor crashes
    CRASH_MAX_INTERVAL       = 3000,    -- 50 minutes maximum

    -- Events
    CRISIS_MIN_INTERVAL      = 1800,    -- 30 minutes minimum between crises
    CRISIS_MAX_INTERVAL      = 5400,    -- 90 minutes maximum
    OPPORTUNITY_MIN_INTERVAL = 3600,    -- 60 minutes between opportunity events
    CRISIS_RESPONSE_WINDOW   = 300,     -- 5 minutes to respond to a crisis

    -- Leaderboard
    LEADERBOARD_UPDATE_RATE  = 300,     -- 5 minutes between OrderedDataStore updates

    -- Contracts
    CONTRACT_DURATION        = 72 * 3600,  -- 72 hours per contract

    -- Board decisions
    BOARD_REFRESH_HOUR       = 0,       -- midnight UTC (os.date comparison)

    -- Takeovers
    TAKEOVER_COOLDOWN        = 24 * 3600,  -- 24 hours between attempts

    -- Season
    SEASON_DURATION_DAYS     = 30,
    IPO_REVENUE_THRESHOLD    = 500000000,  -- $500M
    LEGACY_MULTIPLIER_PER_IPO = 0.10,
    LEGACY_MULTIPLIER_CFO_T3  = 0.15,     -- if CFO T3 is hired at IPO time
}
```

---

# SECTION 20: ALL PLAYER CHOICES — MASTER LIST

## A. Industry & Company Setup
```
1.  Choose industry: Fast Food / Tech / Fashion / Healthcare / Entertainment /
    Coffee & Café / Fitness & Wellness / Luxury Hotels / Retail & E-Commerce /
    Sports & Recreation / Automotive / Real Estate / Music & Record Label /
    Social Media & Apps / Space & Aerospace (15 options — locked until 1st IPO)
2.  Name your company (TextBox input, 2-20 chars, text-filtered)
3.  Choose company logo (1-20 standard, 21-24 with VIP Dossier)
4.  Choose primary brand color (16 presets or full Color3 picker with VIP)
5.  Choose accent brand color (same)
6.  Re-pick industry on each IPO (or keep the same)
```

## B. Branch Decisions
```
7.   Choose which country to unlock next
8.   Choose which city slot to open a branch in
9.   Choose branch upgrade path: Volume / Premium / Seasonal
10-12. Choose sub-upgrade per tier (1-5) for each path (2-3 options each)
13.  Upgrade branch level (1-10): when and which branch
14.  Renovate branch: spend now vs wait
15.  Relocate branch: which city and country
16.  Close branch
17.  Name individual branches
```

## C. Staff Decisions
```
18.  Hire staff for which branch
19.  Accept specialty preview or reroll
20.  Promote staff (L1→L2, L2→L3, L3→L4)
21.  Transfer staff between branches
22.  Fire staff
23.  Assign Regional VP to up to 3 branches
24.  Pay morale bonus (branch) vs buy Morale Package (global)
25.  Prioritize promotions vs new hires
```

## D. Executive Decisions
```
26.  Which executive to hire first (COO / CMO / CFO / CTO)
27.  Which tier to hire (T1 / T2 / T3)
28.  When to replace with higher tier
29.  Fill all 4 slots vs specialize
```

## E. R&D Decisions
```
30.  Which project to start from available pool
31.  Which slot to allocate per project
32.  Buy R&D Accelerator to finish instantly
33.  Cancel an active project (refund 50%)
34.  Order of completion — which bonuses to unlock first
35.  Industry-exclusive R&D choice
```

## F. Brand Score Decisions
```
36.  Run PR Campaign now vs wait
37.  How to respond to crises (Pay / Ride out / Ignore)
38.  Board decision choices affecting brand score
39.  When to hire CMO to raise brand cap
40.  Prioritize brand vs income strategy
```

## G. Stock Market Decisions
```
41.  Buy stocks — which index/company, how much
42.  Sell stocks — when to take profit or cut losses
43.  List your company — yes/no
44.  Delist your company
45.  Respond to crash warnings (sell / hold / buy more)
46.  Use Finance Wizard crash immunity
```

## H. Board Decision Choices
```
47-111. For each of the 65 board decision types: Option A / B / C
        (~180 distinct option choices total across all 65 types)
```

## I. Event Responses
```
112. Crisis response per crisis: Pay / Ride out / Ignore (45 crisis types × 3 = 135)
113. Opportunity event: Accept / Decline (20 types)
114. Hostile takeover defense: Legal / PR / Accept buyout
```

## J. Investor Contracts
```
115. Which contracts to prioritize (when 5 slots)
116. Whether to complete early or let auto-complete
```

## K. Seasonal System
```
117. Whether to IPO (voluntary at $500M)
118. Industry choice for next run (after IPO)
119. Buy Season Pass
120. How to time seasonal events with Seasonal path branches
```

## L. Social Decisions
```
121. Create Corporation vs play solo
122. Who to invite to Corporation
123. Leave Corporation
124. Target for hostile takeover (NPC vs player)
125. List branches on marketplace
126. Listing price (50-300% market value)
127. Buy another player's branch
128. Invest in another player's company stock
```

## M. Monetization Choices
```
129. Revenue Boost (49 R$): timing
130. Morale Package (39 R$): reactive
131. R&D Accelerator (59 R$): planned vs impulsive
132. Takeover Token (99 R$): before specific attempt
133. CEO Pass (349 R$): long-term offline
134. Expansion License (199 R$): which 3 countries to discount
135. Extra R&D Slot (249 R$): R&D-heavy build
136. VIP Dossier (149 R$): cosmetic/social flex
137. Season Pass (199 R$): seasonal player
138. Starter Bundle (129 R$): best on first game
139. Quick Renovation (19 R$): reactive when quality low
140. Branch Slot Unlock (79 R$): per branch decision
```

## N. UI & Display Choices
```
141. World map view vs list view in Branches tab
142. Sort staff by morale / level / specialty
143. View past seasons in leaderboard archive
144. Click another player's dossier
145. Collapse/expand Board History
146. Filter R&D projects by category
147. Solo vs Corp sub-tab in leaderboard
```

---

# SECTION 21: IMPLEMENTATION NOTES

## Development Priority Order

```
PHASE 1 — MVP (4-6 weeks):
  - ProfileStore setup (correct from day one — no shortcuts)
  - Income tick system + client sync (every 5s)
  - Branch system (open, level, path selection, income formula)
  - Staff system (hire, morale decay, fire, quit logic)
  - USA + UK + Germany only (3 countries to test with)
  - Fast Food + Café industries only (one cheap, one standard)
  - Login Summary Screen (OverlayManager)
  - Basic Dashboard tab + Branches tab + Staff tab
  - Top bar + Bottom nav
  - MonetizationL Revenue Boost + CEO Pass only
  → Soft launch as alpha, collect feedback

PHASE 2 — v1.0 (4-6 more weeks):
  - All 15 industries
  - All Tier 1-3 countries (13 countries)
  - Executive system (all 4 roles)
  - R&D system (all 25 projects)
  - Brand reputation system
  - Board decisions (30 types minimum)
  - Crisis + events system (all crisis types)
  - Investor contracts
  - Full UI (all 8 tabs)
  - All monetization items
  → Official release

PHASE 3 — v1.5 (ongoing):
  - Stock market
  - Hostile takeovers + PvP
  - Corporation Mode
  - Player branch marketplace
  - Seasonal system (IPO + prestige)
  - Tier 4+ countries
  - Season Pass system

PHASE 4 — Live Service:
  - Monthly seasons with new Season Pass ID
  - Seasonal events calendar (Section 12)
  - New R&D projects
  - New board decisions
  - Leaderboard badges
  - Community events
```

## Critical "Don't Make These Mistakes" Notes

```
1. SAVE SYSTEM: Use ProfileStore. Not raw DataStoreService. Not DataStore2.
   ProfileStore's session locking prevents dual-server corruption.
   Franchise Empire's broken saves come from poor DataStore management.

2. NEVER TRUST CLIENT: All cash calculations are server-side.
   Never read a cost value from a RemoteEvent argument — always recalculate
   from Config ModuleScripts on the server.

3. INCOME TICK: Don't FireClient every second.
   Server ticks every second for accuracy, but SyncEconomy fires every 5 seconds.
   Client uses NumberFormatter + a lerp loop to animate values smoothly between syncs.

4. OFFLINE CALCULATION: Must run as a single synchronous block BEFORE any sync
   RemoteEvents fire. Player should always load into their post-offline state.
   Never show pre-offline state for even one frame.

5. TEXT FILTER: Every player-entered string (company name, corp name, branch name)
   must pass TextService:FilterStringAsync before being stored or displayed.
   Roblox will moderate/remove the game if player-generated content bypasses this.

6. MOBILE FIRST: All TextButtons and ImageButtons must have Size minimum 44×44 offset
   for accessible touch targets. Test every screen with Roblox's mobile emulator.
   UIPadding around small buttons to increase tap area without changing visual size.

7. LOADING STATES: Every RemoteFunction:InvokeServer call needs a loading spinner
   in the UI while waiting. Players who see blank screens assume the game is broken.
   Use a CanvasGroup with GroupTransparency = 1 overlaid with a spinner during loads.

8. RATE LIMITING: Implement from day one. Roblox exploit scripts are common.
   Use the RateLimiter ModuleScript on every server handler from the start.

9. COLOR3 STORAGE: Store Color3 values in DataStore as hex strings ("#22C55E").
   Color3 objects cannot be serialized to DataStore directly.
   Convert with Color3.fromHex() on load.

10. UIOBJECT REUSE: For large scrolling lists (branch list, staff list), use object
    pooling — don't create/destroy frames on every update. Reuse a fixed pool of
    frame templates and update their content via Lua.

11. INDUSTRY THEMING: When player changes industry (on IPO), update all
    THEME_COLOR references by calling a ThemeService:SetIndustry(industryId)
    function that iterates known UI elements and updates their Color3 values.
    Store theme color lookups in IndustryConfig, not hardcoded in UI scripts.
```

---

END OF DOCUMENT
Mogul Inc. Complete Game Specification — Version 2.0
Total: 55 countries, 15 industries, 15 staff specialties, 25 R&D projects,
65 board decisions, 45 crisis types, 20 opportunity types, 12 seasonal events,
150+ player choices documented.
All web/HTML terminology replaced with Roblox Luau equivalents.
