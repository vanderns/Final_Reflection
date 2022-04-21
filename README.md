# Final_Reflection
For the second half of this semester, my work with Manikumar has pivoted from learning from the activities to using what I've learned in my [project](https://github.com/vanderns/STA_418_Project). Because my focus has been on my project, there are some things that I wish I had learned better, such as making websites or using shiny apps. However, I have made good use of my time by strengthening the techniques I know and applying them in new ways. Much of my coding will be referenced from [here](https://github.com/vanderns/STA_418_Project/blob/main/Project_Overview.Rmd)
## Course Objectives
**1) Import, Manage, and Clean Data**\
So much of my project has been working with data. Manikumar was the one who obtained the Uber data for our project, and while he set to work on analyzing the time aspect, I worked on the Voronoi Diagrams and spacial analysis. Many of the functions I wrote for the project are just to format data in the correct way to display it. These two functions are `get_poly_x/y` and `create_choro`. The former was 
```
get_poly_x <- function(df){
  tiles <- deldir(df$Lon, df$Lat) %>% 
    tile.list
  len <- seq_along(tiles)
  temp_vec <- paste0("tiles$pt.", len, "$x")
  return(map(temp_vec, evparse))
}
```
and used to obtain the coordinates for the Voronoi polygons in the forms of vectors; the latter was
```
create_choro <- function(df){
  ids <- seq_along(df$count)
  id=c()
  value=c()
  for (i in seq_along(df$count)){
    id <- append(id,rep(ids[i], each=length(unlist(df$x_vals[i]))))
    value <- append(value,rep(df$count[i], each=length(unlist(df$x_vals[i]))))
  }
  xs <- c()
  ys <- c()
  for (i in seq_along(df$count)){
    for (j in seq_along(unlist(df$x_vals[i]))){
      xs <- append(xs,unlist(df$x_vals[i])[j])
      ys <- append(ys,unlist(df$y_vals[i])[j])
    }
  }
  data <- data.frame(group=id,Count=value,x=xs,y=ys)
  nymap <- gen_map(coords)
  p <- ggmap(nymap) + 
    xlim(coords[4],coords[3])+ylim(coords[6],coords[5])+
    geom_polygon(data, mapping=aes(x=x,y=y,fill = Count, group = group), alpha=.70)
  return(p)
}
```
used this information to create a choropleth map and then reform the data to be read with `geom_polygon`. The same data was used in both cases, but it had to be in entirely different formats to work. The function `get_poly_x/y` puts the coordinates in together in vectors for their corresponding polygon, while `create_choro` creates a dataframe with a single coordinate in every row and uses an column to identify them by their corresponding polygon.\
\
**2) Create graphical displays and numerical summaries of data for exploratory analysis and presentations**\
Certainly, this project was all about graphical displays for me. Manikumar took most of the work with numerical data, though I did do some with the areas of the polygons. I think that my work in making the maps is very impressive and looks really nice. I have multiple layers to my maps. I used the `ggmap` package to get a streetmap of New York so that we can put the map into context, and then plotting the diagram on top was very convenient. By using
```
get_coords <- function(x_vals,y_vals){
  xs <- c()
  ys <- c()
  for (i in seq_along(x_vals)){
    for (j in seq_along(unlist(x_vals[i]))){
      xs <- append(xs,unlist(x_vals[i])[j])
      ys <- append(ys,unlist(y_vals[i])[j])
    }
  }
  return(c((max(xs)+min(xs))/2,(max(ys)+min(ys))/2,max(xs),min(xs),max(ys),min(ys)))
}
gen_map <- function(coords){
  return(get_map(location=coords[1:2],maptype='roadmap'))
}
```
I got the maps perfectly formated to the area where the Voronoi diagrams occur. What I'm most proud of though are my choropleth maps. They combine multiple things I've learned over the past semester in my other classes like iteration to make an appealing and informing product.\
\
**3) Write R programs for simulations from probability models and randomization-based experiments**\
The programs I've made in this class all deal with a certain level of randomization. The data set Manikumar obtained was huge. Because of the sheer number of the observations we couldn't just plot them all, or the result would be a cluttered mess. Our solution to this was taking a sample of the data and making models from that sample. This was done using
```
df <- read_csv(here::here('Uber-dataset','uber-raw-data-Sep21.csv'))
data <- slice_sample(df, n=10)
```
which allowed us to easily alter how many points we wanted to use in both our Voronoi diagrams and choropleth maps. With this given I was able to test how sensitive the diagrams were. While a lower sample size is generally much more volatile, even when using only 5 points I found our Voronoi diagrams to be surprisingly consistent, commonly clustering points in Manhattan area. A larger sample simply made this more evident.\
\
**4) Use source documentation and other resources to troubleshoot and extend R programs**\
Source documentation was often used for this project. It was through this resource that I came across the `ggvoronoi` and `deldir` packages that were so necessary for the Voronoi diagrams. Beyond just that however, help was found in Stack Overflow. When I was looking for a way to have `R` read a string as an expression, we found the `eval` and `parse` functions, which we used to get
```
evparse <- function(x){
  eval(parse(text = paste0(x)))
}
get_poly_x <- function(df){
  tiles <- deldir(df$Lon, df$Lat) %>% 
    tile.list
  len <- seq_along(tiles)
  temp_vec <- paste0("tiles$pt.", len, "$x")
  return(map(temp_vec, evparse))
}
```
When I need help getting `geom_polygon` to work I found an example of how to get the data formated with a specific coordinate in every row. There are countless times when other people had the same problem as me and their solution was invaluble to me.\
\
**5) Write clear, efficient, and well-documented R programs**\
This is probably the area I struggled in the most. My coding is chaotic and confusing. In my practice programs the code will stay that way. However, in the `Project_Overview.Rmd` I am making an effort to cleanly display all the work I've done and work viewers through my process. Most of the comments take the form of
```
get_area <- function(df){                          # Takes in data set and finds areas of 
  areas <- deldir(df$Lon,df$Lat)$summary$dir.area  # voronoi polygons for numerical analysis
  return(areas)
}
```
To describe what the function is made to do. I think perhaps this sometimes falls short for the more complicated functions, and they could use a step-by-step detail of what happens, but I'm content with it's status.\
\
**Conclusion**\
For this class, I believe I deserve an A. For every learning objective, I believe that my work has exceeded expectations. The one that sufferes the most is my programs being clear, but I believe my work in the others to be exemplary and worthy of an A.\
If I had more time, I would have liked to make a Shiny App with my diagrams. I would allow users to select the month of data, how many points to use to create the Voronoi diagrams, and how many points to use in the choropleth mapping. Unfortunately, learning how to create the diagrams took away from learning how to make the Shiny Apps.
