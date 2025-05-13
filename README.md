

# NTB-Prediction-Model-for-Amazon-Subscribe-&-Save Orders

## 🧠 Overview

Amazon's default customer attribution model creates a critical blind spot in real-time reporting by assigning all unpaid "pending" orders—especially **Subscribe & Save (SNS)** orders—to a placeholder customer ID (`5b42a3b76af065a7ceedfe79deb09f8a`). This skews two vital metrics:

- **Total Customer Count**: Multiple real customers appear as one
- **NTB vs. Repeat Classification**: All orders are falsely flagged as "Repeat"

These errors persist until the order invoices are paid, often up to 21 days later, disrupting week-to-date dashboards and impairing marketing and finance decisions.

---

## 🔍 Problem Breakdown

- **Pending Order Behavior**: Amazon creates a placeholder order ~21 days before shipping for SNS, letting customers modify or cancel.
- **Attribution Error**: All such orders are flagged as Repeat and assigned to one ID.
- **Reporting Gap**: Key NTB performance metrics are invalid during the non-stabilized window (typically the most recent 20 days).

---

## ✅ Solution

To address this, I built a forecasting-based model that estimates NTB performance in real time by:

1. **Segmenting Order Types**: Treating subscription and non-subscription orders separately.
2. **Historical NTB Ratio Modeling**: Using paid invoice data to establish baseline NTB-to-total order ratios.
3. **Forecasted Adjustments**: Applying the modeled ratios to active pending orders in the unstable period.
4. **Live Scorecard Integration**: Updating dashboards with corrected NTB estimates and customer counts.

---

## 🧮 NTB Estimation Formula

To predict New-to-Brand (NTB) customers during the Amazon reporting lag, I implemented the following segmented estimation formula:

\[
\textbf{NTB}_{\text{estimated}} = \text{ntb\_orders} + (\text{placeholder\_non\_sns} \times \text{constant}_{\text{non\_sns}}) + (\text{placeholder\_sns} \times \text{constant}_{\text{sns}})
\]

**Where:**
- `ntb_orders` = Finalized NTB orders with paid invoices
- `placeholder_non_sns` = Unpaid non-subscription orders under placeholder ID
- `placeholder_sns` = Unpaid subscription (SNS) orders under placeholder ID
- `constant_non_sns` = Historical NTB ratio for non-subscription orders
- `constant_sns` = Historical NTB ratio for SNS orders

This logic allowed us to produce real-time NTB predictions aligned with post-invoice results, while separating order types by behavioral pattern.

---
## 📈 Impact

- 🎯 **97%+ Accuracy** in NTB prediction for recent (unstable) 20-day window
- 📊 Enabled **reliable WTD reporting**, eliminating delays from Amazon's post-invoice updates
- 🔍 Exposed **20–25% NTB undercounting** in SKUs with high subscription volumes
- 📉 Improved marketing attribution and CAC/ROAS tracking during live campaign reporting

---

## 🛠️ Tools Used

- **SQL (snowflake)** – Extracted order and customer data
- **Google Sheet** – Built historical ratio models and Initial prototyping and modeling logic
- **Looker** – Integrated corrected metrics into live dashboards

---

## 📌 Key Metrics Corrected

- **New-to-Brand (NTB) Customer Count**
- **Total Unique Customer Count**
- **NTB vs. Repeat Ratio**
- **Week-to-Date Scorecard Accuracy**

---

## 🧩 Recommendation

This model can be further enhanced by dynamically recalculating the NTB-to-order ratio based on rolling performance data. Instead of relying solely on static historical averages, a real-time adjustment mechanism can detect changes in customer acquisition behavior and subscription trends—making NTB prediction more adaptive and responsive to current performance shifts.
 It also highlights the need for Amazon advertisers to build their own real-time attribution layers when native data is delayed or flawed.

---




















# Amazon-DTC-Sales-Optimization-and-Forecasting-Engine

## **SUMMARY**

### **Challenge**

The company faced a critical challenge of aligning finance, operations, and marketing departments under a new change management directive to minimize losses. Given that 85% of sales were conducted on Amazon, it became imperative to understand the impact of paid advertising that was directed to the Shopify website and then attributed to sales on Amazon. The goal was to reduce ad spend while ensuring that enough inventory available in the warehouse could be sold, satisfying the new targets.

### **Solution**

To address this challenge, I developed the **Sales Forecast Modeling Engine** using Google Sheets, leveraging Amazon Attribution data to track the impact of paid advertising on sales. This tool introduced new metrics such as **Cost Per Visit** and **Share of Paid Visits**, enabling precise forecasting. The engine allowed for detailed input of advertising budgets and discount offers across different weeks, providing accurate projections of key metrics like Amazon conversion rate, total sales units, and customer acquisition costs.

![Amazon Attribution](https://github.com/analytisor/Amazon-DTC-Sales-Optimization-and-Forecasting-Engine/blob/main/Paid%20Ads%20Flow%20and%20Attribution%20Pathway.jpg)

### **Impact**

The implementation of this modeling engine enabled all departments to quickly align with the new targets. Finance was pleased as it allowed for accurate cash flow planning, marketing was able to adjust ad spend in line with the new sales targets, and operations successfully managed to sell through the remaining inventory without the need for additional orders. This comprehensive tool ensured that each department's objectives were met efficiently and effectively.

### **Metrics and Dimensions**

**Key Metrics:**
- Amazon Conversion Rate (CR %)
- **Cost Per Visit (CPV)**
- **Share of Paid Visits**
- Paid Visits vs. Organic Visits
- Unit Sales per Week
- Total Discount Amount
- Customer Acquisition Cost (CAC)
- **Ad Spend**: Total advertising budget allocated per week

**Key Dimensions:**
- **SKU Discount Amount:** Discount applied per product for specific campaigns
- **Campaign Timing:** Week-by-week analysis of performance, adjusted for events like Black Friday and Prime Day
- **Traffic Source:** Breakdown between paid and organic traffic on Amazon

### **Summary of Insights**

By identifying a **Cost Per Visit** of $3.50 and a **Share of Paid Visits** of 40%, combined with the historical Amazon conversion rate, we were able to accurately assess the impact of reducing paid advertising on total sales units. This analysis helped in setting a target that satisfied finance's cash flow requirements while ensuring that all remaining inventory was sold by the end of the year. The forecasting also took into account sales spikes during key events like Fall Amazon Prime Day and Black Friday through Cyber Monday.

Another critical insight was the integration of metrics such as Amazon return rate, Shopify return rate, Shopify's share of sales, Amazon commission rate, and overall product Cost of Goods Sold (COGS). These factors allowed us to calculate the new expected total bottom line for the business under the revised targets, providing a clear picture of profitability.

### **Recommendation and Next Steps**

- Develop the engine's capability to process daily discount targets and output daily projections for traffic, ad spend, unit sales, and total costs, making the forecasting even more dynamic and responsive to real-time changes in the market.
- Utilize the weekly targets established by the model to continuously track actual vs. target performance on a weekly basis, ensuring the company remains on the correct path toward achieving its goals.

### **Visualizations**

#### **Sales Forecast Data Flow Overview**

![Data Flow Overview](https://github.com/analytisor/Amazon-DTC-Sales-Optimization-and-Forecasting-Engine/blob/main/Data_flow_overview)

#### **Key Formulas in Forecasting Engine**

![Key FormulasUnit Sales and Ad Spend Projections](https://github.com/analytisor/Amazon-DTC-Sales-Optimization-and-Forecasting-Engine/blob/main/key%20formulas%20in%20forecasting%20engine)

#### **Metric Definitions and Formulas**

![Metrics 1](https://github.com/analytisor/Amazon-DTC-Sales-Optimization-and-Forecasting-Engine/blob/main/Modeling%20Engine%20Equation%201.jpg)
![Metrics 2](https://github.com/analytisor/Amazon-DTC-Sales-Optimization-and-Forecasting-Engine/blob/main/Modeling%20Engine%20Equation%202.jpg)


