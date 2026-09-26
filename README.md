# Power BI Data Modeling: The Nightmare Data Model

This project turns a 23-sheet Excel dataset into a structured Power BI model for analyzing sales, inventory, campaigns, order processing, and targets. I focused on understanding the source data, separating business entities from transactions, and making the results easier to validate.

The main deliverable is the data model in [`project_datamodel.pbix`](project_datamodel.pbix). Its two report pages check totals and filters. This project strengthened my ability to understand source data, define business entities and events, and verify that the resulting numbers make sense.

## The starting problem

The [`dataset.xlsx`](dataset.xlsx) workbook contains 23 sheets. It resembles a raw export from several business systems, with related information split across multiple places:

| Business area | Examples from the source workbook | Modeling question |
| --- | --- | --- |
| Customers | `CUST_MASTER`, `customer_contacts`, `Address`, `user_details` | Which attributes belong in one customer dimension, and which records should be kept? |
| Orders and sales | `ORDERS_2025`, `ORDERS_2026`, `order_line_items` | What does one row of the sales fact represent, and how do order headers relate to lines? |
| Products | `products`, `subcategories` | How can products be described consistently without duplicate matches? |
| Operations | `INVOICES`, `invoice_lines`, `payments`, `shipments` | How should order, invoice, payment, and delivery events be analyzed? |
| Marketing and planning | `CAMPAIGN_LOG`, `campaign_skus`, `sales_targets` | How can campaign activity and targets be analyzed beside sales? |

The source data includes test records and duplicate products, while its related fields are scattered across sheets. These issues matter because a report can look correct while its totals are inflated or its filters behave unexpectedly.

## What I built

I organized the Power BI model around business entities and events:

| Model area | Tables visible in my PBIX |
| --- | --- |
| Dimensions | `dim_customer`, `dim_product`, `dim_geo`, `dim_order_flags`, `dim_campaign`, `dim_date` |
| Facts | `fact_sales`, `fact_inventory`, `fact_campaign_spend`, `fact_promotion_coverage`, `fact_order_process`, `fact_sales_targets` |
| Supporting tables | `_measures`, `security` |

The **dimensions** describe who, what, where, and when. The **facts** represent business activity or targets. Keeping those roles separate makes the model easier to read and helps avoid ambiguous paths between facts. With several fact tables, the result is closer to a fact constellation than a single small star.

The PBIX also contains measures named `total_sales` and `total_orders`. Its two report pages include date-based tables for sales, inventory units, and targets, plus cards for total sales and total orders and a customer-region table. These visuals are useful for checking the model as it is built.

## Project workflow

1. **Explored the source.** Reviewed the 23 sheets to identify keys, repeated fields, and the meaning of each row before modeling relationships.
2. **Organized dimensions.** Created dedicated model tables for customers, products, geography, campaigns, order flags, and dates.
3. **Separated business events.** Represented sales, inventory, campaign spend, promotion coverage, order processing, and sales targets as distinct facts because they have different levels of detail.
4. **Added analytical checks.** Used the date dimension, core measures, and simple report visuals to compare values across time and keep important totals visible.
5. **Considered access and validation.** Included a `security` table in the model. The active role configuration should be checked in Power BI Desktop before claiming that row-level security is implemented.

## What I learned from the project

- **Explore before modeling.** I need to understand each table's meaning and level of detail before deciding how it joins to the rest of the model.
- **Choose the grain of each fact.** An order, an order line, an inventory record, and a campaign record describe different events. Treating them as interchangeable can duplicate values.
- **Create shared dimensions.** Customer, product, geography, campaign, and date tables give related facts a consistent way to be filtered. Directly connecting fact tables can create ambiguous results.
- **Validate the numbers while building.** A sales total in a simple visual provides a baseline to check after merges and relationship changes. Duplicate product matches can otherwise inflate results without being obvious.
- **Keep one useful source for each attribute.** Repeated IDs, hash keys, and unnecessary columns make the model harder to understand and maintain.
- **Treat security as something to test.** A security mapping table is only part of the solution; access rules need to be verified by viewing the report as the intended user.

The biggest lesson for me is that a trustworthy Power BI report starts with a trustworthy model. Clear table roles, known fact grains, and repeated checks of key totals are more valuable than adding visuals before the data is understood.

## How to explore the files

1. Open `project_datamodel.pbix` in Power BI Desktop.
2. Use **Model view** to inspect the dimension, fact, measure, and security tables.
3. Use **Report view** to inspect the two validation pages.
4. If a refresh cannot find the source workbook, update the Excel source path to your local copy of `dataset.xlsx`.
5. To review security, check **Manage roles** and **View as** in Power BI Desktop. The presence of the `security` table alone does not prove that a role is active.

## Data source credit

The Nightmare Data Model dataset and project scenario were created by [Baraa Khatib Salkini (Data with Baraa)](https://www.youtube.com/watch?v=0A2k62YEbfI). This repository contains my Power BI model built from that source material.
