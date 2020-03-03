# Wildfire and Climate Change
### Machine Learning project by Homeira Azari and Mrinmayee Kulkarni

Climate change affects the social and environmental determinants of health, clean air, safe drinking water, enough food, and secure shelter. Between 2030 and 2050, climate change is expected to cause approximately 250000 additional deaths per year.1 The effects of climate change on temperature, precipitation levels, and soil moisture are turning many of our forests into kindling during wildfire season. However, wildfires are not just a result of climate change, they’re also contributing to it much more than imagined. In this research, we want to evaluate to what extent people are aware of climate change and its effect on their life. Additionally, we would like to understand the causes of wildfires to take action and prevent climate change.

## Data Cleaning

* This data publication contains a spatial database of wildfires that occurred in the United States from 1992 to 2015. It is the third update of a publication originally generated to support the national Fire Program Analysis (FPA) system. The wildfire records were acquired from the reporting systems of federal, state, and local fire organizations. The following core data elements were required for records to be included in this data publication: discovery date, final fire size, and a point location at least as precise as Public Land Survey System (PLSS) section (1-square mile grid). The data were transformed to conform, when possible, to the data standards of the National Wildfire Coordinating Group (NWCG). Basic error-checking was performed and redundant records were identified and removed, to the degree possible. The resulting product, referred to as the Fire Program Analysis fire-occurrence database (FPA FOD), includes 1.88 million geo-referenced wildfire records, representing a total of 140 million acres burned during the 24-year period.

* The wildfire dataset is in sqlite format. Therefore, we connected it with the sqlite3 library to open it in jupyter notebook. We then converted this file to a dataframe and explored the data. 

* We went through all the columns to get a better understanding of what data was in each column and if it matched with the data types.And chose only the columns necessary for our analysis. These are the columns that we decided to include in our new dataframe,
FIRE_NAME, FIRE_YEAR, DISCOVERY_DATE, DISCOVERY_DOY, STAT_CAUSE_DESCR, CONT_DATE, CONT_DOY, FIRE_SIZE, FIRE_SIZE_CLASS, LATITUDE, LONGITUDE, STATE, COUNTY, Shape.

* Then we created a function to evaluate how many missing observations are in each column.The column fire name had missing values very close to the dataset row count and we decided delete this column as there would be local , small fires which would remain unnamed and still be a valid indicator for our project.We also decided to delete the column COUNTY as it has almost 40% missing values and we wont need COUNTY information as we already have latitude, longtitude and state information.

* We changed the Julian date format to normal date format for DISCOVERY_DATE and CONT_DATE. We created the YYYY/MM/DD date format columns named DISC_DATE and CONTAIND_DATE and drop the previous columns.

* There are almost 50% missing values for columns CONTAIN_DATE and CONT_DOY. We created a column TOTAL_DAYS to compute the total number of days to contain the fire. In this column the missing values were tagged by NaN which we think they will not effect the data exploration and data modeling.

* Once we cleaned the data for our exploration, we saved it as a new sql table in our sqlite database for further use.

* We noticed that while reading in the newly created table in our exploration notebook the date formats weren't read in properly. Thus, we changed the read in with the correct date format and then subtracted column discovery date from contain date to get total days the fire was burning.



## Data Exploration

* For the data exploration phase we used the newly created sqlite table to create plots for visualising our datset.

 * Count of fires occurred in the top 10 states.
      
 * Frequency of wildfire over time. 
      
 * We also plotted the count of fires based on the cause in a bar chart. In this plot we noticed that the Debris Burning had the most    counts. Therefore, we plotted the bar chart just for the Debris Burning vs Fire Class.
      
 * The next is the fire size vs fire year to understand cumulative hectares affected by fire over the years.
     
 * Correlation matrix for all the features in our datasets. The stronger correlations are the darker greens.

## Methodology

* Currently we are trying to experiment different models by creating dummy variables for the categorical variables, FIRE_CLASS and CAUSE_DESC. It looks like the relationship may not be linear as we run the models, which is obvious as the wildfires would not have a set linear pattern to follow.

* Thus, we are going to explore in other ways to model our data to get the best out of our features.

* We are also modeling and tuning a decision tree with DAYS and FIRE_SIZE to understand the relationship.



## References

1.	Climate change and health. (n.d.). Retrieved from https://www.who.int/news-room/fact-sheets/detail/climate-change-and-health
2.	Short, K. C. (2014). A spatial database of wildfires in the United States, 1992-2011. Earth System Science Data, 6(1), 1–27. doi: 10.5194/essd-6-1-2014
3.	Westerling, A. L., Brown, T. J., Schoennagel, T., Swetnam, T. W., Turner, M. G., & Veblen, T. T. (2016). Climate and Wildfire in Western US Forests. Forest Conservation in the Anthropocene: Science, Policy, and Practice, 43–55. doi:10.5876/9781607324591.c003
4.	Cody, E. M., Reagan, A. J., Mitchell, L., Dodds, P. S., & Danforth, C. M. (2015). Climate Change Sentiment on Twitter: An Unsolicited Public Opinion Poll. Plos One, 10(8). doi: 10.1371/journal.pone.0136092Short, K. C. (2014). A spatial database of wildfires in the United States, 1992-2011. Earth System Science Data, 6(1), 1–27. doi: 10.5194/essd-6-1-2014
5.	Pearce, W., Holmberg, K., Hellsten, I., & Nerlich, B. (2014). Climate Change on Twitter: Topics, Communities and Conversations about the 2013 IPCC Working Group 1 Report. PLoS ONE, 9(4). doi: 10.1371/journal.pone.0094785
6.	1.88 Million US Wildfires. (n.d.). Retrieved from https://www.kaggle.com/rtatman/188-million-us-wildfires
7.	Qian, E. (2019, November 13). Twitter Climate Change Sentiment Dataset. Retrieved from https://www.kaggle.com/edqian/twitter-climate-change-sentiment-dataset

