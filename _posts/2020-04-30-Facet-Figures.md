---
title: "Highlights and Facets for Visualizing Categorical Data"
categories: 
  - Rstats
  - Statistics
  - Visualizations
tags: 
  - dataviz
  - rstats
  - ggplot
  - gghighlight
header:
  teaser: assets/images/2020-04-30/plot-3.png
excerpt: "What's the most effective way to visualize comparisons between variable factors? How do you share a lot of information without muddying up your visualizations? There definitely isn't one answer, but here's one solution: faceted plots with gghighlight."
kramdown:
  parse_block_html: false
---

![](\assets/images/2020-04-30/plot-4.png)
*Side-by-Side Comparison of (a) Generic Plot and (b) Faceted Plots with Highlight*

## Visualizing Categorical Data

What's the most effective way to visualize comparisons between variable factors? How do you share a lot of information without muddying up your visualizations? There definitely isn't one answer, but here's one solution: faceted plots with `gghighlight`. 

For sample data, I’m setting up two normal curves with offset sample means *x̄* =  ± 2. While we're using two factors for simplicity, this method actual becomes more effective when the number of factors increases.[^2] For our sample data, Lefties are disperses around a mean left of center, while Righties collect right of center. The variances are modified as well to exaggerate the difference in factors, but we'll get into that in a second. 

[^2]:  The researcher that inspired this post needed to present characteristics for six separate factors in a concise manner.

<details><summary markdown = 'span'>Show code</summary>
         
``` r
# create a sample dataset of two normal curves with given classes
samples <- data.frame(val = rnorm(100, 2,2), pos = ("Righties")) %>% 
  rbind(data.frame(val = rnorm(100, -2,1), pos = ("Lefties")) )
```
   
</details><br>




|      |     Value | Position |
| ---- | --------: | :------- |
| 1   |   3.728539| Righties |
| 2   |   1.465043| Righties |
| 101 |  -0.210901| Lefties  |
| 102 |  -2.117621| Lefties  |

## Statistics
Summary statistics as a visual annotation are helpful when determining differences in factors. We have a couple of “out of the box” options through the use of `summary` and the like. 

<details><summary markdown = 'span'>Show code</summary>

``` r
# create generic statistical summary
samples %>%
  select_if(is.numeric)  %>%
  map(~tidy(summary(.x))) %>%  # compute tidy summary of each var
  do.call(rbind, .) -> stats   # bind list elements into df
```

</details><br>

|       |   Minimum |        Q1 |     Median |       Mean |       Q3 |  Maximum |
| ----- | --------: | --------: | ---------: | ---------: | -------: | -------: |
| Value | -4.915701 | -2.159441 | -0.8809261 | -0.0567143 | 1.785081 | 6.861341 |

Or we can build our own custom summary table. In this case, we're only interested in adding mean and deviation to our visuals.

<details>
  <summary markdown = 'span'>Show code</summary><p>

``` r
# create a custom summary, in this case, just the mean and sd
summary_stats <- samples %>% 
  group_by(pos) %>% 
  summarize_at(vars(val),
             funs(Mean = mean, SD = sd))
```

</details><br>

| Position |  Mean |   SD |
| :------- | ----: | ---: |
| Righties |  1.92 | 2.22 |
| Lefties  | -2.03 | 0.98 |

## Generic Plots

Generic ggplots tend to be a bit bland, which is fine in some cases. The generic plot is almost identical to  R's `plot()` function.[^1]

[^1]:  I'm oversimplifying a bit. This plot isn't *completely* generic. Titles, transparency, and theming aren't necessarily something you would get with base `plot()`.

![](\assets/images/2020-04-30/plot-1.png)
*Generic Histogram (w/ Bare Bones Aesthetics)*

<details><summary markdown = 'span'>Show code</summary>

``` r
# Create a simple histogram (w/ bare bones aesthetics)
ggplot(samples, aes(x=val)) +
  geom_histogram(alpha= 0.7, bins = 40) +   # 70% opacity, 40 slices
  labs(title ="Distribution of Lefties and Righties", 
       x ="Sample Value", y= "Frequency") + # All Labels     
  theme_bw()                                # B&W Theme
```

</details>


In our case, a generic plot shows us that the distribution is bimodal, but we really can't determine a lot about the characteristics of either factors' distribution. We are somewhat lucky, in this case, that if we were to create a classifier based strictly off of the information above, we can see that the cutoff should be about `x=0`. Aside from that, it's difficult to read exactly what's going on.  

## Faceted Plots 

![](\assets/images/2020-04-30/plot-2.png)
*Histograms Faceted by Categorical Factor*

<details><summary markdown = 'span'>Show code</summary>
  
``` r
ggplot(samples, aes(x=val,fill=pos)) + 
  # Graphs
  geom_histogram(aes(y=..density..),binwidth=.5, alpha=.5, position="identity") + 
  geom_density(alpha=.3) +
    
  # One figure per class
  facet_grid(.~pos, scales = "fixed")+
  
  # Mean line
  geom_vline(data = summary_stats, mapping = aes(xintercept = Mean), 
             linetype="dotted", 
             color = "blue", size=0.7) +

  # Annotations
  geom_text(data=summary_stats, 
             inherit.aes=FALSE, 
             aes(vjust="inward", hjust = "inward",
                 x = Inf, y = Inf, family = "serif",
                 label=paste("\nMean:",Mean,"\nSD:",SD, "\n"))) 
  ...               

```

</details><br>

Even without the summary statistics, it's much easier to discern the differences in two groups. At this stage, I've introduced the summary statistics and a mean line to increase comprehension. 

With that said, there are a handful of important features in this graphic that can be easily overlooked: 

1. Fix the y-axis. Without a fixed axis, we have no ability to quickly discern differences in distribution
2. Drop the opacity of the histogram. Overlapping data can get lost in the shuffle.

## Adding That Highlight

![](\assets/images/2020-04-30/plot-3.png)
*Histograms Faceted by Categorical Factor*

<details><summary markdown = 'span'>Show code</summary>

```r
ggplot(samples, aes(x=val,fill=pos)) + 
  geom_histogram(aes(y=..density..),binwidth=.5, alpha=.5, position="identity") + 
  geom_density(alpha=.3) +
  <b>gghighlight::gghighlight()</b> # add gghighlight
  ...
```

</details>

This is such a beautiful, yet deceptively simple trick to improving readability, a `gghighlight`![^3] It's worth noting that we don't need any additional arguments as the function is highlighting the given data per facet. Put another way, `gghighlight` is intuitive enough to figure out what should be grayed out and what should pop. Highlighting works with more than two factors as well. Anything that isn't the primary data simply sits in the background. 

We're just scraping the surface of what `gghighlight` can do for data viz. It's incredibly effective for singling out notable traits in a class, emphasizing trends, or simply comparing a subset of data to the rest of a sample.

[^3]:  [RDocumentation: gghighlight](https://www.rdocumentation.org/packages/gghighlight/versions/0.0.1/topics/gghighlight).




## GGPlot Summary

There are a lot of bits and pieces to these graphs, here's a quick recap on what role each piece plays. 

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




