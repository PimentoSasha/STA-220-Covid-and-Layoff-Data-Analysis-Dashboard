<a name="br1"></a> 

STA 220

**FINAL PROJECT REPORT**

Presented by Sasha Neil Pimento

**Introduction**

The impact of the Covid-19 pandemic has been unprecedented, aﬀecting economies and

societies worldwide. With the onset of the pandemic, the world saw a surge in job losses,

and businesses had to pivot to stay aﬂoat. As a data enthusiast, I wanted to explore this

phenomenon further and create a tool which could be used by end users to see if there

was a correlation between the Covid-19 outbreak and the layoﬀ data. To that end, I created

a dashboard using Jupyter Dash, which presents visualizations of both the Covid data and

Layoﬀ data, and also combines them to show trends.

The dashboard consists of three tabs, each displaying visualizations for a speciﬁc analysis.

The ﬁrst tab displays all visualizations related to Covid data, such as the number of

conﬁrmed cases, recoveries, and deaths over time. The second tab shows visualizations

related to layoﬀ data, such as the number of layoﬀs by country, company and time. The

third tab shows plots that combine both Covid and layoﬀ data to show trends, such as the

Quarterly trend of Covid Cases and layoﬀs in the US.

My intention was to make the dashboard ﬂexible, so that users could select the type of plot

and the column they want to see visualizations for, which would then show up accordingly.

Using Dash enabled me to create an app that runs locally on my computer and displays all

the graphs using Plotly Express.

This report will elaborate on the data collection and cleaning processes and the methods

used to implement this project using Dash. Overall, the dashboard provides insights into

the impact of the pandemic and job losses on various countries and economies and can be

a useful tool for policymakers, businesses, and researchers.



<a name="br2"></a> 

**1. Research Questions:**

Every tab on the dashboard aims at answering a research question which has been

addressed below:

●

●

●

**Covid Analysis Tab** : Can we analyze the severity of Covid cases from diﬀerent

geographical angles?

**Layoﬀ Analysis Tab**: Can we depict the Layoﬀ data from a geographical and

organizational perspective ?

**Covid Cases and Layoﬀs Analysis Tab:** Is there a way to combine the Covid and

Layoﬀ Data and depict a possible trend/pattern through visualization?

**2. Data Acquisition and Processing**

This project consists of 3 primary datasets which are being used for visualization purposes.

In this section, I have elaborated on the data acquisition,cleaning and processing

techniques used for each dataset.

**2.1 Worldometer Covid 19 Data**

For the purpose of extracting the Covid 19 Data, I used a [script](https://github.com/PimentoSasha/STA-220-Project/blob/main/Data%20Scraping%20Worldometer.ipynb)[ ](https://github.com/PimentoSasha/STA-220-Project/blob/main/Data%20Scraping%20Worldometer.ipynb)which was responsible for

scraping data from the [Worldometer](https://www.worldometers.info/coronavirus/)[ ](https://www.worldometers.info/coronavirus/)website and saved it to a csv ﬁle on my computer. The

script was mainly responsible for scraping the contents of the [Reported](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)[Cases](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)[and](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)[Deaths](https://www.worldometers.info/coronavirus/#main_table)

[by](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)[Country](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)[or](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)[Territory](https://www.worldometers.info/coronavirus/#main_table)[ ](https://www.worldometers.info/coronavirus/#main_table)table. In order to parse the web data, the script uses BeautifulSoup

and proceeds to ﬁnd the target table for my dataset, which is the last table on the

Worldometer website. Once the table has been located, it fetches all the table contents by

iterating through each row and creates a list of elements for every row which is then

appended to a parent list. This list of lists is then converted into a dataframe using the

pd**.**DataFrame() function. At the end of the script, it saves the csv ﬁle using the

to\_csv() function.

I examined the dataset to check if cleaning and processing was needed. There were a lot of

NaN values in the dataset after it was scraped from the Worldometer website (Fig 1). In

2



<a name="br3"></a> 

order to handle the missing values appropriately, the data was cleaned by replacing all NaN

values with 0.

Fig 1: A lot of NaN values seen in the scraped worldometer data prior to Data cleaning

The Worldometer data was primarily going to be used for showing the Total Conﬁrmed

Cases, Active Cases, Recovered Cases and Deaths by country.

Fig 2: A glimpse of the worldometer\_data dataframe

**2.2 Daily Covid 19 Data Country - Wise**

In order to visualize the Quarterly trend of Covid Cases in the USA, I used a Data Cleaning

[script](https://github.com/PimentoSasha/STA-220-Project/blob/main/Data%20Cleaning.ipynb)[ ](https://github.com/PimentoSasha/STA-220-Project/blob/main/Data%20Cleaning.ipynb)to clean the time series data present at [CSSE](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[Time](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[series](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[Covid](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[19](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[Conﬁrmed](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[cases](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)

[(Global](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[)](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)[ ](https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv)which gave the daily count of conﬁrmed cases for every Country. The melt function

helped in unpivoting the Conﬁrmed cases data frame from a wider into a longer format.

For the preprocessing of the data, the script converts Date to a proper Datetime format

using the pd**.**to\_datetime() function. Since NaN values were seen in the columns like

Conﬁrmed, Death etc which indicate the number of cases and should be integer values, all

NaN values were also replaced by 0 cases. The 'Country/Region' column is also processed

3



<a name="br4"></a> 

in a way that ensures that the names remain standard. The csv obtained at the end of this

cleaning process was used for visualizing the Quarterly trend of Covid Cases.

Since I wanted to plot the data only for the US, I ﬁltered the data on the country, but found

that the time series data which I obtained from the csv was a cumulative sum which means

that the number of cases for the previous day was getting added to the cases for the

present day. In order to calculate the actual number of cases for that day, I iterated

through all the rows in the csv and calculated the present day count, by taking the

diﬀerence of the current day cases with the previous day cases. As seen in the screenshot

below, the Conﬁrmed column represents the cumulative sum of cases, but the

Conﬁrmed\_Daily column at the end presents the actual count of cases for that day.

Fig 3: A glimpse of the combined time series dataframe

**2.3 Layoﬀ Data**

In order to analyze the data related to Layoﬀs, I used the [Layoﬀ](https://github.com/PimentoSasha/STA-220-Project/blob/main/layoffs.csv)[ ](https://github.com/PimentoSasha/STA-220-Project/blob/main/layoffs.csv)[Dataset](https://github.com/PimentoSasha/STA-220-Project/blob/main/layoffs.csv)[ ](https://github.com/PimentoSasha/STA-220-Project/blob/main/layoffs.csv)which gives

information about the various companies and the total employees laid oﬀ along with the

dates on which this lay oﬀ occurred. It also gives information about the countries these

companies belong to so the user could get a clear idea of how the layoﬀs have impacted

each country. Once this dataset was loaded, I also checked the number of NaN values and

since these values were primarily in the total\_laid\_oﬀ and percentage\_laid\_oﬀ columns, I

replaced those values with 0. Since there was a NaN value in the date column, which

4



<a name="br5"></a> 

cannot be replaced by any default value, and the date was crucial for the Quarterly trend of

Layoﬀs plot, I deleted that row from the dataframe.

Fig 4: NaN values seen in the layoﬀ\_data dataset

Fig 5: A glimpse of the cleaned layoﬀ\_data dataframe

Depending on the various plots that had to be visualized, various data frames were

merged together. These have been further elaborated on in the following section.

**3. Visualization and Methodology:**

In order to provide users with a ﬂexible and interactive means of visualizing data, a

dashboard was developed as a key component of the project. To achieve this, the [Dash](https://dash.plotly.com/introduction)

framework was utilized, with [plotly](https://plotly.com/python/plotly-express/)[ ](https://plotly.com/python/plotly-express/)[express](https://plotly.com/python/plotly-express/)[ ](https://plotly.com/python/plotly-express/)being used for plotting purposes. Additionally, a

series of callback functions were deﬁned for each tab in the dashboard, allowing for the

dynamic updating of plot types and data parameters based on user input.

5



<a name="br6"></a> 

**3.1. Covid Analysis Tab**

Of particular note is the Covid Analysis tab, which oﬀers users a range of plot types

including TreeMap, Horizontal Bar Graphs and Country Maps, as well as various column

options such as Total Cases, Total Deaths and Total Recovered, etc. Based on user

selections, the appropriate plot function is called through the corresponding callback

function, with the value of the second dropdown used as input to generate the plot on the

selected column. This provides a highly customizable experience for users, enabling them

to conduct their analyses with precision and ease. Another interesting graph that I wanted

to visualize was the Quarterly trend of Covid cases in the US. This was so that I could plot it

alongside the Quarterly trend of Layoﬀs and leave it for the end users to interpret the

pattern and if there was any correlation between the 2 datasets. In order to visualize the

Quarterly trend, I grouped the data by a Quarterly date rule and took the sum of the Covid

cases. From the plot below, we can see that the total conﬁrmed cases in the USA tends to

reduce closer to March, 2023

An example of the dataframe can be seen below:

Fig 6: On the Left, the data frame used for showing the Quarterly Trend of Conﬁrmed Cases in USA

and on the right, the plot

❖ With the help of the treemap, we are able to see the Total Conﬁrmed cases for each

country till date and compare the count of cases for each country, identifying the country

with the most cases to date being the US with a total of 105,599,065 cases.

6



<a name="br7"></a> 

Fig 7: A ﬁrst look at the Dash dashboard which displays a TreeMap showing the total Covid cases for each

country

❖ With the help of the country map below (Fig 8) , we are able to see a map of all the

countries and analyze the death count for each country . The maximum number of Covid

Deaths is in the USA with a count of 1.148765 Million.

Fig 8: A Country Map showing the total Covid deaths for each country, with the hue (on the right side) indicating the country

with range.

7



<a name="br8"></a> 

❖ The Horizontal Bar Graph (Fig 9) below has been used to depict the total number of

active cases by Continent, thus showing that Asia has the highest number of Active

cases.

Fig 9: A Horizontal bar graph showing the total Active Cases for each continent

**3.2. Layoﬀ Analysis Tab**

I implemented the Layoﬀ Analysis tab in a similar way to the Covid Analysis tab, plotting

various plots and columns based on the inputs given by the user.

8



<a name="br9"></a> 

❖ From the plot below, we can see that the company with the maximum number of

layoﬀs is Amazon with a total count of 18150 employees

Fig 10: A Horizontal bar graph showing the total layoﬀs for each organisation for each sorted by the total count.

❖ From the treemap plot below (Fig 11), we can see that the country with the

maximum number of layoﬀs is USA with a total count of 256,059 employees

Fig 11: A Treemap plot showing the total layoﬀs for each country sorted by the total count.

9



<a name="br10"></a> 

I also visualized the Quarterly trend of layoﬀs by grouping the layoﬀs by the date using the

Quarterly rule and summing over the total count of layoﬀs. The results can be seen in the

plot below (Fig 12). From the ﬁgure it can be seen that there is a sharp rise in the number of

layoﬀs in the Jan - March 2023 quarter.

Fig 12: On the Left, the data

frame used for showing the Quarterly Trend of Layoﬀs in USA and on the right, the plot

**3.3. Covid Cases and Layoﬀs Data Analysis Tab:**

In order to visualize the trends of the Covid cases and the layoﬀs, I combined the

dataframes which I had created for plotting the Quarterly trends. I also used a dual axis bar

and line graph for showing the monthly trends. Since the dates for the monthly trend Covid

cases dataset were too large to be plotted on the x axis without cramming, I extracted the

month and year and placed it in a month-year column (Fig 13) so that I could plot the

monthly trend of covid cases without the complete dates. I then extracted the month-year

column, along with the conﬁrmed cases column and placed this in a new dataframe along

with the total layoﬀs count for each month (Fig14).

10



<a name="br11"></a> 

Fig 13: Added Month-year column

Fig 14: Merged dataframe

The plots of the Dual Axis Line graph can be seen in Fig 14 and the plot of Dual Axis Bar

Line Graph can be seen in Fig 15.

❖ From the ﬁgures we can see that while the count of Covid Cases (blue line) tend to decrease

towards March 2023, the count of the total layoﬀs (red) are increasing.

11



<a name="br12"></a> 

Fig 14: Dual Axis Line Graph

Fig 15: Dual Axis Bar Line Graph

12



<a name="br13"></a> 

**Conclusion / Future Work:**

In conclusion, this project has successfully developed a dashboard that provides the end

user with the ability to analyze and gain insights from Covid and Layoﬀ data from diﬀerent

geographical and organizational perspectives. The project has answered the research

questions related to the severity of Covid cases, depiction of Layoﬀ data from a

geographical and organizational perspective, and identiﬁcation of possible trends/patterns

through visualization of both Covid and Layoﬀ data.

Furthermore, the project has the potential for future work to expand the data scraping

script to provide real-time data updates and include additional visualizations and column

values to gain even more insights. This could enhance the usefulness of the dashboard for

users and potentially provide further valuable information related to Covid and Layoﬀ data.

Overall, this project has contributed to the ﬁeld of data analysis and visualization, providing

a practical tool for users to gain insights and understanding related to Covid and Layoﬀ

data. It is hoped that this project can be built upon in the future to continue to provide

valuable insights and inform decision-making in these critical areas.

**STA 220 Github Project Repository (Code & Data):**

<https://github.com/PimentoSasha/STA-220-Project>

**References:**

●

[Plotly](https://www.youtube.com/watch?v=7m0Bq1EGPPg&ab_channel=CharmingData)[ ](https://www.youtube.com/watch?v=7m0Bq1EGPPg&ab_channel=CharmingData)[Dash](https://www.youtube.com/watch?v=7m0Bq1EGPPg&ab_channel=CharmingData)[ ](https://www.youtube.com/watch?v=7m0Bq1EGPPg&ab_channel=CharmingData)[Tutoria](https://www.youtube.com/watch?v=7m0Bq1EGPPg&ab_channel=CharmingData)[l](https://www.youtube.com/watch?v=7m0Bq1EGPPg&ab_channel=CharmingData)

●

●

●

●

●

[Dash](https://dash.plotly.com/dash-core-components/dropdown)[ ](https://dash.plotly.com/dash-core-components/dropdown)[Dropdown](https://dash.plotly.com/dash-core-components/dropdown)[ ](https://dash.plotly.com/dash-core-components/dropdown)[Components](https://dash.plotly.com/dash-core-components/dropdown)

[Multiple](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[ ](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[Callbacks](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[ ](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[for](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[ ](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[an](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[ ](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)[Output](https://community.plotly.com/t/multiple-callbacks-for-an-output/51247)

[Plotting](https://plotly.com/python/multiple-axes/)[ ](https://plotly.com/python/multiple-axes/)[with](https://plotly.com/python/multiple-axes/)[ ](https://plotly.com/python/multiple-axes/)[Multiple](https://plotly.com/python/multiple-axes/)[ ](https://plotly.com/python/multiple-axes/)[Axes](https://plotly.com/python/multiple-axes/)

[COVID](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[ ](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[19](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[ ](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[Web](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[ ](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[scraping](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[ ](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[and](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[ ](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)[cleaning](https://github.com/imdevskp/covid_19_jhu_data_web_scrap_and_cleaning)

[Layoﬀ](https://www.kaggle.com/datasets/swaptr/layoffs-2022)[ ](https://www.kaggle.com/datasets/swaptr/layoffs-2022)[Dataset](https://www.kaggle.com/datasets/swaptr/layoffs-2022)

13

