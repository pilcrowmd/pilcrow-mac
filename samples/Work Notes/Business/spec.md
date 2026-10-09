---
title: Harbour app – tide alerts on the phone
status: In review
owner: product
target_release: Q1 2027
---

# Spec: tide alerts on the phone

> [!NOTE]
> Status: **in review**. Comments by Friday. Numbers come from the
> [Q3 review](q3-review.md#customers).

## Problem

Boat owners call the harbour office to ask about the water level. In September the office
took **1,240 calls**, and 70% asked the same question: *"Can I leave the berth now?"*

## Goal

Let a boat owner see the water level for their berth on the phone, and get an alert before
it becomes too low to leave.

**Success after 3 months:**

| Measure | Today | Target |
|:--|--:|--:|
| Calls about water level per month | 1,240 | under 400 |
| Owners using the app weekly | 0 | 600 |
| Alerts that arrive late (over 2 min) | – | under 1% |

## Who it is for

1. **Boat owners** with a berth in the harbour – about 900 people.
2. **The harbour office** – fewer calls, one place to post notices.
3. **Visiting boats** – later, see [Out of scope](#out-of-scope).

## Requirements

| # | Requirement | Priority | Notes |
|:--:|:--|:--:|:--|
| R1 | Show the current level for the owner's berth | Must | Updated every minute |
| R2 | Alert when the level will drop below the berth limit within 60 min | Must | Push notification |
| R3 | Show the next high and low water times | Must | From the tide tables |
| R4 | Let the owner set their own alert limit | Should | Default from berth depth |
| R5 | Show harbour notices | Should | Posted by the office |
| R6 | Work offline with the last known reading | Could | Marked as "old" |

> [!IMPORTANT]
> R2 depends on the forecast work in [tidewatch](../Engineering/readme.md#roadmap). Without
> it we can only alert on the current level, not on what comes next.

## User flow

1. The owner installs the app and enters their berth number.
2. The app shows the level now, and the next low water.
3. The owner turns on alerts.
4. Sixty minutes before the level drops below the limit, the phone shows:
   *"Berth C-14: water too low to leave from 16:20. Next safe time 19:45."*

## Plan

- [x] Interviews with 12 boat owners
- [x] Berth depths collected from the harbour office
- [ ] Design review – **Tue 14 Oct**
- [ ] Alert service (needs the forecast)
- [ ] Beta with 50 owners – November
- [ ] Release – Q1 2027

## Risks

| Risk | Likelihood | Impact | What we do |
|:--|:--:|:--:|:--|
| Forecast is wrong near storms | Medium | High | Show "forecast uncertain" in storm warnings |
| Owners ignore alerts | Medium | Medium | Let them choose how early the alert comes |
| Gauge goes offline | Low | High | Fall back to the tide tables, say so on screen |

> [!WARNING]
> We must never show a level as current when it is older than 10 minutes. A wrong "safe"
> message could put a boat on the mud.

<details>
<summary>Options we looked at and did not choose</summary>

- **SMS only.** Cheaper, but owners wanted to check the level themselves, not only get alerts.
- **A web page.** Works today, but push alerts on a web page are unreliable on many phones.
- **Buy a product.** The two products we found do not read our gauges.

</details>

## Out of scope

- Visiting boats (no berth number) – next year.
- Booking a berth in the app.
- Weather forecasts – we link to the national service instead.

## Open questions

- Who answers owners' questions about the app – the office or the product team?
- Do we need the app in Polish as well as English for the first release?[^lang]

[^lang]: About a third of owners gave a Polish address in the interviews.
