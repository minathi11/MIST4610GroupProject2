# MIST 4610 Group Project 2

Identifying a data set and answering two interesting questions about the data through Tableau models.

## Team Name & Members
1. David Tran [@dstudent17](https://github.com/dstudent17)
2. Nick Kalenik [@NickKalenik](https://github.com/NickKalenik)
3. Minathi Mekala [@minathi11](https://github.com/minathi11)
4. Ngoc Nguyen [@ngocpn1](https://github.com/ngocpn1)
5. Anthony Ramage [@anthonyramage](https://github.com/anthonyramage)
6. CJ Tumlin [@CJTumlin](https://github.com/CJTumlin)
## Dataset Description
The dataset reports the details of crashes within Montgomery County of Maryland and was obtained from https://catalog.data.gov/dataset/crash-reporting-drivers-data. The dimensions of the dataset contain 43 columns and 170,218 rows. The data is separated into different main categories - report information: report number, local case number, ACRS report type, and agency name; when and whereabouts of the crash: crash date/time, municipality, latitude, longitude, location, route type, road name, cross-street type, cross-street name, off-road description; involved parties: related non-motorist, person ID, driver at fault, driver substance abuse, non-motorist substance abuse, and injury severity, drivers license state, driver distracted by; collision details: collision type, vehicle damage extent, vehicle first impact locations, vehicle second impact location, vehicle body type, vehicle movement, vehicle continuing dir, and vehicle going dir; vehicle information: vehicle ID, vehicle year, vehicle make, vehicle model, equipment problems; environmental conditions: weather, surface condition, light, traffic control, speed limit; and special circumstances: circumstance, driverless vehicle, and parked vehicle.

Almost all of the columns have string data types except for local case number (whole number), crash date/time (Date/Time), speed limit (whole number), vehicle year (whole number), and longitude & latitude (decimal number).

This dataset provided an abundance of information and allowed us to thoroughly build detailed visualizations.


## Our Two Questions Explained
1. How do the frequency and severity of car crashes vary over different months in Maryland, and are there specific patterns associated with levels of injury severity to drivers when the cars are “moving at a constant speed” vs when they are not “moving at a constant speed”?

We chose this first question because it enables us to visualize the relationship between the injury severity, compared with non-constant/constant speed of cars, and frequency of car crashes and how it relates to the months throughout the year in the state of Maryland. From a public safety perspective, police departments can use the data from this question to create strategic plans to prioritize enforcement of traffic laws and road safety services in months of the year with high frequency and severity of car crashes in Maryland. The decision of whether there should be a greater personnel patroling the streets or emergency services readily available be supported by the data from this question. From a regulatory perspective, governmental bodies like the Federal Highway Administration or Maryland Department of Transportation can make adjustments to road infrastructure or traffic laws based on the months of the year that correlate with high crash frequency. Specifically, adjustment of speed laws of roads can be derived from the relationship of whether constant/non-constant speed on the road has led to greater or lower car crash severity on that particular road. An example would be that if there are high amounts of constant speed car crashes, there may be more stop lights. To conclude, this question allows for greater data-backed decisions in Maryland's public safety and highway management which overall make drivers more safe on the road.

2. What are the geographic hotspots for car crashes in Maryland, and how do these locations of crashes correlate with the driver of the vehicles being impaired or under the influence vs not being impaired?

We chose this second question because it enables us to visualize the geographical area of car crashes in Maryland and whether the car crash involved an impaired driver. Through this we are able to recognize patterns of where car crashes happen most or least and what locations involved high or low levels of impaired drivers involved in a crash. This visualization of data gives entities like police departments and emergency health services greater understanding to what geographical areas to focus their services and where their base locations should be held. Further, police departments are able to know to have greater enforcement of the use of substances for drivers in areas of greater car crashes involving impaired drivers. All in all, this question allows for more informed decision-making for police departments and emergency health services which lead to greater well-being of those in Maryland.

## Data Set Manipulations and Filters
For our FIRST question, we had to create a calculated field utilizing the "Vehicle Movement" field. This field had 23 domains, which included: 
- ACCELERATING
- BACKING
- CHANGING LANES
- DRIVERLESS MOVING VEH.
- ENTERING TRAFFIC LANE
- LEAVING TRAFFIC LANE
- MAKING LEFT TURN
- MAKING RIGHT TURN
- MAKING U TURN
- MOVING CONSTANT SPEED
- N/A
- NEGOTIATING A CURVE
- OTHER
- PARKED
- PARKING
- PASSING
- RIGHT TURN ON RED
- SKIDDING
- SLOWING OR STOPPING
- STARTING FROM LANE
- STARTING FROM PARKED
- STOPPED IN TRAFFIC LANE
- UNKNOWN
Because we wanted to analyze the difference in crash severity between a car moving at a constant speed and a car moving at a non-constant speed, we had to condense all of these domains into two categories in a new calculated field named "Constant or Non-Constant Speed?" The two categories included:
- CONSTANT SPEED
- NON-CONSTANT SPEED
The calculation to arrive at this result is as follows:

IF [Vehicle Movement] = 'UNKNOWN' OR [Vehicle Movement] = 'N/A' THEN NULL 
ELSEIF [Vehicle Movement] = 'MOVING CONSTANT SPEED'
THEN 'CONSTANT SPEED'
ELSE 'NON-CONSTANT SPEED'
END

When using this calculated field in our model, we filtered out domains such as "UNKNOWN", "N/A", "OTHER", and any null values to make our model more accurate.

For our SECOND question, we had to create a similar calculated field from the "Driver Substance Abuse" field. This field had 12 members, which included:
- ALCOHOL CONTRIBUTED
- ALCOHOL PRESENT
- COMBINATION CONTRIBUTED
- COMBINED SUBSTANCE PRESENT
- ILLEGAL DRUG CONTRIBUTED
- ILLEGAL DRUG PRESENT
- MEDICATION CONTRIBUTED
- MEDICATION PRESENT
- N/A
- NONE DETECTED
- OTHER
- UNKNOWN
Since we wanted to compare impaired car accidents versus non-impaired car accidents, we created a calculated field named "Impaired or Non-Impaired" with two members that included:
- NO IMPAIRMENT
- IMPAIRED 
The calculation to arrive at this result is as follows:

IF [Driver Substance Abuse] = 'UNKNOWN' OR [Driver Substance Abuse] = 'N/A' THEN NULL
ELSEIF[Driver Substance Abuse] = 'NONE DETECTED'
THEN 'NO IMPAIRMENT'
ELSE 'IMPAIRED'
END

When applying this calculated field to our models, we filtered out "N/A", "OTHER", "UNKOWN", and any null values to make the results more accurate.

## Analysis & Results
![Screenshot 2023-12-04 at 5 39 21 PM](https://github.com/NickKalenik/MIST4610GroupProject2/assets/148160069/c37d04ec-745a-4bec-8f86-d08226635640)
The most obvious result of this analysis is that the frequency of non-constant speed car crashes is always higher than the frequency of constant speed crashes, indicating that variable speeds contribute to a higher risk of crashes across all severity categories. This result makes sense, as it is much more likely for a car to be turning, accelerating, or decelerating as opposed to driving at a constant speed when in an accident. The red segments, representing possible injury crashes, although smaller in comparison to other severities, are an important visual element. Their presence in the non-constant speed section underscores the critical nature of speed variation in the severity of accidents. The only correlation we see between injury severity and car movement is that "Possible Injury" is generally slightly higher in car accidents with non-constant speeds.

Finally, the visualization shows us that car accidents tend to occur more in the winter months of the year. This makes sense in Maryland, as driving conditions are most likely more dangerous in the winter, leading to more accidents. A more in-depth analysis of the data reveals that certain months, such as December and January, could show a marked increase in the incidence of non-constant speed crashes, which may be attributed to holiday travel and adverse weather conditions.

![Screenshot 2023-12-04 at 5 46 30 PM](https://github.com/NickKalenik/MIST4610GroupProject2/assets/148160069/beccc3e6-9040-4bdb-9ee7-a155a073b8a1)
In our second data visualization, the most noticible trend is that car crashes are much more frequent in areas closer to D.C., which makes sense as many more cars would be driving in this area as opposed to further outside of the city. It is evident that impaired driver accidents concentrate closer to D.C., and taper off along roads that lead further away. This is likely due to the fact that many more bars, restaurants, and alcohol serving locations are located closer to D.C. as opposed to further away. While this is a high overview, a closer view allows for distinction of crashes along individual roads.

<img width="1206" alt="Screenshot 2023-12-05 at 11 08 34 AM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/272896d5-badf-4055-b991-5e09b693b115">

A bar graph of the count of accidents within each category helps us to visualize that while the number of impaired driver accidents may seem high when looking at the overview map, they account for a relatively low number of accidents when compared to those of unimpaired drivers.

<img width="1399" alt="Screenshot 2023-12-05 at 11 07 58 AM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/8f889f0d-d2f0-4663-9e73-70e863033ef9">
As stated previously, a more zoomed in observation of this data map allows for crash data visualization along specific roads. In this particular section of the map, it is clear to see that accidents are happening with the greatest frequency on what appears to be main roads, which concentrate around a particular center of activity. This visualization lends to a city center with a highway loop around the outside. Crashes are interspersed along side roads and throughout the loop, but this visualization allows for these "highways" to be indentified as areas of high accident rates. Further, it can be seen that impaired accidents occur along these high traffic roads and in the center of activity at a higher rate than they occur when crashes are recorded off of these clearly identificable "highways".



# Honors Option Third Question
3. What manufacturing years of cars are most frequently involved in accidents and tend to sustain the highest level of damage?

I chose this question to model because I wanted to look at the damage sustained by the different manufacutring years of cars in an attempt to see if there were any noticeable trends that arose around these different years of cars. This visualization could help to determine if any particular year of manufacturing showed poor safety and quality, or if a particular year resulted in less damages due to a new regulation or safety standard. I also wanted to view the body types of cars involved in accidents those years, in order to determine if an increase in a particular body type may have an impact on whether or not the overall damages of cars made in that year increased.

## Data Set Manipulation and Filters
In order to accomplish the first part of this data visualization, the combined bar and line chart, I first filtered the Vehicle Manufacturing Year by a range of dates from 1995 to 2019. I found that not enough data was available on either side of this range to provide enough evidence for determining trends in damage extent.
I then filtered the data based Vehicle Damage Extent. I only used crashes that had reported some form of damages, and removed crashes with N/A, OTHER, or UNKOWN damages incurred.

To accomplish the second part of this data visualization, a bar chart of when the crashes occurred, I used the same two filters as above.

For the third part of this visaulization, the pie chart of vehicle body types, I used the same filters as above, with a slider based filter on the Vehicle Year, as well as a new calculated field. In order to summarize all Vehicle Body Types into a a few similar categories, I had to use a calculated field to aggregate them based on similarities. I grouped all vehicles into 6 Groups, PASSENGER CAR, TRUCK, EMERGENCY VEHICLE, MOTORCYCLE, BUS, and OTHER. I used this code to do that.

IF \
   [Vehicle Body Type] = "ALL TERRAIN VEHICLE" OR \
   [Vehicle Body Type] = "AUTOCYCLE" OR \
   [Vehicle Body Type] = "FARM VEHICLE" OR \
   [Vehicle Body Type] = "LOW SPEED VEHICLE" OR \
   [Vehicle Body Type] = "N/A" OR \
   [Vehicle Body Type] = "OTHER" OR \
   [Vehicle Body Type] = "RECREATIONAL VEHICLE" OR \
   [Vehicle Body Type] = "SNOWMOBILE" OR \
   [Vehicle Body Type] = "UNKNOWN" \
THEN "OTHER" \
ELSEIF \
   [Vehicle Body Type] = "AMBULANCE/EMERGENCY" OR \
   [Vehicle Body Type] = "AMBULANCE/NON EMERGENCY" OR \
   [Vehicle Body Type] = "FIRE VEHICLE/EMERGENCY" OR \
   [Vehicle Body Type] = "FIRE VEHICLE/NON EMERGENCY" OR \
   [Vehicle Body Type] = "POLICE VEHICLE/EMERGENCY" OR \
   [Vehicle Body Type] = "POLICE VEHICLE/NON EMERGENCY" \
THEN "EMERGENCY VEHICLE" \
ELSEIF \
   [Vehicle Body Type] = "CARGO VAN/LIGHT TRUCK 2 AXLES (OVER 10,000LBS (4,536 KG))" OR \
   [Vehicle Body Type] = "MEDIUM/HEAVY TRUCKS 3 AXLES (OVER 10,000LBS (4,536 KG))" OR \
   [Vehicle Body Type] = "OTHER LIGHT TRUCKS (OVER 10,000LBS (4,536 KG))" OR \
   [Vehicle Body Type] = "PICKUP TRUCK" OR \
   [Vehicle Body Type] = "TRUCK TRACTOR" \
THEN "TRUCK" \
ELSEIF \
   [Vehicle Body Type] = "CROSS COUNTRY BUS" OR \
   [Vehicle Body Type] = "SCHOOL BUS" OR \
   [Vehicle Body Type] = "OTHER BUS" OR \
   [Vehicle Body Type] = "TRANSIT BUS" \
THEN "BUS" \
ELSEIF \
   [Vehicle Body Type] = "PASSENGER CAR" OR \
   [Vehicle Body Type] = "LIMOUSINE" OR \
   [Vehicle Body Type] = "STATION WAGON" OR \
   [Vehicle Body Type] = "VAN" OR \
   [Vehicle Body Type] = "SPORT UTILITY VEHICLE (SUV)" \
THEN "PASSENGER CAR" \
ELSEIF \
   [Vehicle Body Type] = "MOTORCYCLE" OR \
   [Vehicle Body Type] = "MOPED" \
THEN "MOTORCYCLE" \
ELSE "OTHER" \
END 

## Analysis and Results
<img width="1406" alt="Screenshot 2023-12-04 at 10 06 53 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/b0e6ab28-7263-4908-903a-bc1e5ceee409">

<img width="1312" alt="Screenshot 2023-12-04 at 10 04 22 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/30054d8f-32c3-448e-9cbd-bc74b6c2585e">

<img width="1247" alt="Screenshot 2023-12-04 at 10 04 45 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/71b787ac-7c7b-48e5-80c8-bb0869b41b6e">

<img width="1409" alt="Screenshot 2023-12-04 at 10 05 04 PM" src="https://github.com/anthonyramage/MIST4610GroupProject2/assets/141188901/2f164fc9-3f0d-40e7-a996-9b6de59e95c9">

To create this analysis, a dashboard was created to combine these different data visualizations into one comprehensive view. Each individual sheet is also included for the purpose of a closer look at each model.

The first trend that is noticeable is that the majority of accidents occur on vehicles that were made in 2015. When looking at the bar graph labeled "Crashes Per Year", 11,723 accidents took place in 2016. This data helps to support the high number of crashes observed for 2015 cars, since the majority of car crashes that are recorded took place in 2016, one year after cars manufactured in 2015 would have been released. 

One factore that can be observed to help explain the level of damages recorded in each year is the pie chart labeled "Pie Chart of Vehicle Body Type and Vehicle Year Involved In Crash". When looking at the makeup of 2015 cars involved in accidents, a large majority of these cars are PASSENGER CARS body type. If the pie chart is filtered either a year up or down, it can be seen that the percent of PASSENGER CARS decreases, as well as the number of DISABLING damages recorded decreases on the chart labeled "Count of Crashes Per Year and Vehicle Damage Extent". An analysis that could be made is that a higher rate of PASSENGER CARS involved in accidents may lead to a higher amount of damages sustained by these cars. A possible explanation is that PASSENEGER CARS are smaller and more fragile than things like a BUS or TRUCK, and therefore may sustain more damages than other vehicle types when involved in accidents. This analysis can be applied to each manufacturing year of car. 

2015 cars are involved in the most accidents and sustain the most damages, while also having one of the relatively lowest number of cars without damages. One possible assumption that can be made from this, and later explored, is that 2015 cars may have been built before newer safety regulations and standards were introduced. The overarching trend is that cars built after 2015 are involved in less crashes, and tend to sustain less damages as well. While this may be due to the fact these cars have been on the road less, some of the variability may be explained by increased safety regulations and quality standards implemented throughout time. Now that this data trend is identified, these factors like safety and quality regulations, can be explored.

# Tableau Packaged Workbook
The tableau workbook which includes the group work and my personal Honors Option Work is included within the ELC Dropbox.
