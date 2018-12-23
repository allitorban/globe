# globe
Create a globe in R
First, I downloaded the data from the Natural Earth site. Under "Admin 0 - Countries" click on "Download countries", which will download a zipped shapefile of the countries in the world: https://www.naturalearthdata.com/downloads/10m-cultural-vectors/

Unzip the file and put the .shp file somewhere convenient.

Run these scripts in R:


# install packages if you don't have these already

install.packages("mapproj")
install.packages("ggplot2")


# then load the libraries for use

Library(mapproj)
Library(ggplot2)


# import the shapefile that you downloaded. Change the part in quotes to where your shapefile is located

world <- rgdal::readOGR ("Desktop/Map Resources/worldshapefile/ne_10m_admin_0_countries.shp")


# get it set up

worldmap <- ggplot(world, aes(x = long, y = lat, group = group)) +
geom_path() +
scale_y_continuous(breaks = (-2:2) * 30) +
scale_x_continuous(breaks = (-4:4) * 45)


# plot it! "ortho" is the type of projection, which you can change. The numbers in the parenthesis are the lat, long, which you can change too. Be patient - it may take a minute to render the map.

worldmap + coord_map("ortho", orientation = c(10, -5, 0))
