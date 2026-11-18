# Domain Category 03: Home-Run Bakery & Pre-Order Drops Overlay

*Synthesized from Dual-Agent Consensus: **Craft & Micro-Bakery Operations Experts** (Hotplate, Bakesy, BakeryFlow, DoughPlan, Cottage Food Compliance & Baker's Math Standards) + **D2C Drop Software Practitioners** (Pessimistic/Atomic Slot Inventory Locks, Baker's Percentage Prep-Sheet Aggregation, Automated Allergen Rollups, 2-Tap Mobile Drop Checkout).*

Load this domain overlay alongside the active lifecycle playbook (`playbooks/01..06`) whenever building software, storefronts, or operations tools for a home-run bakery, cottage food business, or local pre-order food drop.

---

## Phase 01: Menu Drop Validation, Batch Economics & Cottage Compliance
- **Consensus Standards:**
  - **Signature SKU Wedge & Shared Base Doughs:** Anchor each drop around 1–3 high-margin repeatable SKUs sharing base doughs or oven temperatures (e.g., country sourdough, laminated pastry, brown-butter cookie box) plus at most 1 seasonal special.
  - **Sellable-Yield Margin Formula:** Price from **sellable yield** (total batch minus 5%–10% waste/QC buffer), targeting **20%–30% ingredient + packaging COGS** and **30%–40% net profit margin** after paying owner labor (`hourly rate x active minutes`) and 10%–15% overhead:
    `Retail Price = (Ingredient BOM + Packaging + Labor + Overhead) / (Sellable Yield x (1 - Target Net Margin))`
  - **Cottage Food Non-TCS Gate:** Verify every SKU complies with local cottage food non-TCS (Time/Temperature Control for Safety) rules (shelf-stable breads, cookies, cakes) before listing.
- **Hard Bans:**
  - **NO** hobbyist pricing that omits owner labor minutes, boxes/bags/labels, and payment processing fees.
  - **NO** mixing open-ended custom-cake quote workflows into timed batch drops.
  - **NO** listing unapproved refrigerated/TCS fillings (custards, raw dairy creams) under a cottage food permit.

## Phase 02: Storefront & Mobile Drop UX
- **Consensus Standards:**
  - **Drop Countdown + Real-Time Scarcity Counters (`tabular-nums`):** Show the active/upcoming `DropEvent` window, order cutoff timestamp, and live remaining batch caps per SKU (`6 loaves left` / `Sold Out`) and per pickup slot.
  - **Crumb-First Visuals & Explicit Weights:** Pair natural-light macro crumb/crust photography with exact net weights (`g`/`oz`), serving counts, and bold allergen pills.
  - **2-Tap Mobile Checkout + Slot Picker:** Optimize for mobile SMS/Instagram traffic: let buyers pick a specific pickup/delivery time slot (`Sat 10:00–11:00 AM`), acknowledge cottage-food & allergen notices, and pay in 2 taps via Apple Pay, Google Pay, or UPI without password creation.
- **Hard Bans:**
  - **NO** "always-open" e-commerce cart illusions when no drop or pickup slot is active.
  - **NO** manual *"DM on Instagram to order and Venmo"* workflows.
  - **NO** forcing account registration before mobile wallet checkout.

## Phase 03: Middleware, Atomic Slot Locks & SMS Drop Boundaries
- **Consensus Standards:**
  - **Race-Condition-Free Batch & Slot Reservations:** Never use app-level read-then-write stock checks during drop spikes. Reserve inventory per `(drop_id, product_id, pickup_slot_id)` using pessimistic row locks (`SELECT ... FOR UPDATE`) or atomic Redis `DECRBY` with a **5–10 minute cart TTL** sweeper, converting the hold on payment webhook confirmation.
  - **100% Pre-Paid Before Bake Sheet:** Orders enter production only after verified payment; automatically lock edits/cancellations at the fermentation cutoff (**48–72 hours** prior to pickup).
  - **Rate-Paced SMS/WhatsApp Drop & Waitlist Queues:** Dispatch drop-open alerts and sold-out waitlist backfills via queued, rate-paced background workers with `idempotency_key` deduplication so Twilio/WhatsApp never throttles or double-texts subscribers.
- **Hard Bans:**
  - **NO** `"Pay at Pickup"` / cash defaults (unclaimed perishable bakes are a 100% margin loss).
  - **NO** global product stock counters that bleed across separate weekly `DropEvent` records.
  - **NO** synchronous SMS broadcast loops inside an HTTP request handler.

## Phase 04: Backend, Baker's Percentage Engine & Backward Scheduling
- **Consensus Standards:**
  - **Baker's Percentage & Unrounded Gram Aggregation (`RecipeFormula`):** Store formulas in grams (`g`) and baker's percentages (`total flour = 100%`). When a drop closes, compute the master `PrepSheet` by multiplying `SUM(sold_qty) * base_dough_weight_g` (+ 3%–5% levain/bowl loss) and exploding into exact gram requirements per ingredient—**rounding only once at the final total** to prevent hydration drift.
  - **Equipment-Bounded Batch Splitting (`MixerBatch` & `OvenRound`):** Automatically split total dough mass into mixer loads bounded by `max_mixer_capacity_g`, fridge cold-retard shelves, and consecutive oven deck waves.
  - **Backward Production Timeline (`T-48h` to `T-0`):** Generate stage checklists anchored backward from first pickup: `T-36h` Levain Build -> `T-24h` Autolyse/Bulk Ferment & Shaping -> `T-18h` Cold Retard -> `T-4h` Bake Waves -> `T-2h` Mandatory Cool-Down Buffer -> Packaging.
  - **Formula-Derived Allergen & Cottage Labels:** Auto-generate compliant bag labels directly from `RecipeFormula` (ingredients sorted by weight descending, sub-ingredients expanded parenthetically, 9 major allergens bolded, net weight, bake date, and home-kitchen disclaimer).
- **Hard Bans:**
  - **NO** storing or scaling production recipes in volumetric cups/spoons.
  - **NO** setting drop SKU caps higher than physical fridge cold-retard or oven wave capacity.
  - **NO** maintaining ingredient/allergen labels in static Canva/Word files separate from `RecipeFormula`.

## Phase 05: Positioning, Scarcity Drops & Local Retention GTM
- **Consensus Standards:**
  - **Owned SMS/WhatsApp Drop Club Over Social Algorithms:** Convert social traffic into an owned phone waitlist; give SMS subscribers a 15-minute early access link before public Instagram announcement.
  - **Recurring "Bread Club" / Standing Box Subscriptions:** Lock in predictable baseline oven utilization before public drops via bi-weekly/monthly standing boxes for repeat neighbors.
  - **Packaging as Referral Media:** Include crust-refresh/freezing instructions and a QR code on every bag label linking straight to the next drop's SMS waitlist.
- **Hard Bans:**
  - **NO** coupon/discount treadmills; clear any extra loaves via a 1-tap SMS *"Porch Flash Claim"* to the waitlist.

## Phase 06: Porch Fulfillment, Food Safety & Support Ops
- **Consensus Standards:**
  - **Cool-Down Gate & Tamper-Evident Porch Staging:** Enforce the cool-down timer before bagging (sealing warm loaves traps steam, ruins crust, and accelerates mold). Stage sealed orders by time slot with high-contrast `ALLERGY` flags printed on packing tags.
  - **Automated `T-24h` & `T-2h` Pickup Reminders + 1-Tap Check-In:** Send automated WhatsApp/SMS reminders containing exact time window, bag tag code, and porch/gate instructions, paired with a 1-tap baker check-in view and automated waitlist reassignment for unclaimed orders.
- **Hard Bans:**
  - **NO** bagging warm baked goods or staging unlabeled/unsealed items on porch pickup racks.
  - **NO** post-cutoff refunds after bulk fermentation has started unless a waitlist buyer claims the slot.
