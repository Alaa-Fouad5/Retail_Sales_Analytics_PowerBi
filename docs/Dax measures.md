# DAX Measures Documentation (`_Key_Measures`)

This document details all business logic calculations built into the **`_Key_Measures`** table for the Retail Analytics Power BI project.

---

## 1. Core Financial & Volume Metrics

### Total Revenue
Calculates the total gross revenue generated from sales transactions.
```dax
Total_Revenue = SUM( Fact_Sales[Revenue] )
```

### Total Cost
Calculates the total Cost of Goods Sold (COGS).
```dax
Total_Cost = SUM( Fact_Sales[Cost] )
```

### Total Profit
Calculates net sales profit by subtracting total costs from total revenue.
```dax
Total_Profit = [Total_Revenue] - [Total_Cost]
```

### Profit Margin (%)
Evaluates profitability efficiency as a percentage of total revenue.
```dax
Profit Margin (%) = 
DIVIDE(
    [Total_Profit],
    [Total_Revenue],
    0
)
```

---

## 2. Order & Sales Volume Metrics

### Total Orders
Counts the unique number of sales transactions across all channels.
```dax
Total Orders = DISTINCTCOUNT( Fact_Sales[Invoice_ID] )
```

### Total Units Sold
Calculates the total quantity of products sold.
```dax
Total Units Sold = SUM( Fact_Sales[Quantity] )
```

### Sales PM (Previous Month Revenue)
Retrieves the total revenue from the previous calendar month for period-over-period comparisons.
```dax
Sales PM = 
CALCULATE(
    [Total_Revenue],
    DATEADD( 'Dim_Calender'[Date], -1, MONTH )
)
```

### MOM Sales Growth (%)
Measures the percentage month-over-month growth in revenue.
```dax
MOM Sales Growth (%) = 
VAR CurrentSales = [Total_Revenue]
VAR PreviousSales = [Sales PM]
RETURN
    DIVIDE(
        CurrentSales - PreviousSales,
        PreviousSales,
        0
    )
```

---

## 3. Basket Dynamics & Store Efficiency

### Average Order Value (AOV)
Measures the average monetary value generated per sales invoice.
```dax
Average Order Value (AOV) = 
DIVIDE(
    [Total_Revenue],
    [Total Orders],
    0
)
```

### Units Per Transaction (UPT)
Measures the average number of product items purchased per invoice.
```dax
Units Per Transaction (UPT) = 
DIVIDE(
    [Total Units Sold],
    [Total Orders],
    0
)
```

### Cross Selling Score
Evaluates store cross-selling effectiveness based on multi-item invoice proportions.
```dax
Cross Selling Score = 
DIVIDE(
    [Orders Bought Together],
    [Total Orders],
    0
)
```

### Orders Bought Together
Counts the total invoices containing more than 1 distinct item line.
```dax
Orders Bought Together = 
CALCULATE(
    [Total Orders],
    FILTER(
        VALUES( Fact_Sales[Invoice_ID] ),
        CALCULATE( COUNT( Fact_Sales[Product_ID] ) ) > 1
    )
)
```

---

## 4. Returns & Customer Behavior

### N_of_Transactions_Return
Counts the total number of transactions that resulted in a product return.
```dax
N_of_Transactions_Return = 
CALCULATE(
    [Total Orders],
    Fact_Sales[Is_Return] = TRUE()
)
```

### Return (%)
Calculates the return rate as a proportion of total completed transactions.
```dax
Return (%) = 
DIVIDE(
    [N_of_Transactions_Return],
    [Total Orders],
    0
)
```