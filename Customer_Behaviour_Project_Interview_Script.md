# Interview Script — Customer Shopping Behaviour & Segmentation Analytics
*Python | SQL | Statistical Testing | Dashboard (Feb–May 2026)*

A ready-to-speak walkthrough of this project, structured the way interviewers expect: **Problem → Approach → Insights → Business Impact → Recommendations**. Bracketed notes `[...]` are delivery tips, not part of the script.

---

## 1. The Business Problem
*(Open with this when asked "walk me through a project")*

> "I worked on a consumer behavior analytics project for a retail business with about 3,900 customer transactions. The core business question was: **how can the company use its existing shopping data to understand what actually drives revenue and customer loyalty** — so marketing and product teams stop guessing and start targeting the right customers, categories, and channels with their budget."

**Framing line to remember:** this wasn't just an EDA exercise — it was framed as answering *specific* stakeholder questions (who spends more, what drives loyalty, which products perform, when should we run campaigns) rather than open-ended exploration.

---

## 2. What I Did — My Approach
*(This is your technical walkthrough — show the pipeline, not just the tools)*

> "I ran this as an end-to-end pipeline. First, in **Python with Pandas**, I cleaned the raw dataset — imputed missing review ratings using the category median rather than a global average, so ratings stayed realistic per product type. I engineered new features: an age-group segmentation using quantile binning, and converted purchase-frequency labels like 'Weekly' or 'Quarterly' into numeric days-between-purchases so I could do real quantitative comparisons.
>
> Next, I moved into **SQL** to structure the data relationally and answer specific business questions — revenue share by category, top-rated products with a minimum review threshold for reliability, and customer segmentation into New / Returning / Loyal tiers based on purchase history.
>
> Then I applied **statistical hypothesis testing** using SciPy — t-tests, one-way ANOVA, and chi-square tests — plus **95% confidence intervals**, so my conclusions weren't just 'this number looks bigger,' they were statistically validated.
>
> Finally, I packaged everything into a **stakeholder-facing dashboard** — KPI cards, revenue breakdowns, segmentation visuals — and documented the whole project in a structured GitHub repo so it's reproducible."

**Tools to name if asked directly:** Python (Pandas, NumPy, Matplotlib, Seaborn), SciPy (stats module), SQL (PostgreSQL/SQLite), PowerPoint/Power BI-style dashboard, Git/GitHub.

---

## 3. Key Insights — What the Data Actually Showed
*(Lead with numbers. This section is your credibility builder — it shows you can read a p-value, not just a bar chart.)*

**Revenue & spend fundamentals**
- Total revenue across 3,900 customers: **$233,081**, average purchase **$59.76** (95% CI: $59.02–$60.51), average review rating **3.75 / 5**.
- Male customers generated **67.7% of revenue ($157,890)** vs. **32.3% for female customers ($75,191)** — but that's a *volume* effect, not a spend-per-customer effect.

**The nuance that matters (this is the strongest thing you can say in an interview):**
> "When I actually tested it statistically, average spend **per customer** was *not* significantly different between genders — the t-test gave p = 0.38, so I couldn't reject the null hypothesis. The revenue gap is driven by more male customers in the dataset, not higher individual spend. I made sure not to overstate that as a 'men spend more' insight — a common mistake — because the data didn't support it at the per-customer level."

**Seasonality — the one result that *was* statistically significant**
- One-way ANOVA across the four seasons: **F = 3.75, p = 0.0106** → reject H0. Purchase amount *does* vary meaningfully by season.
- Fall had the highest average spend (~$61.56), Summer the lowest (~$58.41).

**Subscribers vs. non-subscribers**
- Contrary to the common assumption, subscribers did **not** spend significantly more (one-tailed t-test, p = 0.67) — average spend was actually nearly identical (~$59.49 vs. ~$59.87). I flagged this so the business wouldn't over-invest in subscription perks expecting a spend lift that the data doesn't support.

**Gender and payment/discount behavior**
- Chi-square test showed gender and payment method preference are **statistically independent** (p = 0.43) — no evidence that checkout UX needs gender-based personalization.

**Segmentation & category performance**
- Customers split roughly **70% Loyal / 20% Returning / 10% New** based on purchase history — a strong, loyalty-heavy base.
- Footwear ($60.26 avg) and Clothing ($60.03 avg) led category spend; Outerwear lagged (~$57.17).
- Blouse, Pants, and Jewelry were the top 3 purchased items (171 units each).
- PayPal, Credit Card, and Cash were the top 3 payment methods, fairly evenly split — no single dominant channel.
- Highest-rated products (min. 10 reviews): Gloves (3.86), Sandals (3.84), Boots (3.82).
- Revenue by age group was fairly even (14.7%–18.6% per bracket), with the under-18 and 46–55 groups contributing the most.

---

## 4. How I Supported the Business — Turning Analysis into Action
*(This is the section that shows business acumen, not just technical skill — connect each insight to a decision.)*

> "My goal wasn't to hand over charts — it was to hand over decisions. For example:
>
> - Because **season, not gender or subscription status**, was the only statistically validated driver of spend, I redirected the framing away from demographic targeting and toward **seasonal campaign timing** — specifically building up marketing spend ahead of Fall, when basket size is naturally highest.
> - Since **70% of the customer base is already 'Loyal,'** I flagged that the growth lever isn't acquisition messaging — it's **retention and upsell** to an already-engaged base, and separately, **converting the 10% 'New' segment** before they churn.
> - Because subscription status showed **no real spend lift**, I recommended the business stop assuming subscribers are automatically higher-value and instead test *why* — e.g., is the subscription perk actually incentivizing bigger baskets, or just convenience?
> - Category and product-rating data gave merchandising a clear signal: **double down on Footwear and Clothing**, and investigate why Outerwear underperforms — price, sizing, or selection.
> - Since **payment method usage was broad and not gender-linked**, I recommended the business not over-invest in single-channel checkout optimization and instead keep multiple payment rails equally frictionless."

---

## 5. Recommendations
*(Deliver as a crisp, numbered list — this is what you'd literally hand to a stakeholder.)*

1. **Shift campaign calendars to lead into Fall**, the only season with a statistically confirmed spend increase.
2. **Prioritize retention programs for the Loyal segment (70% of customers)** rather than broad acquisition spend — tiered rewards for high-frequency buyers.
3. **Build a dedicated onboarding/conversion path for New customers (10%)** to move them into Returning before they drop off.
4. **Re-evaluate the subscription program's value proposition** — current data shows no measurable spend lift, so the perk may need redesigning.
5. **Expand Footwear and Clothing inventory/marketing** (top-performing categories) and audit Outerwear pricing or assortment.
6. **Maintain multi-channel payment support** rather than optimizing for one method, since usage is broad-based and not demographically driven.

---

## 6. Anticipated Follow-Up Questions (Prep for These)

**Q: "Why did you use the median instead of the mean to fill missing review ratings?"**
> "Review ratings can be skewed by a few very high or low reviews within a category, so the median is more robust to outliers than the mean — it gives a more realistic 'typical' rating to impute."

**Q: "Your resume says you validated spending patterns by gender — but you just said there was no significant difference. Isn't that a contradiction?"**
> "No — 'validating' a pattern statistically includes *ruling out* a pattern that looks true at first glance but isn't. The raw revenue split by gender looks dramatic (67.7% vs 32.3%), but I validated *whether that reflects individual spending behavior* — and it doesn't. Reporting that nuance is more valuable to the business than reporting the surface-level number, because it stops them from building a strategy on a false assumption."

**Q: "How would you productionize this if it were a live business, not a one-time analysis?"**
> "I'd move the pipeline from notebook-based Pandas work into scheduled SQL transformations or a lightweight ETL job, connect the dashboard to a live/refreshing data source instead of a static CSV, and re-run the hypothesis tests periodically to catch when a pattern like the seasonal effect shifts over time."

**Q: "What would you do differently if you had more time or more data?"**
> "I'd want more granular data — actual timestamps instead of frequency labels, and a longer time horizon — to test seasonality more rigorously and to build a proper cohort-based retention analysis instead of a static New/Returning/Loyal split based on purchase-count thresholds."

---

*Tip: Keep sections 1–3 tight (60–90 seconds each) for a general "tell me about a project" prompt, and use sections 4–6 only when the interviewer digs deeper.*
