# Sales Analysis Capstone Project

A capstone project using **MySQL** and **Tableau** to explore sales, costs, profit, and purchasing activity across regions and product categories.

## Project Overview

The project combines a CSV dataset, SQL queries, and Tableau worksheets to examine:

- Sales performance across East, North, South, and West regions.
- Sales differences between product categories.
- Customer purchasing quantities and sales values.
- Order-level sales, costs, and profitability.

## Tools

- **MySQL:** stores and retrieves the sales records.
- **MySQL Workbench or another SQL client:** imports the CSV and runs the queries.
- **Tableau Desktop:** connects to MySQL and displays the worksheets.
- **CSV:** provides the source data.

## Files

| File | Purpose |
| --- | --- |
| `Capstone Project (1)(1).csv` | Source dataset with 10 records and 11 columns. |
| `Capstone Project SQL.sql` | Retrieves all records from the capstone table. |
| `Capstone Project SQL Query 1.sql` | Contains the same full-table query as the preceding script. |
| `MySql Capstone Project (3).sql` | Sorts records by region descending and returns five rows. |
| `Tableu Capstone Project Bar Chart Region.twb` | Displays total sales by region. |
| `Tableu Capstone Project Line Chart.twb` | Uses line marks to compare total sales across product categories. |
| `Tableu Capstone Project Pie Chart.twb` | Colors slices by customer, sets slice angles by quantity, and sets mark size by total sales. |
| `Tableu Capstone Project Region Bar.twb` | Shows a detailed view by region, customer, order, product, and category with multiple measures. |
| `Tableu Capstone Project.twb` | Contains the same detailed worksheet configuration as the Region Bar workbook. |

The original filenames are preserved. Each Tableau workbook contains one worksheet named `Sheet 1`; no combined dashboard is included.

## Dataset

The CSV contains **10 unique orders**, **10 customers**, **4 regions**, and **9 product categories**. Order dates span **January 17–December 23, 2025**. Each row contains one product entry for an order.

| Column | Description |
| --- | --- |
| `Order ID` | Order identifier. |
| `Order Date` | Order date, supplied in month/day/year format. |
| `Customer Name` | Customer associated with the order. |
| `Region` | East, North, South, or West. |
| `Product Category` | Product grouping. |
| `Product Name` | Product purchased. |
| `Quantity` | Units purchased. |
| `Unit Price` | Sales price per unit. |
| `Total Sales` | Total sales value for the row. |
| `Total Cost` | Total cost for the row. |
| `Profit` | Total sales minus total cost. |

The provided rows satisfy:

```text
Total Sales = Quantity × Unit Price
Profit = Total Sales − Total Cost
Profit Margin = Profit ÷ Total Sales × 100
```

The source does not specify a currency, so monetary values below are shown without a currency symbol.

## Results from the CSV

| Metric | Value |
| --- | ---: |
| Orders | 10 |
| Units sold | 38 |
| Total sales | 4,120 |
| Total cost | 3,732 |
| Total profit | 388 |
| Overall profit margin | 9.42% |

### Regional Performance

| Region | Total Sales | Profit |
| --- | ---: | ---: |
| East | 2,300 | 283 |
| North | 830 | 55 |
| South | 650 | 22 |
| West | 340 | 28 |

- **East** generates the highest sales and profit, accounting for **55.83% of total sales**.
- **Electronics** produces the highest category sales at **1,500**, across two orders.
- The **Play Station 5** order produces the highest individual-order profit at **250**, or **64.43% of total profit**.

These figures were calculated directly from the supplied CSV. The dataset is small, and its provenance is not documented; the results describe these records and do not establish broader market trends or seasonality.

## SQL Queries

Both `Capstone Project SQL.sql` and `Capstone Project SQL Query 1.sql` contain:

```sql
SELECT * FROM project.`capstone project`
```

`MySql Capstone Project (3).sql` contains:

```sql
SELECT * FROM project.`capstone project`
ORDER BY Region DESC
LIMIT 5;
```

The second query sorts by the **region name**, not by sales or profit. Rows within the same region have no specified secondary order, so the five-row result is not a deterministic ranking of orders.

## How to Run

### 1. Set Up MySQL

Install and start MySQL, then create the database if it does not already exist:

```sql
CREATE DATABASE IF NOT EXISTS project;
```

Using MySQL Workbench's Table Data Import Wizard or an equivalent import tool, import `Capstone Project (1)(1).csv` into the `project` database with the table name **`capstone project`**.

Preserve the CSV column names. Use integer types for identifiers and quantity, text types for descriptive fields, and decimal types for monetary fields. Parse `Order Date` as month/day/year and store it as a date where possible. Ignore the trailing blank line in the CSV.

The supplied SQL files contain retrieval queries only; they do not create the database or table or load the data.

### 2. Run the SQL Scripts

Open the `.sql` files in your SQL client and execute them against your MySQL instance. Confirm that the full-table query returns the 10 source records.

### 3. Open the Tableau Workbooks

Open a `.twb` file in a compatible Tableau Desktop installation with MySQL connection support. Install the required MySQL driver if prompted.

The saved workbooks reference a local MySQL server at **`localhost:3306`**, with the saved username **`root`** and connections to the `project` and `mysql` databases. Edit the relevant data-source connections to use your own host, credentials, and imported table, then refresh the worksheet.

These are `.twb` workbook definitions, rather than packaged `.twbx` workbooks. The CSV is supplied separately; a working data connection must be configured to reproduce the views.

## Visualization Notes

- **Regional sales chart:** compares the sum of total sales across regions.
- **Category line chart:** connects category sales values with line marks. Its saved axes contain product category and total sales, so it does not show sales over time.
- **Customer pie chart:** uses quantity for slice angles and total sales for mark size. It should be interpreted as a quantity-based customer breakdown, not a sales-share pie chart.
- **Detailed workbooks:** display profit, quantity, total cost, total sales, and unit price across order details. Summed unit prices should not be interpreted as revenue.

## Skills Demonstrated

- Retrieving records with SQL.
- Sorting and limiting SQL query results.
- Connecting Tableau to MySQL.
- Comparing regional and product-category sales.
- Exploring order-level profitability and customer purchasing activity.

## Potential Improvements

- Combine the worksheets into one dashboard with region, category, and date filters.
- Add a date-based sales trend chart.
- Use total sales for pie slice angles if the goal is to display sales share.
- Add SQL aggregations for regional sales, category sales, and profit margins.
- Include a table-creation and data-import script for easier reproduction.
- Document the dataset source and expand the number of records before drawing broader business conclusions.
