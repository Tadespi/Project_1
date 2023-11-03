# Shark attack analysis

First, run "Get_Clean_Starter_Data.ipynb"
	This will download current data and do some very basic cleaning.

After that, each of the ipnyb files is it's own cleaning and analysis for a different topic/question.
We divided the project by question, and each of us cleaned the data (beyond the initial steps) with regard to the specific question being analyzed.

1) Are there differences between sexes when it comes to shark attacks? (Shark attack gender analysis.ipynb)
Analysis: For gender analysis, the focus was on the Sex column. To clean the data, entries that were non-determinant or empty were dropped. Then incidents involving males and females were compared, including a closer look at provoked/unprovoked attacks and whether the findings were consistent across countries.
Conclusion: Men are attacked by sharks more than women. Among reported incidents of shark attacks, men provoked sharks more. Findings that men are attacked more is also true across the top 20 countries, though the difference varies.


2) What activities are associated with shark attacks? (shark_activities_species.ipynb)
Analysis: For activity analysis, the focus was on the activities, whether the attacks were provoked or unprovoked, and whether the attacks were fatal. There was a lot of clean up needed to categorize the activities. In the initial dataset, activities were general descriptions, so we had to do a lot of manual review and string replacement to fit them into general categories. Once the data was cleaned sufficiently, we analyzed the number of attacks by activity to see how many of each were provoked, unprovoked, or questionable, and how many were fatal or nonfatal. Finally, we analyzed the percentage of attacks that were fatal by whether they were provoked, unprovoked, or questioanble.
Cleanup also included attempting to categorize species, but after some work it was determined that the amount of data on species was not sufficient to draw any conclusions.
Conclusion: Most attacks involve common water activites, such as swimming, surfing, and fishing. Most attacks - fatal or otherwise - are unprovoked, so it follows that people would be doing commonplace activies when they are attacked. Swimming has the highest number of fatal attacks, possibly because it is the water activity with the least protection from nature.


3) What time of day / year has the most attacks? (Shark Attacks based on Month and Time.ipynb)
Analysis: For time of day analysis, the biggest hurdle was data formating. The reported times varied from numerical (12h00) to nominal (Afternoon). To get all as many values as possible into categories, a series of regex string replacements were done to try to get everything to a numerical hour. We did substitution for nominal values ("Afternoon" became "14", for example). After converting nearly all of the values to an number, the hours were binned into parts of the day: Morning, Midday, Evening.
Months were easier to access as most of the data have an 8 digit date (format 'YYYY-MM-DD'). A simple regex that extracted the middle set of digits got us the month.
Finally, counts of the number of incidents in each time category and month were evaluated.
Conclusion: Sharks attack more people during the middle of the day and the middle of the year.

4) Where do sharks attack most frequently? (Shark_Attack_Locations.ipynb)
Analysis: For location analysis, the most difficult part was finding latitude and longitude coordinates for the locations. This was complicated by the fact that locations are stored inconsistently across three fields: Country, Area, and Location. To find coordinates, we created a string from these three fields and attempted an API call to Geoapify. If the confidence level was greater than 80%, we accepted the results. For results below 80%, additional API call attempts were made with varying deconstructions and rearrangments of the location-based fields until an acceptable result was found or all reasonable options were exhausted.
Next, the coordinates were rounded to the nearest integer, effectively grouping the results. The count of each latitude-longitude pair was determined and the data was plotted on a map plot with the size of the dot corresponding to the number of incidents in a given location. Additionally, for coordinates with only a single incident, the description of the injury was added to the hover. This allowed for results to be literally spot-checked on the interactive map.
Finally, the absolute value of the latitude was determined and groups of 10 were binned. The number of attacks in each latitude group was compared to determine if distance from the equator is a factor in shark attacks.
Conclusion: Attacks are more common in warm places that have an ocean coast. Subtropical zones are the location of the highest number of attacks, followed closely by tropical zones - suggesting that sharks are most likely to attack in warm waters. Colder, non-tropical zones have very few attacks. Also, in some places, shark attacks are particularly common, likely due to factors not included in our analysis.

Implications:
Avoid swimming in warm waters where sharks live, especially during the middle months of the year and during the middle of the day. Avoid activities that involve splashing near the surface of the water. Males should be extra cautious.

Further research:
There are a lot of unanswered questions brought up by this analysis. For example:
Are shark more likely to attack in warm waters, or is it just that people are more likely to spend time in waters that are warm - resulting in greater opportunities for an attack? 
Are sharks attracted to people who are swimming and surfing, or are swimming and surfing just the most common activities in waters that happen to have sharks living in them?
Are men more likely to be attacked because they smell different to a shark, or do men just spend more time in the water? Have the advances in women's equality in society - and the greater freedom to engage in recreational activities - had any impact on this disparity?
