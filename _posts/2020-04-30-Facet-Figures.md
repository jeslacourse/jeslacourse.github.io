Project Focus and Setup
-----------------------

The goal is to create histogram plots for each factor level for a given
response. In this case, I’m setting up two normal curves with offset
sample means *x̄* =  ± 2.

``` r
knitr::opts_chunk$set(message = FALSE, warning = FALSE)
# set up libraries
library(tidyverse)   # for plots and pipes
library(broom)       # for tidy statistics
library(knitr)       # for tables
library(gridExtra)   # for table formatting

# create a sample dataset of two normal curves with given classes
samples <- data.frame(val = rnorm(100, 2,2), pos = ("Righties")) %>% 
  rbind(data.frame(val = rnorm(100, -2,1), pos = ("Lefties")) )

kable(samples[c(1:5,101:105),])
```

|     |        val| pos      |
|-----|----------:|:---------|
| 1   |   3.423820| Righties |
| 2   |   5.146713| Righties |
| 3   |   3.771962| Righties |
| 4   |   4.854979| Righties |
| 5   |   3.540786| Righties |
| 101 |  -2.213623| Lefties  |
| 102 |  -1.488287| Lefties  |
| 103 |  -1.558750| Lefties  |
| 104 |  -3.146650| Lefties  |
| 105 |  -2.082855| Lefties  |

We want to prepare summary statistics for as a visual annotation as
well. We have a couple of “out of the box” options through the use of
`summary` and the like, or we can build our own.

``` r
#
# create generic statistical summary
samples %>%
  select_if(is.numeric)  %>%
  map(~tidy(summary(.x))) %>%  # compute tidy summary of each var
  do.call(rbind, .) -> stats   # bind list elements into df

kable(stats)
```

|     |    minimum|         q1|      median|        mean|        q3|   maximum|
|-----|----------:|----------:|-----------:|-----------:|---------:|---------:|
| val |  -4.915701|  -2.159441|  -0.8809261|  -0.0567143|  1.785081|  6.861341|

``` r
#
# create a custom summary, in this case, just the mean and sd
summary_stats <- samples %>% 
  group_by(pos) %>% 
  summarize_at(vars(val),
             funs(Mean = mean, SD = sd))

summary_stats[,2:3] <-  round(summary_stats[,2:3],2)

kable(summary_stats)
```

| pos      |   Mean|    SD|
|:---------|------:|-----:|
| Righties |   1.92|  2.22|
| Lefties  |  -2.03|  0.98|

Visualization
-------------

The plots will be completed with ggplot, which is well suited for both
html and pdf formats.

`geom_histogram`: creates histogram, plotting feature values against
their frequencies

-   `y=..density..` shifts the y-axis to a relative frequency

-   `bin_width`: the number of “slices” that we cut our data into. Play
    with this number! Can be relative, 0-1, or a number of slices
    (i.e. `binwidth = 10` for ten equal sized bins)

-   `alpha`: the transparency of our data, from fully transparent (0.0)
    to opaque (1.0)

-   `position`: relationship between the classes, can be “identity”,
    “stack”, “dodge”. Using `facet_grid`, “identity” has the added
    benefit of creating equal axes for each figure.

`geom_density`: smooths the histogram into a density plot, with y-axis
as the relative frequency for a point

`geom_vline`: vertical line, in this case used to create a mean line

`gghighlight`: great way to show our data compared to the relative
spread. Creates a “shadow” of the overall distribution.

`facet_grid`: breaks visuals into individual figures by feature.

``` r
#
# Create our visualization

#install.packages("gghighlight")

ggplot(samples, aes(x=val,fill=pos)) + 
  # Graphs
  geom_histogram(aes(y=..density..),binwidth=.5, alpha=.5, position="identity") + 
  geom_density(alpha=.3) +
  gghighlight::gghighlight()+
  
  
  # Mean line
  geom_vline(data = summary_stats, mapping = aes(xintercept = Mean), linetype="dotted", 
              color = "blue", size=0.7) +
  
  # One figure per class
  facet_grid(.~pos, scales = "fixed")+
  
  #Labels 
  ggtitle("Title")+
  xlab("X-axis") + 
  ylab("Y-axis")+ 
  
  # Annotations
  geom_text(data=summary_stats, 
             inherit.aes=FALSE, 
             aes(vjust="inward", hjust = "inward",
                 x = Inf, y = Inf, family = "serif",
                 label=paste("\nMean:",Mean,"\nSD:",SD, "\n"))) +
  
  
  # Overall Theme
  theme_bw()   
```

![](2020-04-30-Facet-Figures_files/figure-markdown_github/plot-1.png)
