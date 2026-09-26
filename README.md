# Power BI Data Modeling Project

A guided Power BI data modeling project based on [Baraa Khatib Salkini's Nightmare Data Model tutorial](https://www.youtube.com/watch?v=0A2k62YEbfI). I used the supplied messy Excel data to practice organizing a business model for analysis.

## What I did

- Worked with an Excel workbook containing 23 source sheets covering customers, products, orders, invoices, payments, inventory, campaigns, and other business data.
- Built a Power BI model with dimension tables such as `dim_customer`, `dim_product`, and `dim_date`, alongside fact tables such as `fact_sales`, `fact_inventory`, and `fact_sales_targets`.
- Added measures for total sales and total orders.
- Created two report pages with tables and summary cards that use the model to explore sales, targets, inventory, dates, and customer regions.

## What I learned

- How to identify dimensions and facts when source data is spread across many tables.
- Why a clear model and date dimension make analysis easier to build and maintain.
- How to use measures and report visuals to check and present results from the model.
- Why data modeling deserves attention before building a polished dashboard.

## Files

| File | Description |
| --- | --- |
| [`dataset.xlsx`](dataset.xlsx) | Excel source workbook used for the project. |
| [`project_datamodel.pbix`](project_datamodel.pbix) | Power BI Desktop model and report. |

## Open the project

1. Download or clone this repository.
2. Open `project_datamodel.pbix` in Power BI Desktop.
3. If Power BI asks for a missing data source during refresh, point the Excel source to the local `dataset.xlsx` file.

## Credit

This is a learning project completed while following [Baraa Khatib Salkini's YouTube tutorial](https://www.youtube.com/watch?v=0A2k62YEbfI). The tutorial and original dataset concept are his; this repository documents my practice work.
