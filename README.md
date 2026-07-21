# 📊 Sales Pipeline Progression Dashboard

> **The Problem:** Sales leadership is flying blind. Deals disappear between stages. Some reps crush it, others don't. Nobody knows why.
>
> **This Dashboard:** Shows exactly where deals stall, which rep is struggling where, and what to coach.

---

## 🎯 The Real Problem

Your sales team looks like this:

```
Lead → Qualified → Proposal → Sold ✓
Lead → Qualified → Proposal → ??? (disappeared)
Lead → Qualified → ??? (never got proposal)
```

Leadership has spreadsheets. They know total revenue. But they don't know:
- ❌ **Where do 82% of leads die?**
- ❌ **Why does Ahmad close at 16.7% but Chen at 38.5%?**
- ❌ **Is Raj slow because he's bad at proposals, or because his clients need more time?**

So coaching is generic. Reporting takes 3-4 hours weekly. Deals slip through the cracks.

<img width="1586" height="712" alt="1" src="https://github.com/user-attachments/assets/87f77697-d041-4ea6-86ff-784816084d01" />

## 💡 The Solution: Stop Guessing, Start Diagnosing

This dashboard captures the **full lead journey**, not just the endpoints:

```
100 Leads Enter
    ↓
100 Qualified (100%)
    ↓
70 Get Proposals Sent (30 got stuck here ⚠️)
    ↓
18 Close as Sales (52 got stuck here ⚠️⚠️)
```

**Each lead appears multiple times** as it moves through stages. So you can answer:
- *When* do deals stall
- *Which rep* is struggling
- *Why* they're struggling (different problem = different solution)

---

## 🚨 What The Data Actually Shows

### The Two Bottlenecks

| Bottleneck | Cases Stuck | What It Means |
|-----------|-------------|--------------|
| 📌 Qualified → Proposal | **30 cases** | Proposals aren't being sent fast enough |
| 🔴 Proposal → Sold | **52 cases** | Proposals sent but deals aren't closing |

**Overall:** Only **18% of leads actually close**. That's the problem you're solving for.

---

### The Per-Rep Coaching Story

**Proposal Initiation** (Qualified → Proposal):
- 🟢 **Ahmad: 80%** — Strong. Getting proposals out.
- 🟢 **Siti: 79%** — Strong. Getting proposals out.
- 🟡 **Chen: 62%** — Lagging. Why? Client readiness? Approval bottleneck?
- 🟡 **Raj: 56%** — Lagging hardest. This is your 30-case leak.

**Proposal Closing** (Proposal → Sold):
- 🟢 **Chen: 38.5%** — Benchmark. She knows how to close.
- 🟢 **Raj: 35.7%** — Second best. Strong closer.
- 🟡 **Siti: 21.1%** — Trailing. Losing deals Ahmad should close.
- 🟡 **Ahmad: 16.7%** — Worst closer. Half Chen's rate. This is your 52-case leak.

### What This Means for Coaching

| Rep | Problem | Solution |
|-----|---------|----------|
| **Ahmad** | Sends proposals fine (80%) but closes poorly (16.7%) | Learn Chen's closing playbook — 2.3x better |
| **Siti** | Sends proposals well (79%) but closes okay (21.1%) | Refine closing; study Chen (38.5%) |
| **Raj** | Sends fewer proposals (56%) but closes well (35.7%) | Speed up proposal creation; maintain closing strength |
| **Chen** | Sends fewer proposals (62%) but closes best (38.5%) | Speed up proposal creation; keep coaching others |

**The Key Insight:** This isn't one problem. It's *two different problems affecting different reps*. Generic training won't work.

## 📈 Dashboard Structure (The Story You Tell)

### Page 1️⃣ : **Diagnosis — Where Are We Losing Deals?**

**Opening visual. This is what you show first.**

```
┌───────────────────────────────────────────────────────────┐
│  18% Lead-to-Sold  │  30 Cases Lost  │  52 Cases Stalled  │
│  (only this %      │  at Initiation  │  at Closing        │
│   make it)         │  (no proposal)  │  (proposal sent)   │
└───────────────────────────────────────────────────────────┘

Overall Funnel: 100 → 100 → 70 → 18
```
<img width="1257" height="711" alt="2" src="https://github.com/user-attachments/assets/992389f7-8cc6-44e2-87b9-43f84c30d428" />

**The talking point:**
> "We're losing deals at two different stages. First, 30 cases never get proposals sent. Second, 52 proposals are sent but don't close. These are different problems — they need different coaching."



---

### Page 2️⃣: **Breakdown — Which Rep Struggles Where?**

**The drill-down. Now you show the real story.**

Visual: Horizontal stacked funnel by rep, showing who's strong at initiation vs. closing.

**The talking point:**
> "Ahmad and Siti are great at getting proposals out (80%, 79%) but struggle closing (16.7%, 21.1%). Raj and Chen are great closers (35.7%, 38.5%) but aren't sending enough proposals (56%, 62%). Different problems, different coaching."

<img width="1263" height="698" alt="3" src="https://github.com/user-attachments/assets/0b2bd731-a2be-48f6-ab19-b16bbddec248" />

---

### Page 3️⃣: **Context — Revenue Impact**

**Why this matters.** Show the business numbers.

- Revenue by rep (~$4M each)
- Closed deal count by rep
- Conversion rate ranking

**The talking point:**
> "All four reps carry the load revenue-wise. But because of these pipeline gaps, we're leaving deals on the table. If Raj sent proposals at Ahmad's rate AND closed at his current 35.7% rate, we'd pick up ~8 more deals per year."

<img width="1263" height="711" alt="4" src="https://github.com/user-attachments/assets/496e26f4-b119-423d-89b2-9b66bb333071" />


## Technical Implementation

### Data Model: Progression Tracking
Each lead appears multiple times with a stage progression:
```
Lead_ID  | Sales_Rep | Stage      | Date       | Unit_Value
---------|-----------|------------|------------|------------
L-001    | Ahmad     | Lead       | 2026-01-15 | 500000
L-001    | Ahmad     | Qualified  | 2026-02-01 | 500000
L-001    | Ahmad     | Proposal   | 2026-02-10 | 500000
L-001    | Ahmad     | Lost       | 2026-03-05 | 500000
```

**Why this model?**
- Captures actual lead journey with timestamps
- Enables stage-by-stage conversion analysis
- Tracks *when* deals stall (not just that they did)
- Supports per-rep performance benchmarking

### Power Query Transformations
1. **Aggregated Stage Counts:** Group by Sales_Rep and Stage → count distinct leads per stage
2. **Conversion Rate Calculation:** (Sold count / Total unique leads) × 100 per rep
3. **Proposal Metrics:** 
   - Qualified → Proposal conversion
   - Proposal → Sold conversion
   - Closed deal count

### Tools
- **Python:** Data generation (if using synthetic data for portfolio)
- **Power Query:** ETL and transformations
- **Power BI Desktop:** Dashboard design and visuals
- **Power BI Service:** Publishing and refresh schedule

## Key Visuals

1. **Progression Overview Funnel** — Shows overall lead flow with drop-off counts
2. **Progression Funnel by Sales Rep** — Stacked horizontal funnel with per-rep percentages
3. **Conversion Rate by Rep** — Bar chart ranking reps on conversion %
4. **Sales Performance Overview** — Revenue by rep with lead count overlay
5. **KPI Cards** — Lead-to-Sold %, cases in each bottleneck gap

## 🎬 Interview Story (STAR)

**SITUATION**
> Sales team is losing deals, but leadership doesn't know where. Reps track spreadsheets. There's no visibility into *when* deals stall — proposal creation? Closing discipline? Leading to blind coaching and 3-4 hour weekly manual reporting.

**ACTION**
> Built a progression funnel dashboard that captures the full lead journey. Instead of just "Lead" or "Sold" status, each lead appears multiple times as it moves through stages. This reveals *exactly where* deals stall and *which rep* is struggling.

Three dashboard pages:
1. **Overall funnel** — "Where do 82% of leads disappear?"
2. **By-rep breakdown** — "Which rep has which problem?"
3. **Revenue context** — "Why does this matter to the business?"

**RESULTS**
> ✅ **Diagnosis:** Two distinct bottlenecks with different root causes
> - 30 cases stuck at Qualified→Proposal (Raj/Chen aren't sending proposals fast)
> - 52 cases stuck at Proposal→Sold (Ahmad/Siti aren't closing)
>
> ✅ **Coaching Clarity:** Per-rep gaps revealed
> - Ahmad needs to learn Chen's closing playbook (16.7% → 38.5%)
> - Raj needs to send proposals faster while maintaining his strong close rate
>
> ✅ **Operational:** Eliminated 3-4 hour manual reporting
>
> ✅ **Strategic:** Created foundation for predictive intervention — flag leads likely to stall before it's too late

## How to Use

1. **Load the progression data** into Power BI (CSV with Lead_ID, Sales_Rep, Stage, Date, Unit_Value)
2. **Apply Power Query transformations** (see Technical Implementation section)
3. **Build the three dashboard pages** in the order listed above
4. **Start with Page 1** — diagnosis always leads, then drill into Page 2
5. **Tell the story** — "Here's where we lose deals, here's which rep struggles where, here's what to coach"

## Assumptions & Limitations

- Dashboard assumes clean CRM data with stage progression timestamps
- "Stalled" status assumes a deal is lost if no forward movement after X days (configurable)
- Rep coaching gaps may reflect client segment differences, not pure skill — requires qualitative follow-up
- Data quality depends on consistent stage tagging and rep assignment

---

## 🔧 What Makes This Project Stand Out (Portfolio-Wise)

### ✨ Data Modeling (Not Just Visuals)
Instead of tracking "final status," the **progression model captures the full journey**. This is harder to design but WAY more powerful. Shows you think about data structure, not just dashboard pretty-printing.

### 🧠 Diagnostic Thinking
Doesn't just say "Ahmad is bad." Asks *why* — is it lead quality? Proposal timing? Closing discipline? Each gets a different coaching approach. Shows business maturity.

### 📊 Storytelling Discipline
Three pages in intentional order: diagnosis → drill-down → context. Not just "here are all the charts." Shows you understand how to lead someone through an insight.

### 🎯 Specificity Over Generics
Real numbers. Real rep names. Real conversion gaps. "Ahmad at 16.7% vs Chen at 38.5%" is way more credible than "some reps close better."

### 🚫 Calls Out What You *Don't* Know
"30 cases stuck at initiation — is it client readiness, process bottleneck, or something else?" Shows intellectual honesty. Impresses interviewers more than false confidence.

---

## 🚀 Next Steps / Extensions

- **Predictive:** Flag leads likely to stall based on time-in-stage (e.g., "stuck in Proposal > 14 days")
- **Temporal:** Track if coaching actually worked — did closing rates improve?
- **Deal Size:** Do larger deals stall more often? Different patterns?
- **Rep Segmentation:** Group reps by skill gap, deliver targeted training per group
- **Proposal Lag:** Measure days from Qualified → Proposal (is it a process speed issue?)

---

## 📚 Tech Stack

- **Data Model:** Progression tracking (each lead = multiple records)
- **ETL:** Python (if synthetic data) + Power Query (transformations)
- **Visualization:** Power BI Desktop + Power BI Service
- **Metrics:** Conversion rates, funnel drop-off, per-rep stage progression

---

## 🤝 How to Use This Project

1. **As a portfolio piece:** Show this README + live Power BI dashboard during interviews
2. **As a coaching tool:** Run this for your actual sales team (modify rep names/numbers)
3. **As a template:** Use the progression model for *any* multi-stage pipeline (hiring, customer onboarding, support tickets)

---

**Last note:** The real skill here isn't the Power BI — it's the *data thinking*. The progression model is what makes this work. Everything else follows from that.
