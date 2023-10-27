---

title: "Barriers in Biology"
date: 2021-11-18
showTableOfContents: TRUE
slug: /barriers
categories: 
  - Rstats
  - Statistics
  - Visualizations
  - IR
tags: 
  - dataviz
  - rstats
  - ggplot
  - IR
summary: "This study tracks the impact of course-taking and change-in-major habits on award-earning and transfers for the 224 Biology for Transfer majors in the 2017-18 cohort."

---

<style>

.prose :where(p):not(:where([class~="not-prose"] *)) {
  margin-top: 0.25em;
  margin-bottom: 0.5em;
}

.max-w-prose {
  max-width: 80ch;
}
</style>



{{< badge >}}
{{< icon "github" >}}
 Sierra College
{{< /badge >}}


### Project Scope


This study tracks the impact of course-taking and change-in-major habits on award-earning and transfers for the 224 Biology for Transfer majors in the 2017-18 cohort.

> The Associate in Science in Biology for Transfer degree (AS-T) prepares students to transfer into the CSU system to complete a bachelor’s degree in biology, or a major deemed similar by a CSU campus. This program provides students with a strong foundation in biology.  <br>
 — <cite>[*Biological Sciences*. Sierra College. 2021.](https://catalog.sierracollege.edu/archive/2020-2021/departments/biological-sciences/#degreescertificatestext)</cite>

Looking back on the 2017-18 cohort allows for adequate tracking of the degree-earning process. For consistency, students are tracked based on their last declared major.



## Key Findings and Action Items

**Persistence and Award-Earning**

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Biology for Transfer Majors: Years to Completion, First Award or Transfer</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> 1 </th>
   <th style="text-align:left;"> 2 </th>
   <th style="text-align:left;"> 3 </th>
   <th style="text-align:left;"> 4+ </th>
   <th style="text-align:left;"> No Award </th>
   <th style="text-align:left;"> Total </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Distinct Students </td>
   <td style="text-align:left;"> 1 </td>
   <td style="text-align:left;"> 9 </td>
   <td style="text-align:left;"> 11 </td>
   <td style="text-align:left;"> 56 </td>
   <td style="text-align:left;"> 147 </td>
   <td style="text-align:left;"> 224 </td>
  </tr>
</tbody>
</table>

First-year persistence is low for this cohort. 

Of new 224 Biology for Transfer majors in the 2017-18 cohort, 36.6% (n:82) persisted from their first term into coursework a year later. With that said, 77 (34.38%) earned an award or transferred within four years. 

Overall, 28 students earned an award or certificate. 60 students transferred to a four-year college, and 44 students transferred without an award. 

Just 23.3% (14 of 60) students completed degree-required Physics coursework before transferring. 58.3% (35 of 60) completed some Biology coursework before transferring with a total of 38.1% (23 of 60) completing `BIOL 2` or `3`. 


**Summer Coursework is Critical**

Every student who earned an `AS Natural Science` or `AS-T Biology` took at least one `CHEM` and/or `PHYS` course during a Summer session. 


**Student Preparedness Clashes With Course Availability**

Only `20.1%` of students took a major course in their first year. Taking major coursework in the first year led to a `29.3%` point increase in award-earning, `55.6%` of students taking first-year major coursework earn an award, compared to `26.3%` without first-year major coursework. Incoming students appear to be well prepared for college-level coursework. The majority of first-year major enrollments were made up of `MATH 30` (n:19) and `CHEM 1A` (n:17), followed up by `CHEM 3A` (n:11).  

Students who didn't enroll in Chemistry their first year but persisted to next Fall typically enrolled in `CHEM 1A` or `CHEM 3A` during their second year or during a Summer session. Preliminary findings from a concurrent study on entry-level Chemistry coursework indicate that late registration dates for new cohorts may be playing a key factor in limiting prepared students from enrolling in first-year `CHEM 1A` and `CHEM 3A`. Similar trends with course availability play out near the end of the student journey as students attempt to enroll in `PHYS 105\L` and `110\L`.


**Major Courses**

Early enrollment in `CHEM 1A` or `CHEM 3A` and/or `MATH 27` or `MATH 30` are the the best early indicators that a Biology for Transfer student is on track.

Students who enroll in `PHYS 110/L`, `BIOL 2`, and/or `BIOL 3`, regardless of outcome, have successfully navigated several prerequisite barriers and have a nearly guaranteed chance of earning an award. With that said, the number of students who make it to these courses is relatively low. Nearly all students who enrolled in Physics opted for the `PHYS 100` series in lieu of the `200` series. `MATH 30` is highly preferred by this cohort over `MATH 16A`. 

**General Education** 

General education completion is not a major concern for this cohort. Enrollment in `IGETC 5A|B Physical and Biological Science` coursework outside of their degree coursework, i.e. `ANTH 1` or [*Academic Plan*](https://academics.sierracollege.edu/biological-sciences)-aligned courses `ESS 1` and `GEOG 3`, tend to have a lower chance of award-earning or transfer.

 

# The Program

##  Requirements and Prerequisites

Link: [Sierra College Catalog, 2020-21](https://catalog.sierracollege.edu/archive/2020-2021/departments/biological-sciences/#degreescertificatestext)

The Biology for Transfer degree is prerequisite heavy: In order to complete `BIOL 2` or `3`, students must take at least three consecutive semesters of degree-applicable coursework. Similar trends develop for completion of the `PHYS 100` and `200` series. 

![AS-T Biology Requirements](/barriers/plotCourses.PNG)

**Hidden Units**: Students taking the `CHEM 3` series in lieu of `CHEM 1A` must enroll concurrently in `CHEM X|Y`. The additional corequisite increases the overall unit load from 6 units over two semesters to 10 units. 


# Persistence


Of 224 Biology for Transfer majors, 63.4% (n:142) persisted onto their second term. After a year, that number drops to 36.6% (n:82). 

Of the 82 students who continued to their second term: `87.8%` (n: 72) completed their English requirement, `81.7%` (n: 67) completed college math, and `52.4%` (n: 43) completed college level chemistry. 

Of the 142 students who didn't continue to their second term: `54.6%` (n: 64) completed their English requirement, `43.3%` (n: 61) completed college math, and `15.6%` (n: 22) completed college level chemistry. 

**Still in the Game**

Seventeen students from the 2017-18 cohort have enrolled in coursework during the 2020-21 academic year. The last major courses to be completed include `BIOL 1` (n:5), `PHYS 110|L` (n:5), `BIOL 2` (n:4), `BIOL 3` (n:3), and `CHEM 1B` (n:3). 


# Awards 

By 2020-21, 28 students earned an award or certificate. Twenty-seven of the 28 award earners held at least one `AS Degree` and one student earned a certificate. Eighteen students earned an `AS-T Biology`, all of whom picked up an `AS Natural Science` award along the way. 

Every student that earned an AS-T Biology or AS Natural Sciences took Chemistry or Physics coursework over the summer. The mean completion time for completers in the 2017-18 cohort is just over three years including one or more summer sessions.

![Awards by Years to Completion](/barriers/tileAwards-1.png)




 

## The Great Bottleneck (And the Summer Savior) 

All 27 Biology for Transfer majors who earned an `AS Degree` took at least one `CHEM` or `PHYS` course over a Summer session. Similarly, 61.6% of the 60 students who ultimately transferred took least one course over Summer. Thirty-two of the 37 students, `86.9%`, who took Summer courses before successfully transferring took at least one `CHEM` or `PHYS` over the Summer. 

Successful students need to complete `MATH` and `CHEM` coursework early in their academic plan. Of the 82 students who continued to their second term, 81.7% (n: 67) completed college math and 52.4% (n: 43) completed college level chemistry. In contrast, of the 142 students who didn’t continue to their second term, 43.3% (n: 61) completed college math and 15.6% (n: 22) completed college level chemistry.

## Skipping the Award


Ten students earned an award or transferred in two years. After four years, 77 (34.38%) students earned an award or transferred. The majority of the 74 four-year college transfers did so with out completing the `AS-T`; 49 (66.2%) students transferring without award. 

<table class="table" style="margin-left: auto; margin-right: auto;">
<caption>Crosstabs: Award- and Transfer-Earning by Headcount</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> No Transfer </th>
   <th style="text-align:right;"> 4-Year Transfer </th>
   <th style="text-align:right;">   </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Has an Award </td>
   <td style="text-align:right;"> 12 </td>
   <td style="text-align:right;"> 16 </td>
   <td style="text-align:right;font-weight: bold;"> 28 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> No Award </td>
   <td style="text-align:right;"> 152 </td>
   <td style="text-align:right;"> 44 </td>
   <td style="text-align:right;font-weight: bold;"> 196 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;">  </td>
   <td style="text-align:right;font-weight: bold;"> 164 </td>
   <td style="text-align:right;font-weight: bold;"> 60 </td>
   <td style="text-align:right;font-weight: bold;font-weight: bold;"> 224 </td>
  </tr>
</tbody>
</table>


## A Difference in Trends: Transferring With or Without an Award

Students who transfer without an award enrolled in fewer major courses and tend to skip Physics coursework before moving to a four-year college.



<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Transfer Students: Frequently Skipped Coursework</caption>
<tbody>
  <tr>
   <td style="text-align:left;"> Took </td>
   <td style="text-align:left;"> Any Physics </td>
   <td style="text-align:left;"> Any Biology </td>
   <td style="text-align:left;"> Biology 2 or 3 </td>
   <td style="text-align:left;font-weight: bold;"> Total Transfers </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Headcount </td>
   <td style="text-align:left;"> 14 </td>
   <td style="text-align:left;"> 35 </td>
   <td style="text-align:left;"> 23 </td>
   <td style="text-align:left;font-weight: bold;"> 60 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Proportion </td>
   <td style="text-align:left;"> 23.3% </td>
   <td style="text-align:left;"> 58.3% </td>
   <td style="text-align:left;"> 38.1% </td>
   <td style="text-align:left;font-weight: bold;"> 100.0% </td>
  </tr>
</tbody>
</table>

Overall, 23.3% (14 of 60) students completed Physics coursework before transferring. 58.3% (35 of 60) completed some Biology coursework before transferring with a total of 38.1% (23 of 60) completing `BIOL 2` or `3`. Transfer students are also more likely to enroll in `BIOL 3` (n:22) over `BIOL 2` (n:19) and are less likely to pass their coursework on their first attempt. 

### Repeating Key Courses

Students transferring without an award tend to complete fewer units than award-earners. 



Students who repeat `BIOL 1` and `CHEM 1A` tend to earn an award before transferring. Both award and non-award earning transfer students are more likely to repeat `MATH 30` than any other course.  

# First-Year Course-Taking Trends

## Frequently Taken Courses

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Major Courses Taken During First Year</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Took Major Coursework </th>
   <th style="text-align:right;"> Distinct Students </th>
   <th style="text-align:left;"> Prop </th>
   <th style="text-align:right;"> Awards </th>
   <th style="text-align:left;"> Prop </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Yes </td>
   <td style="text-align:right;"> 45 </td>
   <td style="text-align:left;"> 20.1% </td>
   <td style="text-align:right;"> 25 </td>
   <td style="text-align:left;"> 55.6% </td>
  </tr>
  <tr>
  <tr>
   <td style="text-align:left;"> No </td>
   <td style="text-align:right;"> 179 </td>
   <td style="text-align:left;"> 79.9% </td>
   <td style="text-align:right;"> 47 </td>
   <td style="text-align:left;"> 26.3% </td>
  </tr>

   <td style="text-align:left;font-weight: bold; !important;"> Total </td>
   <td style="text-align:right;font-weight: bold; !important;"> 224 </td>
   <td style="text-align:left;font-weight: bold; !important;"> - </td>
   <td style="text-align:right;font-weight: bold;!important;"> 72 </td>
   <td style="text-align:left;font-weight: bold;!important;"> - </td>
  </tr>
</tbody>
</table>


Only 20.1% of students took a major course in their first year. Taking major coursework in the first year led to a 29.3% point increase in award-earning. 55.6% of students with first-year major coursework earned an award. That number is up from 26.3% for students without first-year major coursework.

`MATH 30` (n:19), `CHEM 1A` (n:17), and `CHEM 3A` (n:17) are among the most popular major courses attempted in the first year, though the number of students taking these courses is relatively small. `ENGL 1A` & `1B` (n:104 & 35, resp), `PSYC 100` (n: 50), and `MATH 12` (n:32) are the most popular general education courses attempted in the first year.





![Top 20 First-Year Courses: Biology for Transfer](/barriers/plotFirstYearCourses-1.png)

![First Year Courses: Proportion Led to Degree or Transfer](/barriers/plotPropFirstYearAwards-2.png)


## Early Signs: A Difference in First-Year Courses by Award-Earners



Award-earners had a higher proportion of enrollments in `MATH 30`, `CHEM 1A`, and `CHEM 3A`, along with GE courses `PSYC 0105`, and `COMM 0003` during their first year. Award earners were less likely to attempt `ENGL 0000N` or `MATH 0000A`.


## Resilient Courses

**First Year Math and Chemistry or Bust**

Enrollment in `MATH 0030` during the first year, regardless of outcome, is one of the best predictors for success, 85.0% of enrollments ultimately lead to an award.  

Regardless of course outcome, 72.0% (n:75) of first-year enrollments in `CHEM 0001A`, `CHEM 0003A`, `ENGL 0001C`, or `MATH 0030` directly contributed to an award or transfer. First-year enrollments in `MATH 0013`, `MATH 0027`, and/or `MATH 0029` were also very good indicators that the student is on track for completion. 53.2% (n:62) of enrollments in those courses led to an award.

Preparedness plays it part. These courses tend to have higher than average course success rates: All `ENGL 0001C` (n:16) passed, along with 76.5% (n:17) in `CHEM 1A`, 72.7% (n:11) in `CHEM 3A`, and 60.0% (n:20) in `MATH 0030`. These students also tend to be relatively tenacious: Two out of the three `CHEM 0003A` students, and 75.0% (n:8) of the `MATH 0030` students who did not pass their first course attempts still completed their award or transfer goal.  

**Follow Up: ** Course availability likely plays a key role as well. Preliminary findings from a concurrent study on entry-level chemistry courses (i.e. `CHEM 1A`, `2A`, and `3A`) show that the 2017-18 cohort tend to complete `CHEM 3A` or `CHEM 1A` in their second year. Priority registration placement may be playing a critical role, as the new incoming cohort tend to have later registration dates in their first year than continuing students.

## B's Aren't Leading to Degrees



<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;border-bottom: 0;">
<caption>First-Year Enrollments: Grade Distribution</caption>
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> A </th>
   <th style="text-align:left;"> B </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;"> D </th>
   <th style="text-align:left;"> F </th>
   <th style="text-align:left;"> W </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Grade Frequency </td>
   <td style="text-align:left;"> 216 </td>
   <td style="text-align:left;"> 126 </td>
   <td style="text-align:left;"> 95 </td>
   <td style="text-align:left;"> 31 </td>
   <td style="text-align:left;"> 85 </td>
   <td style="text-align:left;"> 82 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Proportion of Grades </td>
   <td style="text-align:left;"> <span style="     ">34.0%</span> </td>
   <td style="text-align:left;"> <span style="     ">19.8%</span> </td>
   <td style="text-align:left;"> <span style="     ">15.0%</span> </td>
   <td style="text-align:left;"> <span style="     ">4.9%</span> </td>
   <td style="text-align:left;"> <span style="     ">13.4%</span> </td>
   <td style="text-align:left;"> <span style="     ">12.9%</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Grade Led to Award </td>
   <td style="text-align:left;"> <span style="     ">62.5%</span> </td>
   <td style="text-align:left;"> <span style="     ">41.3%</span> </td>
   <td style="text-align:left;"> <span style="     ">27.4%</span> </td>
   <td style="text-align:left;"> <span style="     ">29.0%</span> </td>
   <td style="text-align:left;"> <span style="     ">11.8%</span> </td>
   <td style="text-align:left;"> <span style="     ">15.9%</span> </td>
  </tr>
</tbody>
<tfoot><tr><td style="padding: 0; " colspan="100%">
<sup>*</sup> Ten P/NP Grades Omitted</td></tr></tfoot>
</table>

Of `645` enrollments, `419` were a `B` or lower. In general, enrollments earning a `B`, `C`, `D`, `F`, or `W` led to an award only `24.1%` of the time. An `A` grade leads to an award `60.6%` of the time. The proportion of enrollments leading to awards drops to `38.9%` for a `B` grade. These figures can be seen in detail in the table below. 

Award-earning shifts significantly if the `B` was earned in one or more of the significant courses noted in the last section.: A `B` in `CHEM 0001A`, `CHEM 0003A`, `ENGL 0001C`, and/or `MATH 0030` improves award earning to `71.1%` (n:45). A `B` in `ENGL 0001B`, `HIST 0017A`, `MATH 0013`, `MATH 0027`, `MATH 0029`, and/or `NUTF 0010` also improve award-earning to `57.1%` (n:88).

On the other side, the list of courses that do not lead to an award is substantial. Only `12.2%` (n:286) of enrollments earning `B` or lower in this group lead to an award: `ANTH 0001`, `ANTH 0002`, `ARHI 0101`, `CHEM 0000A`, `COMM 0001`, `ENGL 0000N`, `ENGL 0001A`, `HDEV 0001`, `HED 0002`, `HIST 0017B`, `MATH 0000A`, `MATH 0000D`, `MATH 0012`,`MUS 0002`, `PSYC 0100`, `SOC 0001`,`SPAN 0001`. These courses make up a two-thirds, 429 of 645, of the cohort's first-year enrollments. 




# Major Coursework Trends 

The figures below calculate the odds of a course enrollment's likelihood of leading to an award, regardless of the grade earned in that class. **An odds ratio (OR) of 1 is equivalent to a 50/50 chance of leading to an award. ORs higher than one indicate enrollment in that course improves the odds of earning an award.** Similarly, ORs lower than one indicate enrollment in that course lessen the odds of earning an award.   

Enrollment in `PHYS 0105\L` `PHYS 0110\L`,  `BIOL 0002` or `BIOL 0003` are the best indicators that the student is on track for an award. Looking back at the degree requirements and prequisite tree, this finding is relatively intuitive. Biology for Transfer students tend to tackle their Chemistry and Math requirements in their first two years, leading to the completion of Physics and Biology coursework in later years. 

![Odds of Earning Award by Major Course-Taking](/barriers/plotGLMmajor-2.png)

Students tend to opt for `MATH 30` (OR: 0.68, n: 46) over `MATH 16A` (OR: 0.39, n: 12). While enrollment in either course isn't particularly indicative of award-earning, both courses have odds ratios under `1`, those who enroll in `MATH 30` have a slightly better odds of earning an award or transferring. 

In Physics, students tend to enroll in `PHYS 105\L` (OR: 1.56, n:30) and `110\L` (OR: 12.5, n:20) over `PHYS 205\L` (OR: 1.25, n:3). No students in this cohort (to date) have completed `PHYS 210\L`. The odds for award earning with a `PHYS 110/L` enrollment are quite literally off the charts. This is a good indicator that `PHYS` coursework is some of the last work to be completed before earning an award or transferring. 
 
# General Education and Prerequisite Courses

An odds ratio of `1` is equivalent to a 50-50 probability that enrolling in a class, regardless of outcome, will lead to an award or transfer. Three-quarters of the courses have an odds ratio greater than 3 (`OR >3`), indicating that attending these courses are three times as likely to lead to an award than other overall coursework the student is taking. 
  



![Odds of Earning Award by Non-Major and GE Course-Taking](/barriers/plotGLMnonMajor-2.png)

## The Math Ladder

There is a laddering effect in the data. Near the lowest "rungs" of the ladder are prep courses `ENGL N`, `MATH A` & `D`. At the highest end is the runaway leader for award-earning, `MATH 31` (OR: 41.7, n:27), a prerequisite for the `PHYS 200` series. Most groups appear to cluster around a Math course following a natural hierarchy: 

`MATH A` & `D` (ORs < 1), `MATH 12` (OR: 1.97, n:60), `MATH 27` (OR: 3.7, n:46), `MATH 29` (OR: 8.23, n:23), `MATH 13` (OR 10.3, n:60), before reaching `MATH 31`. 

`MATH 13` is not a required or recommended course, yet 78.3% (n:47) of the 60 students took `MATH 13` as declared Biology for Transfer majors. 

## Plenty of Time to Complete General Education

Students in Biology tend to complete their general education early in their academic career. The degree's required courses follow a hierarchical design (i.e. `CHEM 1A` must precede `BIOL 1`, which precedes `BIOL 2` & `3`, etc). The degree structure may also give a partial explanation as to why the overall odds for award earning by general education and prep courses is so high. Students are taking longer to complete their required coursework, giving them plenty of time to complete their general education.   

Much of the [Academic Plan](https://www.sierracollege.edu/academics/interest-areas/science-technology-engineering-math/biological-sciences/) is open to the student. 

Successful students tend to meet: 
 
 * `IGETC 3A|B: Arts and Humanities` with `MUS 2` (OR: 6.67, n:43), `ARHI 101` (OR: 5.79, n:30), and `HIST 17B` (OR: 6.45, n: 49);  
 
 * `IGETC 4: Social and Behavioral Sciences` with `SOC 0001` (OR: 6.67, n: 43) and `PSYC 100` (OR: 4.14, n: 74); and 
 
 * `IGETC 6: Language Other Than English` with `SPAN 1` (OR: 8.33, n: 22). 
 
 Only `IGETC 4` has explicit recommendations on the Academic Plan. 
 
Contrary to the plan, students tend to forgo `IGETC 5A|B Physical and Biological Sciences` courses `ESS 1` and `GEOG 3` as recommended in the Academic Plan. These courses are not included in Figure 7 due to low enrollment. `IGETC 5A|B` is typically met with the major's required coursework. Similarly, students who attempt `ANTH 1` (OR: 0.10, n:22) tend to have the lowest odds of completion in the cohort. Enrollment in `ANTH 1` as a Biology for Transfer major may be a good indicator the student is off-track.   





