# Power BI Data Modeling: The Nightmare Data Model

This is my guided Power BI data modeling project, completed while following [Data with Baraa's *Power BI Data Modeling Portfolio Project End-to-End (Nightmare Data Model)*](https://www.youtube.com/watch?v=0A2k62YEbfI). The exercise starts with 23 messy Excel tables and focuses on turning scattered business data into a model that can support reliable analysis.

The main deliverable is the data model in [`project_datamodel.pbix`](project_datamodel.pbix). The report pages are simple checks of the model, rather than a finished dashboard.

## The starting problem

The [`dataset.xlsx`](dataset.xlsx) workbook contains 23 sheets. Customer details are spread across master, contact, address, and user tables; orders are split by year; sales lines, invoices, payments, shipments, inventory, campaigns, and targets live in separate structures. The tutorial also calls out test records, duplicate products, and confusing relationships as reasons to inspect the data before connecting tables.

## What I built

I organized the Power BI model around business entities and events:

| Model area | Tables visible in my PBIX |
| --- | --- |
| Dimensions | `dim_customer`, `dim_product`, `dim_geo`, `dim_order_flags`, `dim_campaign`, `dim_date` |
| Facts | `fact_sales`, `fact_inventory`, `fact_campaign_spend`, `fact_promotion_coverage`, `fact_order_process`, `fact_sales_targets` |
| Supporting tables | `_measures`, `security` |

The model separates descriptive tables from sales, inventory, campaign, order-process, and target data. My PBIX also contains measures named `total_sales` and `total_orders` and two report pages. The pages include date-based tables for sales, inventory units, and targets, plus cards for total sales and total orders and a customer-region table.

## What I learned from the project

- **Explore before modeling.** I need to understand each table's meaning and level of detail before deciding how it joins to the rest of the model.
- **Choose the grain of each fact.** An order, an order line, an inventory record, and a campaign record describe different events. Treating them as interchangeable can duplicate values.
- **Create shared dimensions.** Customer, product, geography, campaign, and date tables give related facts a consistent way to be filtered. The tutorial explains why directly connecting fact tables creates ambiguous results.
- **Validate the numbers while building.** A sales total in a simple visual provides a baseline to check after merges and relationship changes. Duplicate product matches can otherwise inflate results without being obvious.
- **Keep one useful source for each attribute.** Repeated IDs, hash keys, and unnecessary columns make the model harder to understand and maintain.
- **Treat security as something to test.** The tutorial's final section shows row-level security and checks the result by viewing the report as a regional user.

## How to explore the files

1. Open `project_datamodel.pbix` in Power BI Desktop.
2. Use **Model view** to inspect the dimension, fact, measure, and security tables.
3. Use **Report view** to inspect the two validation pages.
4. If a refresh cannot find the source workbook, update the Excel source path to your local copy of `dataset.xlsx`.

## Tutorial credit

This is practice work based on [Baraa Khatib Salkini's video](https://www.youtube.com/watch?v=0A2k62YEbfI), not an original dataset or course. The video's chapters cover [source exploration](https://www.youtube.com/watch?v=0A2k62YEbfI&t=418s), [customer and product dimensions](https://www.youtube.com/watch?v=0A2k62YEbfI&t=1149s), [fact modeling](https://www.youtube.com/watch?v=0A2k62YEbfI&t=3491s), [date table and measures](https://www.youtube.com/watch?v=0A2k62YEbfI&t=7067s), and [row-level security and final validation](https://www.youtube.com/watch?v=0A2k62YEbfI&t=8246s). The creator also explains the modeling principles in [his project write-up](https://www.blog.datawithbaraa.com/p/the-nightmare-data-model-project).
