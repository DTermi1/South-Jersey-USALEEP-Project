---
layout: default
---

A brief analysis of possible correlation between several geographic variables and life expectancy at birth, as collected by the [U.S. Small-area Life Expectancy Estimates Project - USALEEP](https://www.cdc.gov/nchs/nvss/usaleep/usaleep.html). Specifically looking at the census tracts within seven New Jersey counties: Atlantic, Burlington, Camden, Cape May, Cumberland, Gloucester and Salem counties. Though it is something of a hot topic in the state, the census tracts making up this group of counties will herein be known as [South Jersey](https://www.state.nj.us/transportation/about/directory/southregion.shtm).   


# Datasets

Principally, used the U.S. Small-area Life Expectancy Estimates Project as base information. Made use of several American Community Survey (ACS) variables from the 2015 5 Year Estimates: Group B02001: Race, B19013_001: Median Household Income in the Last 12 Months, and B16010_002: Less than High School Graduate. Also used [Hospitals in NJ](https://njogis-newjersey.opendata.arcgis.com/datasets/newjersey::hospitals-in-nj/about) created by the New Jersey Office of GIS. National Historical Geographic Information System (NHGIS) coast clipped census tracts (2010) were used to convey both the census and life expectancy data geogrpahically.   

## (NHGIS) Coast Clipped Census Tracts
From https://www.nhgis.org/. Based on TIGER/Line Files created and publish by the Census Bureau. TIGER/Line Files have been clipped to more accurately reflect the geography of coastal areas. A shapefile with the entire nations census tracts was downloaded and subsequently filtered down to NJ and the seven target counties. The filtered data was saved as its own GeoJson.    

## U.S. Small-area Life Expectancy Estimates Project - USALEEP
Data retrieved from https://www.cdc.gov/nchs/nvss/usaleep/usaleep.html. USALEEP was created through a partnership of the National Center for Health Statistics, the Robert Wood Johnson Foundation (RWJF), and the National Association for Public Health Statistics and Information Systems (NAPHSIS). Life expectancy estimates were created in two phases, Phase 1 consisted of Census tracts with 6-year total population size of 5,000 or more and at least 1 death in all age groups, for tracts in this category estimates were created purely through the aggregation of vital statistics. In Phase 2, Census tracts with 6-year total population size of 5,000 or more and 1 or more age groups with zero deaths were given life expectancy estimates based on both vital statistics and a statistical model based on Phase 1 tracts. Vital statistics from 2010-2015 were used; population data from the 2010 decennial census and the 2015 ACS 5 Year survey were used to estimate rolling population. Census tracts with 6-year total population size smaller than 5,000 were excluded from the project. Data was downloaded in CSV format and table joined to the NHGIS census tract file using GEOID/Tract ID.    

## ACS 5 Year Estimate 2011-2015
Made use of several Census Tract level variables.

### Group B02001: Race
My goal was to find the estimated percentage of the population within each Census Tract that was non-white. This group does not seperate white only and white only hispanic. As the Census Bureau only notes how calculate MOE through [aggregation](https://www.census.gov/content/dam/Census/library/publications/2018/acs/acs_general_handbook_2018_ch08.pdf) all non-white variables were summed. This sum was divided by the total population of each Census Tract and then converted to percentage. CV was calculated from another formula on the [previously linked site](https://www.census.gov/content/dam/Census/library/publications/2018/acs/acs_general_handbook_2018_ch08.pdf). This data was imported directly into Google Colab as a list and converted into a dataframe, also table joined to the USALEEP/NHGIS file. Derived data was reliable; no census tracts within the study area had CVs greater than 40%.     

### B19013_001: Median Household Income in the Last 12 Months 
Imported into Google Colab as a list, converted into a dataframe and table joined to the USALEEP/NHGIS file. Data was generally reliable, there were only two census tracts with CVs of over 40%.

### B16010_002: Less than High School Graduate
Imported into Google Colab as a list with B02001_1:Total Population. Both converted into a dataframe. B16010_002 was divided by total population for each census tract and converted to percentage. CV was calculated in the same fashion as Group B02001: Race. This data was also table joined to the USALEEP/NHGIS file. No tract had a CV over 40%.    

## Hospitals in NJ
Retrieved from https://njogis-newjersey.opendata.arcgis.com/datasets/newjersey::hospitals-in-nj/about, and published by the New Jersey Office of GIS. Was last updated on May 14, 2020, definitely not ideal as changes in bed number, the main attribute I used, could have changed a good deal since the pandemic. Hospitals were clipped using the filtered pre-USALEEP join NHGIS census tract file. I also did a 5-mile buffer around South Jersey hospitals to see if there was any correlation between proximity to hospital and life expectancy. 



#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
