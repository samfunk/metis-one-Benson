## Project Benson: Optimizing the effectiveness of WTWY's street teams.  

### Overview  
WomenTechWomenYes (WTWY) has an annual gala at the beginning of the summer. Beforehand, they send out street teams to pass out flyers for the event and collect email signups. WTWY wants to optimize their street teams so that they can get the most email signups. Ideally, the email signups will convert at a high rate to gala attendees, and among attendees, many will make contributions to WTWY.

### Data
We combined MTA data with census data, specifically data from the 2011-2015 American Community Survey 5-Year Estimates. The MTA data provided information on locations with high foot traffic. The census data helped sort these locations by two demographics: women between the ages of 20-34 with degrees in STEM fields and general wealth.
  
* [MTA Turnstile Data](http://web.mta.info/developers/turnstile.html)
* [Median Income in the Past 12 Months (in 2015 inflation-adjusted dollars)](https://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?pid=ACS_15_5YR_S1903&prodType=table)   
* [Field of Bachelor's Degree for First Major](https://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?pid=ACS_15_5YR_S1502&prodType=table)  
* [Age and Sex](https://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?pid=ACS_15_5YR_S0101&prodType=table)  

### Analysis

The MTA data contains cummulative entries and exits for every turnstile in the New York subway system. Using the timestamps, these data can be converted into average and entries and exits per hour for both morning and evening rush hour.  

These Census datasets contain information about people who live in each zip code, not the people who work in each zip code. To combine the two datasets we need to make some assumptions about subway ridership. For this analysis, we assume subway riders work normal office hours of about 9-5 and that subway riders have simple commutes - boarding where they live and exiting where they work. This allows us assume that morning entries and evening exits correspond to folks who live near that station.

For each zip code in New York City, we pulled three statistics from the Census data:
* Percent of population that are women between the ages of 20 and 34
* Percent of women with bachelor degrees that have bachelor degrees in science, engineering, or a related field
* Median income

The first two statistics allowed us to form an estimate of women interested in STEM for each zipcode. Accessing median income allows us to rank zip codes by general wealth, which is important for requesting donations. The statistic maxes out at a median income of $250,000 or above.

### Scoring

After the data was combined, we converted the following features to percentiles:  
* "Average Morning Entries" or "Average Evening Exits"
* Product of "Percent Female" and "Percent Female with STEM Degrees"
* "Median Income"

We next calculated a weighted sum of these percentiles using the following weights:  
* `weight_foot_traffic = 0.4`
* `weight_STEM_women = 0.4`
* `weight_income = 0.2`

The attached presentation contains our recommended stations to visit in the morning and evening based on this weighted sum.
