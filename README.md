# 💊 Pharma Sales Dashboard - Power BI

This Power BI dashboard was built using pharma sales data to uncover key sales insights and performance metrics across different time dimensions and drug types. The goal of this project was to provide a user-friendly and interactive analytics experience for understanding trends in pharmaceutical sales.

---

## 📊 Dashboard Overview

The dashboard includes the following key performance indicators (KPIs) and visualizations:

### ✅ KPIs Calculated:
- **Highest Selling Drug**
- **Total Sales**
- **Peak Hour**
- **Top Sales Day of the Week**
- **Lowest Selling Drug**
- **Average Sales per Hour**
- **Weekend to Weekday Sales Ratio**
- **Lowest Sales Day of the Week**

🧮 *[DAX and Power Query formulas for each KPI are included in a separate section below]*

---

## 📈 Visualizations

1. **Pie Chart** – Top Sales by Year  
   > ![Screenshot: Pie Chart](./screenshots/pie_chart_yearly_sales.png)

2. **Stacked Area Chart** – Top Sales by Month and Drug Type  
   > ![Screenshot: Stacked Area Chart](./screenshots/stacked_area_monthly_sales.png)

3. **Line Chart** – Hourly Sales by Drug Type  
   > ![Screenshot: Line Chart](./screenshots/line_chart_hourly_sales.png)

4. **Heatmap** – Day vs Hourly Sales Pattern  
   > ![Screenshot: Heatmap](./screenshots/heatmap_day_hour.png)

---

## 🧮 KPI DAX & Power Query Formulas

### 1. **Highest Selling Drug**
```dax
Highest Selling Drug = 
CALCULATE(
    SELECTEDVALUE(saleshourly[Drug Type]),
    TOPN(1,
	SUMMARIZE(
		saleshourly,
		saleshourly[Drug Type],
		"Total Drug Sales",sum(saleshourly[Value])
	),
	[Total Drug Sales], DESC
)
)
```

### 2. **Total Sales**
```dax
Total Sales = SUM(saleshourly[value])
```

### 3. **Peak Hour**
```dax
Peak Hour = 
CALCULATE(
    SELECTEDVALUE(saleshourly[Hour]),
    TOPN(1,
    SUMMARIZE(saleshourly, saleshourly[Hour],
    "Total Hourly Sales", SUM(saleshourly[Value])),
    [Total Hourly Sales], DESC)
)
```

### 4. **Top Sales Day of the Week**
```dax
Top Sales Day of Week = 
CALCULATE(
    SELECTEDVALUE(saleshourly[Weekday Name]),
    TOPN(1,
	SUMMARIZE(
		saleshourly,
		saleshourly[Weekday Name],
		"Total Drug Sales per weekday",sum(saleshourly[Value])
	),
	[Total Drug Sales per weekday], DESC
)
)
```

### 5. **Lowest Selling Drug**
```dax
Lowest Selling Drug = 
CALCULATE(
    SELECTEDVALUE(saleshourly[Drug Type]),
    TOPN(1,
	SUMMARIZE(
		saleshourly,
		saleshourly[Drug Type],
		"Total Drug Sales",sum(saleshourly[Value])
	),
	[Total Drug Sales], ASC
)
)
```

### 6. **Average Sales per Hour**
```dax
Average Sales Per Hour = 
DIVIDE (
    SUM(saleshourly[Value]),
    COUNTROWS(saleshourly),
    0
)
```

### 7. **Weekend/Weekday Ratio**
```dax
Weekend to Weekday Ratio = 
DIVIDE([Weekend Sales], [Weekday Sales],0)

Weekend Sales = 
CALCULATE(

    SUM(saleshourly[Value]),
    FILTER(
        'calendar',
        WEEKDAY('calendar'[Date],2)>=6 )
)

Weekday Sales = 
CALCULATE(

    SUM(saleshourly[Value]),
    FILTER(
        'calendar',
        WEEKDAY('calendar'[Date],2)<6 )
)
```

### 8. **Lowest Sales Day of the Week**
```dax
Lowest Sales Day of Week = 
CALCULATE(
    SELECTEDVALUE(saleshourly[Weekday Name]),
    TOPN(1,
	SUMMARIZE(
		saleshourly,
		saleshourly[Weekday Name],
		"Total Drug Sales per weekday",sum(saleshourly[Value])
	),
	[Total Drug Sales per weekday], ASC
)
)
```

---

## 🧩 Power Query (M Code)

> *(Add any Power Query logic here for transformations, date extraction, type conversions, and calculated columns like "IsWeekend" or "Hour")*

---

## 🗂️ Folder Structure

```
pharma-sales-dashboard/
│
├── PharmaDashboard.pbix
├── README.md
├── /data
│   └── sales_data.csv
├── /screenshots
│   ├── pie_chart_yearly_sales.png
│   ├── stacked_area_monthly_sales.png
│   ├── line_chart_hourly_sales.png
│   └── heatmap_day_hour.png
```

---

## 📬 Contact

For questions or feedback, please contact **[Your Name]** at **[your.email@example.com]**

---