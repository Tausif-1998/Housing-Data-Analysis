# Housing-Data-Analysis
This Power BI project presents a comprehensive Housing Data Analysis Dashboard consisting of three interactive pages:\
**House Market Overview** – Visualizes key trends in the housing market, including average prices, growth rates, and regional comparisons.\
**Sales Performance** – Highlights sales metrics over time, such as volume, revenue trends, and top-performing locations.\
**House Type Analysis** – Breaks down data by house types to understand demand patterns, pricing differences, and buyer preferences.\

This dashboard helps stakeholders make data-driven decisions in the real estate domain by providing clear insights into market dynamics and sales performance.

## Tools/Technologies Used
1. Microsoft Excel
2. Google BigQuery
3. Power BI
4. DAX
5. Power BI Service

## Approach
1. Importing data from Google BigQuery to Power BI
2. Transforming Data in Power BI
3. Data Visualization
4. Publishing the report

## Steps Followed
1. Uploaded CSV file in BigQuery and created a table for it. Data loaded into a BigQuery table.
2. Connect the BigQuery table to Power BI and import data into Power BI.
3. Data cleaning, transforming, and modeling in Power BI :
   - Check null values and replace with average values.
   - Created custom columns and Measures
     
   Custom Column and DAX formulas listed below: <br>

   <ins>New Columns:</ins>
   1. Age = _ABS(YEAR(Housing[date (MM/DD/YYYY)].[Date]) - Housing[year_build])_
   2. Offer Price = _(100*Housing[purchase_price])/(100-Housing[%_change_between_offer_and_purchase])_
      
   <ins>Measures|DAX</ins>
   1. Average Price SQM = _AVERAGE(Housing[sqm_price])_
   2. Last 12 Month Sales = _CALCULATE(SUM(Housing[purchase_price]),DATESINPERIOD(Housing[date (MM/DD/YYYY)],MAX(Housing[date (MM/DD/YYYY)]),-12,MONTH))_
   3. Offer to SQM Ratio = _DIVIDE(SUM(Housing[Offer Price]),SUM(Housing[sqm]))_ 
   4. Sales by Region = _CALCULATE(SUM(Housing[purchase_price]),ALLEXCEPT(Housing,Housing[region]))_
   5. TotalYTD Sales = _TOTALYTD(SUM(Housing[purchase_price]),Housing[date (MM/DD/YYYY)].[Date])_
   6. Units sold in latest Year & Quarter = <br>
        CALCULATE(DISTINCTCOUNT(Housing[house_id]),YEAR(Housing[date (MM/DD/YYYY)])= YEAR(MAX(Housing[date (MM/DD/YYYY)])) && QUARTER(Housing[date (MM/DD/YYYY)])=QUARTER(MAX(Housing[date (MM/DD/YYYY)])))
   7. YOY_Sales_Growth = <br>
          _Var CurrYearSales =CALCULATE(SUM(Housing[purchase_price]),YEAR(Housing[date (MM/DD/YYYY)])=YEAR(max(Housing[date (MM/DD/YYYY)]))) <br>
          Var Prevyearsales =CALCULATE(SUM(Housing[purchase_price]),YEAR(Housing[date (MM/DD/YYYY)])=year(max(Housing[date (MM/DD/YYYY)]))-1) <br>
          Return <br>
              IF(Prevyearsales<>0, (CurrYearSales-Prevyearsales)/Prevyearsales,BLANK())_
   8. Median Sales Price Change = <br>
     _Var CurrMedianPrice = MEDIANX(FILTER(Housing,YEAR(Housing[date (MM/DD/YYYY)].[Date])=YEAR(MAX(Housing[date (MM/DD/YYYY)].[Date]))),Housing[purchase_price]) <br>
      Var PreMedianPrice =MEDIANX(FILTER(Housing,YEAR(Housing[date (MM/DD/YYYY)].[Date])=YEAR(MAX(Housing[date (MM/DD/YYYY)].[Date]))-1),Housing[purchase_price]) <br>
      RETURN  <br>
          IF(PreMedianPrice<>0, (CurrMedianPrice-PreMedianPrice)/PreMedianPrice,BLANK())_
4. Create three pages and add a canvas background to the pages.
5. Used the below data visualization charts: <br>
   1. Stacked Bar chart
   2. Clustered bar chart
   3. Cards
   4. Line chart
   5. Scatter chart
   6. Donut Chart
   7. Line and stacked column chart
   8. Table
   9. Slicers
   10. Page navigation button
6. Save the project and publish to Power BI Service under the workspace.
7. Dashboard Web URL: https://app.powerbi.com/view?r=eyJrIjoiYTFjYjY0MjQtMGVhOS00OGE2LTgxNDQtMmFiNjFmMTYwNWRlIiwidCI6IjUyYTdhZTM0LTk2MjQtNDNkYS05MjhlLWRmMTEyZTdlNmFjNCJ9

  




     
     
