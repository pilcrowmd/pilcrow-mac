---
document: Services Agreement
version: draft 3
parties: [Northgate Harbour Authority, Tidewatch Systems Ltd]
governing_law: England and Wales
status: For review – not for signature
---

# Services Agreement

**Between** Northgate Harbour Authority (the **"Customer"**)
**and** Tidewatch Systems Ltd (the **"Supplier"**).

> [!IMPORTANT]
> Draft 3. Changes since draft 2 are in clauses 4.2, 7.1 and Schedule B. Both parties and
> all names are invented for this demo.

## Contents

1. [Definitions](#1-definitions)
2. [Services](#2-services)
3. [Fees and payment](#3-fees-and-payment)
4. [Service levels](#4-service-levels)
5. [Data](#5-data)
6. [Liability](#6-liability)
7. [Term and termination](#7-term-and-termination)
8. [General](#8-general)

## 1. Definitions

In this Agreement:

| Term | Meaning |
|:--|:--|
| **Agreement** | This document and its Schedules |
| **Business Day** | A day other than a Saturday, Sunday or public holiday in England |
| **Data** | All readings, alerts and logs produced by the Services |
| **Effective Date** | The date of the last signature below |
| **Services** | The services described in [Schedule A](#schedule-a--services) |
| **Uptime** | The share of minutes in a month in which the Services are available |

## 2. Services

2.1 The Supplier shall provide the Services from the Effective Date.

2.2 The Supplier shall:

1. read the Customer's tide gauges at least once every 60 seconds;
2. send alerts to the contacts named by the Customer; and
3. keep the Data for at least 24 months.

2.3 The Customer shall give the Supplier network access to each gauge, as set out in
Schedule A.

## 3. Fees and payment

3.1 The Customer shall pay the fees in [Schedule B](#schedule-b--fees).

3.2 The Supplier shall invoice monthly in arrears. Invoices are due within **30 days**.

3.3 Late payments carry interest at 4% a year above the Bank of England base rate.[^interest]

## 4. Service levels

4.1 The Supplier shall keep Uptime at or above **99.9%** each month.

4.2 If Uptime falls below that level, the Customer is entitled to a credit:

| Monthly Uptime | Credit (% of monthly fee) |
|:--|--:|
| 99.0% – 99.9% | 10% |
| 95.0% – 99.0% | 25% |
| below 95.0% | 50% |

> [!NOTE]
> **Customer comment (draft 3):** we asked for a 100% credit below 95%. The Supplier offered
> 50%. Open point for the meeting on 14 October.

4.3 Credits are the Customer's only remedy for missed service levels, except under clause 7.2.

## 5. Data

5.1 The Customer owns the Data.

5.2 The Supplier shall:

1. use the Data only to provide the Services;
2. keep the Data in the United Kingdom or the European Economic Area; and
3. return or delete the Data within 30 days after this Agreement ends, at the Customer's
   choice.

> Personal data is not expected to be processed. If it is, the parties shall sign a data
> processing agreement before it starts.

## 6. Liability

6.1 Neither party limits its liability for death or personal injury caused by negligence,
or for fraud.

6.2 Subject to clause 6.1, each party's total liability in any year is limited to the fees
paid in the 12 months before the claim.[^cap]

6.3 Neither party is liable for loss of profit or indirect loss.

## 7. Term and termination

7.1 This Agreement runs for **36 months** from the Effective Date, then renews for 12 months
at a time unless either party gives 90 days' written notice.

7.2 Either party may end this Agreement at once by written notice if the other party:

1. commits a material breach and does not fix it within 30 days of notice; or
2. becomes insolvent.

## 8. General

8.1 This Agreement is governed by the law of England and Wales.

8.2 Notices must be in writing and sent to the addresses in Schedule A.

---

## Schedule A – Services

<details>
<summary>Gauges covered (4)</summary>

| Gauge | Location | Connection |
|:--|:--|:--|
| north-pier | North pier head | Fibre |
| south-basin | South basin entrance | Fibre |
| fuel-quay | Fuel quay | 4G |
| outer-mark | Outer channel mark | Radio |

</details>

## Schedule B – Fees

| Item | Fee |
|:--|--:|
| Service fee per gauge, per month | £420 |
| Set-up, one time, per gauge | £1,800 |
| Extra alert contacts above 20, per month | £15 each |

## Before signature

- [x] Definitions agreed
- [x] Data clauses agreed
- [ ] Service credit below 95% (clause 4.2)
- [ ] Notice addresses in Schedule A
- [ ] Sign-off by both legal teams

[^interest]: The Late Payment of Commercial Debts (Interest) Act 1998 may give a higher rate.
[^cap]: For the first year, the cap is the fees expected for that year.
