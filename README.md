# CovidbyDistVisualization

Tableau Visualization of Poverty, Lower Income and Ethnicity in Relationship to COVID-19

- Analyze regions highly populated with racial minorities and lower income/high poverty regions and effect COVID-19 had on them.
- We are using Tableau to visualize the effects of COVID-19.
- Data from Census, NYCHealth was used in this project.

Links to Data Sets Used:
- COVID-19 data set: https://github.com/nychealth/coronavirus-data
- Poverty data set: https://www1.nyc.gov/site/opportunity/poverty-in-nyc/data-tool.page
- Income levels: https://censusreporter.org/
- Income levels, demographic by dist: https://data.cccnewyork.org/data/map/66/median-incomes#66/39/3/107/40/a/4

# Creating the sheets 

Covid Cases and Poverty/Median Income by Dist
1.	Drag geometry under geo_export file and neighborhood under Sheet1 into the panel to generate all districts unaggregated. 
2.	Drag latitude onto rows to create another graph on the bottom. We will dual axis them.
3.	Click on the left latitude. Add covid case count to color and change color scheme to purple. Then click on the right latitude and add poverty to color as well as median income to size. Right click on the right latitude and click dual axis.

Positivity, Tests, and Income follows the same pattern but with different attributes dragged on. 
1.	Same as above step one.
2.	Same as step 2.
3.	Create calculated field because we don’t want tableau to aggregate the average percentages because we can’t do that. Instead, go to bottom of data panel and right click and create a calculated field. Name it to something like “positivity rate” and make it SUM([Covid Case Count]) / SUM[# Covid Tests].
4.	Drag this median income to color on the left latitude and drag this new calculated field as color on the right latitude and put covid tests as the size and dual axis.
 	
Correlation Between Positivity and Income
1.	Drag the new calculated field as color and covid tests as size. Drag neighborhood under sheet1 as detail to have neighborhood level data.
2.	Create trendline and make it exponential. This gave us the best r squared value.

Race demographic and Positivity/CovidTests
1.	Drag neighborhood into detail. Drag neighborhood again onto columns.
2.	Right click measure values and show filter. Start by only having white as the only one checked. Then drag measured value onto rows. Sort it from least to greatest. Then tick Asian, Black, Hispanic, and Other. The racial minorities will be stacked on top on White majority to create stacked bar chart. 
3.	For bottom graph, drag positivity on rows. Make it an area graph. Drag # covid test to right that in rows. Make it a line graph. Dual axis.

White Majority
1.	Make median income as columns and drag white as rows. Make positivity rate as color and # covid test as size. 

Overtime Case Rate 
1.	In data source, we’ve pivoted all the rate numbers already. But, we want to see the lines according to a specific neighborhood, not all at once. We will create a parameter field by scrolling to bottom in left panel and right clicking, create param.
2.	Name it to something like districts, data type as string, and allowable values as list. Click add values from Neighborhood then add an extra one called “All” at bottom. Once you have that, right click this new parameter field and click show parameters.
3.	Drag Date as column and covid rate per 100k in thousands as row, both under sheet2 in left panel. Drag neighborhood to tool tip. We also need to create a filter, call it DistrictFilter, so the data shows when we click a certain district in our created parameter list dropdown. 
4.	Create calculated field and type in, IF [Districts] = [Neighborhood] THEN ‘true’ ELSEIF [Districts] = ‘ALL’ THEN ‘TRUE’ END
5.	Drag this onto the filters.

Demo: https://public.tableau.com/profile/hunter.zhao#!/vizhome/CovidAnalysisbyDistrict/CaseCountandPovertyIncomeLevels?publish=yes

Collaborators: Enxhi Osmanllari, Hunter Zhao, Edwin Pineda, Jackson Lu

Moderator: Dr. Oyewole Oyekoya, Hunter College
