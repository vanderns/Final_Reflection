# Final_Reflection
For the second half of this semester, my work has pivoted from learning from the activities to using what I've learned in my [project](https://github.com/vanderns/STA_418_Project). Because my focus has been on my project, there are some things that I wish I had learned better, such as making websites or using shiny apps. However, I have made good use of my time by strengthening the techniques I know and applying them in new ways.
## Course Objectives
**1) Import, Manage, and Clean Data**\
So much of my project has been working with data. Manikumar was the one who obtained the Uber data for our project, and while he set to work on analyzing the time aspect, I worked on the Voronoi Diagrams and spacial analysis. Many of the functions I wrote for the project are just to format data in the correct way to display it. These two functions are `get_poly_x/y` and `create_choro`, which can be seen [here](https://github.com/vanderns/STA_418_Project/blob/main/Project_Overview.Rmd). The former was used to obtain the coordinates for the Voronoi polygons in the forms of vectors; the latter used this information to create a choropleth map and then reform the data to be read with `geom_polygon`. The same data was used in both cases, but it had to be in entirely different formats to work.\
\
**2) Create graphical displays and numerical summaries of data for exploratory analysis and presentations**\
Certainly, this project was all about graphical displays for me. Manikumar took most of the work with numerical data, though I did do some with the areas of the polygons. I think that my work in making the maps is very impressive and looks really nice. I have multiple layers to my maps. I used `ggmap` to get a streetmap of New York so that we can put the map into context, and then plotting the diagram on top was very convenient. What I'm most proud of though are my choropleth maps. They combine multiple things I've learned over the past semester in my other classes like iteration to make an appealing and informing product.\
\
**3) Write R programs for simulations from probability models and randomization-based experiments**\
The programs I've made in this class all deal with a certain level of randomization. The data set Manikumar obtained was huge. Because of the sheer number of the observations we couldn't just plot them all, or the result would be a cluttered mess. Our solution to this was taking a sample of the data and making models from that sample. With this given I was able to test how sensitive the diagrams were. With a lower sample size they were much more volatile, but a larger sample was more consistent, to a startling degree.\
\
**4) Use source documentation and other resources to troubleshoot and extend R programs**\
Source documentation was often used for this project. It was through this resource that I came across the `ggvoronoi` and `deldir` packages that were so necessary for the Voronoi diagrams. Beyond just that however, help was found in Stack Overflow. When I was looking for a way to have `R` read a string as an expression, we found the `eval` and `parse` functions. When I need help getting `geom_polygon` to work I found an example of how to get the data formated. There are countless times when other people had the same problem as me and their solution was invaluble to me.\
\
**5) Write clear, efficient, and well-documented R programs**\
This is probably the area I struggled in the most. My coding is chaotic and confusing. In my practice programs the code will stay that way. However, in the `Project_Overview.Rmd` I am making an effort to cleanly display all the work I've done and work viewers through my process. \
\
**Conclusion**\
For this class, I believe I deserve an A. For nearly every learning objective, I believe that my work has exceeded expectations. The one that sufferes the most is my programs being clear, but I believe my work in the others to be exemplary and worthy of an A.
