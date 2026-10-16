# Peer Benchmarks Mock-Up: Build Instructions (Duo License Utilization)

> **Sample Data notice:** Every name, ID, seat count, percentage, and dollar amount in this document and in the mock-up is **Sample Data**. It illustrates layout and behavior only and must **not** be used in place of actual requirements.

**Document owner:** Jayne Booth, CXPM (Customer Experience Product Management), AI Programs
**Related ticket:** CXP-51239 "Peer Benchmarks – Build Foundation"
**Status:** Draft for Engineering review

---

## 1. Executive Summary

**What's the point:** These instructions produce a clickable mock-up with two views of the same Cisco Duo benchmark. The Customer Success (CS) view is segmented by Annual Recurring Revenue (ARR). The Renewals view is segmented by Available to Renew (ATR). Each view shows the customer against peers, explains the gap, and recommends actions. Engineering can react to the layout, the peer-group logic, and the privacy behavior before the build starts.

**Use case:** Show one customer's Duo license utilization versus peers. Explain the gap. Recommend what Customer Success should do.

---

## 2. Explore: What the Sources Say

| Finding | Source |
|---|---|
| License Utilization Rate is a Minimum Viable Product (MVP) lagging metric. | CXP-51239 v2, Adoption Rate Metrics |
| Peer groups need at least 10 accounts (k-anonymity). Smaller groups roll up to the parent tier. | CXP-51239 v2; PRD Phase 1, Section 4 |
| Accounts without telemetry are excluded, not scored as 0%. | PRD Phase 1, Section 5 |
| Distribution is P25 / P50 / P75 / P90. | Phase 4 PRD, Section 4.1 |
| Duo features have enablement, engagement tier, weight, and license tier. | CXP-51239 v1 |
| CS segments by ARR: Extra Large (>$20M), Large ($6M–$20M), Medium ($2M–$6M), Small ($300K–$2M), Extra Small (<$300K). | Risk Data Segmentation slide |
| Renewals uses Sales segments (Premier/Key/Major, Select, Midsize, Small), which carry ATR totals. | Risk Data Segmentation and Customer Segments slides |
| Layout pattern: "Your Company Profile", filters, Peers vs. You bars, "View in Assets" link. | Cisco IQ Peer Benchmarks screenshot |

### Gaps to confirm before this is treated as a requirement

1. **ATR dollar bands are not defined.** The sources give ATR totals per Sales segment, not thresholds. The mock-up uses Sales segment names as ATR tiers.
2. **ARR bands conflict.** The Phase 4 PRD uses >$10M / $2M–$10M / <$2M. The Risk Data Segmentation slide uses five bands. The mock-up follows the slide.
3. **The utilization formula is not defined.** Assumed: *seats with a sign-in in the last 30 days ÷ seats purchased.*
4. **Pilot product is not named** in CXP-51239 v2. Duo is assumed.

---

## 3. Plan: Build Specification

### 3.1 Layout (top to bottom)

1. **View toggle:** Customer Success (by ARR) | Renewals (by ATR).
2. **Contextual header** (shown once, never repeated in tables): customer name, CAV BU ID, Deployment ID, product, journey stage. CS view adds the ARR band. Renewals view adds ATR tier, renewal date, days to renewal, and ATR dollars.
3. **Peer group card:** sample size, a dropdown to change the group, and a "Fallback" chip when a parent tier is used.
4. **Chart card:** Peer median (P50) bar vs. You bar, plus a P25 / P50 / P75 / P90 range strip with a "You" marker and percentile.
5. **Feature table** (4 columns, no horizontal scrolling): Feature | You | Peer P50 | Gap. Rows expand to show engagement level and license needed.
6. **"Why is there a gap?" card.**
7. **"Recommended actions" card** with a **Copy talk track** button.
8. **Footer:** "Peer data is combined across customers. Groups with fewer than 10 accounts are merged into a broader group."
9. **Persistent "Sample Data" bar** at the top and a Sample Data notice at the bottom.

### 3.2 Sample Data

| Item | Value (Sample Data) |
|---|---|
| Customer / CAV BU ID / Deployment ID | Acme Corp / 1234567 / DUO-0042 |
| Seats purchased / enrolled / active in last 30 days | 5,000 / 3,100 / 2,400 |
| Utilization | 48% |
| CS peer group (Medium ARR) | P25 55%, P50 71%, P75 84%, P90 92%; n = 212 |
| Renewals peer group (Select tier) | P25 52%, P50 69%, P75 82%, P90 91%; n = 176 |
| Renewal | 2026-12-15; ATR $410K |

| Feature | You | Peer P50 |
|---|---|---|
| Verified Push | 41% | 68% |
| Platform / Roaming authenticators | 6% | 18% |
| Duo Desktop (device health) | 22% | 47% |
| Trusted Endpoints | 10% | 31% |

**Percentile note:** 48% is below the CS peer P25 (55%), so the mock-up shows about the 18th percentile and the label "below the 25th percentile." The estimate interpolates between the sample points and is illustrative only.

### 3.3 Gap diagnosis rules

Each rule shows a tag (Likely, Not a cause, or Check) and its evidence line.

| Reason | Rule |
|---|---|
| Seats bought but users not enrolled | Flag if enrolled seats < 70% of purchased |
| Enrolled users rarely sign in | Flag if active ÷ enrolled < 60% |
| Features licensed but not set up | Flag if license entitles the feature and enablement = 0 or far below peers |
| Early in the deployment | Flag if deployed < 6 months (gap may close on its own) |
| Seat count may be too high | Always "Check" (headcount change, merger, over-purchase) |
| Applications not yet protected | Always "Check" (compare with application inventory) |

### 3.4 Actions

| View | Action content |
|---|---|
| CS | Ordered by journey stage, each with owner and timing |
| Renewals | Adds a **renewal posture** line: Drive adoption first / Right-size seats / On track, plus days to renewal and ATR at risk |

### 3.5 Negative scenario handling

| Demo state | Required behavior |
|---|---|
| No telemetry | Show "Usage data is not available for this customer." Never show 0%. Hide the chart and feature table. Show license-only facts and the action "Enable Duo telemetry sharing." |
| Peer group under 10 accounts | Show a "Broader group used" banner, the parent tier, and the Fallback chip. |
| Peer data out of date (> 7 days) | Show a warning with the age of the data. |

### 3.6 Interactions

- The view toggle swaps peer group, header fields, and actions without a page reload.
- Hovering any bar shows its value and sample size.
- Feature rows expand to show engagement level (Low / Medium / High) and the license needed.
- **Copy talk track** copies customer-ready wording to the clipboard.

---

## 4. Acceptance Criteria

1. Both views render from the same Sample Data object.
2. Customer name, CAV BU ID, and Deployment ID appear only in the header.
3. The "No telemetry" state never shows 0%.
4. A peer group under 10 accounts shows the fallback banner and chip.
5. No table needs horizontal scrolling.
6. "Sample Data" is visible at all times.

## 5. How to Test

| Check | Steps | Expected result |
|---|---|---|
| Views share data | Toggle CS and Renewals | Same customer and seat counts; different peer group and actions |
| Header only | Search the page for the CAV BU ID | Appears once, in the header |
| No telemetry | Choose "No telemetry" | Message shown; no 0%; chart hidden |
| Fallback | Choose "Cohort under 10 accounts" | Banner and Fallback chip appear |
| Stale data | Choose "Peer data out of date" | Warning appears |
| Width | Narrow the browser to phone width | No sideways scrolling in tables |
| Copy | Select **Copy talk track** | "Copied" appears; text pastes elsewhere |

---

## 6. Open Items

- Confirm ATR dollar thresholds with Renewals leadership.
- Confirm the utilization formula and the pilot product.
- Confirm the Renewals view shares the CS peer data and differs only in segmentation.
- Reconcile the ARR band conflict between the Phase 4 PRD and the Risk Data Segmentation slide.
