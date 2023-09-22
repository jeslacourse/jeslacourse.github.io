---
title: "California Canvass Map"
date: 2020-04-18
permalink: /ccmproject/
categories: 
  - GIS
  - Statistics
tags: 
  - GIS 
  - spatial analysis
  - statistics
  - volunteer work
header:
  teaser: /canvass/folsom1.jpg

---

> I'll likely be revisiting this project in the future to see how my analysis has changed. With that said, I'm presenting this project as I did in 2016. So much has changed in the last four years. I'm excited to rework this project and pull in some fresh data. It should make for a very interesting before-and-after. 


<figure>
<a href="/canvass/Marin.png"><img src="/canvass/Marin.png"></a>
<figcaption>Final product, top left, with the three layers used for analysis and composition</figcaption>
</figure>

{% include gallery id="gallery" caption="Paper Map Examples at Regional, District and City Levels" %}

__________________________

__________________________

<center>Grassroots Organization for Presidental Primary Campaigning • Spring 2016</center><br>

![Washoe County Canvass, Feb 2016](\canvass\washoe.PNG)

*Washoe County Canvassing, Feb 2016*

## Project Idea and Timeline
Create a canvass map to help direct campaign efforts, with a focus on targeting likely voters in Northern California. Ideally this will be a dynamic project, updated as precincts are contacted.

## Primary Data
American Community Survey 5‐Year Estimates — TIGER/Line[^1] 

Statewide Database – Hosted by University of California, Berkeley [^2] 

## Timeline

- Collect and sort 2008/2012 elections data and precinct information 
- Find hotspots, Precincts with higher turnouts and moderate to high Democrat preference, to canvass first. Most valuable precincts will have a moderate to high population of registered voters and good election turnouts. 
- Compile map, determine most effective map style
- Compile statistical analysis
- Develop an interface to display precincts with canvassed and not canvassed information
  - May be best done through a web app

## Project Summary
The intent of this project is to determine the best voting precincts, within the state of California, in which to send political canvassers. Priority will be based on favorable 2012 General Election and Registration
demographics, as well as 2014 Census demographics. The map will be best utilized by a small team or individual campaign coordinator who will then send teams out to the highest priority precincts.

## Purpose

It’s a given fault that canvassing efforts generally cannot reach all of the neighborhoods that they want to. So how do you prioritize which neighborhoods to visit and which get the inevitable pass?

I’ve established three criteria:

High density areas are a big target. High density areas, in the context of this project, will be defined in two different ways.

1. Precincts with the highest rate of Democrat and “No Party Preference (NPP)” counts.

2. Areas with overall high population densities as well, since voters can register or change their affiliation up until May 23rd, 2016.

It’s important to know the difference between high population densities and high voter registration densities. It’s not enough to know how many people can vote. It’s more important, at this stage, to focus on confirmed registered voter numbers. With that said,

3. Turnout, the quantity of registered voters that actually voted in past elections, will weigh in on a precinct’s canvass priority.
    In a hypothetical situation, a high turnout in a lower population precinct may prove more valuable than a moderately low turnout in a higher population area. Giving each value an equal weight will allow us to quantitatively determine where to send our canvassers.

## Process
### Data Research
**Voter Turnout and Registered Voter Data**

Our state is broken up into over 21,000 voter precincts, which may also be referred to as election districts. Each precinct divides a city or census designated place to distribute the population among relatively equal
populations.

Election results and voter demographic information can be linked to precinct shapefiles.

*2008 v. 2012*

The differences in voting demographics between 2008 and 2012 is not substantial, so emphasis is placed on relevance. The more recent information should prove more accurate and influential than any trends that
occurred with the higher turnout of 2008.

**Population Density**

Likewise, Census information via the TIGER database can be used to collect general population density
information. The detailed Census demographic and population information, linked to the land area of the
state’s census shapefiles, can provide us with the population density. Creating a population density graphic
will be most accurate at the block group level (block level unavailable).

### Data Sources 

*Statewide Database – Hosted by University of California, Berkeley*[^2]

- 2012 State Precincts Shapefile
- 2012 Voter Turnout Demographics Table (.dbf)
- 2012 Voter Registration Demographics Table (.dbf)

*American Community Survey 5-Year Estimates — TIGER/Line*[^1]

- 2014 California Block Group Shapefile
- 2014 5‐Year Estimate “X01 Age and Sex” Demographics Table (.dbf)

*TIGER/Line Shapefile – California Primary and Secondary Roads, State County Shapefiles*
*USGS Water Resources – California Lakes*
*Natural Earth Data – Oceans*

[^1]:  https://www.census.gov/geo/maps‐data/data/tiger‐data.html
[^2]:  http://statewidedatabase.org/d10/index.html

### Data Management and Joins

Before joining the data, some adjustments had to be made to make the information more palatable for
mapping. Joins were made between the Precinct shapefile and both the voter turnout table and registration
table. The Census block groups and demographic table were joined based on the block group ID number. The newly joined tables and shapefiles were then exported as three shapefiles into the master geodatabase.

**Null Values**

The precinct data tables included areas referred to as “unassigned”. For voter turnout this meant that the
geographic area had no voters turn out. Likewise for registration, unassigned areas did not have any
registered voters.

To aid with the conversion from vector to raster, as well as visualization with the vector data itself, several
custom tables were created to reduce null value and divide‐by‐zero errors. Null values were converted to zero.

A pre‐logic script code was then added to several new custom fields eliminate the divide‐by‐zero errors. The
custom field details are noted in the next section. This is a snippet of VB Script used to divert values to zero in locations where there are no registered voters. If the number of registered voters is greater than zero, the calculation will run as expected.

```vb
​```
If [TOTREG] = 0 Then 
    val = 0 
Else val = [TOTVAL]/[TOTREG]
End If
​```
```

**Custom Fields and Field Calculations**

Three custom fields were created for this project:

- Turnout Rate
- Target Voters
- Census Density and Demographic

*Turnout Rate* – Calculate the percentage of registered voters that turned out to vote. Divide the number of vote by the number of registered voters accounted for.

<p><center> <code>[Turnout] = [TOTREG]/[TOTVOTE]</code></center></p>


*Target Voters* – Calculate the percentage of total registered voters that have declared themselves as Democrats or have declined to state a party.

<p><center> <code>[TV_Vote] = ([DEM]+[DCL])/[TOTREG_R]</code> <br>
Target Vote = (Democrat + Decline to State)/Total Registered Voters </center></p>


*Census Density with Target Demographic* – a) Remove all children from each block group’s total counts, then,
b) divide the adult count by the land area of their respective block group

<p><center><code>[Voting_Age] = [B00001e1] ‐ ([B01001e3]‐[B01001e4]‐[ B01001e5]‐[B01001e27]‐[B01001e28]‐[ B01001e29])</code> <br>
Voting Age = Total Count – (“Male <5” – “Male 5‐9” – “Male 10‐14” – “Female <5” – “Female 5‐9” – “Female 10‐14”)<br></center></p>

<p><center><code>[Census_Density] = [Voting_Age]/[ALAND]</code> <br>
Block Group Density = Voting Age Adults/Block Group Land Area (sq. meters)</center></p>


**Modifications to Jenks**

<figure class="half">
    <a href="/canvass/folsom1.jpg"><img src="/canvass/folsom1.jpg" height="250" hspace="5"></a>
    <a href="/canvass/folsom2.jpg"><img src="/canvass/folsom2.jpg" height="250" hspace="5"></a>
    <figcaption>(a) Jenks on Target Voters Layer and (b) Turnout Raster </figcaption>
</figure>

All vector maps were symbolized using the Jenks method with four breaks (five sections). 

In order to adequately show the difference between areas with no and low respective rates, the Jenks scale was modified to show six sections instead of five. The sixth section is simply zero values.

A section of the target voters map is above, (a). The white stripes over what is effectively Folsom Lake are areas with no registered voters. This contrasts the low Democrat and Decline to State (NPP) rates in the Lake’s surrounding neighborhoods, shown in red. The blue symbology in the northeast corner is an area of substantially higher Democrat/NPP rates.

### Polygon to Raster Conversion 

Using the three newly created fields outlined in the *Custom Fields and Field Calculations* section, each of the three main shapefiles were converted to raster using the *Polygon to Raster* tool. Below is the conversion for the Turnout_Rate shapefile to raster. This process creates three new rasters:

`Turnout_Rate_Raster`, `Target_Voter_Raster`, and `Census_Density_Raster`. The new rasters were added to the master geodatabase upon completion. A snippet of the turnout rate near Folsom Lake is shown above, (b). Areas of dark green have the highest turnouts. The scale moves through the light
greens to yellows, oranges, then to bright red denoting zero turnout.

![Polygon to Raster](\canvass\2rastermath.jpg)



### Raster Math
<figure class="half">
    <a href="/canvass/3rastermath.jpg"><img src="/canvass/3rastermath.jpg" height="350" hspace="5"></a>
    <a href="/canvass/4rastermath.jpg"><img src="/canvass/4rastermath.jpg" height="350" hspace="5"></a>
    <figcaption>(a) The Multiplier and (b) Multiplier Raster with Precinct Poly Overlay </figcaption>
</figure>

Using the raster calculator, the three raster layers are multiplied together to produce a new raster, `The_Multiplier`. By multiplying the raster layers together, equal weight is given to the turnout, target voters and population densities of a specific area. Precinct boundaries and census block group boundaries are completely disregarded in this step.

Above, (a), is Folsom Lake and it’s surrounding areas, primarily to the south and west. As we’ve seen with the vector and raster maps previously, the Lake holds a very low priority value with regard to canvassing. To the south, however, is the northern section of the City of Folsom. City of Folsom shows off it’s highest priority areas, in dark green, to it’s lowest, deep red. Gray areas hold no significant population, near zero election turnouts, or near zero Democrat/NPP numbers and are considered the lowest priority.

### Zonal Statistics

With the now blended `Multiplier` raster created, the information needs to be related back to the precinct shape files. The image, (b), shows the “blended” raster layer with the precinct overlaid. It’s clear
that several precincts are not well defined. This next step will resolve that.

The *Zonal Statistics as Table tool*, below, takes the mean of each of the `Multiplier` raster layer within each precinct boundary. The mean information is then added to a newly created table (.dbf)

![Zonal Statistics](\canvass\5.jpg)

The new table, `Multiplier_Table`, is joined to the `Precinct Boundary` shapefile. The data is symbolized by the mean value the raster cells within each precinct.

 By using the `Multiplier` raster and table as an intermediary, we’ve effectively converted our original census and precinct vector data into a dataset that fits neatly within the precinct boundaries.

<figure class="half">
    <a href="/canvass/6.jpg"><img src="/canvass/6.jpg"></a>
    <a href="/canvass/7.jpg"><img src="/canvass/7.jpg"></a>
    <figcaption>Precincts now prioritized based on voter turnout, registration demographic, and population density </figcaption>
</figure>

### Finishing Touches

<figure class="half">
    <a href="/canvass/8.jpg"><img src="/canvass/8.jpg" height="340" hspace="5"></a>
    <a href="/canvass/9.jpg"><img src="/canvass/9.jpg" height="340" hspace="5"></a>
    <figcaption>Congressional District 13 (a) without and (b) with Highways, Hydrology and Cities </figcaption>
</figure>

To improve the map’s readability, recognizable features like highways, lakes and major city labels have been added to the map.

This map is heavily based on voting precinct boundaries and Congressional District boundaries. These are two features that may not be inherently recognizable to the reader. More familiar boundaries (e.g. county lines, hydrologic features) have been added to improve readability.

## Problems
### Data Sources
*Precinct Information*

California, more specifically the Secretary of State, does not have an aggregated list of general election votes and voter registrations by precinct available to the public. As a result, the 2012 demographic and voter information is sourced through a third party. The *Berkeley School of Law* information has aggregated datasets from the Statements of Vote (SOV) and Statements of Registration from California’s 58 counties, as collected by each county’s respective County Registrar of Voters or County Clerks.

*Census Information*

There is a modest learning curve that comes with the readability of Census data. With some research, there are resources available to decode file names, field names and field descriptions. Census data is also laden with concatenations and acronyms. Fortunately, the Census has made documentation widely available online.

### Variance in Population

<figure class="half">
    <a href="/canvass/10.jpg"><img src="/canvass/10.jpg"  hspace="5"></a>
    <a href="/canvass/11.jpg"><img src="/canvass/11.jpg"  hspace="5"></a>
    <figcaption>Congressional District 1, Lowest Density CD Still Has A
Well Represented City – Chico, CA</figcaption>
</figure>

The initial intent of this project was to create a canvass map for Northern California. Unfortunately, the state has a delegate distribution process that would make it very difficult to focus on the northern part of the state alone.

With six delegates assigned to each Congressional District, then 105 delegates at‐large distributed after the primary election, it was increasingly apparent that the population heavy Los Angeles precincts should be included in dataset. The decision was made to prevent any major skewing of the prioritization process. It also had the added benefit of providing the same spatial analysis to what potentially
could be the most delegate rich section of the state.

<figure>
<a href="/canvass/12.jpg"><img src="/canvass/12.jpg"></a>
<figcaption>Congressional District 12 – San Francisco
Largely Overrepresented</figcaption></figure>

Creating a scale that allowed for at least one high priority precinct in each Congressional District was essential. The statistical over-representation of more populated areas was considered acceptable, as they will ultimately have the largest influence on at‐large delegates.



## Production

Web Map, Limited Congressional Districts ‐ ~~http://arcg.is/1TnmgNs~~ Link out of date

I developed this project to challenge myself. Many aspects of this project were brand new to me and it was an absolute thrill to be able to troubleshoot my way through it.

The data research proved more challenging than I expected, but good data is the literal cornerstone of a good project. Utilizing two completely different data sources, finding the shapefiles, inspecting the data tables then ensuring my joins would be adequate, took up the first third of my semester.

Creating a formula that answered the question, “What gives a precinct a higher priority over another?” proved to be the largest challenge. My answer: a top priority precinct will have a moderate to high population density, high voter turnout in the 2012 General Election, and a high rate of Democrat and unaffiliated voters. These are the best areas to send an individual out into the field to canvass and expect not only a good number of contacts made, but fair majority of positive interactions.

Converting data from vector to raster is old hat. But how do you convert a custom raster layer to fit the
polygons of an established vector file? What would the data quality be like? What I loved about this project
was the opportunity to dive right into the spatial analysis tools like the raster calculator and zonal statistics. This project’s two major shapefiles, 2012 Election Precincts and 2014 Census Block Groups, were not compatible with regard to sharing information back‐and‐forth. With the data converted to raster, I had a whole new picture to look at.

Raster math allowed me to set equal rates for each of my three criteria, zero to one, then give each rate equal weight by multiplying the three rates together. What came next was all new. I have a raster map that no longer fits the shapes I started with. The Zonal Statistics toolset was an absolute treat to work with. Creating the statistics table based on the raster cells, limited to the precinct shapefile boundaries, was the most novel part of this project for me.

An unexpected result of this project was the depth in which I was able to work with the raster data. Previous projects made rasters feel heavy and unnecessary. This project allowed me to manipulate data to the extent I needed to, then convert it back to vector data with the intent of using the shapefiles in an online environment. Had I not planned to create a web map, the raster data may have proven robust enough for its own project.
