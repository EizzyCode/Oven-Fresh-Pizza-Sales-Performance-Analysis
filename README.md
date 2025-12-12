# OVEN FRESH PIZZA SALES PERFORMANCE ANALYSIS

<img width="1100" height="618" alt="image" src="https://github.com/user-attachments/assets/9bdeb047-0be3-44ae-8400-920f319aa625" />

## INTRODUCTION
The pizza industry represents a significant segment of the food service sector, with businesses continuously seeking data-driven insights to optimize operations and maximize profitability. Understanding sales patterns, customer preferences, and operational trends is crucial for making informed business decisions in this competitive market.

This analysis examines sales data from Oven Fresh Pizza to uncover actionable insights that drive strategic decision-making. The scope encompasses revenue performance, order patterns, product preferences, and temporal trends. These insights are critical for restaurant management, operations, and marketing teams seeking to optimize inventory, staffing, menu offerings, and promotional strategies.

## PROJECT OVERVIEW
The primary objective of this analysis is to examine pizza sales data to identify patterns, trends, and opportunities for business optimization. This project demonstrates end-to-end data analysis skills by combining Microsoft Excel for data preparation, PostgreSQL for advanced SQL-based exploratory data analysis, and Microsoft Power BI for interactive dashboard visualization and business intelligence delivery.

By analyzing temporal patterns, product preferences, category distributions, and revenue metrics across multiple dimensions, this project provides actionable intelligence for strategic planning and operational improvements. The integrated approach showcases proficiency in the complete data analysis workflow — from raw data cleaning and database design through complex SQL querying to dynamic visualization development — skills essential for modern data analyst and business intelligence roles.

### Problem Statement
Restaurant management requires detailed insights into sales performance to optimize operations, manage inventory effectively, and maximize revenue. Understanding which products drive sales, when customers place orders, and how different pizza categories and sizes perform is essential for resource allocation, staffing decisions, and menu optimization. This analysis addresses the critical need for data-driven insights that inform operational and strategic decisions.

**Key questions driving this analysis include:**

* What are the overall revenue performance and key sales metrics?
* How do order volumes vary by day of week and hour of day?
* Which pizza categories and sizes generate the highest sales?
* Which specific products are the top and bottom performers?
* What patterns can inform inventory, staffing, and promotional strategies?
  
Understanding these relationships is essential for optimizing operations, reducing waste, improving service during peak times, and maximizing profitability through strategic menu engineering and data-driven decision making.

## DATASET OVERVIEW
The analysis utilizes a comprehensive transactional dataset from Oven Fresh Pizza covering the full year 2015, containing detailed sales information across all pizza categories and sizes.

### Primary Data Source
**Dataset:** Pizza Place Sales Dataset.  
**Source:** Kaggle — https://www.kaggle.com/datasets/mysarahmadbhat/pizza-place-sales.  
**Structure:** Four relational tables (Orders, Order Details, Pizzas, Pizza Types) with order IDs, dates, times, pizza types, sizes, quantities, prices, categories, and ingredients.  

### Key Metrics Analyzed
* **Revenue Metrics:** Total revenue of $817,860 representing complete annual sales performance, average order value of $38.31 indicating customer spending per transaction, total pizzas sold of 49,574 units tracking volume, total orders of 21,350 measuring transaction frequency, and average pizzas per order of 2.32 showing typical order composition and upselling effectiveness.

* **Temporal Patterns:** Daily order trends across all seven days of the week revealing peak demand days (Friday at 3,500 orders) and slower periods (Sunday at 2,600 orders), plus hourly order patterns throughout operating hours identifying two distinct demand peaks at lunch (12–1pm) and dinner (5–6pm) critical for staffing and preparation planning.

* **Categories:** Four pizza categories analyzed for sales distribution — Classic pizzas showing traditional favorites, Supreme pizzas featuring premium toppings, Veggie pizzas catering to vegetarian preferences, and Chicken pizzas highlighting poultry-based options. Performance measured by both sales volume (total pizzas sold) and revenue contribution (percentage of total sales).

* Sizes:** Five size options tracked across the menu — Large pizzas dominating at 45.89% of sales, Medium pizzas representing 30.49%, Small pizzas at 21.77%, with XL (1.72%) and XXL (0.12%) sizes showing minimal adoption. Distribution analysis reveals customer value perception and optimal pricing strategy opportunities.

* **Products:** Individual pizza performance identifying top sellers like The Classic Deluxe Pizza (2,500 units), The Barbecue Chicken Pizza, The Hawaiian Pizza, The Pepperoni Pizza, and The Thai Chicken Pizza (all approximately 2,400 units each), plus bottom performers requiring menu optimization or promotional intervention to improve sales velocity.

## TOOLS AND TECHNOLOGIES
This analysis leveraged Microsoft Excel for data cleaning, PostgreSQL for exploratory data analysis, and Power BI for interactive dashboard visualization.

### Microsoft Excel: Data Cleaning and Preparation
Excel served as the initial data preparation platform, performing critical quality assurance before database import.

* Conducted comprehensive data profiling to identify missing values, duplicate records, and inconsistent formatting across the four CSV files.

* Standardized date formats to ensure PostgreSQL compatibility, normalized time values for accurate temporal analysis, and unified text casing for pizza names and categories to prevent duplicate groupings in analysis.

* Applied data validation to verify that all foreign key relationships would maintain integrity during database import, confirming that every pizza_id in order details existed in the pizzas table, and every pizza_type_id in pizzas existed in the pizza types table. This validation prevented orphaned records and ensured accurate join operations in subsequent SQL analysis.

### PostgreSQL: Exploratory Data Analysis and Database Design
PostgreSQL served as the analytical engine, with comprehensive database design and complex SQL queries driving all exploratory analysis and business intelligence generation.

**Database Schema Design and Implementation**
Designed and implemented a normalized relational database with four interconnected tables, demonstrating understanding of database architecture principles:

* **Orders Table:** Created with order_id as PRIMARY KEY, plus date and time fields. This table serves as the transaction header, capturing when each order occurred.
  
  <img width="683" height="160" alt="image" src="https://github.com/user-attachments/assets/ea1f3888-44fe-4e3d-b110-17cd32de0947" />

* **Pizza_Types Table:** Master reference table with pizza_type_id as PRIMARY KEY, containing name, category, and ingredients for each unique pizza type.

<img width="722" height="209" alt="image" src="https://github.com/user-attachments/assets/59d53735-df83-4a3b-a1c6-a16463f43113" />

* **Pizzas Table:** Contains pizza_id as PRIMARY KEY and pizza_type_id as FOREIGN KEY linking to Pizza_Types table. Includes size and price fields for each pizza variant, enabling price-based revenue calculations.

<img width="832" height="221" alt="image" src="https://github.com/user-attachments/assets/9c24a7c9-561e-4497-a547-8df9257ffe99" />

* **Order_Details Table:** Designed as the transaction line-item table with order_details_id, linking to Orders via order_id FOREIGN KEY and to Pizzas via pizza_id FOREIGN KEY. The quantity field tracks items per order line.

<img width="806" height="241" alt="image" src="https://github.com/user-attachments/assets/3ead8962-3c47-459e-9c3f-ca1d70981a27" />

This schema design demonstrates proper normalization (avoiding data redundancy), referential integrity through foreign key constraints, and logical separation of transactional data (orders, order details) from reference data (pizzas, pizza types).

**Data Import and Validation**  
After table creation, imported cleaned CSV data using PostgreSQL’s COPY command, then validated import success through record count verification and foreign key constraint testing. Confirmed that all relationships maintained integrity with zero orphaned records.

**SQL Analysis — Key Performance Indicators**  
Developed comprehensive SQL queries utilizing multi-table JOINs, aggregate functions, and calculated fields:

* **Total Revenue:** Used RIGHT JOIN between Pizzas and Order_Details, multiplying quantity by price at transaction level, then aggregating with SUM = $817,860
* **Average Order Value:** Calculated total revenue divided by COUNT(DISTINCT Order_ID) with ROUND function for clean decimal = $38.31
* **Total Pizzas Sold:** Simple SUM aggregation of quantity field from order_details = 49,574 pizzas
* **Total Orders:** COUNT of order_id from orders table = 21,350 orders
* **Average Pizzas Per Order:** Total quantity divided by distinct order count = 2.32 pizzas/order

**SQL Analysis — Business Intelligence Questions**  
Demonstrated advanced SQL techniques including date/time functions, subqueries, and complex JOINs:

* **Daily Trends:** Used TO_CHAR(date, ‘Day’) with TRIM to extract day names, GROUP BY for aggregation, revealing Friday peak (3.5K orders) vs Sunday low (2.6K orders)
* **Hourly Trends:** Applied EXTRACT(HOUR FROM time) to parse hours, identifying bimodal demand at lunch (12–1pm, 2.5K orders) and dinner (5–6pm, 2.4K orders)
* Category Sales Percentage:** Multi-table JOIN (Pizzas → Pizza_Types → Order_Details) with subquery calculating total revenue as denominator, showing balanced distribution: Classic (26.91%), Supreme (25.46%), Chicken (23.96%), Veggie (23.68%)
* Size Sales Percentage:** Similar structure grouped by size instead of category, revealing Large dominance at 45.89%, Medium (30.49%), Small (21.77%)
* **Category Volume:** Aggregated SUM(quantity) by category showing Classic leading with 14.9K pizzas, Supreme (12K), Veggie (11.6K), Chicken (11.1K)
* **Top 5 Performers:** ORDER BY DESC with LIMIT 5 identifying best sellers: Classic Deluxe (2.5K), Barbecue Chicken (2.4K), Hawaiian (2.4K), Pepperoni (2.4K), Thai Chicken (2.4K)
* **Bottom 5 Performers:** ORDER BY ASC with LIMIT 5 revealing underperforming products needing attention.
  
This SQL work demonstrates proficiency in database design, complex query construction, multi-table relationships, aggregate functions, subqueries, and date/time manipulation — essential skills for data analyst roles.

### Microsoft Power BI: Interactive Dashboard Development**  
Power BI transformed SQL analysis into an interactive visualization platform, with strategic evolution from CSV imports to direct database connectivity.

* **Initial Approach and Learning:** Initially exported each SQL query result as CSV and imported into Power BI. This created isolated tables preventing cross-filtering, when selecting Friday, hourly trends couldn’t filter accordingly because data existed in disconnected tables.

* **Optimized Solution:** Removed CSV imports and connected Power BI directly to PostgreSQL database, importing all four tables with automatic relationship recognition. This enabled full dashboard interactivity and dynamic filtering across all dimensions.

* **DAX Calculations and Measures**  
Developed comprehensive DAX (Data Analysis Expressions) measures to calculate total revenue, average order value, total pizzas sold, average pizzas per order, and percentage distributions across categories and sizes.

## METHODOLOGY
The analysis employed a systematic three-stage approach demonstrating end-to-end data analysis proficiency: Excel for data preparation and quality assurance, PostgreSQL for database design and SQL-driven exploratory analysis, and Power BI for DAX-based calculations and interactive dashboard visualization.

### Stage 1: Data Preparation (Excel)
Began with four CSV files containing raw transactional data. Performed comprehensive data profiling to assess quality, identifying and resolving issues including inconsistent date/time formats that would break PostgreSQL imports, varying text case that would create duplicate category groupings, missing values that could skew aggregations, and potential duplicate records requiring deduplication.  

Validated relational integrity before database import by confirming that all pizza_id values in order details existed in pizzas table, and all pizza_type_id values in pizzas existed in pizza types table. This pre-import validation prevented foreign key constraint violations and ensured accurate join operations in subsequent SQL analysis.

### Stage 2: Database Design and SQL Analysis (PostgreSQL)
Designed normalized database schema with four interconnected tables, establishing primary keys (order_id, pizza_id, pizza_type_id) and foreign key relationships (Order_Details → Orders, Order_Details → Pizzas, Pizzas → Pizza_Types). This schema demonstrates understanding of referential integrity, data normalization, and logical entity separation.

Executed comprehensive SQL analysis across 12 business questions, progressing from basic aggregations (revenue, order counts) through temporal analysis (date/time functions extracting days and hours) to advanced analytics (multi-table JOINs with subqueries for percentage calculations). Each query was systematically developed, tested for accuracy, and documented for reproducibility.

Initial approach involved exporting each SQL query result as CSV for Power BI import. However, this created isolated datasets preventing the cross-filtering functionality essential for interactive dashboards. This discovery drove the strategic pivot to direct database connectivity.

### Stage 3: Visualization and DAX Development (Power BI)
Established direct PostgreSQL connection in Power BI, importing all four tables with automatic relationship mapping. Developed comprehensive DAX measures recreating SQL calculations in Power BI’s context-sensitive environment, enabling dynamic recalculation as users apply filters.

Created calculated columns (Day of Week, Order Hour) for dimensional analysis and percentage measures using CALCULATE and ALL functions for proper context manipulation. Designed dashboard layout prioritizing KPIs for immediate visibility, followed by temporal patterns for operational insights, concluded by product performance for strategic decisions.

This methodology showcases the complete data analysis workflow from raw data through database implementation to interactive business intelligence delivery.

##DASHBOARD ANALYSIS
The Power BI dashboard presents a comprehensive view of sales performance through strategically designed visualizations that reveal operational patterns and business opportunities.

### Key Performance Indicators (Top Cards)
Five prominent cards display critical metrics: Total Revenue ($817.86K), Average Order Value ($38.31), Total Pizzas Sold (49,574), Total Orders (21,350), and Average Pizzas Per Order (2.32). These KPIs immediately communicate business health, with the $38.31 average order value and 2.32 pizzas per order indicating healthy transaction sizes and successful upselling.

<img width="1100" height="113" alt="image" src="https://github.com/user-attachments/assets/0a1311c0-0e30-49cb-be8f-0f8b96b67c01" />

### Hourly Order Trends (Area Chart)
The area chart reveals a clear bimodal demand pattern with two distinct peaks: lunch rush (12–1pm reaching ~2.5K orders) and dinner rush (5–6pm reaching ~2.4K orders). Orders gradually increase from 9am, peak at midday, decline mid-afternoon, surge again for dinner, then taper after 7pm. This pattern creates clear implications for staffing optimization and kitchen preparation schedules.

<img width="664" height="294" alt="image" src="https://github.com/user-attachments/assets/dcc3a9c6-74c3-4fcf-91c9-7ad959784175" />

### Total Orders by Day (Horizontal Bar Chart)
Friday dominates with 3.5K orders, followed by Thursday and Saturday (~3.2K each). Wednesday and Tuesday show moderate volumes (~3.0K), while Monday (~2.8K) and Sunday (~2.6K) represent the slower days. The 35% difference between Friday and Sunday presents both operational challenges and marketing opportunities for demand smoothing.

<img width="680" height="453" alt="image" src="https://github.com/user-attachments/assets/7bce046f-a48f-4fef-a95a-81bd1877a4bc" />

### Percentage of Sales per Category (Donut Chart)
Category distribution is remarkably balanced: Classic (26.91%), Supreme (25.46%), Veggie (23.68%), and Chicken (23.96%). This near-equal split indicates diverse customer preferences with no dominant category, requiring comprehensive inventory management across all pizza types rather than focusing on a single category.

<img width="504" height="440" alt="image" src="https://github.com/user-attachments/assets/46d6b3f6-a2af-48a3-b63e-3d5b5f78138c" />

### Top 5 Most Sold Pizza (Horizontal Bar Chart)
The Classic Deluxe Pizza leads at 2.5K units, followed closely by The Barbecue Chicken Pizza, The Hawaiian Pizza, The Pepperoni Pizza, and The Thai Chicken Pizza (all ~2.4K units). These five products represent significant revenue concentration, indicating that a small menu subset drives substantial volume.

<img width="1040" height="441" alt="image" src="https://github.com/user-attachments/assets/52df38b1-2658-4502-a30c-bd5ad1db8d12" />

### Pizzas Sold by Category (Vertical Bar Chart)
Volume analysis shows Classic leading with 14.9K pizzas, followed by Supreme (12.0K), Veggie (11.6K), and Chicken (11.1K). Despite Classic’s lead, the relatively narrow 26% gap between highest and lowest categories confirms the need for balanced ingredient stocking across all categories.

<img width="681" height="451" alt="image" src="https://github.com/user-attachments/assets/790adb1c-39fb-4ec1-9ef9-84c3ebf6224b" />

### Percentage of Sales per Size (Donut Chart)
Large pizzas dominate at 45.89% of sales — nearly double Medium (30.49%) and far exceeding Small (21.77%). XL (1.72%) and XXL (0.12%) represent minimal volume, suggesting customers perceive Large as optimal value. This clear preference has major implications for dough preparation, ingredient portioning, and operational focus.

<img width="514" height="474" alt="image" src="https://github.com/user-attachments/assets/bf0c1fd7-716a-4067-93f0-ba305fe9cdd2" />

## KEY OBSERVATIONS

### Strong Sales Performance with Healthy Transaction Economics
$817.86K in revenue from 21,350 orders yields a $38.31 average order value, significantly above typical quick-service transaction values. With 49,574 pizzas sold averaging 2.32 per order, transaction sizes indicate successful upselling strategies and family-oriented purchasing patterns. This healthy order composition suggests customers frequently add second pizzas, appetizers, or beverages, creating robust per-transaction revenue that supports profitability and provides foundation for incremental growth through targeted upselling programs.

### Bimodal Demand Pattern Requires Strategic Resource Allocation
Two distinct peaks at lunch (12–1pm, 2.5K orders) and dinner (5–6pm, 2.4K orders) create predictable high-demand windows requiring maximum kitchen capacity and service staff. Morning period (9–11am) shows minimal activity under 1,000 orders, while late evening (post-9pm) drops below 700 orders, presenting clear opportunities for labor optimization. The 3-hour gap between lunch and dinner peaks (2–5pm at ~1,500 orders) provides ideal preparation window for evening rush. This bimodal pattern enables data-driven staffing schedules aligning labor costs directly with revenue-generating periods while minimizing waste during low-demand hours.

### Friday-Sunday Gap Presents Revenue Opportunity
Friday’s 3.5K orders versus Sunday’s 2.6K represents a 35% variance — the largest day-to-day gap in the weekly pattern. Thursday and Saturday cluster near 3.2K orders, while Monday through Wednesday hover around 2.8–3.0K. This concentration creates operational stress on peak days (potentially leading to longer wait times or service quality issues) while leaving Sunday significantly underutilized with idle capacity. The consistency of this pattern across the year makes it highly predictable and actionable for targeted interventions. Sunday’s position as the slowest day suggests missed opportunity for family dining occasions and weekend carryover demand that competitors may be capturing.

### Balanced Category Performance Requires Comprehensive Inventory
With only 3.23 percentage points separating Classic (26.91%) and Veggie (23.68%), no category dominates customer preferences. This remarkably even distribution across Classic, Supreme, Chicken, and Veggie indicates diverse customer base with varying taste profiles successfully served by current menu variety. Unlike businesses where a single category drives 50%+ of sales, this balance prevents over-reliance on any single pizza type but necessitates maintaining full ingredient range across all categories. The near-equal distribution also suggests that promotional efforts boosting one category won’t cannibalize others significantly, creating flexible marketing opportunities without risk of unbalancing inventory.

### Large Pizza Dominance Shapes Operational Focus
At 45.89% of sales, Large pizzas nearly double Medium sales (30.49%) and exceed Small by more than 2:1. The dramatic drop-off to XL (1.72%) and XXL (0.12%) suggests customers perceive Large as the value sweet spot — offering sufficient servings for families/groups without premium pricing of extra-large sizes. This dominance creates operational efficiency opportunities through standardization, as nearly half of all production focuses on a single size. The pattern also indicates pricing strategy success, with Large positioned at optimal value point driving customer choice. Medium maintains respectable 30% share suggesting couples or smaller groups, while Small’s 22% likely serves individual/lunch customers.

### Top Performers Drive Revenue Concentration
Five pizzas (Classic Deluxe at 2.5K, followed by Barbecue Chicken, Hawaiian, Pepperoni, and Thai Chicken at ~2.4K each) represent substantial sales concentration, likely accounting for 20–25% of total volume despite representing small fraction of total menu SKUs. This follows classic Pareto principle where minority of products drive majority of results. The clustering of top performers around 2,400–2,500 units (versus bottom performers potentially under 500 units) reveals significant performance gaps. Classic Deluxe’s leadership position makes it the signature product warranting premium ingredient quality and consistent execution. The presence of diverse flavors in top 5 (classic, barbecue, Hawaiian, pepperoni, Thai) indicates customer appreciation for variety rather than single dominant flavor profile.

### Category Volume Reveals Inventory Balance Requirements
Classic’s 14.9K pizzas lead Supreme (12K), Veggie (11.6K), and Chicken (11.1K), but the 26% gap between highest and lowest is relatively narrow considering Classic’s 1st place position. This distribution pattern means ingredient purchasing must maintain breadth across all categories — can’t simply focus procurement on Classic ingredients. The 3,800-unit difference between Classic and Chicken seems significant in absolute terms but represents balanced demand requiring sophisticated inventory management preventing both stockouts and spoilage across full ingredient spectrum. Production scheduling must accommodate all categories daily rather than rotating category focus throughout week.

## STRATEGIC RECOMMENDATIONS

### Operational Efficiency and Staffing Optimization
* **Peak-Hour Staffing Strategy:** Deploy maximum kitchen and service staff during the 12–1pm lunch rush and 5–7pm dinner rush when order volumes peak at 2,400–2,500 orders per hour. The SQL hourly analysis provides precise timing for staffing ramp-up — begin increasing staff at 11am for lunch preparation and 4pm for dinner preparation. Reduce staffing during the 9–11am morning period and post-9pm when volumes drop below 1,000 orders, potentially reducing labor costs by 15–20% while maintaining service quality during revenue-generating periods. Consider implementing split shifts or staggered schedules that concentrate labor during demand peaks while minimizing idle time.

* **Leverage Preparation Window:** Use the 2–5pm moderate period (approximately 1,500 orders per hour) systematically for dinner rush preparation including dough portioning, ingredient prep stations setup, and advance preparation of high-volume items identified through SQL analysis. This strategic use of the mid-afternoon valley ensures kitchen readiness for the dinner surge without compromising lunch service quality. Implement standardized prep protocols specific to this window that position the operation for smooth evening execution.

* **Day-Specific Labor Planning:** Implement Friday-specific protocols to handle the 35% higher volume (3,500 orders) versus Sunday (2,600 orders), including additional staff, expanded prep areas, or adjusted break schedules. Use SQL daily patterns to create precise day-of-week staffing schedules that align labor costs with actual demand rather than flat weekly averages. Consider differential hourly rates or shift premiums for Friday coverage to ensure adequate staffing during this critical revenue day.

### Menu Engineering and Product Strategy
* **Promote Top-Performer Visibility:** Feature The Classic Deluxe, Barbecue Chicken, Hawaiian, Pepperoni, and Thai Chicken pizzas (2,400–2,500 units each identified through SQL analysis) in prominent menu positions both physical and digital. These proven sellers should anchor promotional bundles, combo deals, and featured item marketing. Consider “Staff Favorites” or “Customer Top 5” branding that leverages their popularity while creating social proof for new customers. Ensure these items never experience stockouts as they represent core revenue drivers.

* **Address Bottom-Performer Portfolio:** SQL analysis reveals specific underperforming pizzas requiring strategic intervention. For each bottom performer, conduct root cause analysis — is it poor marketing/visibility, unappealing flavor profile, higher price point, or ingredient combinations that don’t resonate? Consider limited-time reformulation tests, promotional pricing experiments, or strategic menu removal if improvements don’t materialize. Reducing menu complexity by eliminating persistent underperformers can streamline operations, reduce ingredient waste, and simplify kitchen execution without meaningful revenue impact.

* **Optimize for Large Pizza Economics:** With Large pizzas representing 45.89% of sales (SQL size analysis), ensure that dough preparation, ingredient purchasing, box inventory, and even oven capacity prioritize this dominant size. Consider value-focused promotional pricing that encourages Large selection (e.g., “Large at Medium price” limited offers) to improve operational efficiency through increased standardization. Evaluate whether Medium and Small pricing adequately reflects portion differences or if pricing adjustments could further shift demand toward the operationally efficient Large size.

* **Menu Mix Optimization:*** Analyze margin contribution by pizza (not just volume) to identify whether top sellers are also top profit generators. If high-volume items have compressed margins, consider strategic price increases on proven sellers where demand is relatively inelastic. Conversely, if low-volume items carry premium margins, evaluate targeted marketing to boost their sales rather than elimination.

### Revenue Growth and Marketing Initiatives
* **Sunday Sales Activation Campaign:** Address Sunday’s position as weakest day (2,600 orders vs Friday’s 3,500) through targeted promotional interventions. Consider “Sunday Family Feast” bundles offering multiple pizzas at promotional pricing, religious institution partnerships for post-service family dining, or “Sunday Funday” campaigns targeting families seeking weekend meal solutions. A 20% increase in Sunday orders (adding 520 orders at $38.31 AOV) could generate approximately $63,000 in incremental annual revenue while better utilizing fixed operational capacity.

* **Category-Rotating Promotions:** With balanced performance across all categories (23.68% to 26.91% per SQL percentage analysis), implement monthly rotating category features that maintain customer engagement across the full menu. January focuses on Classic category with “Traditional Favorites Month,” February highlights Supreme as “Premium Pizza Month,” etc. This approach maintains interest across all pizza types without cannibalizing other categories, while creating recurring promotional calendar that customers anticipate.

* **Order Value Enhancement Programs:** Current 2.32 pizzas per order presents clear upselling opportunity. Implement “Add a Second Pizza for $X” offers, where $X represents marginal cost plus modest markup (e.g., $8–10 for second pizza). Train staff/optimize online ordering to suggest second pizza selections based on first choice. Create combo deals bundling popular items from top-performer analysis (e.g., “Classic Deluxe + Barbecue Chicken for $Y”). Even modest 5% increase in average pizzas per order (from 2.32 to 2.44) would yield substantial annual revenue gains.

* **Strategic Pricing Review:** Analyze pricing elasticity on top performers to determine whether modest price increases (3–5%) on proven high-demand items would impact volume significantly. Given Classic Deluxe’s 2,500-unit leadership, even $0.50 price increase generates $1,250 incremental revenue if volume remains stable.

### Inventory Management and Cost Optimization
* **Day-Specific Inventory Ordering:** Use SQL daily pattern data (Friday 3,500 vs Sunday 2,600 orders representing 35% variance) to develop precise day-specific ingredient ordering that minimizes waste while ensuring peak-day availability. Calculate ingredient requirements based on actual day-of-week demand patterns rather than using flat weekly averages. For example, if Friday requires 35% more dough, cheese, and toppings than Sunday, ordering systems should reflect these specific needs. This precision can reduce food waste by 10–15% while preventing stockouts during peak demand, directly improving cost of goods sold percentages.

* **Size-Aligned Ingredient Portioning:** Match ingredient preparation and portioning to the 46% Large, 30% Medium, 22% Small distribution revealed through SQL analysis. If current prep assumes equal distribution across sizes, it creates waste on Small ingredients while potentially causing Large shortages. Implement prep protocols that produce pizza-size-specific ingredient quantities in proportions matching actual sales patterns, reducing overproduction waste while ensuring sufficient availability of high-demand Large pizza components.

* **Focus Premium Ingredients on Volume Drivers:** Allocate highest-quality or specialty ingredients to the top 5 performing pizzas (Classic Deluxe, Barbecue Chicken, Hawaiian, Pepperoni, Thai Chicken) that drive 20–25% of volume. Ensure these menu stars maintain consistent quality that builds repeat business. For slower-moving items, evaluate whether premium ingredient upgrades would boost sales or if cost optimization opportunities exist without significantly impacting customer satisfaction on low-volume products.

* **ABC Inventory Classification:** Implement inventory management system classifying ingredients by consumption rate and cost — A items (high volume/cost like cheese, dough, pepperoni), B items (moderate volume/cost), C items (low volume/specialty toppings). Apply tightest controls and most frequent ordering to A items while accepting higher safety stock on low-cost C items to prevent specialty pizza stockouts.  

## CONCLUSION
This analysis of Oven Fresh Pizza reveals a successful operation with $817.86K in annual revenue, healthy transaction economics ($38.31 AOV, 2.32 pizzas per order), and clear operational patterns creating significant optimization opportunities.

The combination of Excel for data cleaning, PostgreSQL for SQL-driven exploratory analysis, and Power BI for interactive visualization enabled comprehensive examination of sales patterns. The SQL analysis provided precise insights through sophisticated queries including multi-table JOINs, date/time manipulation, and percentage calculations across 12 business questions. The evolution from CSV exports to direct database connection in Power BI demonstrated critical lessons about maintaining data relationships for full dashboard interactivity.

Key findings reveal bimodal demand peaks (lunch 12–1pm, dinner 5–6pm), Friday dominance (3.5K orders vs Sunday’s 2.6K), balanced category performance (all within 24–27%), and Large pizza preference (46% of sales). These patterns inform strategic recommendations for peak-hour staffing optimization, Sunday promotional campaigns, and inventory alignment with actual demand.

The interactive dashboard provides ongoing business intelligence for monitoring performance and making data-driven decisions that enhance operational efficiency, increase revenue, and strengthen competitive positioning in the pizza market.










  

