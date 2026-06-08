# 🎯 Interview Questions — Global Superstore Power BI Project

These questions are commonly asked in Data Analyst interviews when discussing a Power BI dashboard project. Each question is tied to a real insight or decision from the Global Superstore dashboard.

---

## 🔷 Section 1: Power BI & Dashboard Design

**Q1. Walk me through your Power BI dashboard — what business problem does it solve?**

> The dashboard helps retail business stakeholders understand where profit is being made and lost across products, geographies, customer segments, and shipping channels. Instead of reading flat spreadsheets, decision-makers can filter by region, segment, or time to find specific opportunities and problem areas in seconds.

---

**Q2. What visuals did you use and why did you choose them?**

> I used a world map for geographic profit distribution (spatial patterns are best shown geographically), horizontal bar charts for city and category rankings (easy to compare and rank), and a dual-axis line + bar combo for the Segment × Ship Mode view (to show both volume and profitability on the same chart without two separate visuals).

---

**Q3. How did you handle slicers and cross-filtering in your report?**

> I used two slicers — one for Customer Segment (Consumer, Corporate, Home Office) and one for Region. All visuals are connected through Power BI's default cross-filter behaviour, so selecting a region automatically updates every chart on the page. I also verified that bi-directional filtering was only enabled where needed to avoid ambiguous filter propagation.

---

**Q4. What DAX measures did you create?**

> Key measures included:
> - `Total Sales = SUM(Orders[Sales])`
> - `Total Profit = SUM(Orders[Profit])`
> - `Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)`
> - `Total Quantity = SUM(Orders[Quantity])`
> These were used as the base KPIs across all visuals.

---

**Q5. What is the difference between a calculated column and a measure in Power BI?**

> A calculated column is computed row-by-row at data refresh time and stored in the model — it adds a new column to a table. A measure is computed on the fly at query time based on the current filter context. Measures are preferred for aggregations because they don't increase model size, while calculated columns are useful for row-level logic like bucketing or flags.

---

**Q6. What is filter context in DAX and how did it affect your measures?**

> Filter context is the set of filters currently active when a measure is evaluated — it comes from slicers, row/column headers in a matrix, or visual-level filters. For example, when a user selects "Consumer" in the segment slicer, `Total Profit` automatically recalculates only for Consumer rows. I used `CALCULATE()` to override or extend filter context where needed, such as calculating market share against total profit regardless of the active segment filter.

---

**Q7. How did you optimise your Power BI model for performance?**

> I removed unused columns during Power Query transformation, used integer keys for relationships instead of text, avoided calculated columns where measures could do the same job, and ensured the data model used a star schema structure — one fact table (Orders) connected to dimension tables — to keep DAX calculations efficient.

---

## 🔷 Section 2: Data Cleaning & Transformation

**Q8. What data cleaning steps did you perform on this dataset?**

> The dataset was generally clean but I checked for: null values in key columns (Sales, Profit, Order Date), duplicate Order IDs with the same product line, correct data types on date columns (important for time intelligence functions), and trimmed whitespace from string fields like City and Country using Power Query's `Text.Trim()`.

---

**Q9. How did you handle the date fields to enable time-based analysis?**

> I extracted Year, Month, and Week Number from the Order Date using Power Query's date functions. I also created a separate Date dimension table marked as a date table in Power BI, which enabled proper use of DAX time intelligence functions like `SAMEPERIODLASTYEAR` and `DATESYTD`.

---

**Q10. The dataset has a "Discount" column ranging from 0 to 1. How did you use this in your analysis?**

> I created a calculated column bucketing discounts into bands: No Discount (0), Low (0–20%), Mid (20–40%), and High (40%+). This allowed me to group transactions and compare average profit per band — which revealed a critical insight: orders with discounts above 40% averaged negative profit (-$90 per order), while zero-discount orders averaged +$61.

---

## 🔷 Section 3: Data-Driven Insights & Business Thinking

**Q11. What was the most surprising insight you found in this dataset?**

> The Tables sub-category was the only sub-category with a negative total profit (-$64,083) across four years of data. Despite being part of the Furniture category which had $4.1M in sales, Tables consistently lost money — likely due to high discounting combined with expensive shipping. That's a product line that looks busy on the surface but is actively destroying margin.

---

**Q12. Furniture has $4.1M in sales but a 6.9% margin. What would you recommend?**

> I'd recommend three actions: (1) review the discount policy on Furniture — our data shows high discounts correlate with negative profit; (2) audit shipping costs since large furniture items carry disproportionate shipping costs; and (3) consider deprioritising the Tables sub-category specifically, which is the only loss-making product group in the entire dataset.

---

**Q13. APAC is the most profitable market. How would you use this insight?**

> APAC generating $436K profit — more than North America and EU individually — suggests it should receive increased marketing and inventory investment. I'd also want to drill down into which APAC countries and cities are driving this: are a few cities responsible (similar to NYC in North America), or is it broadly distributed? That changes the expansion strategy significantly.

---

**Q14. New York City generates double the profit of the next city. Is that a good thing?**

> It's both a strength and a risk. It's a strength because it validates market fit in one high-value location. It's a risk because concentration in a single city makes the business vulnerable — economic downturns, local competition, or supply chain issues in NYC could have an outsized impact on overall performance. I'd recommend both deepening NYC investment and actively developing the next tier of cities (LA, Seattle, San Francisco) to reduce concentration.

---

**Q15. The Consumer segment has the highest profit. Should the business focus purely on Consumers?**

> Not necessarily. Corporate customers, while fewer in number, have higher average order values and transact with less discounting. Home Office has the highest margin percentage (12%) of all three segments. A diversified segment strategy — growing Corporate transaction volume and protecting Home Office margin — is safer than over-indexing on Consumer volume, which is more price-sensitive and discount-driven.

---

**Q16. Standard Class shipping dominates. Should the company cut First Class and Same Day options?**

> I wouldn't recommend cutting them. While Standard Class carries most revenue, Same Day and First Class serve customers with urgent or high-value needs — removing them could lose Corporate and Home Office customers who value speed. The margin difference is also small (11.8% vs 11.4%), so these modes aren't losing money. The right move is to ensure Same Day isn't being used for low-value orders where the cost isn't justified.

---

**Q17. How would you explain the discount-to-profit relationship to a non-technical stakeholder?**

> "Think of it this way: when we give no discount, we make about $61 on average per order. When we give more than 40% off, we actually lose $90 per order on average. So we're not just making less money — we're paying customers to buy from us. Every order above 40% discount costs us money. We need a discount cap policy."

---

## 🔷 Section 4: SQL & Analytical Thinking

**Q18. Write a SQL query to find the top 5 most profitable cities.**

```sql
SELECT
    City,
    ROUND(SUM(Profit), 2) AS Total_Profit
FROM orders
GROUP BY City
ORDER BY Total_Profit DESC
LIMIT 5;
```

---

**Q19. Write a SQL query to find sub-categories with negative total profit.**

```sql
SELECT
    Sub_Category,
    ROUND(SUM(Profit), 2) AS Total_Profit
FROM orders
GROUP BY Sub_Category
HAVING SUM(Profit) < 0
ORDER BY Total_Profit ASC;
```

---

**Q20. How would you calculate profit margin by category in SQL?**

```sql
SELECT
    Category,
    ROUND(SUM(Sales), 2)                          AS Total_Sales,
    ROUND(SUM(Profit), 2)                         AS Total_Profit,
    ROUND(SUM(Profit) / NULLIF(SUM(Sales), 0) * 100, 2) AS Profit_Margin_Pct
FROM orders
GROUP BY Category
ORDER BY Profit_Margin_Pct DESC;
```

---

**Q21. Write a query to find the average profit per order by discount bucket.**

```sql
SELECT
    CASE
        WHEN Discount = 0        THEN 'No Discount'
        WHEN Discount <= 0.2     THEN 'Low (0-20%)'
        WHEN Discount <= 0.4     THEN 'Mid (20-40%)'
        ELSE                          'High (40%+)'
    END AS Discount_Band,
    COUNT(*)                        AS Order_Count,
    ROUND(AVG(Profit), 2)           AS Avg_Profit
FROM orders
GROUP BY Discount_Band
ORDER BY Avg_Profit DESC;
```

---

**Q22. How would you identify customers who are always ordering with high discounts?**

```sql
SELECT
    Customer_ID,
    Customer_Name,
    COUNT(*)                    AS Total_Orders,
    ROUND(AVG(Discount), 2)     AS Avg_Discount,
    ROUND(SUM(Profit), 2)       AS Total_Profit
FROM orders
GROUP BY Customer_ID, Customer_Name
HAVING AVG(Discount) > 0.4
ORDER BY Total_Profit ASC;
```

---

## 🔷 Section 5: Behavioural / Situational

**Q23. How did you decide which KPIs to put on the dashboard?**

> I started by asking: what decisions would someone make using this dashboard? The primary decisions are about where to sell more (geography, segment), what to sell more of (category, sub-category), and how to fulfil orders (ship mode). That led to four core KPIs — Sales, Profit, Margin, and Quantity — and visuals that slice each one by the relevant dimensions.

---

**Q24. If a stakeholder asked you why profit is low in EMEA, how would you investigate?**

> I'd drill down in three steps: (1) check if low profit is caused by low sales volume or poor margin — EMEA has $806K in sales but only $44K profit, suggesting a margin issue not a volume issue; (2) look at discount rates in EMEA vs. other markets — are EMEA orders being over-discounted?; (3) examine shipping costs, since EMEA may have high cross-border logistics costs eating into margin.

---

**Q25. Your dashboard shows Tables as loss-making. A sales manager says "but we sell a lot of tables." How do you respond?**

> "You're right that Tables have strong order volume — and that's exactly why this matters. A product that's frequently ordered but always sold below its true cost is a hidden drain. We're not just missing out on profit — we're actively subsidising those sales. High volume at negative margin scales the loss, not the gain. The fix isn't to stop selling Tables; it's to fix the pricing and discount structure so each sale contributes positively."

---

**Q26. How would you validate the accuracy of your dashboard numbers?**

> I'd validate in three ways: (1) aggregate totals — cross-check Total Sales and Profit against raw data using a simple Excel pivot or SQL query; (2) spot-check individual records against the source file to confirm no transformation errors in Power Query; (3) compare year-over-year totals with any existing reports from the business to confirm alignment. I'd also add a "last refreshed" timestamp to the dashboard so users know when the data was last updated.

---

**Q27. What would you add to this dashboard if you had more time?**

> I'd add: (1) a Year-over-Year trend line to show whether the business is growing or declining; (2) a Returns analysis if return data were available — high-discount orders likely have high return rates too; (3) a customer RFM (Recency, Frequency, Monetary) segmentation to identify the top 20% of customers driving 80% of profit; and (4) a forecast visual using Power BI's built-in analytics pane to project next quarter's sales by segment.

---

**Q28. How is this project relevant to a real business analyst role?**

> It demonstrates the full analyst workflow: understanding a business dataset, cleaning and modelling it, building meaningful visuals, and — most importantly — translating numbers into decisions. Identifying that Tables is loss-making, that heavy discounting destroys margin, and that APAC is the growth story are the kinds of insights that change budget allocation, pricing policy, and market expansion strategy in a real business.

---

## 🔷 Bonus: Quick-Fire Concepts

| Question | Answer |
|---|---|
| What is a star schema? | A fact table (e.g. Orders) surrounded by dimension tables (Date, Customer, Product, Region). Optimised for analytical queries. |
| What is cardinality in Power BI? | The uniqueness of values in a relationship column — One-to-Many is most common in star schemas. |
| What does CALCULATE() do in DAX? | Evaluates an expression in a modified filter context — the most powerful and commonly used DAX function. |
| What is the difference between SUM and SUMX? | SUM aggregates a column directly. SUMX iterates row by row and applies an expression first — used for calculated aggregations like revenue = price × quantity. |
| What is RLS in Power BI? | Row-Level Security — restricts data access per user role. E.g. a regional manager only sees their region's data. |
| What is the DIVIDE() function used for? | Safe division in DAX that returns a specified alternate value (default 0) instead of an error when the denominator is zero. |

---

*Good luck with your interview! The best answers combine technical accuracy with clear business thinking — show that you understand not just how to build the dashboard, but why it matters.*
