Access to Drinking Water  Data Analysis Project
Project Overview
This project investigates global access to safe and affordable drinking water, in alignment with the United Nations Sustainable Development Goal 6 (SDG 6: Clean Water and Sanitation).
Using the WHO/UNICEF JMP (Joint Monitoring Programme) dataset (2020), the analysis explores patterns of water access across:
Geography (national, urban, rural)
Population size
Income groups (based on GNI per capita)
Levels of water service (basic, limited, unimproved, surface)
The findings are visualized in Power BI dashboards, supported by data cleaning, transformation, and exploratory analysis.
Dataset Description
The dataset contains 16 original features describing water access and population characteristics for different countries.
Key Features
name → Country/region
year → Year of observation
pop_n → National population (000s)
pop_u → Urban population share (%)
wat_bas_n/r/u → Basic service access (national/rural/urban)
wat_lim_n/r/u → Limited service access
wat_unimp_n/r/u → Unimproved service access
wat_sur_n/r/u → Surface water reliance
Additional derived features were engineered during the project (e.g., population in millions, rounded urban/rural shares, calculated totals, other calculated columns and measures using DAX formulas)
Data Transformation Summary
To prepare the WHO/UNICEF JMP dataset (2000–2020) for analysis, I carried out several transformation steps:
Data structuring and cleaning – Sorted the dataset by country and year, ensured consistency in country names, and created a y_diff column to calculate the gap between recorded years. Duplicate and erroneous rows were identified and removed.
Annual Rates of Change (ARC) – Calculated new features ARC_n, ARC_r, and ARC_u to measure yearly changes in access to basic water services across national, rural, and urban populations. Null and error values were handled using conditional and error-checking formulas.
Rounding and full-access flags – Created rounded versions of access indicators (wat_bas_n/r/u) and derived new columns (ARC_n_full, ARC_r_full, ARC_u_full) to identify countries with full (≈100%) access.
Comparing rural vs urban progress – Engineered a new feature ARC_diff to capture the difference in progress rates between rural and urban populations, supported with distribution analysis (e.g., histograms).
Regional classification – Merged the dataset with an external Regions.csv file to add a region variable. This enabled grouping and comparison of ARCs across world regions.
Summary and validation – Produced summary statistics (averages, minimums, maximums) and counts of countries by ARC category (null, zero, negative, positive). These checks ensured data quality and prepared the dataset for visualization in Power BI.
As a result of these steps, the dataset expanded from the original 16 features to 28 engineered features, making it more suitable for exploring geographic, temporal, and socio-economic patterns in access to drinking water.
Querying the Data Summary Using (Exploratory Data Analysis) EDA
To interrogate the Maji Ndogo water services database, I applied SQL queries in Jupyter Notebook and MySQL Workbench, focusing on uncovering usage patterns, water quality issues, and data inconsistencies.
Database exploration and schema mapping – Used DESCRIBE and SHOW TABLES queries to understand table structures (water_sources, visits, locations, water_quality, well_pollution) and their foreign key relationships (e.g., source_id).
Sampling and record inspection – Queried each table (SELECT * FROM … LIMIT n) to inspect sample records, validate column meanings, and confirm join relationships across tables.
Analyzing water sources – Wrote aggregation queries (COUNT, GROUP BY) to classify and quantify water source types (rivers, wells, shared taps, taps in homes, broken taps). This highlighted the reliance on a limited number of shared taps.
Investigating visits and access – Queried the visits table with filtering and sorting (WHERE, ORDER BY) to examine queue times. Identified extreme waiting periods (8+ hours), which pointed to capacity issues at shared taps.
Assessing water quality – Queried subjective_quality_scores and joined them with visit records. Found inconsistencies where sources labeled “clean” were frequently revisited, raising data reliability concerns.

Pollution data validation – Inspected well_pollution with LIKE and conditional update queries (UPDATE … SET) to correct mislabeled wells where “Clean” entries still had measurable biological contamination.
Error and anomaly detection – Designed queries to flag duplicates, null values, and conflicting classifications. Applied string manipulation and conditional logic (CASE, IFNULL) to standardize records for consistency.
By leveraging SQL joins, aggregations, filters, and update operations, I was able to clean, validate, and interrogate the relational database directly. Conducting this process in both Jupyter Notebook (for reproducible querying) and MySQL Workbench (for schema inspection and testing) showcased my ability to combine database management, querying skills, and analytical reasoning.
Click here to download the codes used. You can open with either Jupyter Notebook(recommended) or Visual Studio


Business Intelligence & Visualization Summary
I moved into Power BI to transform the cleaned dataset into an interactive reporting solution. My focus was on creating relationships, building measures, refining the data model, and creating dashboards that could tell a clear story about global access to safe drinking water. 
Project Context Part 1: Understanding Maji Ndogo’s Water Crisis
To gain a deeper understanding of the water access challenges in Maji Ndogo, I developed a series of interactive Power BI dashboards that visualize key aspects of the ongoing water crisis. Through these visual analytics, it became evident that the issue is multi-dimensional, influenced by factors such as water source distribution, population location, infrastructure reliability, and daily usage patterns. Each dashboard was designed to highlight a specific dimension of the problem; ranging from the availability and type of water sources to queue times and demographic composition at collection points.
The visualizations not only provided a clearer picture of how water resources are distributed and utilized across provinces and towns but also revealed underlying inequalities and operational inefficiencies that need to be addressed. In the following sections, I present each dashboard and summarize the key insights drawn from them to support evidence-based decision-making and targeted interventions for improving water access in Maji Ndogo.
Analytical Summary: Water Sources in Maji Ndogo


The Power BI dashboard above provides a national overview of water access in Maji Ndogo, serving a population of approximately 28 million through about 40,000 water sources. Most people (around 64%) live in rural areas, highlighting the importance of rural-focused water interventions. Shared taps serve the largest portion of the population (about 12 million), followed by wells and tap-in-home connections. However, a significant portion of household taps are non-functional, pointing to infrastructure maintenance challenges.
In terms of distribution, wells are the most common water source (over 17,000), while rivers remain the least used. The map visualization reveals regional disparities, with some western provinces appearing better served than others. Town-level analysis shows that urban centers like Harare, Amina, and Lusaka have a higher variety and count of water sources, while smaller towns rely more on shared taps and wells. Overall, the data emphasizes the need to improve infrastructure reliability, particularly by repairing broken tap systems, and to expand equitable water access across under-served rural areas.




Analytical Summary: Queue Times and Composition in Maji Ndogo
This dashboard provides an analytical overview of water collection patterns in Maji Ndogo, focusing on queue times, gender composition, and regional variations. The average queue time across all regions is 137 minutes, indicating significant waiting periods for access to water, particularly at shared tap sources.

Gender analysis shows that females constitute the majority (65.78%) of those in queues, followed by males (24.23%) and children (9.99%). This reflects a gendered burden in water collection, with women disproportionately affected by long waiting times.
At the provincial level, Kilimani records the longest cumulative queue time, followed by Akatsi and Sokoto, while Amanzi and Hawassa experience relatively shorter wait times. This suggests spatial disparities in service efficiency and water point distribution.
Temporal analysis reveals that Saturday has the longest average queue duration (246 minutes), likely due to increased weekend demand, while Sunday shows the shortest waiting time (82 minutes). Hourly trends indicate sustained queuing throughout the day, with noticeable peaks in the late afternoon and early evening hours.
Overall, the data highlights systemic inefficiencies in water access, emphasizing the need for better scheduling, expanded infrastructure, and targeted interventions in high-queue provinces such as Kilimani and Akatsi. Furthermore, gender-sensitive strategies should be prioritized to alleviate the disproportionate time burden borne by women in accessing water resources.
Analytical Summary: Gender-Based Crimes Related to Water Collectors in Maji Ndogo
The dashboard below investigates the social and safety dimensions of the water crisis by analyzing gender-based crimes associated with water collection activities. It visualizes the distribution of incidents by province, gender, time of day, and day of the week. The data reveals a total of approximately 77,000 reported crimes, with females representing 64% of victims, followed by males (25%) and children (10%), highlighting a pronounced gender disparity.

Temporal analysis indicates that crimes increase during late afternoon and evening hours, suggesting heightened vulnerability during peak water collection times. Spatially, Kilimani and Akatsi provinces record the highest number of cases, consistent with areas that also experience longer queue times and limited water infrastructure. The most common crimes include theft, harassment, and sexual assault, underscoring the intersection between inadequate water access and public safety risks.Overall, the dashboard emphasizes the urgent need for gender-sensitive interventions and improved infrastructure security measures at water collection points to protect vulnerable populations, particularly women and children.



Project Context Part 2: Strategic Restoration Plan for Maji Ndogo’s Water Supply
Building on the insights gained from the initial diagnostic phase, Phase Two of the Maji Ndogo project focuses on outlining a strategic, data-driven plan to restore reliable and safe water access across all provinces. This stage establishes when key interventions will take place, how they will be executed, and what resources; financial, technical, and operational are required to achieve sustainable improvement. By integrating project timelines, infrastructure needs, cost forecasts, and vendor assignments, Phase Two provides a clear blueprint for coordinated action and effective progress tracking. This ensures that every improvement effort is both targeted and impactful, paving the way for long-term water security in Maji Ndogo
Enhancing Project Tracking Through Calculated Columns and DAX Measures
After introducing the project_progress dataset into the Maji Ndogo model, I created several calculated columns and DAX measures to transform raw project records into actionable insights. These included standardized improvement categories, formatted date fields, project completion indicators, cost fields, and progress percentages. I also developed measures to calculate total improvements, cumulative cost, cumulative budget, and completion rates across regions. These transformations ensured accurate tracking of timelines, spending patterns, vendor performance, and overall project progress.

Through this process, I strengthened my skills in advanced DAX, data modeling, time-intelligence calculations, and financial analysis. I learned how to use context manipulation functions such as CALCULATE, FILTER, and ALL to build dynamic KPIs and trend measures that power the dashboards. These enhancements allowed me to create more meaningful visualizations and provide deeper, data-driven insights into the improvement efforts across Maji Ndogo.

Business Intelligence Summary: Budget Allocation Infrastructure Improvements & Planning
This dashboard examines the financial and infrastructural dimensions of the water crisis by analyzing how budgets, improvement projects, and population needs align across provinces. It provides a national overview of the 28 million residents, a total improvement budget of $147M, and the resulting 63% increase in water system improvements achieved so far.

The dashboard compares rural and urban populations per province, highlighting significant variations in service distribution. It also breaks down aggregated improvement costs—such as installing RO filters, diagnosing local systems, drilling wells, and implementing UV treatment—showing which interventions require the highest investment. Additionally, the budget allocation chart reveals that provinces like Sokoto and Akatsi receive higher funding, reflecting their greater infrastructure gaps and population demands.
The analysis further explores the cost of each improvement type and the resulting progress across rural and urban areas. This supports data-driven decision-making by identifying which interventions deliver the greatest impact and which provinces require additional investment to achieve equitable water access.
Provincial Water Survey Overview
This dashboard provides a detailed breakdown of how water-related improvements and budgets are distributed across Maji Ndogo’s provinces. By analysing improvement types, costs, population distribution, and cost-per-citizen metrics, this report highlights where the greatest investment needs lie and how resources are being allocated. 

The visual summaries; ranging from improvement counts to budget allocations by province and town, offer a clear picture of progress and disparities across regions. This forms a crucial foundation for understanding localised needs as the country moves into the next phase of restoring and strengthening its national water supply system.






Forecasted Budget Analysis Dashboard Overview
To support strategic decision-making around water infrastructure improvements in Maji Ndogo, I developed a Forecasted Budget dashboard that aggregates costs across different improvement types and provinces. Using DAX measures, I calculated the total budgeted improvement cost, cost distribution per province, and the budget share of each improvement category. This allowed me to translate raw project data into meaningful financial insights that reveal how resources should be allocated to maximize impact.

The dashboard highlights key financial patterns, such as which provinces require the largest investment, how improvement costs compare across regions, and which infrastructure upgrades contribute most significantly to the national budget. Through this process, I strengthened my skills in data modeling, financial aggregation, DAX calculations, and the communication of budget insights through visually compelling, interactive Power BI reports.





Actual Improvement Costs Analysis Dashboard Overview
The Actual Improvement Costs dashboard below reveals that Maji Ndogo’s water infrastructure upgrades exceeded initial estimates, with actual spending rising to $154.49M compared to the $146.74M budget. Rural areas consistently demanded higher investment than urban locations due to the complexity of accessing remote systems and rehabilitating aging infrastructure. 
Across provinces, Sokoto displayed the highest projected costs, though its actual spending aligned more closely with expectations, while regions like Akatsi and Kilimani experienced the largest overruns, pointing to unanticipated work during implementation. A deeper breakdown by province and location type shows that rural projects in Sokoto, Akatsi, and Kilimani required the greatest funding, and several provinces; especially Akatsi Rural and Kilimani Rural, recorded substantial gaps between budgeted and actual expenses. Overall, the dashboard highlights that while budgeting captured general cost patterns, real-world execution, especially in rural environments, introduced higher and more variable financial demands.





Vendor Performance and Cost Efficiency Analysis
The Costs by Vendors dashboard provides a detailed view of how project expenditures are distributed across service providers in Maji Ndogo, highlighting both cost efficiency and operational capacity. The data shows that vendor performance varies significantly by province and improvement type, with firms such as Aswan Infrastructure Diagnostics, Kano Urban Planning, and Bamako Survey Co. handling some of the highest volumes of improvement work. 
Average vendor costs generally fall between $370 and $680, suggesting a relatively consistent pricing structure, though some vendors show higher averages in provinces such as Sokoto and Hawassa. By combining vendor cost, improvement count, location type, and completion timelines, the dashboard helps pinpoint which vendors deliver the most cost-effective outcomes and in which regions they perform best. The interactive filters—including improvement type, rural versus urban classification, and project timelines—enable stakeholders to quickly evaluate vendor reliability, understand geographical cost differences, and identify opportunities to optimize procurement strategies in the next phases of Maji Ndogo’s water restoration program.





Project KPIs and Progress Overview
As the second phase of the Maji Ndogo Water Improvement Programme came to a close, the project dashboard told a story of transformation across the entire nation. What began as a fragmented system with millions lacking reliable water access had now become a fully completed national initiative—every planned improvement delivered, every community reached. The KPIs revealed the scale of what had been achieved: 25,000 water access improvements rolled out, 100% of the population now receiving basic water services, and 18 million citizens directly benefiting from the work. Even the financial narrative supported the success—while actual costs reached $154M against a planned $146M, the fluctuation remained within an acceptable variance for a multi-year, multi-province intervention of this size. Provinces like Sokoto and Kilimani emerged as the major cost centers, reflecting their size and infrastructure complexity, while the cost distribution across improvement types remained consistent and well-managed. Watching the final indicator switch to “0 sources left to go” captured the project’s completion in a single moment, marking not just the end of a dashboard, but the culmination of a nationwide effort to restore safe, accessible water for every person in Maji Ndogo.





KPI Insights & Key Drivers of Cost Efficiency
In the final phase of the analysis, I examined the key influencers behind Maji Ndogo’s improvement costs to understand what most significantly drives budget variations across the project. The KPI model revealed a clear pattern: cost reductions were strongly associated with targeted diagnostic work, particularly when improvements focused on Diagnosing Local Infrastructure. This intervention consistently lowered average improvement costs, indicating that early assessment and issue identification helped prevent unnecessary or misaligned spending later in the project cycle. Conversely, installations requiring advanced filtration such as UV or RO filters naturally contributed to higher cost averages due to their technical complexity and resource requirements. By linking these findings back to provincial performance and overall project progress, the KPI insights helped validate the strategic value of starting with diagnostic initiatives before deploying higher-cost interventions, ultimately guiding more precise budget forecasting and supporting long-term financial sustainability across the water restoration program.







