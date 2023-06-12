# Andmetehnika mitteinformaatikutele (LTAT.02.026) project

Authored by:
1) Eva Meinson
2) Margus Varjak
3) Fred Väärtnõu

Software information, only a single file for code: 'projekt.ipynb'
1) The code was written in *.ipynb format using Visual Studio Code, ver. 1.79.0
2) The code is running on Python, ver. 3.11.3
3) Necessary additional libraries for the project:
requests - to carry out web requests
pandas - to handle dataframes
numpy - for mathemicals operations
zipfile - to handle zip files
matplotlib.pyplot and seaborn together for visualization
'%pip install <library>' command will get the library downloaded and installed, currently commented out.
4) We carried out additional visualization using Microsoft Power BI Desktop, Version: 2.117.984.0 64-bit (May 2023).
We published the created dashboard into Web as embedded report, with following link: https://app.powerbi.com/view?r=eyJrIjoiMjk3N2YyMDktYmUwYS00MjdlLWFlODEtMzk0NGVkMGRiYjQwIiwidCI6IjM2YTc0ZjA4LTYwMDUtNDA5OS05ZTFjLTg1NDU5ZGFjMjEzZiIsImMiOjh9 

We derived data from The World Bank publicly available repository:
https://data.worldbank.org/
There are one can chose data that is available for a sepcific country or focus on a particular indicator
We chose indicators:
https://data.worldbank.org/indicator

We downloaded three different datasets, for data fetching, cleaning, combining, and visualization.
GDP per capita:     https://api.worldbank.org/v2/en/indicator/NY.GDP.PCAP.PP.CD?downloadformat=csv

Life expectancy:    https://api.worldbank.org/v2/en/indicator/SP.DYN.LE00.IN?downloadformat=csv

Literacy:           https://api.worldbank.org/v2/en/indicator/SE.ADT.LITR.ZS?downloadformat=csv

<i>Remark: there are numerous other indicators available as well, for climate, agriculture, energy, health. </i>

Our aim was to download *.csv files, however, .zip files where provided by the website. Thus, *.zip files were download and unpacked, a separate folder was each indicator. Following, in each *unpacked folder, the file starting with 'API*' denotes the *.csv file of interest, other two are for meta information.
However,  the first few rows in 'API*' file contains some extra unnecessary information, which was removed and following that we get three inital files to start working on: gdp_per_capita.csv, life_expectancy.csv, and literacy.csv (these are in the same folder level as file 'projekt.ipynb')

<b>gdp_per_capita.csv top row:</b>
"Country Name","Country Code","Indicator Name","Indicator Code","1960","1961", ..., "2022",
<b>gdp_per_capita.csv example value row:</b>
gdp_per_capita.csv texample row:
"Aruba","ABW","GDP per capita, PPP (current international $)","NY.GDP.PCAP.PP.CD","", ...,'',

<b>gdp_lifeexp.csv top row:</b>
"Country Name","Country Code","Indicator Name","Indicator Code","1960","1961", ...,"2022",
<b>gdp_lifeexp.csv example value row:</b>
"Aruba","ABW","Life expectancy at birth, total (years)","SP.DYN.LE00.IN","64.152","64.537", ...,'',

<b>gdp_literacy.csv top row:</b>
"Country Name","Country Code","Indicator Name","Indicator Code","1960","1961", ...,"2022,
<b>gdp_literacy.csv example value row:</b>
"Aruba","ABW","Literacy rate, adult total (% of people ages 15 and above)","SE.ADT.LITR.ZS","","",...,'',

For these files, the column names are self-explanatory, however, The World Bank also provided the necessary meta information, the data is available in '*unpacked' folder.

Further, we required another file, which contains a list countries and their corresponding regions and sub-regions. That information is needed for grouping as the analysis progresses.
Manual option to download at website: 
https://unstats.un.org/unsd/methodology/m49/overview/
Or downloadable option:
https://github.com/lukes/ISO-3166-Countries-with-Regional-Codes/raw/master/all/all.csv"

That information is provided by a separate file 'countries.csv':
<b>countries.csv top row:</b>
name,alpha-2,alpha-3,country-code,iso_3166-2,region,sub-region,intermediate-region,region-code,sub-region-code,intermediate-region-code
<b>countries.csv example value row:</b>
Afghanistan,AF,AFG,004,ISO 3166-2:AF,Asia,Southern Asia,"",142,034,""

In that file for each country, given are its name, country codes in different formats and regions, sub-regions and their codes
Important for us: 'Country Name' corresponds to 'name' and 'Country Code' corresponds to 'alpha-3' column, which permits joining

gdp_per_capita with countries --> df_gdppcap, 
life_expectancy with countries --> df_lifeexp, 
literacy with countries --> df_literacy

<i>For detailed data processing understanding, we commented the code.</i>

Important notes regarding processing: due to the nature of datasets, there are many NaN values, essentially data earlier than 1990s is lacking, thus we can look back 30 years.
Further, literacy data is relatively incomplete, meaning that not for every year literacy values are given. However, to estimate the literacy levels in 2021, we extrapolate the values from a earlier year, when measurements had been conducted.

Using Python Matplotlib and Seaborn libraries, we made following graphical representations of the the data:
Figure 1:
Scatterplot for GDP per capita vs Literacy rate in 2021, coloring done based on Regions.
- Strong correlation between country's richness and literacy
- However, not all countries with high literacy are rich
- In Africa many countries have low literacy rate and these are poorer as well
- Europe has very high literacy rate, Americas and Asia are mixed
Figure 2:
Line graph, we looked at the progression of GDP per capita over last 30 years, in different sub-regions.
- Based on that North America and Western Europe are the richest (no surprises)
- Eastern Asia has gone through rapid progress
- Eastern Europe has still catching up to do (cought up with Souther Europe)
- African countries do not show much progress
Figure 3:
Scatterplot, GDP per capita vs Life expectancy in 2021 in different sub-regions
-Strong correlation between country's richness and life expectancy
Figure 4:
Similar, as above, GDP per capita vs Life expectancy in 2021 in different European countries, coloring based on regions
-Again, very strong correlation
Figure 5:
Line graph, Estonia specific, GDP per capita progression and life expectancy, over the last 30 years.
On the same graph two different lines with separate scales are given.
- From the graph, we can see that people are living longer, as country gets richer

The dataframes we used to make figures, have been also exported as csv files.

Using Microsoft Power BI Desktop we created a data model including Country, GDP, Life expectancy and Literacy data. The data model reads data directly from .csv files in github repository. We used Power Query for data transformation - for example unpivot  table to get data into rows per different years for visualization. Example transformation script in M for the "df_gdppcap.csv" file:

let

    Source = Csv.Document(Web.Contents("https://raw.githubusercontent.com/varjakm/Andmetehnika_projekt/main/ForPowerBI/df_gdppcap.csv"),[Delimiter=",", Columns=69, Encoding=65001, QuoteStyle=QuoteStyle.None]),

    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),

    #"Removed Columns" = Table.RemoveColumns(#"Promoted Headers",{"", "Country Name", "region", "sub-region", "Indicator Name", "Indicator Code"}),

    #"Unpivoted Columns" = Table.UnpivotOtherColumns(#"Removed Columns", {"Country Code"}, "Attribute", "Value"),

    #"Replaced Value" = Table.ReplaceValue(#"Unpivoted Columns",".",",",Replacer.ReplaceText,{"Value"}),

    #"Changed Type" = Table.TransformColumnTypes(#"Replaced Value",{{"Value", type number}, {"Attribute", type date}}),

    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Country Code", "Country"}, {"Attribute", "Year"}})

in

    #"Renamed Columns"

The final dashboard consists of three different sheets, each has focus on specific data area (GDP, Life expectancy and Literacy). User can navigate between sheets using navigation buttons on dashbboard header.

The whole dashboard can be filtered using filters on the right side of the dashboard where are visible filters for year, region, sub-region and country.

In the left upper corner of the dashboard are displayed the average, minimum and maximum values as dynamic fact boxes based on user selection.

The main visual on dashboard compares the average value in the world to user selected value. This allows to compare how specific region or country compares to the world average and how numbers have changed over time.

The scatter plot visual on bottom of the dashboard shows the correlation of selected life expectancy or literacy to GDP. The tooltip on selected datapoint displays information about county and it's location on the map.

The bar chart visual on the left enables to drill-down from region numbers to country level numbers. 


