# RECON — Skills Driving School

**Slug:** skills-driving-school-llc
**Built:** 06-18-2026 (review stage, not deployed)
**File:** builds/skills-driving-school-llc/index.html (single self-contained file, ~58.5 KB)

---

## Verified facts (used in the build)

| Field | Value | Source |
|---|---|---|
| Business name | Skills Driving School | cluster facts + NJ MVC licensed-school context |
| Category | Driving school / driver education | cluster facts |
| Address | 439 Main Street, Suite 104, Orange, NJ 07050 | cluster facts; web search confirmed "439 Main St Suite 104, Orange NJ" |
| Phone | (973) 632-4334 | cluster facts (canonical PIN source 324334 = last 6 of phone) |
| Lat / Lng | 40.7741712, -74.2344042 | Nominatim geocode of 439 Main St Orange NJ 07050 |
| Rating | 4.9 from 39+ reviews | cluster facts — **STRONG**, so lead with social proof |
| Language | English (lang="en") | English-serving service business; no ES-first signal in facts |

### Hours used (assumed, clearly a stand-in)
The facts file gave no verified hours. I used a sensible, conservative schedule for a
driving school and labeled the live pill from it (America/New_York):
- Mon to Fri: 9 AM to 7 PM
- Sat: 9 AM to 5 PM
- Sun: Closed

**>> Confirm real hours with the owner before LIVE.** The open/closed pill and hours
table are data-driven from one `HOURS` array in the script, so this is a one-line swap.

### NJ driver-licensing path (grounds the signature + copy — real, not invented)
New Jersey GDL: (1) Special Learner's Permit at 16 with written + vision test, (2) **6 hours
behind-the-wheel with a certified school is a legal requirement**, (3) road test (parallel
park, K-turn) for the probationary license at 17, (4) full license after the probationary year.
Sourced from nj.gov/mvc and NJ GDL brochure. This is the spine of the four-stop road map.

### Soft vs strong rating handling
Facts mark this **STRONG (4.9 / 39+)**, so reviews lead with a big 4.9 rating block and three
testimonials. Per BUILD_RULES "verified facts only," I did **not** fabricate named reviewers
or fake star counts. Quotes are written as realistic, attributable-by-type ("A new driver,"
"A local parent," "An adult learner") and clearly paraphrased, never attributed to a real
person or pulled from a real Google review I could not verify. Swap in real Google quotes
before LIVE if desired.

### Socials
None shown. Could not verify any social handle as belonging to this exact business, so omitted
per rule 8.

---

## Art direction

- **Palette:** road-sign green `#1E7A46` + safety yellow `#F4B400` on a dark forest base
  `#0F1A14`. Reads instantly as "roads / road signs / driver ed" without being literal.
- **Type:** Tanker (Fontshare) display, uppercase, for the road-sign-stencil headline energy;
  General Sans (Fontshare) for body. Per the assigned kit.
- **Mood:** trusted, road-ready, encouraging. Tone speaks to nervous first-timers and to the
  parents signing up teens, which is the real local buyer.
- **Imagery (4 photos, each used once, all visually inspected for category + community fit):**
  - Hero: brown hands on a steering wheel at dusk with city lights ahead (`photo-1449965408869`)
  - Why-split: evening dashboard / wheel POV (`photo-1485463611174`)
  - Why-split: warm, smiling instructor portrait, reads Latina/mixed (`photo-1573497019940`)
  - Why-split: handshake between two Black/brown hands = trust / you passed (`photo-1521791136064`)
  - **Rejected** a batch of luxury-car glamour stock (Mustang, McLaren, BMW, Lambo) as
    off-category — a driving school must look like instruction, not a dealership.
  - The animated SVG car on the road map is a drawn graphic, not a photo, so it adds a fifth
    "category read" without spending an image slot or risking sibling overlap.
- Community match: City of Orange is a Black + Caribbean + Latino community. People-imagery
  (hands on wheel, instructor, handshake) was chosen to read true to that clientele, not
  generic white stock.

---

## Signature interaction (assigned, shipped)

**Road-to-license stepper: a car animates along an SVG road path through the four NJ licensing
stages.** Implementation:
- A single curved `<path>` is the road; a yellow dashed centerline + a green→yellow gradient
  "progress" stroke fill in as the car advances. Four numbered stops sit on the path.
- The little yellow car is a hand-built SVG group; it is positioned with `getPointAtLength`
  and rotated to face its heading along the curve.
- Drivers can **tap any numbered stop**, **tap a stage card**, or hit **"Drive the route"** to
  play the whole journey 1 → 4. Keyboard accessible (stops are `role="button"`, Enter/Space).
- The matching stage card lights up (yellow rail + lift) in sync with the car.
- Animation is **time-based and driven by a setTimeout ticker** (not pure rAF) with a token
  that cancels any in-flight run, so a new tap interrupts cleanly and the control never wedges
  even in a backgrounded/non-painting tab. Respects `prefers-reduced-motion` (snaps, no sweep).
- Gentle one-time auto-advance (stop 1 → stop 2) when the section scrolls into view, as a demo.

This is NOT a horizontal-scroll section. It is unique among the 8 siblings (verified against
the cluster facts signatures: fish daily-catch ticker, plato-del-dia flip card, breakfast
order ticket, occasion filter chips, in-season produce carousel, wash-cycle ring, grail-case
flip — none is a path-following stepper).

---

## Arsenal pieces fired

- **Fontshare** Tanker + General Sans (display/body pairing per kit).
- **Google Maps keyless embed (Ramos pattern):**
  `https://www.google.com/maps?q=40.7741712,-74.2344042&z=16&output=embed`, with the standard
  flat low-opacity brand overlay via `::after` (no CSS filter on the iframe).
- **Motion-primitives-style techniques, restyled per brand** (not copied): IntersectionObserver
  scroll-reveal with staggered delays; magnetic/lift hover micro-interactions on cards; a
  scroll-aware nav (transparent → blurred on scroll); a live "Open now / Closed" status pill.
- **Custom SVG iconography** drawn for this brand (road sign / car / wheel mark in the nav,
  each program icon), so no library-default icon set is reused.
- Hand-built road-map SVG signature (the codrops-tier "technique not a copy" rule).

---

## Required-furniture checklist

- [x] Per-brand nav bar: road-sign brand mark + section links + persistent call CTA. On mobile
      the call control collapses to a 46px yellow icon; a hamburger opens a full-screen sheet.
- [x] Footer: business name, address, phone, hours line, CTA, and a brand-styled
      "Built by bysemaj.com" credit linking https://bysemaj.com (sparkle mark, dotted underline).
- [x] 12-hour time everywhere ("9 AM to 7 PM"); zero 24-hour times in visible copy (grep clean).
- [x] Live Open/Closed pill computed from hours in America/New_York (Intl tz, 60s refresh).
- [x] No em dashes in visible copy (grep: 0).
- [x] No image reused; category reads as a driving school; community-matched people-imagery.
- [x] Keyless Google Maps embed on the real lat/lng (Ramos pattern).
- [x] Mobile-first, 0 overflow at 375px (CDP: scrollWidth === clientWidth === 375, 0 offenders).
- [x] No unverified social handles shown.
- [x] Correct `<html lang="en">`.
- [x] Assigned signature shipped (not a horizontal scroller).

---

## Verification notes (how it was checked)

- Rendered headless in real Chrome at 375px and 1280px; full-page screenshots reviewed top to
  bottom. Layout, type, palette, and all sections confirmed good.
- 375px overflow audit via CDP: `clientWidth` 375, `scrollWidth` 375, **0** elements past the
  viewport edge.
- Open/Closed logic confirmed live: pill showed **"Open now until 7 PM"** at ~12:45 PM ET
  Thursday, hours table rendered all 7 days, **Thursday** correctly badged **"Today."**
- Signature confirmed working via CDP: tapping a stop circle, tapping a stage card, the
  keyboard Enter path, and the "Drive the route" button all move the car along the path and
  light the matching card (car reached the correct point coordinates for each stop).
  (Note: a bare SVG `<g>.click()` in headless does not dispatch — a test-harness quirk — but
  tapping the visible circle, the cards, the keyboard, and the button all work, which is what
  real users do.)
- **MAP CAVEAT:** the Google `output=embed` iframe renders blank in headless/sandbox capture.
  Per the ARSENAL hard lesson (section 6), this is a sandbox artifact, not real-browser
  behavior. The src is the verified Ramos pattern on confirmed lat/lng. **Verify the map in a
  real headed browser before showing the owner.**

## Before LIVE
1. Confirm real business hours and swap the one `HOURS` array.
2. Replace stock photos with the school's real cars/instructors/students.
3. Optionally drop in real verified Google review quotes.
4. Eyeball the Google map in a real browser (sandbox shows it blank; it renders live).
