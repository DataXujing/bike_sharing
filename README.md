Read an article on the usage of open data for bicycle traffic planning on my [Medium](https://medium.com/@alex_kruse/nutzung-von-open-data-im-rahmen-der-radverkehrsstrategie-9cf85a813c48).

## Visualization of usage of bike sharing network in Hamburg (StadtRAD)
 + Data: http://data.deutschebahn.com/dataset/data-call-a-bike
 + Use the map here: http://207.154.245.18/shiny/stadtrad/ or https://alexkruse.shinyapps.io/stadtrad/
 + I created a [Poster](https://github.com/kruse-alex/bike_sharing/blob/master/Kruse_poster-session.pdf) for [useR 2017](https://user2017.brussels/posters) Poster Session and done a [workshop](https://github.com/kruse-alex/osm_brussels) for [OpenStreetMap](https://www.eventbrite.com/e/open-bike-data-mapping-with-openstreetmap-registration-34806438996).
 
My interactive map shows the bike sharing usage of StadtRAD, the bike sharing system in Hamburg – Germany. The data is available on the open data platform from Deutsche Bahn, the public railway company in Germany. The last new StadtRAD station was put into operation in May 2016, that is why a have chosen to display the usage of June 2016. The brighter the lines, the more bikes have been cycled along that street. 

![alt text](https://github.com/kruse-alex/bike_sharing/blob/master/bike_usage_HH.png) 
 
From data processing and spatial analysis to visualization the whole project was done in R. I have used [leaflet](https://rstudio.github.io/leaflet/) and [shiny](https://shiny.rstudio.com/) to display the data interactively. The bikes themselves don’t have GPS, so the routes are estimated on a shortest route basis using the awesome [CycleStreets API](https://www.cyclestreets.net/api/). The biggest challenge has been the aggregation of overlapping routes. I found the overline function from the [stplanr package](https://github.com/ropensci/stplanr) very helpful. It converts a series of overlaying lines and aggregates their values for overlapping segments. The raw data file from Deutsche Bahn is quite huge so I struggled to import the data into R to process it. In the end the read.csv.sql function from the [sqldf package](https://cran.r-project.org/web/packages/sqldf/sqldf.pdf) did the job.

To further analyze the StadtRAD data I also took the full booking data from 2016 and did some diagrams. The first one is a calendar heatmap where you can see the amount of rented bikes aggregated on a daily basis. On the top of the graph you can see a barplot representing the rented bikes aggregated by the day of week. On the right you see a barplot to display the StadtRAD usage for each calendar week of 2016. The idea to use calendar heatmaps to display bike sharing usage comes from [Via Velox](http://infovis-mannheim.de/viavelox/). The code to create this heatmap is also in this Repo.

![alt text](https://github.com/kruse-alex/bike_sharing/blob/master/superheat.png)

I also created joyplots with ggplot to display and analyze the data. The first one shows the daily usage of every weekday. You can see big differences between working days and the weekend.

![alt text](https://github.com/kruse-alex/bike_sharing/blob/master/joyplot_dayofweek-time.png)

The next diagram shows the daily usage per month. You can see that people renting bikes earlier in the summer.

![alt text](https://github.com/kruse-alex/bike_sharing/blob/master/joyplot_month-time.png)

The last diagram shows the differences between the months on a daily basis. You can see that people were not using StadtRAD a lot during chrismas.

![alt text](https://github.com/kruse-alex/bike_sharing/blob/master/joyplot_month-weekdays.png)
