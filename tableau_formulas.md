# Tableau Formula Reference

All parameters and calculated fields used in the **Sales Performance Dashboard** (Sample Superstore dataset). Formulas are taken directly from `Sales_Performance_Dashboard.twb`.

## Parameters

| Parameter | Data type | Allowable values | Initial value |
|-----------|-----------|------------------|---------------|
| Primary Region | String | List: Central, East, South, West | Central |
| Secondary Region | String | List: Central, East, South, West | East |

## Region selection fields

These Boolean fields return `TRUE` for rows in the region chosen in the matching parameter. Every other measure uses them as a filter inside `IF ... THEN ... END`.

**Primary Region**
```
[Region] = [Parameters].[Primary Region]
```

**Secondary Region**
```
[Region] = [Parameters].[Secondary Region]
```

## Total sales and sales comparison

**Primary Total Sales** (also used as **Primary Sales** and **Primary Sales Trend**)
```
SUM(
    IF [Primary Region] THEN [Sales]
    END
)
```

**Secondary Total Sales** (also used as **Secondary Sales** and **Secondary Sales Trend**)
```
SUM(
    IF [Secondary Region] THEN [Sales]
    END
)
```

The Sales Trend measures are plotted against **Order Date** at the month level to show monthly sales for each region.

## Average sales per order

**Primary Average Sales per Order**
```
SUM(
    IF [Primary Region] THEN [Sales]
    END
)
/
COUNTD(
    IF [Primary Region] THEN [Order ID]
    END
)
```

**Secondary Average Sales per Order**
```
SUM(
    IF [Secondary Region] THEN [Sales]
    END
)
/
COUNTD(
    IF [Secondary Region] THEN [Order ID]
    END
)
```

## Counts

**Primary No. of Customers**
```
COUNTD(
    IF [Primary Region] THEN [Customer ID]
    END
)
```

**Secondary No. of Customers**
```
COUNTD(
    IF [Secondary Region] THEN [Customer ID]
    END
)
```

**Primary No. of Orders**
```
COUNTD(
    IF [Primary Region] THEN [Order ID]
    END
)
```

**Secondary No. of Orders**
```
COUNTD(
    IF [Secondary Region] THEN [Order ID]
    END
)
```

**Primary No. of Products**
```
COUNTD(
    IF [Primary Region] THEN [Product ID]
    END
)
```

**Secondary No. of Products**
```
COUNTD(
    IF [Secondary Region] THEN [Product ID]
    END
)
```

## First order date

**First Order Date**
```
MIN([Order Date])
```

**Primary First Order Date**
```
MIN(
    IF [Primary Region] THEN [Order Date]
    END
)
```

**Secondary First Order Date**
```
MIN(
    IF [Secondary Region] THEN [Order Date]
    END
)
```

## Hierarchy

**Location** hierarchy: Country > State > City > Postal Code
