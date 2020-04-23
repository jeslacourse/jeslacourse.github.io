---
title: "California Canvass Map"
permalink: /ccmproject/
categories: 
  - GIS
  - Statistics
tags: 
  - GIS 
  - spatial analysis
  - statistics
  - volunteer work
---



> I'll likely be revisiting this project in the future to see how my analysis has changed. With that said, I'm presenting this project as I did in 2016. So much has changed in the last four years. I'm excited to rework this project and pull in some fresh data. It should make for a very interesting before-and-after. 

![Washoe County Canvass, Feb 2016](\assets\images\canvass\washoe.PNG)

*Washoe County Canvassing, Feb 2016*

# California Canvass Map

Grassroots Organization for the Democratic Campaign • Spring 2016

### Project Idea and Timeline
Create a canvass map to help direct campaign efforts, with a focus on targeting likely voters in Northern California. Ideally this will be a dynamic project, updated as precincts are contacted.

### Primary Data
American Community Survey 5‐Year Estimates — TIGER/Line[^1] 

Statewide Database – Hosted by University of California, Berkeley [^2] 

### Timeline

- Collect and sort 2008/2012 elections data and precinct information 
- Find hotspots, Precincts with higher turnouts and moderate to high Democrat preference, to canvass first. Most valuable precincts will have a moderate to high population of registered voters and good
  election turnouts. 
- Compile map, determine most effective map style
- Compile statistical analysis
- Develop an interface to display precincts with canvassed|not canvassed information, may be best done through a web app

### Project Summary
The intent of this project is to determine the best voting precincts, within the state of California, in which to send political canvassers. Priority will be based on favorable 2012 General Election and Registration
demographics, as well as 2014 Census demographics. The map will be best utilized by a small team or individual campaign coordinator who will then send teams out to the highest priority precincts.

### Purpose

It’s a given fault that canvassing efforts generally cannot reach all of the neighborhoods that they want to. So how do you prioritize which neighborhoods to visit and which get the inevitable pass?

We’ve established three criteria:

High density areas are a big target. High density areas, in the context of this project, will be defined in two different ways.

1. Precincts with the highest rate of Democrat and “No Party Preference (NPP)” counts.

2. Areas with overall high population densities as well, since voters can register or change their affiliation up until May 23rd, 2016.

It’s important to know the difference between high population densities and high voter registration densities. It’s not enough to know how many people can vote. It’s more important, at this stage, to focus on confirmed registered voter numbers. With that said,

3. Turnout, the quantity of registered voters that actually voted in past elections, will weigh in on a precinct’s canvass priority.
    In a hypothetical situation, a high turnout in a lower population precinct may prove more valuable than a moderately low turnout in a higher population area. Giving each value an equal weight will allow us to quantitatively determine where to send our canvassers.

### Process
#### Data Research
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

#### Data Sources 

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

[^1]:   https://www.census.gov/geo/maps‐data/data/tiger‐data.html
[^2]:  http://statewidedatabase.org/d10/index.html

#### Data Management and Joins
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

<center> <code>[Turnout] = [TOTREG]/[TOTVOTE]</code>


*Target Voters* – Calculate the percentage of total registered voters that have declared themselves as Democrats or have declined to state a party.

<center> <code>[TV_Vote] = ([DEM]+[DCL])/[TOTREG_R]</code> <br>
Target Vote = (Democrat + Decline to State)/Total Registered Voters


*Census Density with Target Demographic* – a) Remove all children from each block group’s total counts, then,
b) divide the adult count by the land area of their respective block group

<center><code>[Voting_Age] = [B00001e1] ‐ ([B01001e3]‐[B01001e4]‐[ B01001e5]‐[B01001e27]‐[B01001e28]‐[ B01001e29])</code> <br>
Voting Age = Total Count – (“Male <5” – “Male 5‐9” – “Male 10‐14” – “Female <5” – “Female 5‐9” – “Female 10‐14”)<br>

<center><code>[Census_Density] = [Voting_Age]/[ALAND]</code> <br>
Block Group Density = Voting Age Adults/Block Group Land Area (sq. meters)    




#### Modifications to Jenks

<figure class="half">
    <a href="/assets/images/canvass/folsom1.jpg"><img src="/assets/images/canvass/folsom1.jpg" width="250" hspace="5"></a>
    <a href="/assets/images/canvass/folsom2.jpg"><img src="/assets/images/canvass/folsom2.jpg" width="250" hspace="5"></a>
    <figcaption>(a) Jenks on Target Voters Layer and (b) Turnout Raster </figcaption>
</figure>

All vector maps were symbolized using the Jenks method with four breaks (five sections). 

In order to adequately show the difference between areas with no and low respective rates, the Jenks scale was modified to show six sections instead of five. The sixth section is simply zero values.

A section of the target voters map is above, (a). The white stripes over what is effectively Folsom Lake are areas with no registered voters. This contrasts the low Democrat and Decline to State (NPP) rates in the Lake’s surrounding neighborhoods, shown in red. The blue symbology in the northeast corner is an area of substantially higher Democrat/NPP rates.

#### Polygon to Raster Conversion 
Using the three newly created fields outlined in the *Custom Fields and Field Calculations* section, each of the three main shapefiles were converted to raster using the *Polygon to Raster* tool. Below is the conversion for the Turnout_Rate shapefile to raster. This process creates three new rasters:

`Turnout_Rate_Raster`, `Target_Voter_Raster`, and `Census_Density_Raster`. The new rasters were added to the master geodatabase upon completion. A snippet of the turnout rate near Folsom Lake is shown above, (b). Areas of dark green have the highest turnouts. The scale moves through the light
greens to yellows, oranges, then to bright red denoting zero turnout.

![Polygon to Raster](\assets\images\canvass\2rastermath.jpg)



#### Raster Math
<figure class="half">
    <a href="/assets/images/canvass/3rastermath.jpg"><img src="/assets/images/canvass/3rastermath.jpg" width="350" hspace="5"></a>
    <a href="/assets/images/canvass/4rastermath.jpg"><img src="/assets/images/canvass/4rastermath.jpg" width="350" hspace="5"></a>
    <figcaption>(a) The Multiplier and (b) Multiplier Raster with Precinct Poly Overlay </figcaption>
</figure>
Using the raster calculator, the three raster layers are multiplied together to produce a new raster, The_Multiplier. By multiplying the  raster layers together, equal weight is given to the turnout, target voters and population densities of a specific area. Precinct boundaries and census block group boundaries are completely disregarded in this step.

Above, (a), is Folsom Lake and it’s surrounding areas, primarily to the south and west. As we’ve seen with the vector and raster maps previously, the Lake holds a very low priority value with regard to canvassing. To the south, however, is the northern section of the City of Folsom. City of Folsom shows off it’s highest priority areas, in dark green, to it’s lowest, deep red. Gray areas hold no significant population, near zero election turnouts, or near zero Democrat/NPP numbers and are considered the lowest priority.

#### Zonal Statistics
With the now blended `Multiplier` raster created, the information needs to be related back to the precinct shape files. The image, (b), shows the “blended” raster layer with the precinct overlaid. It’s clear
that several precincts are not well defined. This next step will resolve that.

The *Zonal Statistics as Table tool*, below, takes the mean of each of the `Multiplier` raster layer within each precinct boundary. The mean information is then added to a newly created table (.dbf)

![Zonal Statistics](\assets\images\canvass\5.jpg)

The new table, `Multiplier_Table`, is joined to the `Precinct Boundary` shapefile. The data is symbolized by the mean value the raster cells within each precinct.

 By using the `Multiplier` raster and table as an intermediary, we’ve effectively converted our original census and precinct vector data into a dataset that fits neatly within the precinct boundaries.

<figure class="half">
    <a href="/assets/images/canvass/6.jpg"><img src="/assets/images/canvass/6.jpg"></a>
    <a href="/assets/images/canvass/7.jpg"><img src="/assets/images/canvass/7.jpg"></a>
    <figcaption>Precincts now prioritized based on voter turnout, registration demographic, and population density </figcaption>
</figure>

#### Finishing Touches

<figure class="half">
    <a href="/assets/images/canvass/8.jpg"><img src="/assets/images/canvass/8.jpg" width="300" hspace="5"></a>
    <a href="/assets/images/canvass/9.jpg"><img src="/assets/images/canvass/9.jpg" width="300" hspace="5"></a>
    <figcaption>Congressional District 13 (a) without and (b) with Highways, Hydrology and Cities </figcaption>
</figure>

To improve the map’s readability, recognizable features like highways, lakes and major city labels have been added to the map.

This map is heavily based on voting precinct boundaries and Congressional District boundaries. These are two features that may not be inherently recognizable to the reader. More familiar boundaries (e.g. county lines, hydrologic features) have been added to improve readability.

### Problems
#### Data Sources
*Precinct Information*

California, more specifically the Secretary of State, does not have an aggregated list of general election votes and voter registrations by precinct available to the public. As a result, the 2012 demographic and voter information is sourced through a third party. The *Berkeley School of Law* information has aggregated datasets from the Statements of Vote (SOV) and Statements of Registration from California’s 58 counties, as collected by each county’s respective County Registrar of Voters or County Clerks.

*Census Information*
There is a modest learning curve that comes with the readability of Census data. With some research, there are resources available to decode file names, field names and field descriptions. Census data is also laden with concatenations and acronyms. Fortunately, the Census has made documentation widely available online.
