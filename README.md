# SQL-Assignment-Witle
This project uses SQL to analyse the Sizwe Coffee dataset and answer eight business questions for the company's year-end review. Sizwe Coffee is a South African coffee roastery and wholesale supplier based in Isando, Johannesburg, with a second distribution centre in Epping, Cape Town.It serves approximately 1,400 business customers through Wholesale and Subscription channels.

The analysis supports business decisions about revenue, product profitability, invoice collections, customer accounts, trade promotions, sales representative performance and monthly revenue trends.

## Business questions

1. How did revenue by channel change from FY2024 to FY2025?
2. Which product lines generate the most gross profit, and which have the highest gross margins?
3. How do invoice settlement and outstanding balances compare between channels?
4. Which ten customers generated the most revenue in FY2025?
5. Which high-revenue Wholesale customers have never received a trade promotion?
6. Are sales representatives meeting their monthly revenue targets?
7. What does monthly revenue show about seasonality and the quietest month?
8. Which product-line changes help explain the decrease in overall gross margin from FY2024 to FY2025?

## Dataset

The dataset covers 1 July 2023 to 30 June 2025. Sizwe Coffee's financial year runs from 1 July to 30 June.

| Table | Description |
|---|---|
| `workspace.default.sizwe_customers` | Customer details, including trading name, channel, segment, province and assigned representative |
| `workspace.default.sizwe_products` | Product SKU, product line, pack size, list price and unit cost |
| `workspace.default.sizwe_sales_orders` | Order details, including customer, date, channel and sales representative |
| `workspace.default.sizwe_sales_lines` | Order-line details, including SKU, revenue and cost of goods |
| `workspace.default.sizwe_ar_ledger` | Invoice number, customer, invoice date, due date, invoice amount, amount settled and settlement date |
| `workspace.default.sizwe_reps` | Sales representative details, territory and monthly target |
| `workspace.default.sizwe_rep_visits` | Sales representative visits and outcomes |
| `workspace.default.sizwe_trade_promotions` | Promotional support provided to customers and SKUs |
| `workspace.default.sizwe_vendors` | Supplier details, including supplier type and payment terms |

### Table relationships

- `sizwe_sales_orders.customer_id` connects to `sizwe_customers.customer_id`.
- `sizwe_sales_orders.order_id` connects to `sizwe_sales_lines.order_id`.
- `sizwe_sales_lines.sku` connects to `sizwe_products.sku`.
- `sizwe_sales_orders.rep_id` and `sizwe_customers.rep_id` connect to `sizwe_reps.rep_id`.
- `sizwe_ar_ledger.customer_id` connects to `sizwe_customers.customer_id`.
- `sizwe_rep_visits.customer_id` and `sizwe_trade_promotions.customer_id` connect to `sizwe_customers.customer_id`.

Revenue and cost of goods are stored in the sales-line table, so revenue calculations join orders to their sales lines. The accounts receivable ledger is linked to customers using `customer_id`; it uses `invoice_no` rather than `order_id` to identify invoices.

## SQL skills demonstrated

| SQL technique | Tasks | Purpose |
|---|---|---|
| `JOIN` and `LEFT JOIN` | 1–8, where relevant | Combine related tables while retaining required records |
| Aggregate functions (`SUM`, `COUNT`, `AVG`) | 1–8 | Calculate revenue, costs, invoice counts, averages and balances |
| `CASE` expressions | 1, 3, 8 | Apply conditional calculations and classify records |
| `GROUP BY` and `ORDER BY` | 1–8 | Aggregate results and sort them for interpretation |
| `NULLIF` and `COALESCE` | 1, 3, 6–8 | Handle zero denominators and missing values |
| `NOT EXISTS` | 5 | Identify customers with no matching trade-promotion record |
| Common table expressions (CTEs) | 6–8 | Break multi-step calculations into readable sections |
| Window functions (`LAG`, rolling `AVG`, `SUM OVER`) | 7–8 | Compare months, calculate rolling averages and calculate product-line revenue share |
| Monthly date sequence | 7 | Analyse revenue month by month across the two-year period |

## How to run

1. Open the project in Databricks SQL or the SQL environment supplied for the assignment.
2. Confirm that the tables are available under `workspace.default`.
3. Open `queries.sql`.
4. Run each task query separately and review the returned results.
5. Read the written-answer comments below Tasks 2, 3, 5, 7 and 8 alongside the query results.
6. Before submission, ensure the remaining figures for Tasks 1, 4 and 6 in the key insights section match the outputs from your own runs.

## Key business insights

- **Product profitability (Task 2):** House Blend generated the highest gross profit, approximately R107.15 million. Single Origin had the highest gross margin at 44.27%, so the product line with the highest profit was not the one with the highest margin.
- **Collections (Task 3):** Wholesale had 3,454 open invoices and R87,848,227.20 outstanding, compared with 44 open Subscription invoices and R751,178.89 outstanding. Average settlement time for settled invoices was 68.68 days for Wholesale and 3.85 days for Subscription. Wholesale should be investigated first.
- **Promotion gap (Task 5):** The highest-revenue Wholesale customers without a recorded promotion were Umhlanga Fresh 108 (about R6.22 million), Ridgeway Foods 308 (about R4.45 million) and Kalahari Kitchen 42 (about R4.45 million). They are potential candidates for targeted offers, after considering profitability and customer potential.
- **Monthly trends (Task 7):** December 2023 was the quietest month in the reported 24-month results, with revenue of approximately R29.87 million. Revenue declined by 13.09% month on month in December 2023 and by 12.89% in December 2024, suggesting a recurring year-end slowdown followed by a recovery early in the new year.
- **Gross margin movement (Task 8):** Overall gross margin fell from 34.7% in FY2024 to 33.0% in FY2025, a decrease of 1.7 percentage points, while revenue grew by nearly 9%. Bulk Commercial's share of revenue increased from 25.02% to 33.65%, while its gross margin remained low at about 19.9%. This shift in revenue mix is a plausible contributor to the overall margin decline.
- **Channel performance (Task 1):** Add the FY2024 and FY2025 revenue and growth percentages from the Task 1 output.
- **Top customers (Task 4):** Add the highest-revenue FY2025 customer and revenue from the Task 4 output.
- **Sales representative performance (Task 6):** Add the number of representatives meeting or exceeding target and the lowest-performing representative from the Task 6 output.

## Conclusion

The analysis shows that Sizwe Coffee should pay particular attention to Wholesale collections and understand how its changing product mix affects profitability. It also identifies high-revenue Wholesale customers without recorded promotions and a possible year-end slowdown in monthly revenue. The remaining conclusions should be completed using the actual outputs from Tasks 1, 4 and 6.
