# Microsoft SSMS Database to Power BI Desktop & Service

## Contoso Retail: Competitive Sales Channel & Marketing Analysis

![Front Page Cover Images](Images/Database_to_PowerBI.png)

# Table of Content
- [Project Title](#Project-Title)
- [My Role](#My-Role)
- [Project Overview](#Project-overview)
- [Problem Statement](#Problem-statement)
- [Stakeholder Engagement](#Stakeholder-Engagement)
    - [Target Stakeholder](#Target-stakeholder)
    - [Use Cases](#Use-cases)
    - [Stakeholders Stories](#Stakeholder-stories)
    - [Acceptance Criteria](#Acceptance-criteria)
    - [Success Criteria](#Success-criteria)
- [Data Source](#Data-source)
  - [Dataase Structure](#Access-Database-Structure)
  - [Access Database Benefit](#Benefit-of-Access-Storage)
- [Methodology](#Methodology)
  - [Tool used](#Tool-Used)
  - [Development](#Development)
      - [Project Planning & Requirement Gathering](#Project-Planning-&-Requirement-Gathering)
      - [Data Sources Setup and Access](#Data-Sources-Setup-and-Access)
      - [Data Exploration & Profiling](#Data-Exploration-&-Profiling)
      - [ETL Process Using Power Query](#ETL-Process-Using-Power-Query)
      - [Data Modelling](#Data-Modelling)
      - [Measures Development Using DAX](#Measures-Development-Using-DAX)
      - [Dashboard Design & Visualisation](#Dashboard-Design-&-Visualisation)
          - [Mock up Design](#Mukkup_design_Dashboard)
      - [Publishing and Collaboration](#Publishing-and-Collaboration)
      - [Documentation & Version Control](#Documentation-&-Version-Control)
      - [Review & Iteration](#Review-&-Iteration)
- [Detailed Insights and Recommendations](#Detailed-Insights-and-Recommendation)
  - [Dashboard 1](#Sales-Pulse-Performance,-Frequency-&-Return-(Executive-Overview))
  - [Dashboard 2](#Sales-Performance-&-Customer-Behaviour-(Net-sales-by-Customer-Demographic))
  - [Dashboard 3](#Product-portfolio-performance-(Based-on-Gross-Proft))
 
# Project Title:
Contoso Competitive Sales Channel Analysis

# My Role
Power BI Developer/Data Analyst  

  - Designed the relational data model in Power BI through direct query option to  Microsoft SQL Server Management Studio data sources.
  - Developed Power BI dashboard for executive decision-making marketing and sales channel strategy.
  - Created advanced DAX measures for sales, margin, and trend analysis
  - Conducted ETL and data cleansing with Power Query
  - Delievered insights into channel Profitability, product performance, and geographic sales behavior

# Project Overview  

This project analyses Contoso’s multi-channel retail operations (Store, Online, Reseller, Catalog) to uncover sales trends, profit margins, and geographic performance using a SQL-based backend. Interactive Power BI dashboards support executive-level decisions regarding marketing strategy, resource allocation, and inventory planning.

# Problem Statement

Contoso lacked clear visibility into how different sales channels, products, and regions performed over time.
Key business questions included:  

- Which sales channels drive the most revenue and profit?
- What are the most profitable product subcategories?
- How do sales and margins differ by region and time period?  

This project resolves these issues by delivering a suite of Power BI dashboards with intuitive visualizations and actionable metrics.

# Stakeholder Engagement
### Target Stakeholder

- Executives (Sales, Marketing, Finance)
- Regional Managers
- Product Strategy Teams

### Use Cases

- Sales channel analysis that identify channels KPI's highlighting Total sales with YoY channel performance, breakdown products across all channel and monthly sales trends of across each channel.
- identifying top performing Brand name for each sale channel, what sales products contributed to it, and brand name performance across sales location.
- Localise marketing based on regional sales behavior
- Evaluate channel-specific ROI and margin performance

### Stakeholder Stories

- "As a Channel Manager, I need to see which channels are underperforming YoY so I can act quickly."
- "As a Marketing Head, I want to know which products have the best margins in each region."
- "As an Executive, I need to see overall sales, profitability, and performance trends in one dashboard."

### Acceptance Criteria

- Clear display of KPIs: Overall and top 5 brand Total Sales, Profit Margin, YoY Changes
- Filters for year, region, channel
- Channel-level breakdowns of product performance and margin
- Geo-mapping and trend visuals
- channels Bookmark button to interchange insights visual chanel profit, trends of sales and profit margin and product subcategory breakdown.

### Success Criteria

- Senior stakeholders can make informed, strategic decisions
- Analysts gain self-service access to performance metrics
- Marketing campaigns are aligned with profitable regions/products
- Product teams reduce inventory waste through data-backed insights

### Data Source

### Microsoft SQL Server Management Studio (SSMS) Structure  

    ## Add a picture of each table and ERD diagram, but mainly picture of tables that was used.

#### Fact Table
- FactSales Table: ChaneelKey, DateKey, DiscountAmount, DiscountQuantity, Gross Profit, Gross-Margin, Net Sales, ProductKey, Profit Margin, ReturnAmount, ReturnQauntity, Sales, SalesQuantity, StoreKey, Subcategory_Channel, TotalCost, UnitCost, and UnitPrice.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| SalesKey | Whole Number | Unique Identifier of each sales |
| DateKey | Date | Date of each sales |
| ChannelKey | Whole Number | Foreign key referencing channel table (ChannelKey) |
| StoreKey | Whole Number | (Delete) not needed |
| SalesKey | Whole Number | Unique Identifier of each sales |
| DateKey | Date | Date of each sales |
| ChannelKey | Whole Number | Foreign key referencing channel table (ChannelKey) |
| ProductKey | Whole Number | Forforeign key referencing product table (Productkey) |
| SalesKey | Whole Number | Unique Identifier of each sales |
| DateKey | Date | Date of each sales |
| ChannelKey | Whole Number | Foreign key referencing channel table (ChannelKey) |
| UnitCost | Fixed decimal number | Cost per product sold |
| UnitPrice | Fixed decimal number | unit price per product sold |
| SalesQuantity | Whole Number | qauntity of product sold |
| ReturnedQuantity | Whole Number | Quantity of product sold amount returned |
| ReturnedQuantity | Fixed decimal number | Returned Sold Amount |
| DiscountQuantity | Whole Number | qauntity of product that is being discounted |
| DiscountAmount | Fixed decimal number | amount on discounted qauntity |
| TotalCost | Fixed decimal number | cost of goods sold |
| Sales | fixed decimal number | products qauntity sales |
| Gross_Margin | Fixed decimal number | Difference between sales and total cost amount | 


#### Dimension Tables

- DimProductCategory Table: Including ProductCategoryDecription, ProductCategoryKey, ProductCategoryLabel, and ProductCategoryName.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| ProductCategoryKey | Whole Number | Unique identifier for each Product Category |
| ProductCategoryLabel | Text | Deletd |
| ProductCategoryName | Text | Name of each product category |
| ProductCategoryDescription | Text | short note to decribe each product category |  


- DimProductSubcategory Table: ProductCategoryKey, ProductSubcategoryDescrition, ProductSubcategoryKey, ProductSubcategoryLabel, and ProductSubcategoryName.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| ProductSubCategoryKey | Whole Number | Unique identifier for each Product Subcategory |
| ProductSubCategoryName | Text | Name of each product subcategory |
| ProductSubCategoryDescription | Text | short note to describe the product subCategory |
| ProductCategoryKey | Whole Number | Foreign key referencing  product category table (ProductCategoryKey) |  


- DimProduct Table: AvailableForSaleDate, BrandName, ColorID, ColorName, Manufacturer, ProductDescription, ProductKey, ProductLabel, and ProductName.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| ProductKey | Whole Number | Unique identifier for each product |
| ProductLabel | Text | (Delete) not needed in this analysis |
| ProductName | Text | Name of selling product |
| ProductDescrition | Text | short note of product description |
| ProductSubcategory | Whole Number | Foreign key referencing product Product Subcategory (ProductSubcategoryKey) |
| Manufacturer | Text | Manufacturer of contoso products |
| BrandName | Text | products brand name |
| ColorID | Text | (Delete) not needed |
| ColorName | Text | (Delete) not needed |
| StockTypeID | Whole Number | (Delete) not needed |
| StockTypeNmae | Text | (Delete) not needed |
| UnitCost | Fixed decimal number | Cost per product sold |
| UnitPrice | Fixed decimal number | unit price per product sold |
| AvailableForSaleDate | Date/Time | (Delete) Date when product would be available for sale |
| StopSaleDate | (Delete) Date/Time | Date when product is stopped being sold |
| Status | Text | (Delete) not needed |  


- DimChannel: ChannelDescription, ChannelKey, ChannelLabel, ChannelName, LoadDate, and UpdateDate.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| Channelkey | Whole Number | Unique Identifier of each channel |
| ChannelLabel | Text | (Delete) not needed |
| ChannelName | Text | name of each Sales channel |
| ChannelDescription | Text | short note to explain channel further  |
| LoadDate | Date/Time | (delete) not needed |
| UpdateDate | Date/Time | (delete) not needed |  


- DimGeography Table:  ContinentName, GeographyKey, Region-State/Province, RegionCountryName, StateProvinceName.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| GeographyKey | Whole number | Unique identifier to DimGeopgraphy |
| ContinentName | Text | Continent of each customers |
| SateProvinceName | Text | store or customer Continent Name |
| RegionCountryName | Text | store or customer countryname |  


- DimStore Table: AddressLine1, CloseDate, EmployeeCount, GeographyKey, Geolocation, Geometry, LastRemodelDate, OpenDate, Satus, StoreKey, StoreManager, StoreNmae, and Storetype.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| StoreKey | Whole Number | Unique Key Identifier of each store  |
| GeographyKey | Whole Number | Foreign Key referencing the Geograpgy table (GeographyKey)  |
| StoreManger | Whole Number | this a number that is attached to each manager |
| StoreType | Text | Available store type used for sales of goods  |
| StoreName | Text | Name of each store |
| Status | Text | This indicate if the store is still active or shutdown |
| OpenDate | Date/Time | Date the store will shutdown from dervices |
| ColseDate | Date/Time | Date the store was close for services |
| AdressLine1 | Text | Address to the sotres |
| EmployeeCount | Whole Number | Total number of employee for each store |
| GeoLocation | Text | Longitude and Latitude point of each store Location |
| Geometery | Text | longitude or latitude point of each store location |  


This table is not needed for now but for future purpose is would be needed so in that case while cleaning transforming data, the table would not be loaded in the report pane.  

#### Time Intelligence Date Table
- Date Table: Date, FY-Month, FY-Quarters, FY-Year, Month, Month Name, Month-Short, Month-VSH, Period, Quarter, and Year.  

| Column Name | Data Type | Description |
| --- | --- | --- |
| Date | Date | Full date of day/Month/Year and a unique identifier  |
| Year | Whole Number | Calendar year |
| Month | Whole Number | month number of calendar year |
| Month Name | Text | Month name of calendar name |
| Quarter | Whole Number | Quarter of calendar year |
| Month Short | Text | Uses the first three character of each month |
| Period |  Text | Combination of year and month of the year |
| FY - Month | Whole Number | Fiscal year month  |
| FY - Year | Whole Number | Fiscal year |
| FY - Quarter | Whole Number |  Fiscal year quarter |  

### Benefit of Microsoft SSMS Storage.

# Methodology  

### Tools Used
- Microsoft SQL Server Management Studio (SSMS):
SSMS was primarily used as a data storage and management tool. A DirectQuery connection was established from Power BI Desktop to the SQL Server database, allowing real-time querying of essential tables (e.g., FactSales, DimChannel, DimProduct, DimGeography, etc.). This approach ensured data freshness and reduced duplication during analysis.

- Power BI Desktop:
The main tool for creating the data model, writing DAX measures, and building interactive reports. It served as the development environment for all dashboards and calculations.

- Power Query:
Used within Power BI Desktop for the ETL process—cleaning, shaping, and transforming data after extraction via DirectQuery. Operations included column renaming, deleting unwanted columns, data type conversion, table joins, filtering, and calculated columns.

- Power Bi Service:
Dashboards were published to the Power BI Service for stakeholder access, real-time collaboration, and scheduled refresh management. The service also enabled dashboard sharing, mobile access, and usage monitoring.

- GitHub:
Used to host the documentation, project files (e.g., .pbix, .sql, .md), and provide public access for version control and portfolio presentation. It also served as a backup repository and platform to showcase the project in a professional setting.

### Development

General Approach to Creating the Solution:  

1. Project Planning & Requirement Gathering
2. Data Exploration & Profiling
3. Data Exploration & Profiling
4. ETL Process Using Power Query
5. Data Modelling
6. Measure Development Using DAX
7. Dashboard Design & Visualization
8. Publishing and Collaboration
9. Documentation & Version Control
10. Review & Iteration

#### Project Planning & Requirement Gathering

- Defined project scope and objectives (e.g., analyse sales channel performance,  product profitability, and geographical and sales trends).
- Identified key stakeholders (Sales, Marketing, and Executives) and gathered reporting requirements and KPIs.  
#### Data Source Setup and Access  

- Microsoft SQL Server was used to host the primary Contoso dataset.
- Connected Power BI Desktop to SQL Server using DirectQuery to enable real-time data access.
- Identified and extracted essential tables such as FactSales, DimChannel, DimProduct, DimGeography, and Date.

#### Data Exploration & Profiling  

- Reviewed data structures, row volumes, null values, duplicates, and relationships.
- Verified foreign key integrity across fact and dimension tables.
- Identified the appropriate grain of analysis (e.g., sales transactions per channel, date, and product).

#### ETL Process Using Power Query  

- Cleaned and transformed data using Power Query within Power BI Desktop.
- Applied business rules such as standardizing product labels, calculating derived columns (e.g., ROI, Net Sales), and removing unnecessary fields.
- Joined related tables for initial dimensional shaping.

#### Data Modelling  

- Built a star schema by establishing relationships between the fact table (FactSales) and relevant dimension tables.
- Ensured appropriate cardinality (e.g., many-to-one) and cross-filter directions.
- Added a dynamic date dimension for robust time intelligence.

![Contoso semantic model](Images/Contoso_semantic_model.png)

From the above Power BI data model pane image above we can see that a many to one (*:1) was establish between the FactSales  (The Fact Table) and Dimensions Table (Product, Customer, and date table).The other tables shown are the Dax measure and measure documentation tables. 

#### Measure Development Using DAX  

- Created key DAX measures for KPIs: Total Sales, Profit Margin, YoY Sales, ROI, Gross Profit, etc.
- Used calculated columns and measures to support visuals requiring trend analysis, comparisons, and percentage breakdowns.

    ##### Here are some of the Dax measures created to enrich the project insights

```DAX
% Return_Quantity = 
 DIVIDE(
    SUM(FactSales[ReturnQuantity]),
    SUM(FactSales[SalesQuantity]),
    0
)
```
```DAX
% Total_Cost = 
DIVIDE(
    SUM(FactSales[TotalCost]),
    SUM(FactSales[Sales]),
    0
)
```
```DAX
Profit Margin = 
DIVIDE(
    SUMX(FactSales, FactSales[Gross Profit]), 
    SUM(FactSales[Net Sales]), 
    0
)
```
```DAX
Profit Margin = 
DIVIDE(
    SUMX(FactSales, FactSales[Gross Profit]), 
    SUM(FactSales[Net Sales]), 
    0
)
```
```DAX
Profit Margin % by BrandName = 
DIVIDE(
    SUM(FactSales[Gross Profit]), 
    CALCULATE(SUM(FactSales[Net Sales]), ALL(DimProduct[BrandName])), 
    0
)
```
```DAX
Profit Margin % by Channel = 
DIVIDE(
    SUM(FactSales[Gross Profit]), 
    CALCULATE(SUM(FactSales[Net Sales]), ALL('DimChannel'[ChannelName])), 
    0
)
```
```DAX
Profit Margin % by Product = 
DIVIDE(
    SUM(FactSales[Gross Profit]), 
    CALCULATE(SUM(FactSales[Net Sales]), ALL('DimProductSubcategory'[ProductSubcategoryName])), 
    0
)
```
```DAX
YoY Catalog Store = 
VAR CurrentYear = MAX('Date'[Year])
VAR PreviousYr = CurrentYear - 1
VAR CurrentSales = 
    CALCULATE(
        SUM('FactSales'[Sales]),
        'Date'[Year] = CurrentYear,
        'DimChannel'[ChannelName] = "Catalog"
    )
VAR PreviousSales = 
    CALCULATE(
        SUM('FactSales'[Sales]),
        'Date'[Year]= PreviousYr,
        'DimChannel'[ChannelName] = "Catalog"
    )
RETURN 
    CurrentSales - PreviousSales
```
```DAX
YoY Catalog Store (%) = 
VAR CurrentYear = MAX('Date'[Year])
VAR PreviousYr = CurrentYear - 1
VAR CurrentSales = 
    CALCULATE(
        SUM('FactSales'[Sales]),
        'Date'[Year] = CurrentYear,
        'DimChannel'[ChannelName] = "Catalog"
    )
VAR PreviousSales = 
    CALCULATE(
        SUM('FactSales'[Sales]),
        'Date'[Year] = PreviousYr,
        'DimChannel'[ChannelName] = "Catalog"
    )
RETURN 
    IF(
        PreviousSales <> 0,
        DIVIDE(CurrentSales - PreviousSales, PreviousSales),
        BLANK()  // This handles the scenario where there are no previous year sales to compare against.
    )
```

#### Dashboard Design & Visualization

- Mockup Design
- Designed three themed dashboards in Power BI Desktop:
  - Executive Overview (sales trends & KPIs)
  - Channel & Brand Analysis
  - Profit Margin Analysis
- Incorporated slicers (e.g., Year, Channel, Product) for interactivity.
- Used best practices for visual hierarchy, color consistency, and user-friendly layout.

#### Publishing and Collaboration  
- Published the reports to Power BI Service for stakeholder access and automated refresh.
- Set up appropriate workspace permissions and dashboard sharing.

#### Documentation & Version Control  

- Documented the entire process including the model schema, DAX measures, and dashboard usage instructions.
- Uploaded final .pbix file, SQL scripts, and documentation to GitHub for version control and public portfolio presentation.

#### Review & Iteration  

- Collected feedback from stakeholders and refined visuals and measures accordingly.
- Monitored performance and usability, making adjustments to filters, visuals, and tooltips for clarity.

#  
### DASHBOARD_1: COMPETITIVE SALES CHANNEL ANALYSIS REPORT (Executive Overview)

FOCUS: High-level sales performance comparison across sales channels (Store, Online, Reseller Catalog) overall, in 2007, 2008, and 2009.  

##### KPI CARDS(Top Section):  

Total Sales (Multiyear/All Channels): £12bn  
Indicates the overall revenue generated by sales activities. Where the Revenue accounted for is the revenue generated before sales amount impacted.  

Store: £6.9bn | YoY Change: -£297.2M (2009 - 2008) | YoY Change: -£554.7M (2008 - 2007)  
Leads in sales but showing a significant YoY drop ( over quater a billion pound) indicating saturation or shifting customer behavior.  

Online: £2.7bn | YoY Change: £14.1M (2009 - 2008) | YoY Change: £147.7M (2008 - 2007)  
Takes the next lead when it comes to sales and is gaining traction with a healthy YoY, suggesting success in digital tranformation or e-commerce growth.  

Reseller: £1.7bn | YoY Change: -£56.4M (2009-2008) | YoY Change: £29.0M (2008 - 2007)  
This has modest sales but experience a reversed growth as indicated in the YoY sales different.

Catalog: £1.1bn | YoY Change: -£31.2M (2009 - 2008) | YoY Change: -£72.6M (2008 - 2007)
catalog  sales are the weakest performer both in volume and growth - sales decling with no recovery throughout the year.

#### Channel Breakdown: (Year 2008)  
- Store: 559%
- Online: 22.7%
- Reseller: 14.6%
- Catalog: 8.4%

Store is the dominant channel (£2.2bn, 55.9% of total sales), followed by Online (£0.9bn), Reseller (£0.6bn), and Catalog (£0.3bn).

#### Channel-by-Brand Breakdown: 
Insights: Contoso and Fabrikam are the leading brands across all channels.  

### Product-Channel Performance:  
- The top Products by sales are all sales from Store channel (Camcorders, Projectors, Refigirator and so on) except couples from online channel (Washer & Dryer and Camcorders). While worst products sales are more partain to Reseller and Catologs channels.

- Certain durable goods (e.g., Refrigerators, Laptops) are consistently strong performers across channels, especially in stores.



Store sales dominate brand revenue, particularly Contoso (£1.5bn) and Fabrikam (£1.3bn).

Online brand performance is more fragmented, with smaller brands like Litware and Proseware performing better in niche areas.

🗺️ Geographic Distribution:
North America is the highest-contributing region across all channels, followed by Europe and Asia.

Catalog sales are notably strong in North America, but weak in other continents.

Online presence is more globally distributed, especially in Asia and Europe.

🧩 Strategic Takeaways:
Focus online growth in Asia and Europe, where penetration is increasing.

Explore catalog consolidation or localization in North America to maintain profitability.

Invest in top-performing brands (Contoso, Fabrikam) while evaluating long-tail brands for improvement or removal.

💹 Dashboard 3: Profit Margin Analysis
Focus: Deep-dive into Catalog profitability by product, geography, and time.

🔍 Key Insights:
Catalog Profit Margin: 4.69%, which is low relative to typical retail benchmarks.

Top Profitable Product Subcategories:

Laptops, Camcorders, Projectors, and Refrigerators are the highest-margin categories.

Low-margin items include Bluetooth Headsets, MP3 Players, and Movie DVDs, indicating potential overstock or price competition.

🌍 Profitability by Region:
North America is the only region with a healthy Catalog margin, implying optimized logistics, pricing, or customer base.

Catalog underperforms in Europe and Asia, possibly due to distribution costs or lower product appeal.

📈 Sales and ROI Trend:
ROI fluctuates seasonally—while sales volumes peak in mid-year (May to August), margins don't increase proportionately, indicating possible discounting or increased returns.

ROI stability can be enhanced by revising promotional timing or improving return policies.

🧩 Strategic Takeaways:
Reposition the Catalog strategy to focus only on high-ROI products (e.g., Laptops, Camcorders).

Consider sunsetting underperforming Catalog categories or merging them into digital/online offerings.

Regionalize the Catalog—focus on North America, and reevaluate Europe and Asia for feasibility.

🧩 Final Strategic Recommendations:
Reallocate Marketing Spend:

Shift from Catalog to Online and Store—where either ROI or volume is growing.

Target promotions around peak Store months and growing Online regions.

Product Mix Optimization:

Double down on high-margin categories like Laptops and Camcorders across channels.

Reassess or bundle low-performing subcategories (e.g., Bluetooth Headsets).

Geographic Strategy:

Expand Online efforts in Asia and Europe.

Restructure Catalog operations to focus on North America only.

Invest in Data-Driven Personalization:

Use regional and brand-level insights to personalize offers and stock decisions.

Monitor Channel ROI & Adjust:

Continuously monitor YoY trends and adjust product-channel alignment quarterly.




 
  









