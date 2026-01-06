# Retail Customer Retention Analytics – ADIDAS 📊

## Project Overview

A comprehensive Power BI analytics project analyzing **customer retention, churn patterns, and lifetime value** for Adidas retail operations. This project uses advanced data modeling, DAX formulas, and multi-page dashboards to provide actionable insights for improving customer loyalty and reducing churn.

---

## 🎯 Objectives

1. **Understand Churn Patterns** – Identify why customers leave and which segments are most at risk
2. **Optimize Retention Strategies** – Develop targeted retention initiatives for high-value customers
3. **Maximize Customer Lifetime Value (CLV)** – Segment customers and focus resources on high-value segments
4. **Enhance Loyalty Program** – Improve point redemption rates and engagement across loyalty tiers
5. **Evaluate Channel Performance** – Compare store types, regions, and preferred channels
6. **Improve Promotion Impact** – Analyze how promotions affect purchase behavior and retention

---

## 📁 Data Sources

The project integrates **5 key datasets**:

| Table | Records | Key Columns |
|-------|---------|------------|
| **Customer Demographics** | 300 | Customer_ID, Age, Gender, Region, Income_Level, Membership_Since, Preferred_Channel |
| **Customer Transactions** | 1,000+ | Transaction_ID, Customer_ID, Store_ID, Product_Category, Transaction_Date, Amount, Promotion_Applied |
| **Churn Labels** | 500 | Customer_ID, Churn_Flag, Last_Purchase_Date, Churn_Reason |
| **Loyalty Program** | 500 | Customer_ID, Loyalty_Tier, Points_Earned, Points_Redeemed |
| **Store Locations** | 50+ | Store_ID, Store_Type, Region, Opening_Year |


-<a href="https://github.com/akshayjariyal73-sys/Retail_Customer_Retention_Analytics-_ADIDAS-_PowerBI/blob/main/Adidas%20customer%20transactional%20.xlsx"> customer transaction </a>
---

## 🔧 Technical Stack

- **BI Tool:** Power BI Desktop
- **Data Cleaning:** Power Query (ETL)
- **Calculations:** DAX (Data Analysis Expressions)
- **Data Modeling:** Star Schema with relationships
- **Visualization:** Multi-page interactive dashboards

---

## 📊 Key Metrics & KPIs

### Core Retention Metrics
- **Churn Rate %** = (Churned Customers / Total Customers) × 100
- **Retention Rate %** = (Active Customers / Total Customers) × 100
- **Repeat Rate %** = (Repeat Customers / Total Customers) × 100
- **Repeat Customer Count** = Customers with 2+ transactions

### Customer Value Metrics
- **Customer Lifetime Value (CLV)** = Total Amount Spent / Membership Duration (Years)
- **Average Purchase Amount** = SUM(Amount) / COUNT(Transactions)
- **Average Transaction Frequency** = AVERAGE(Purchase Count per Customer)

### Loyalty Program Metrics
- **Point Utilization Rate %** = Points_Redeemed / Points_Earned
- **Loyal Customers Count** = Customers with tier above "Base"
- **Average Points Earned/Redeemed** = By Loyalty Tier

### Promotion Effectiveness
- **% Transactions with Promotions** = Promotion Applied Count / Total Transactions
- **Avg Purchase Amount (with/without promo)** = Compare promotional impact

---

## 📈 Dashboard Pages

### **Page 1: KPIs & Overview**
High-level metrics dashboard showing:
- Total Customers, Repeat Customers, Churned Customers
- Churn Rate % by Region, Channel, Gender, Loyalty Tier
- Repeat Rate % and Average CLV
- Funnel chart: Customer journey (Total → Repeat → Churned)
-<a href="<img width="875" height="422" alt="image" src="https://github.com/user-attachments/assets/a46a7de3-98a1-41bf-bbab-d4461a560e4a"> </a>


### **Page 2: Loyalty & Promotion Impact**
Deep dive into loyalty program and promotion effectiveness:
- Point Utilization Rate and Loyalty Tier performance
- Churn Rate by Loyalty Tier (Elite, Premium, Plus, Base)
- Points Earned vs. Redeemed (Clustered Column Chart)
- Promotion impact on average purchase amount
- No. of Loyal Customers and Regional breakdown
-<a href="<img width="878" height="459" alt="image" src="https://github.com/user-attachments/assets/93ae6381-ab2c-4e05-bf34-b9705a6c9265"> </a>

### **Page 3: Store & Channel Performance**
Channel and store type analysis:
- Average Transaction Amount by Store Type (Franchise, Outlet, Online, Flagship)
- Churn Rate by Store Type and Preferred Channel
- Total CLV by Store Type and Region
- Transaction volume by channel
- Correlation between store opening year and retention
-<a href="<img width="870" height="465" alt="image" src="https://github.com/user-attachments/assets/3350f36c-1726-422d-b610-ea357d309afd"> </a>
### **Page 4: Customer Segmentation**
Customer segments for targeted retention:
- CLV Segments (Low, Medium, High CLV)
- Purchase Tier Segments (Low, Mid, High)
- Average CLV by segment
- Churn Rate and Repeat Rate by segment
- Priority matrix: High CLV + High Purchase Tier customers
-<a href="<img width="875" height="467" alt="image" src="https://github.com/user-attachments/assets/2571ede5-7c43-4748-9c91-284840cec36b"> </a>
---

## 🛠️ Data Transformation & Modeling

### Data Cleaning (Task 1)
✅ Removed duplicates using Transaction_ID, Customer_ID, Store_ID  
✅ Handled missing values (replaced NULLs with "NA")  
✅ Standardized data types (dates, numbers, text)  
✅ Cleaned text fields (removed extra spaces)  
✅ Validated data quality (100% valid records)

### Calculated Columns Created
```
Membership_Duration (Years) = DATEDIFF(Membership_Since, TODAY(), YEAR)
Transaction_Year = YEAR(Transaction_Date)
Transaction_Month = MONTH(Transaction_Date)
Transaction_Month_Name = FORMAT(Transaction_Date, "MMMM")
Days_Since_Last_Purchase = DATEDIFF(Last_Purchase_Date, TODAY(), DAY)
Age_Group = GROUP ages into bins (18-24, 25-34, 35-44, 45-54, >55)
Segment_Customers = SWITCH statement for Low/Mid/High tier by purchase count
CLV_Segment = SWITCH statement for Low/Medium/High CLV
Loyal_Customers = IF(Loyalty_Tier ≠ "Base", 1, 0)
```

### Key DAX Measures
```DAX
Total Customers = DISTINCTCOUNT(Customer_Demographics[Customer_ID])
Churned Customers = CALCULATE(COUNT(...), Churn_Flag = 1)
Active Customers = CALCULATE(COUNT(...), Churn_Flag = 0)
Churn Rate % = DIVIDE([Churned Customers], [Total Customers]) * 100
Retention Rate % = DIVIDE([Active Customers], [Total Customers])
Average CLV = AVERAGE(Customer_Demographics[CLV])
Total Amount Spend = CALCULATE(SUM(Transactions[Amount]), ...)
Point Utilization Rate = DIVIDE(SUM(Points_Redeemed), SUM(Points_Earned))
% Transactions with Promotion = DIVIDE(COUNT(..., Promotion="Yes"), COUNT(...))
```

---

## 📋 Key Findings & Insights

### 1️⃣ **Churn Risk Analysis**
- **Overall Churn Rate:** 27.33% (82 customers out of 300)
- **Highest Churn:** Asia-Pacific (33.33%) and Middle East (28.99%)
- **Lowest Churn:** Europe (24.00%)
- **Churn by Loyalty Tier:** Elite tier has highest churn (44.83%) despite high value

### 2️⃣ **Channel & Store Performance**
- **Underperforming:** Flagship stores (lowest revenue: $32.32K, lowest avg CLV)
- **Best Performers:** Franchise stores ($58.55K total CLV), Online channels (51.4% of transactions)
- **Store Type Performance:** Franchise > Outlet ≈ Online > Flagship

### 3️⃣ **Loyalty Program Issues**
- **Point Utilization Rate:** Only 57.86% (40%+ points go unredeemed)
- **Total Points Wasted:** 891.36K points
- **Redemption Opportunities:** Simplify redemption process, make rewards more desirable

### 4️⃣ **Customer Value Insights**
- **Average CLV:** $237.95 overall
- **High CLV Segment:** $930.69 avg (only 32 customers but highest value)
- **Priority Segment:** High CLV + High Purchase Tier = 32 customers, avg repeat rate 78.28%

### 5️⃣ **Promotion Effectiveness**
- **52.70% of transactions** include promotions
- **Avg Purchase with Promo:** $272.43 (vs $258.79 without)
- **Promotion Impact:** +5.3% higher average purchase amount

### 6️⃣ **Customer Segments**
- **Low Tier (0-3 purchases):** 170 customers, 21.88% churn
- **Mid Tier (4-8 purchases):** 128 customers, 26.77% churn
- **High Tier (9+ purchases):** 32 customers (only!), 31.43% churn

---

## 🎯 Top 3 Recommendations

### **1. PRIORITY: Focus on High CLV & High Purchase Tier Customers**
- These 32 customers have avg CLV of $930.69 but 21.88% churn rate
- Risk: Losing just 7 customers = $6.5K revenue loss
- **Action:** Launch personalized retention campaigns, exclusive perks, dedicated account managers

### **2. Fix Flagship Store Operations & Asia-Pacific Region**
- Flagship stores have lowest revenue and CLV
- Asia-Pacific has 33.33% churn (9% above average)
- **Action:** Audit operations, train staff, implement regional loyalty programs, benchmark against Franchise success

### **3. Strengthen Loyalty Program Engagement**
- 40%+ of earned points go unredeemed
- Elite tier members (most valuable) have highest churn (44.83%)
- **Action:** Simplify redemption, create fast-track offers for Elite/High CLV, add gamified rewards, communicate value clearly

---

## 📁 Project Files

```
Retail-Customer-Retention-Analytics-ADIDAS/
│
├── README.md (This file)
├── Retail Customer Retention Analytics – ADIDAS.pbix (Power BI File)
├── Data/
│   ├── Customer_Demographics.xlsx
│   ├── Customer_Transactions.xlsx
│   ├── Churn_Labelled_Customers.xlsx
│   ├── Loyalty_Program.xlsx
│   └── Store_Locations.xlsx
└── Documentation/
    ├── Data_Dictionary.xlsx
    └── DAX_Formulas.txt
```

---

## 🚀 How to Use This Project

### **Open the Power BI File**
1. Download `Retail Customer Retention Analytics – ADIDAS.pbix`
2. Open in Power BI Desktop
3. Navigate through 4 dashboard pages
4. Use slicers to filter by Region, Channel, Loyalty Tier, etc.

### **Refresh Data**
1. Click **Home** → **Transform Data**
2. Update Excel connections to your data sources
3. Click **Close & Apply** to refresh all calculations

### **Customize for Your Needs**
- Modify DAX measures for different date ranges
- Add filters for specific product categories
- Create new calculated columns for additional segments

---

## 🎓 Learning Outcomes

This project demonstrates expertise in:
- ✅ **Data Modeling:** Star schema design with relationships
- ✅ **Power Query:** ETL, data cleaning, transformations
- ✅ **DAX Formulas:** Complex measures, conditional logic, calculated columns
- ✅ **Data Visualization:** Multi-page dashboards, best practices, interactivity
- ✅ **Business Analytics:** KPI development, segmentation, insights generation
- ✅ **Statistical Analysis:** Churn patterns, correlation analysis, customer lifetime value
- ✅ **Communication:** Executive insights, recommendations, storytelling with data

---

## 📊 Metrics Summary Table

| Metric | Value | Insight |
|--------|-------|---------|
| **Total Customers** | 300 | Base customer population |
| **Churn Rate %** | 27.33% | 1 in 4 customers at risk |
| **Retention Rate %** | 72.67% | 3 in 4 customers remain loyal |
| **Repeat Rate %** | 85.33% | 256 customers made repeat purchases |
| **Average CLV** | $237.95 | Customer revenue over membership lifetime |
| **Highest Churn Region** | Asia-Pacific | 33.33% (action needed) |
| **Lowest Churn Region** | Europe | 24.00% (best performer) |
| **Point Utilization Rate** | 57.86% | 40%+ points go unredeemed |
| **Promotion Impact** | +5.3% | Promotions drive higher avg purchase |
| **High CLV Customers** | 32 | 10.67% of customer base, highest value |

---

## 📺 Video Walkthrough

[Google Drive Link to Video Demo](https://drive.google.com/file/d/1ivuPlrgljtmBFzbYaH1KwvnJGn4vX2CM/view?usp=sharing)

---

## 👤 Author

**Akshay Jariyal**  
Data Science Learner | Data Analyst (In Training)  
📧 **ajaries1997@gmail.com**  
📍 Shimla, Himachal Pradesh, India

---

## 📝 License

This project is created for educational and analytical purposes.  
Feel free to use, modify, and share for learning and professional development.

---

## 🙏 Acknowledgments

- **Data Source:** Internshala Trainings Python Data Preparation & Analysis Course
- **Tools:** Power BI Desktop, Power Query, DAX
- **Inspiration:** Real-world retail analytics challenges

---

## 🔗 Connect & Collaborate

Looking to collaborate on data science and analytics projects?  
📧 Reach out: **ajaries1997@gmail.com**  
💼 Open to Data Analyst roles and freelance projects

---

**Last Updated:** January 2026  
**Status:** ✅ Complete & Ready for Portfolio

---

## 📌 Quick Links

-<a href="https://github.com/akshayjariyal73-sys/Retail_Customer_Retention_Analytics-_ADIDAS-_PowerBI/blob/main/Retail%20Customer%20Retention%20Analytics%20%E2%80%93%20ADIDAS.pdf"> Project PDF </a>

---

**Happy Analyzing! 📊✨**
