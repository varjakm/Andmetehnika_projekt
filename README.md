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
4) We carried out additional visualization using commercial PowerBI, ver. ...
For that we provide a link report link: 

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
