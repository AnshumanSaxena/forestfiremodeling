# Forest Fire Modeling and Visualization Project

A project designed by Anshuman Saxena, June You, Lingxiao Leng, Katty Wu and Aidan Miller for the STAT 385 course offered at the *University of Illinois at Urbana-Champaign* during the Spring 2017 semester.

## Description of Project

We intended to create a dynamic and interactive visualization of the occurences of forest fires all over the United States. This visualization was designed to be used as a go-to for online news and media outlets when looking for historical forest fire records and data. 

This project was divided into two major parts: 
* data procurement and cleaning
* data visualization

### Data Procurement and Cleaning

The data was obtained in geospatial format (.shp) from the Monitoring Trends in Burn Severity (MTBS) website (http://mtbs.gov/data/individualfiredata.html). Since we were not familiar with this type of data, we used the software **QGIS** to convert this data into a *.csv* file. The dataset had 19,184 observations and 31 variables; it contained information on the occurences of forest fires from 1984-2014 in the United States. The variables of use to us in this data set were the Latitude, Longitude, Year, Month, Day and State. Since the Year, Month, and Day were in seperate columns, we decided to paste the three columns together in order to make further analysis easier; we decided to drop the Year, Month and Date and just keep one variable called 'Date'.

Upon subsetting the dataset to retain just these five variables, we decided to use the R package **ggmap** to translate the coordinates to their approximate city using the *revgeocode* function. By gathering the city name and combining it with the date, we were able to cross-reference it with the weather data found on *wunderground.com*'s API, using the **weatherData** package. Initially, we tried to extract the weather data for all 19,184 observations, but that seemed to be too cumbersome and hence took a very long time. Therefore, we decided to to further subset the data by selecting forest fires in few of the Midwest states after the year 2010, which were of personal importance to us since we were located in Champaign, IL. The states we chose were Illinois, Indiana, Missouri, Michigan, Wisconsin and Iowa. Finally, we ended up with 96 observations. 

Our data was now ready for visualization...

### Data Visualization
