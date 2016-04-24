# Project-Luther blue blue blue blue bleh bleh bleh

## Situation
Metis Films, a movie production company, is about to release a film titled "Luther" in July 2016. However, they found out that there will be a number of similar movies that will be released in the same month ("density"). Metis took out a high-yield debt to fund the production and is worried that the competition might affect its box office sales and be unable to pay back the debt. The alternative is to delay the release of the film, but this would delay box office cash flows that will be used to pay the interest.

The managers at Metis Films reached out to McKennSo, a consultancy, to help them on this issue. With a board meeting in two days, the Metis managemet asked McKennSo to come back with a recommendation by the next day. 

## Methodology
Given the time limits (and budgetary constraints), McKennSo decided to scrape the web for data and perform a linear regression to determine whether density will materially affect Luther's box office revenues.

## Data & Assumptions
*Data*: Movies from 2011-2015  
*Data Source*: Boxofficemojo  
*Webpages scraped*: ~3,500  
*Features*: Movie density within a week and month by same genre and number of high budget production films  
*Data Munging*: Through preliminary analysis, budget is the strongest (statistically significant) predictor of box office revenues. As such, only movies with domestic box office gross and production budget of more than US$1 million are included  
*Final Data Set # of Observations*: ~600

## Model
The goal is to focus on the value and statistical significance of movie density. 
Domestic Box Office Gross (Adj. 2015)  = Budget + Rating + 
