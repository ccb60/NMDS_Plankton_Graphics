# NMDS_Plankton_Graphics
Exploring different ways to improve graphics summarizing data on planton communities in Casco Bay , Maine.


## Contents
Data and starting code were received from Erin Ambrose, in March of 2021.  Erin 
was completing graduate work looking at species composition of plankton in 
Penobscot Bay, Maine, working with Rachel Lasley Rasher, at University of 
Southern Maine.

Lasley Rasher is on the faculty at the University of Southern Maine, which also 
houses the Casco Bay Estuary Partnership.  She has been kind enough to allow us 
to work in her lab when we worked on some coastal nutrient monitoring projects.

So, at Lasley Rasher's request, I helped Ambrose early on in her graduate work
with some R coding issues. As she was preparing a manuscript for publication,
she and Lasley Rasher again asked for assistance with finalizing some graphics.

## The charge
In e-mail, Ambrose and Lasley Rasher asked me the following:

> These [two graphics] are actually the same data but these plots were made using 
two different codes in R to highlight the groupings (fig 4) and the drivers of 
those groupings (fig 5).

>   Ideally, we would like to  
    1. Make the scales match  
    2. Keep the polygons in place in fig 5   
    3. Not sure how much we should worry about the color scheme matching?  

## Initial Analysis of the Challenge
Fig 4 and Fig 5 were NMDS plots, with one highlighting clusters of similar 
species composition (by drawing polygons around each cluster) and the other 
highlighting environmental variables (by showing `envfit` vectors).  

The problem was, the two graphics relied on different plotting tools, and so did
not play well together.

Looking at the two draft graphics, it appeared that Figure 4 was produced in 
"Base R" graphics, using plot functions included in the `vegan` package. In 
particular, it was the default output of the `ordihull()` function.

Figure 5 was constructed, more or less by hand, using the `ggplot2` graphic
system.

## Proposed Solution
Most plotting functions invisibly return a data frame (or other R object)
containing the underlying plot coordinates.  An initial approach, therefore, was 
to isolate the necessary data structure from the `ordihull()`  call from 
Ambrose's existing code, and figure out how to use it in `ggplot2` graphics.

The help page for the `ordihull()` function says the following:

>  Function ordihull and ordiellipse return invisibly an object that has a 
   summary method that returns the coordinates of centroids and areas of the 
   hulls or ellipses.

That suggested the path forward.

