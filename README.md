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

