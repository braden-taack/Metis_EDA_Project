Braden Taack
### NYC Subway EDA for WTWY
#### September 17, 2021
---

#### Abstract
  
The goal of this project is to use exploratory data analysis methods to help direct the canvassing resources of the WomenTechWomenYes (WTWY) organization. I worked with turnstile data from the [MTA subway data website](http://web.mta.info/developers/turnstile.html) and used it to filter down to the busiest stations, days, and times. After cleaning the data I plotted my results for each using Matplotlib and Seaborn. 

#### Design

This project originates from the request for help from the WTWY organization. They are a newer, inclusive group focused on increasing the participation of women in technology, and to concurrently build awareness and reach. The group canvasses subways entrances to gather emails and to send out tickets to their annual gala to responders. Their goal is to maximize attendance at their gala, so my goal is to maximize the number of people they can potentially talk to at the subway entrances. Leveraging the MTA data, I aimed at calculating daily and hourly entries for each station to categorize the busiest. Leading WTWY to the busiest stations at the right times should be sure to get extra gala attendees. 

#### Data

The MTA dataset consists of 2,720,549 entries for cumulative turnstile entries and exits with their respective date and times. The time range of the data is 03/27/2021 to 06/25/2021. The basis for this date range was to line up the analysis with the 3 months leading up to the gala which is said to take place at the beginning of summer. The data can be grouped into C/A, UNIT, SCP, STATION, and LINENAME. See the [MTA reference](http://web.mta.info/developers/resources/nyct/turnstile/ts_Field_Description.txt) for the descriptions of each grouping. For the purposed of this project, station was used as the primary grouping method. Exits were excluded from analysis based on the knowledge that subway riders only have to scan into the station. A sure scan and turn of the turnstile was deemed more reliable than faith on 1:1 exits through turnstiles. Further work could go into doing analysis on more specific groups or incorporating exits. 

#### Algorithms

*Feature Engineering*
1. Calculating the true entries per day and per hourly period from cumulative turnstile data. 
2. Developing a column of datetime ojects using the string based columns date and time for chronological sorting. 
3. Cleaning out 55 discovered duplicates. 
4. Converting inconsistent time frames from different turnstiles into distinct 2 hour intervals for all data. 
5. Creating dataframes for and plotting the top 10 busiest stations, top 5 stations daily entries time series for full date range of database, average entrances by day of the week for the top 5 stations, and the average entries over 2 hour periods for the weekdays using the top 5 stations. 

*1. Calculating the true entries*  
The MTA data presented some unique scenarios that made the data unusable at first glance. The count for the entries and exits were actually cumulative from an unknown point in time, and the direction they counted differed between some turnstiles. Some turnstiles increased through the day and others decreased. This presented a unique challenge. The challenge was solved by grouping the turnstiles together, using the .diff() method to calculate the actual change in the time block, taking the absolute value to ensure all were counting in the right direction, and lastly excluding outliers with a entries count > max_obs. The max_obs was set at 100,000 with the goal of excluding obvious outliers and differences calculated for different turnstiles. The risk of excluding real days or hours with abnormally large entries was deemed acceptable as the focus was on looking at the average day and the patterns that followed it. 100,000 was justified after calculating the mean daily entries for the busiest station, 34 ST-PENN STATION, to be just over 40,000 from the raw data. 100,000 seemed to be large enough as not to influence the results after trial and error. 

*2. Developing datetime object based DATE_TIME column*  
The MTA data also presented an issue with having the date and time as strings in seperate columns. In its raw state, chronological sorting, which was needed to get the .diff() calc correct, was not working. Thanks to pandas intelligent datetime integration, the .to_datetime() method was performed to generate the necessary column.  

*3. Cleaning out duplicate data*  
Upon inspection, there were 55 duplicate data points with the same turnstile and datetime. The reason for these was due missed audits that had been recovered described as 'RECOVR AUD'. The desired data for the analysis came with 'REGULAR' as the descriptor, as these had sensicle values for the cumulative data based on the surrounding entries. The dataframe was grouped by turnstile again, ordered such that 'REGULAR' appeared first, and then duplicates were dropped will keeping the first occurence. 

*4. Converting inconsistent time frames*  
Another issue came about when attempting to plot the hourly data. The time intervals for data collection were irregular amongst the turnstiles. A simple for loop was utilized to iterate through the datetime objects and group them into the appropriate 2 hour interval bin. 

*5. Plotting the calculated data*  
Dataframes were utilized as the core for each chart. The first was a bar plot of the 10 busiest stations calculated by the mean for daily entries. The 3 subsequent charts all used the top 5 stations discovered in the first chart. The second chart visualized the calculation of the average daily entries by day of the week. The third chart plotted the calculation for the time series of average entries for 2 hour periods but only on weekdays. Weekends were excluded because of their low average entry results. Originally, a plot was developed for each weekday. However, these were converged into a single average weekday after noting the likeness between the individual days. Lastly, the fourth plot was a line chart of the cleaned time series of daily entries for the full date range of the data. 

#### Tools

- [get_mta.py](https://github.com/braden-taack/Metis_EDA_Project/blob/main/get_mta.py) for SQL database creation (Provided by [Metis](https://github.com/thisismetis))
- SQLAlchemy for data ingestion and basic exploration
- Numpy and Pandas for data manipulation
- Matplotlib and Seaborn for plotting

#### Communication
Please see my [presentation deck](https://github.com/braden-taack/Metis_EDA_Project/blob/main/NYC%20Subway%20Analysis%20for%20WomenTechWomenYes%20Gala.pdf) or images in my [github repo](https://github.com/braden-taack/Metis_EDA_Project) for accompanying charts and code. 
