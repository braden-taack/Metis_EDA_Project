___
Braden Taack
### WTWY EDA Project Proposal
#### September 8th, 2021
___
  

#### Question/need:
* What is the framing question of your analysis, or the purpose of the model/system you plan to build?   
  
  The framing question is how can we best direct the canvasing resources of the WomenTechWomenYes organization. The group utilizes street teams at entrances to subway stations to collect email addresses and send out tickets to their gala. With it being impossible to be present at every station, it is key to focus on the ones that have the most opportunity for WTWY. By analzing the subway data, we can direct them to the best areas to focus on to maximize the number of people at their gala. 

* Who benefits from exploring this question or building this model/system?  
  
  The WTWY team will benefit from knowing the subway system better. They can hopefully get more people attending their Gala to grow their group. As a second effect, women of NYC will benefit by learning about opportunities in tech. 

#### Data Description:
* What dataset(s) do you plan to use, and how will you obtain the data?  
  
  I will start with the [MTA Turnstile Data](http://web.mta.info/developers/turnstile.html). The website has data files on turnstile data across the subway system with a file for each day. I will write a Python script based on the one provided by Metis to automatically pull in data starting on 9/9/2021 and ending on 6/9/2021 into a pandas dataframe.  
  
* What is an individual sample/unit of analysis in this project? What characteristics/features do you expect to work with?  
  
  An individual unit will be an entry or exit from a specific turnstile. This can be generalized to turnstile entries/exits per station or even per line.  
  
* If modeling, what will you predict as your target? 

  No modeling expected on this project.  
  
#### Tools:
* How do you intend to meet the tools requirement of the project?  
  
  The data will be ingested into a SQL database. Basic cleanup and filtering will likely be done using SQLite, DB broswer for exploration, and SQLAlchemy on a Jupyter Notebook to create a final version of the database. The final database will be imported into python using pandas dataframes. More advanced analytics will be performed using pandas. Final results will be made into histograms/barcharts/line charts using Matplotlib. 
* Are you planning in advance to need or use additional tools beyond those required?  
  
  At this time, additional tools are not planned on being used. Though, I may mess around with writing the python code in VIM given enough time. 

#### MVP Goal:
* What would a [minimum viable product (MVP)](./mvp.md) look like for this project?  
  
  The goal MVP will have 3 months of data from the MTA turnstile data analyzed. It will include several of the hottest stations and time frames for those stations. A top 10 stations with several times per station and their respective number of visitors presented in a bar chart or histogram will be included. A line chart plotting the number of entries vs time of day with a line for each of the top 10 stations could also work. Both plots could provide a large enough subset of stations to WTWY to have a direct path forward with some flexibility on when and where to set up. 
