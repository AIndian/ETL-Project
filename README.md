# ETL Project:
# Impact of Presidential Events on the U.S. Stock Market

April 17, 2021

By Amol Bhatia, Jennifer Duffy, Robin Evans

Objective
Our objective was to Extract, Transform, and Load data concerning the United States stock market in relation to recent presidential administrations so that analysts can track movements of the market during presidencies, based on events such as executive orders and cabinet appointments. 

Our time period included: the first and second terms of Barack Obama (January 20, 2009 – January 20, 2017), the only term of Donald Trump (January 20, 2017 – January 20, 2021), and the beginning of the first term of Joe Biden (January 20 , 2021 – April 17, 2021).

Extraction

We used three different datasets from the platforms listed below. These were the most recent ones available. The sources for our data are as follows:
 
•	Alpha Vantage API (https://www.alphavantage.co/documentation/)
•	Executive Orders from the Federal Register of the National Archives (https://www.federalregister.gov/presidential-documents/executive-orders)
•	U.S. Cabinet Appointments from data.world (https://data.world/government/us-cabinet-appointments)

Prior to choosing these three datasets, we looked at a number of other sources, including 34 different “president” datasets on data.world; however, we rejected them because the information was not recent enough or the datasets were linked to elections, which is not in our scope.  The Alpha Vantage API is the most up-to-date as it provides live market data with no delay other than network delay. We used csv files for the executive order and cabinet appointment files, which we read into our Jupyter notebooks using Pandas. For the stock market, we extracted data about an exchange-traded fund (ETF) termed the Dow Jones Industrial Average (DIA) using an API. According to https://www.ssga.com:

•	“The SPDR® Dow Jones® Industrial AverageSM ETF Trust seeks to provide investment results that, before expenses, correspond generally to the price and yield performance of the Dow Jones Industrial AverageSM (the “Index”).
•	The Dow Jones Industrial AverageSM (DJIA) is composed of 30 “blue-chip” U.S. stocks.
•	The DJIA is the oldest continuous barometer of the U.S. stock market, and the most widely quoted indicator of U.S. stock market activity.
•	The DJIA is a price weighted index of 30 [blue-chip] component common stocks.”


Transformation

Our first step in cleaning the datasets involved figuring out which data and columns were relevant. For example, we filtered the date range for all datasets to match the same time frame (for the Obama, Trump, and Biden presidential terms) and then converted the object to datetime.   We dropped unnecessary columns such as “Dividend Amount” for the stock market dataset, the “Scandal Flag” for the appointments’ dataset, and  “Citation” and “Document Number” from the executive orders’ dataset. We renamed columns to more comparable names. Because we are matching the data on date, we renamed all the columns relating to dates to “Date.”  

![image](https://user-images.githubusercontent.com/75215001/115121947-5a553d80-9f83-11eb-90a3-2ba608342fcd.png)

Figure 1: Screenshot of original ETF data extracted from API


![image](https://user-images.githubusercontent.com/75215001/115122024-c46de280-9f83-11eb-800a-a3e89d4c90ff.png)


Figure 2: Screenshot of cleaned stock market dataframe

For the executive orders data, we merged three different .csv files (one for each of the three presidents) into one final .csv file, titled eo_df.csv.


 ![image](https://user-images.githubusercontent.com/75215001/115122039-d059a480-9f83-11eb-8563-cf80075227b1.png)

   	        
Figure 3:  Screenshot of Trump executive orders .csv file from Federal Register website


![image](https://user-images.githubusercontent.com/75215001/115122048-dc456680-9f83-11eb-97cd-c653458d8817.png)
 

Figure 4: Screenshot of final Executive Orders dataframe
			   
After cleaning the datasets, we started merging. To start, we created an ERD using quickdatabasediagrams.com.  Using this diagram, we planned our primary and foreign keys for connecting the datasets and confirmed that our link between the datasets would be both dates and president. For example, we made “President” a foreign key to link the “appointments.csv” and “eo_df.csv.”  



Load

During the Load phase, we prepared the final .csv files (executive.csv,  DIAdata.csv, and eo_df.csv) to be loaded into PgAdmin. We set an index column and dropped extra columns. We changed the headers of each data frame so that the relationship between the fields could  be seen more easily. Next, using Python in our Jupyter Notebook, we created an engine to connect to the postgreSQL server running through PgAdmin4. We created a database and respective tables to match the columns from the final Panda’s data frame (see SQLLoad.ipynb) using MYSQL. Next, we connected to the database using SQLAlchemy and loaded the result. If a database already existed, it was opened; otherwise, a new one was created. Our data was then pushed to the server. This allows the performance of queries depending on the desired criteria.

![image](https://user-images.githubusercontent.com/75215001/115122057-ec5d4600-9f83-11eb-8475-6cc3dc7039b3.png)
 

Figure 5: Screenshot of PgAdmin database


Summary

We extracted and cleaned these datasets so that analysts can track the movement of the stock market based on factors relating to the three most recent presidencies, such as signed executive orders and cabinet appointments.  According to Investopedia.com, in an article (https://www.investopedia.com/presidents-and-their-impact-on-the-stock-market-4587369)  titled, “Presidents and the Stock Market,” presidents can affect the market in a number of ways. The article states, “Because the president is responsible for implementing and enforcing laws, they have some control over business and market regulation. This control can be direct or through the president's ability to appoint cabinet secretaries, such as the head of the Department of Commerce, as well as trade representatives.” Using this data, analysts can compare when executive orders were signed and how performance of the DIA ETF, which we used as an indicator for the stock market, was affected. They will also be able to examine when cabinet secretaries were appointed to see the affects on the stock market at those times.  The final output will help analysts to show whether the events of certain presidencies have a positive or negative effect on the stock market so that we can better predict market behavior for the Biden and future administrations based on these factors. 



# ETL-Project Proposal 
Tracking trends using Presidential Events


ETL Project Proposal


ETL Project: Impact of presidential events for Pres. Obama & Pres. Trump on the US Stock Market

Purpose/Scope: Track movement in the stock market based on presidential events during the presidencies of Obama & Trump.  Also, the dataset is inclusive of events during Present Biden for future projections.

Summary: The datasets used for ETL Project will be presented to the assigned Data Analysts for the purposes of determining how the stock market is impacted by events that occurred during the precedency for Pres. Obama and Pres. Trump.

The following data transformations will be performed on the data:
drop all null values
drop duplicate dates
sort by date
filtered by average date
drop irrelevant columns

Data Source:
1. Federal Register - https://www.federalregister.gov/presidential-documents/executive-orders
2. Data World - https://data.world/datasets/president
3. Yahoo Finance API - finance - [pip install finance] (yahoo finance library)



	

![image](https://user-images.githubusercontent.com/76014274/114641840-cf352880-9ca0-11eb-9875-25ba93eab0be.png)
