# SalesKSA
# 📊 Sales Analytics Dashboard - Saudi Arabia

A comprehensive Power BI dashboard analyzing sales performance across Saudi Arabian regions for 2024. This project demonstrates advanced data visualization, DAX formulas, and business intelligence best practices.

![Dashboard Preview](assets/overview-dashboard.png)

## 🎯 Project Overview

This interactive dashboard provides actionable insights into sales performance, customer behavior, profitability, and VAT compliance for a retail business operating across 13 Saudi Arabian regions.

### Key Features
- **Dynamic KPI Cards** - Context-specific metrics for each analysis page
- **Interactive Filters** - Year, Region, Product, and Sales Channel slicers
- **Multi-page Analysis** - 5 specialized pages covering different business aspects
- **Saudi Arabia Focus** - Regional analysis across all 13 Saudi regions
- **VAT Compliance Tracking** - 15% VAT monitoring and reporting

## 📈 Dashboard Pages

### 1. Overview
Main landing page with high-level business metrics and trends.

**Key Metrics:**
- Total Sales: 1.89M SAR
- Total Profit: 464.40K SAR
- Profit Margin: 25%
- Average Order Value: 1.89K SAR
- Total Quantity Sold: 5K units
- Total VAT: 282.94K SAR

**Visualizations:**
- Monthly Sales Trend (Line Chart)
- Sales by Channel (Bar Chart)
- Key Insights and Highlights

### 2. Sales Performance
Deep dive into sales patterns and product performance.

**Key Metrics:**
- Total Sales: 1.89M SAR
- Growth Rate: 2.72%
- Best Month: December
- Lowest Month: October

**Visualizations:**
- Sales by Month & Quarter (Line Chart)
- Top 10 Products by Sales (Bar Chart)
- Sales by Region (Table)

**Top Selling Products:**
1. External Hard Drive
2. Printer
3. Smartphone
4. Desktop PC
5. Smartwatch

### 3. Customer Analysis
Customer behavior, segmentation, and value analysis.

**Key Metrics:**
- Total Customers: 500
- Average Order Value: 1.89K SAR
- Avg Orders per Customer: 2.00
- Customer Lifetime Value: 4.53M SAR

**Visualizations:**
- Sales by Gender & Age Group (Stacked Bar Chart)
- Average Order Value by Sales Channel (Donut Chart)
- Top 20 Customers by Sales & Quantity (Table)

**Customer Insights:**
- Age Group 35-44 has highest spending
- Gender distribution fairly balanced
- Online channel has highest AOV (1.95K SAR)

### 4. Profitability & Discounting
Profitability analysis with scenario simulation capabilities.

**Key Metrics:**
- Total Profit: 464.40K SAR
- Profit Margin: 25%
- Average Unit Cost: 290.24 SAR
- Total Quantity: 5K
- Top Profit Product: Printer

**Visualizations:**
- Total Profit by Product (Bar Chart)
- Profit Margin % by Product (Bar Chart)
- Discount vs Profit Margin (Scatter Plot)
- Profit Margin % by Region (Bar Chart)
- Interactive Discount Scenario Simulator

**Features:**
- Adjustable discount rate slider
- Real-time simulated profit calculation
- Product and regional profitability comparison

### 5. VAT & Time Analysis
VAT collection tracking and temporal sales patterns.

**Key Metrics:**
- Total VAT: 282.94K SAR
- VAT Compliance Rate: 100%
- Peak Sales Day: Tuesday
- Weekday/Weekend Ratio: 2.43

**Visualizations:**
- VAT Collected by Month (Line Chart)
- Weekend vs Weekday Sales (Bar Chart)
- Sales by Day of Week (Bar Chart)
- VAT by Region & Channel (Stacked Bar Chart)

## 🛠️ Technologies Used

- **Power BI Desktop** - Dashboard development and visualization
- **DAX (Data Analysis Expressions)** - Custom measures and calculations
- **Power Query** - Data transformation and cleaning
- **M Language** - Data loading and preprocessing

## 📊 Data Model

### Tables
- **SalesData_SA** - Main fact table with sales transactions
- **Calendar** - Date dimension table
- **Products** - Product master data
- **Customers** - Customer information
- **Regions** - Saudi Arabian regions

### Key Relationships
- SalesData_SA[Order Date] ↔ Calendar[Date]
- SalesData_SA[Product ID] ↔ Products[Product ID]
- SalesData_SA[Customer ID] ↔ Customers[Customer ID]

## 📐 DAX Formulas

### Core Measures

```dax
Total Sales Excl VAT = SUM(SalesData_SA[Total Sales Excl VAT])

Total Profit = SUM(SalesData_SA[Total Profit])

Profit Margin % = 
DIVIDE(
    [Total Profit],
    [Total Sales Excl VAT],
    0
)

Average Order Value = 
DIVIDE(
    [Total Sales Excl VAT],
    DISTINCTCOUNT(SalesData_SA[Order ID]),
    0
)
```

### Advanced Measures

```dax
Avg Orders per Customer = 
DIVIDE(
    COUNTROWS(SalesData_SA),
    DISTINCTCOUNT(SalesData_SA[Customer ID]),
    0
)

Customer Lifetime Value = 
SUMX(
    VALUES(SalesData_SA[Customer ID]),
    CALCULATE([Total Sales Excl VAT])
)

Simulated Profit = 
VAR DiscountRate = SELECTEDVALUE('Discount Scenario'[Discount Rate], 0)
VAR AdjustedRevenue = [Total Sales Excl VAT] * (1 - DiscountRate)
VAR TotalCost = SUM(SalesData_SA[Unit Cost]) * SUM(SalesData_SA[Quantity])
RETURN
    AdjustedRevenue - TotalCost
```

## 🎨 Design Principles

### 1. Context-Specific KPIs
Each page displays metrics relevant to its focus area, avoiding repetitive information across pages.

### 2. Data-Driven Insights
Automatic text insights highlight key findings and anomalies in the data.

### 3. Clean Visual Design
- Consistent color scheme
- Minimal chart decorations
- Clear typography hierarchy
- Appropriate white space

### 4. Interactive Elements
- Cross-filtering between visuals
- Drill-through capabilities
- Tooltips with additional context
- Dynamic titles based on selections

## 📁 Project Structure

```
sales-dashboard-saudi-arabia/
│
├── README.md
├── SalesData_SA.pbix                 # Power BI file
├── data/
│   └── SalesData_SA.xlsx             # Source data
├── assets/
│   ├── overview-dashboard.png
│   ├── sales-performance.png
│   ├── customer-analysis.png
│   ├── profitability.png
│   └── vat-time-analysis.png
└── documentation/
    └── DAX-Formulas.md
```

## 🚀 Getting Started

### Prerequisites
- Power BI Desktop (latest version)
- Basic understanding of Power BI and DAX

### Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/sales-dashboard-saudi-arabia.git
```

2. Open the `.pbix` file in Power BI Desktop

3. Refresh the data source if needed
   - Go to Home → Transform Data → Data Source Settings
   - Update the file path to your local `SalesData_SA.xlsx` location

4. Explore the dashboard!

## 📊 Sample Data

The dashboard uses 2024 sales data from a retail business including:
- **5,000** total transactions
- **500** unique customers
- **113** products across 10 categories
- **13** Saudi Arabian regions
- **3** sales channels (Retail Store, Online, Direct Sales)

## 🔍 Key Insights

### Sales Performance
- December had the highest sales (179.69K SAR), 40.25% higher than October
- External Hard Drives are the top-selling product category
- Al Jawf region leads in total sales (177.21K SAR)

### Customer Behavior
- Average customer places 2 orders
- Age group 35-44 shows highest spending
- Online channel has the highest average order value

### Profitability
- Overall profit margin of 25%
- Printer is the most profitable product (51K profit)
- Regional profit margins are consistent (23-28%)

### Temporal Patterns
- Weekday sales are 2.43x higher than weekend sales
- Tuesday is the peak sales day
- Sales show seasonal variation with Q4 being strongest

## 🎓 Learning Outcomes

This project demonstrates proficiency in:
- ✅ Power BI dashboard design and development
- ✅ DAX formula creation (basic to advanced)
- ✅ Data modeling and relationships
- ✅ Business intelligence best practices
- ✅ Visual storytelling and UX design
- ✅ KPI selection and context awareness
- ✅ Regional market analysis

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/yourusername/sales-dashboard-saudi-arabia/issues).

## 📝 License

This project is [MIT](LICENSE) licensed.

## 👤 Author

**Haya M.**

- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your LinkedIn](https://linkedin.com/in/yourprofile)
- Portfolio: [yourportfolio.com](https://yourportfolio.com)

## 🙏 Acknowledgments

- Data generated for educational purposes
- Inspired by real-world retail analytics requirements
- Built as part of data analytics portfolio development

---

⭐ **If you found this project helpful, please consider giving it a star!** ⭐

## 📸 Screenshots

### Overview Dashboard
![Overview](assets/overview-dashboard.png)

### Sales Performance
![Sales Performance](assets/sales-performance.png)

### Customer Analysis
![Customer Analysis](assets/customer-analysis.png)

### Profitability & Discounting
![Profitability](assets/profitability.png)

### VAT & Time Analysis
![VAT Analysis](assets/vat-time-analysis.png)

---

**Last Updated:** February 2026
