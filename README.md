# Forest Fire Modeling and Visualization Project

A project designed by Anshuman Saxena, June You, Lingxiao Leng, Katty Wu and Aidan Miller for the STAT 385 course offered at the *University of Illinois at Urbana-Champaign* during the Spring 2017 semester.

## Description of Project

We intended to create a dynamic and interactive visualization of the occurences of forest fires all over the United States. This visualization was designed to be used as a go-to for online news and media outlets when looking for historical forest fire records and data. 

This project was divided into two major parts: 
* data procurement and cleaning
* data visualization

### Data Procurement and Cleaning

The data was obtained in geospatial format (.shp) from the Monitoring Trends in Burn Severity (MTBS) website (http://mtbs.gov/data/individualfiredata.html). Since we were not familiar with this type of data, we used the software **QGIS** to convert this data into a *.csv* file. The dataset had 19,184 observations and 31 variables; it contained information on the occurences of forest fires from 1984-2014 in the United States. The variables of use to us in this data set were the Latitude, Longitude, Year, Month, Day, State and Acres Burned. Since the Year, Month, and Day were in seperate columns, we decided to paste the three columns together in order to make further analysis easier; we decided to drop the Year, Month and Date and just keep one variable called 'Date'.

Upon subsetting the dataset to retain just these five variables, we decided to use the R package **ggmap** to translate the coordinates to their approximate city using the *revgeocode* function. By gathering the city name and combining it with the date, we were able to cross-reference it with the weather data found on *wunderground.com*'s API, using the **weatherData** package. Initially, we tried to extract the weather data for all 19,184 observations, but that seemed to be too cumbersome and hence took a very long time. Therefore, we decided to to further subset the data by selecting forest fires in few of the Midwest states after the year 2010, which were of personal importance to us since we were located in Champaign, IL. The states we chose were Illinois, Indiana, Missouri, Michigan, Wisconsin and Iowa. Finally, we ended up with 96 observations. 

Our data was now ready for visualization...

### Data Visualization

In order to efficiently display all the data points, we decided to create a map. This was a challenge in itself; finding the right package and getting it to properly display the points proved hectic. The package we started with was a **plotly** map, but it was not detailed enough, especially when viewing areas on the map up close. Finally, we decided to use the **leaflet** package, which allowed us to create a much more detailed map. For our project, the plot required a more location-based map; using towns and states as a reference rather than the land conditions. Used in conjunction with ‘Shiny’, our model finally began to take shape. 

**Shiny** turned out to be perfect for our intentions, as it is centered around user interactivity; taking user input on what points were to be filtered, and then automatically updating the display to match the requests. Once we managed to plot our data on the map, we set out to take advantage of **Shiny's** features. The UI our model implements a slider for each year, or period of years from anywhere in the data set, a checkbox for each of the selected US States, and a histogram of the selected data points. That Histogram is generated automatically when the results are updated, and shows frequency over time. Another feature we added was a visual representation of the size of each wildfire, in acres, represented with color; going from red, at 200,000 acres, to blue, at 1,000,000 acres.

Lastly, to bring it all together within the model, a pop-up function was created. This would be activated by clicking any point on the map. This would display a textbox containing information about the incident including the date, the approximate town, the size of the blaze, and the predicted likelihood of an incident occurring at that location now; all in one little paragraph. 
