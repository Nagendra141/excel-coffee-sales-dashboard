# Data Dictionary

Source: Mo Chen, [excel-project-coffee-sales](https://github.com/mochen862/excel-project-coffee-sales). Three sheets in `data/coffeeOrdersData_raw.xlsx`.

## orders (1,000 rows)

Each row is one product line within an order. An order with two products appears twice, which is why there are 1,000 rows but only 957 unique Order IDs.

| Column | Type | Description |
|---|---|---|
| Order ID | Text | Order reference, e.g. QEV-37451-860 |
| Order Date | Date | 2 Jan 2019 to 19 Aug 2022 |
| Customer ID | Text | Links to customers sheet |
| Product ID | Text | Links to products sheet, e.g. R-M-1 = Robusta, Medium roast, 1 kg |
| Quantity | Whole number | Units bought, 1 to 6 |

Columns I added with formulas: Customer Name, Email, Country, Coffee Type, Roast Type, Size, Unit Price, Sales, Coffee Type Name, Roast Type Name, Loyalty Card. See [formulas.md](formulas.md).

## customers (1,000 rows)

| Column | Type | Description |
|---|---|---|
| Customer ID | Text | Unique key |
| Customer Name | Text | Full name |
| Email | Text | Missing for 204 customers |
| Phone Number | Text | Missing for 130 customers |
| Address Line 1 | Text | Street address |
| City | Text | 386 different cities |
| Country | Text | United States, Ireland or United Kingdom |
| Postcode | Text | Postal or ZIP code |
| Loyalty Card | Text | Yes or No |

## products (48 rows)

| Column | Type | Description |
|---|---|---|
| Product ID | Text | Unique key |
| Coffee Type | Text | Ara (Arabica), Exc (Excelsa), Lib (Liberica), Rob (Robusta) |
| Roast Type | Text | L (Light), M (Medium), D (Dark) |
| Size | Number | Pack size in kg: 0.2, 0.5, 1 or 2.5 |
| Unit Price | Currency (USD) | Price per pack, about $2.69 to $36.46 |
| Price per 100g | Currency (USD) | Unit Price divided by size in 100 g units |
| Profit | Currency (USD) | Profit per pack |

## Data quality notes

- No missing values in orders or products.
- Missing emails come back from XLOOKUP as 0, so the Email formula converts them to blank.
- Every Customer ID and Product ID in orders has a match, so no lookup returns #N/A.
