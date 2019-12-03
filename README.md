# Visualisation competition for NHS England health data.  

### Child obesity data

[National Child Measurement Programme, England 2018/19 School Year - NHS Digital](https://digital.nhs.uk/data-and-information/publications/statistical/national-child-measurement-programme/2018-19-school-year)

### Wealth inequality data

[ONS-link](https://www.ons.gov.uk/economy/regionalaccounts/grossdisposablehouseholdincome/datasets/regionalgrossdisposablehouseholdincomebylocalauthoritiesbynuts1region?fbclid=IwAR0-LsdWeAcnDnCQxUzgie0umJRGaW4DDuRr2jzzpnPNKIN1DvnshlKZ6UU)

### Useful coding links

[Munging complex excel docs](https://github.com/nacnudus/tidyxl)

####Plotting a map of the UK

```R

library(maps)
library(mapdata)
library(maptools)
library(rgdal)
library(ggmap)
library(ggplot2)
library(rgeos)
library(broom)
library(plyr)

#http://geoportal.statistics.gov.uk/datasets/48b6b85bb7ea43699ee85f4ecd12fd36_0
#Click on the Download button and then select the Shapefile option. Download and unzip the files into a folder on your computer.
#Load the shapefile - make sure you change the filepath to where you saved the shapefiles
shapefile <- readOGR(dsn=".", layer="NUTS_Level_2_January_2018_Full_Clipped_Boundaries_in_the_United_Kingdom")

#Reshape for ggplot2 using the Broom package
mapdata <- tidy(shapefile, region="nuts218nm") #This might take a few minutes

#Check the shapefile has loaded correctly by plotting an outline map of the UK
gg <- ggplot() + geom_polygon(data = mapdata, aes(x = long, y = lat, group = group), color = "#FFFFFF", size = 0.25)
gg <- gg + coord_fixed(1) #This gives the map a 1:1 aspect ratio to prevent the map from appearing squashed
print(gg)

```


