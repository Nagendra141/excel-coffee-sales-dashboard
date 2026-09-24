# Formulas Used

All formulas are in the orders sheet, row 2, and copied down to row 1001.

## Customer details (XLOOKUP)

Customer Name:
```
=XLOOKUP(C2, customers!$A$1:$A$1001, customers!$B$1:$B$1001,, 0)
```

Email (blank instead of 0 when the customer has no email):
```
=IF(XLOOKUP(C2, customers!$A$1:$A$1001, customers!$C$1:$C$1001,, 0) = 0, "",
    XLOOKUP(C2, customers!$A$1:$A$1001, customers!$C$1:$C$1001,, 0))
```

Country:
```
=XLOOKUP(C2, customers!$A$1:$A$1001, customers!$G$1:$G$1001,, 0)
```

## Product details (INDEX + MATCH, one formula for four columns)

Used for Coffee Type, Roast Type, Size and Unit Price:
```
=INDEX(products!$A$1:$G$49,
       MATCH(orders!$D2, products!$A$1:$A$49, 0),
       MATCH(orders!I$1, products!$A$1:$G$1, 0))
```
The row MATCH finds the product. The column MATCH reads the header of the current column, so the same formula returns a different field in each column. The `$D2` and `I$1` anchoring is what makes it copy correctly both across and down.

## Sales

```
=L2 * E2
```
Unit Price x Quantity.

## Readable labels (nested IF)

Coffee Type Name:
```
=IF(I2="Rob","Robusta", IF(I2="Exc","Excelsa", IF(I2="Ara","Arabica", IF(I2="Lib","Liberica",""))))
```

Roast Type Name:
```
=IF(J2="M","Medium", IF(J2="L","Light", IF(J2="D","Dark","")))
```

## Loyalty Card (structured reference inside the Orders table)

```
=XLOOKUP(Orders[[#This Row],[Customer ID]], customers!$A$2:$A$1001, customers!$I$2:$I$1001)
```

## Pivot tables and dashboard

| Pivot sheet | Rows | Columns | Values | Chart |
|---|---|---|---|---|
| Total Sales | Year, Month of Order Date | Coffee Type Name | Sum of Sales | Line chart |
| Country Bar Chart | Country | | Sum of Sales | Bar chart |
| Top 5 Customers | Customer Name (Top 5 filter) | | Sum of Sales | Bar chart |

Filters connected to all three pivots: Order Date timeline, and slicers for Roast Type Name, Size and Loyalty Card.
