# Adventure Works Sales Analysis

This project focuses on analyzing data from the Adventure Works database to provide insights and recommendations to the sales and leadership teams. The project includes a presentation to showcase the analysis and dashboards to provide interactive visualizations of the data. 

## Table of Contents

- [Introduction](#introduction)
- [Data Sources](#data-sources)
- [Data Cleaning and Analysis](#data-cleaning-and-analysis)
- [Presentation](#presentation)
- [Dashboards](#dashboards)
- [Conclusion](#conclusion)

## Introduction

The project consists of three main parts:

- Presentation: A summary of the findings and recommendations for the sales and leadership teams.
- Dashboards: Interactive visualizations of the data using Tableau to provide more insights into the sales performance.
- Analysis: A detailed exploration of the data to identify trends, patterns, and opportunities to improve sales.
Overall, this project aims to help the sales and leadership teams make informed decisions based on the insights gained from the data.

## Data Sources

The data for this project was sourced from the Adventure Works database. The database contains information about sales, customers, products, and more. The data was accessed using Google Bigquery.

## Data Cleaning and Analysis

The data was cleaned and analyzed using SQL queries in Bigquery.

```sql

-- Leadership dashboard query
SELECT 
  DATE_TRUNC(OrderDate, MONTH) AS OrderMonth,
  SalesOrderID,
  SalesPersonID,
  SUM(TotalDue) AS Revenue,
  SUM(TaxAmt + Freight) AS Expenses,
  SUM(TotalDue - LineTotal) AS Profit
FROM 
  `your-project-id.adventureworks.salesorderheader` SOH
  JOIN (
    SELECT 
      SalesOrderID, 
      SUM(LineTotal) AS LineTotal
    FROM 
      `your-project-id.adventureworks.salesorderdetail`
    GROUP BY 
      SalesOrderID
  ) SOD ON SOH.SalesOrderID = SOD.SalesOrderID
GROUP BY 
  OrderMonth, SalesOrderID, SalesPersonID
ORDER BY 
  OrderMonth
 ```

```sql

-- Sales dashboard query
SELECT
  SP.SalesPersonID,
  CON.Firstname,
  SQH.QuotaDate,
  SQH.SalesQuota AS Generated,
  SP.SalesQuota AS Need_To_Reach,
  CASE
    WHEN SQH.SalesQuota >= SP.SalesQuota THEN 'Reached'
    ELSE 'Not reached'
  END AS QuotaStatus
FROM
  `tc-da-1.adwentureworks_db.salesperson` AS SP
JOIN 
  `tc-da-1.adwentureworks_db.salespersonquotahistory` AS SQH
  ON SP.SalesPersonID = SQH.SalesPersonID 
JOIN `tc-da-1.adwentureworks_db.employee` AS EMP
  ON SP.SalesPersonID = EMP.EmployeeId
JOIN `tc-da-1.adwentureworks_db.contact` AS CON
  ON EMP.ContactID = CON.ContactId
ORDER BY SQH.QuotaDate
 ```

The analysis focused on understanding the sales performance across different regions, products and sales types. The analysis also looked at trends over time and identified opportunities to improve sales. 

## Presentation

The presentation summarizes the findings from the data analysis and provides recommendations for the sales and leadership teams. The presentation includes charts and graphs to visually represent the data and communicate the insights. 

## Dashboards

The dashboards provide interactive visualizations of the data using Tableau. The dashboards include charts and graphs that allow users to explore the data in more detail and gain additional insights. 

## Conclusion

This project has provided valuable insights into the sales performance of Adventure Works. The analysis has identified opportunities to improve sales and provided recommendations for the sales and leadership teams. The dashboards provide an easy-to-use tool for exploring the data and gaining additional insights. Overall, this project aims to help the sales and leadership teams make informed decisions based on the insights gained from the data.

---

[Insert any additional information or acknowledgments here.] 
