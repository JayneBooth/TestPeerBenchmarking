# Peer Benchmarks Mock-Up: Duo License Utilization

> **Sample Data only.** Every name, ID, seat count, percentage, and dollar amount in this folder is invented for illustration. This mock-up shows layout, behavior, and wording. It must **not** be used in place of actual requirements.

## What this is

A clickable, single-page mock-up that shows how Peer Benchmarking could look for Customer Success (CS) and Renewals teams. The use case: show one customer's Cisco Duo license utilization versus its peers, explain the gap, and recommend what to do.

- **CS view:** peers grouped by Annual Recurring Revenue (ARR).
- **Renewals view:** peers grouped by Available to Renew (ATR).

Related ticket: CXP-51239 "Peer Benchmarks – Build Foundation."

## Files

| File | Purpose |
|---|---|
| `index.html` | The working mock-up. No install or build needed. |
| `BUILD_INSTRUCTIONS.md` | Full specification: sources, Sample Data, gap rules, acceptance criteria, how to test |
| `README.md` | This file |

## How to open it

- **Hosted:** If GitHub Pages is on for this repository, open the Pages address shown under **Settings > Pages**.
- **Locally:** Download `index.html` and double-click it. It works offline and loads nothing from the internet.

## What to try

1. Switch between **Customer Success: by ARR** and **Renewals: by ATR**.
2. Hover the bars to see values and sample size.
3. Select a feature row to see engagement level and the license needed.
4. Use the **Demo state** menu:
   - **No telemetry:** usage is never shown as 0%.
   - **Cohort under 10 accounts:** a broader group is used, with a banner.
   - **Peer data out of date:** a warning appears.
5. Select **Copy talk track** for customer-ready wording.

## Privacy behavior shown

- Peer groups need at least 10 accounts. Smaller groups roll up to a broader group.
- Customers without telemetry are left out of the comparison, not scored as 0%.
- Only combined peer values are shown, never another customer's data.

## Open items

- ATR dollar bands are not defined in the source material.
- The utilization formula is assumed: seats active in the last 30 days ÷ seats purchased.
- Duo is assumed as the pilot product; CXP-51239 v2 does not name one.

## Update the page

Edit `index.html`, commit, and push. GitHub Pages refreshes within a few minutes.

## Owner

Jayne Booth, CXPM, AI Programs
