# Project Luther

## Situation 
LutherFilms, a movie production company, plans to release a film in July 2016. However, they found out that there will be a number of similar movies that will be released in the same month ("density"). Luther took out a high-yield debt to fund the production and is worried that the competition might affect its box office sales and be unable to pay back the debt. The alternative is to delay the release of the film, but this would delay box office cash flows that will be used to pay the interest.

The managers at Luther Films reached out to Metis, a consultancy, to help them on this issue. With a board meeting in two days, Luther managemet asked Metis to come back with a recommendation by the next day. 

## Methodology
Given the time limits (and budgetary constraints), Metis decided to scrape the web for data and perform a linear regression to determine whether density will materially affect Luther's box office revenues.

## Data & Assumptions
*Data*: Movies from 2009-2015  
*Data Source*: Boxofficemojo  
*Webpages scraped*: ~4,400  
*Features*: Movie density within a week and month by same genre and number of high budget production films  
*Filters*: Through preliminary analysis, budget is the strongest (statistically significant) predictor of box office revenues. As such, only movies with domestic box office gross and production budget of more than US$1 million are included. Removed foreign films(naively) by filtering out 'Foreign' genre. Only considered complet cases (drop all observations with null values in any parameter).     
*Final Data Set # of Observations*: ~730

## Model
The goal is to focus on the value and statistical significance of movie density so 100% of the data is used to estimate the model. 
```
adj. dom. gross =  1 + budget + runtime + # days in release + largest # of theater + (largest # of theater)2 + density + genre + distributor + month
```
OLS and elastic net regressions were evaluated. Both produced the similar R-squared values and p-values for the density coefficients. OLS is the chosen final model due. It is more interpretable and less biased without lost of model fit.   
  
OLS results:
<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>dom_gross_adj_2015</td> <th>  R-squared:         </th> <td>   0.738</td> 
</tr>
<tr>
  <th>Model:</th>                    <td>OLS</td>        <th>  Adj. R-squared:    </th> <td>   0.724</td> 
</tr>
<tr>
  <th>Method:</th>              <td>Least Squares</td>   <th>  F-statistic:       </th> <td>   52.91</td> 
</tr>
<tr>
  <th>Date:</th>              <td>Thu, 28 Apr 2016</td>  <th>  Prob (F-statistic):</th> <td>1.47e-175</td>
</tr>
<tr>
  <th>Time:</th>                  <td>15:00:05</td>      <th>  Log-Likelihood:    </th> <td> -3759.5</td> 
</tr>
<tr>
  <th>No. Observations:</th>       <td>   732</td>       <th>  AIC:               </th> <td>   7595.</td> 
</tr>
<tr>
  <th>Df Residuals:</th>           <td>   694</td>       <th>  BIC:               </th> <td>   7770.</td> 
</tr>
<tr>
  <th>Df Model:</th>               <td>    37</td>       <th>                     </th>     <td> </td>    
</tr>
<tr>
  <th>Covariance Type:</th>       <td>nonrobust</td>     <th>                     </th>     <td> </td>    
</tr>
</table>
<table class="simpletable">
<tr>
              <td></td>                 <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th> <th>[95.0% Conf. Int.]</th> 
</tr>
<tr>
  <th>runtime</th>                   <td>    0.5364</td> <td>    0.125</td> <td>    4.284</td> <td> 0.000</td> <td>    0.291     0.782</td>
</tr>
<tr>
  <th>budget</th>                    <td>    0.2452</td> <td>    0.056</td> <td>    4.377</td> <td> 0.000</td> <td>    0.135     0.355</td>
</tr>
<tr>
  <th>in_release_days</th>           <td>    0.5892</td> <td>    0.055</td> <td>   10.784</td> <td> 0.000</td> <td>    0.482     0.696</td>
</tr>
<tr>
  <th>max_no_theaters</th>           <td>   -0.0325</td> <td>    0.007</td> <td>   -4.438</td> <td> 0.000</td> <td>   -0.047    -0.018</td>
</tr>
<tr>
  <th>month_genre_density_count</th> <td>   -1.9830</td> <td>    1.162</td> <td>   -1.707</td> <td> 0.088</td> <td>   -4.264     0.298</td>
</tr>
<tr>
  <th>theater_squared</th>           <td> 1.647e-05</td> <td> 1.84e-06</td> <td>    8.963</td> <td> 0.000</td> <td> 1.29e-05  2.01e-05</td>
</tr>
<tr>
  <th>Action</th>                    <td>    9.2824</td> <td>    7.929</td> <td>    1.171</td> <td> 0.242</td> <td>   -6.286    24.851</td>
</tr>
<tr>
  <th>Adventure/Fantasy</th>         <td>  -18.0783</td> <td>    9.676</td> <td>   -1.868</td> <td> 0.062</td> <td>  -37.076     0.920</td>
</tr>
<tr>
  <th>Animation</th>                 <td>   -5.8590</td> <td>    9.644</td> <td>   -0.608</td> <td> 0.544</td> <td>  -24.795    13.077</td>
</tr>
<tr>
  <th>Comedy</th>                    <td>   16.1960</td> <td>    7.759</td> <td>    2.087</td> <td> 0.037</td> <td>    0.962    31.430</td>
</tr>
<tr>
  <th>Drama</th>                     <td>    4.3549</td> <td>    7.491</td> <td>    0.581</td> <td> 0.561</td> <td>  -10.352    19.062</td>
</tr>
<tr>
  <th>Family</th>                    <td>  -16.4469</td> <td>   10.740</td> <td>   -1.531</td> <td> 0.126</td> <td>  -37.533     4.639</td>
</tr>
<tr>
  <th>Horror</th>                    <td>   14.7559</td> <td>    8.322</td> <td>    1.773</td> <td> 0.077</td> <td>   -1.583    31.094</td>
</tr>
<tr>
  <th>Romance</th>                   <td>    9.8894</td> <td>    9.145</td> <td>    1.081</td> <td> 0.280</td> <td>   -8.066    27.845</td>
</tr>
<tr>
  <th>Sci-Fi</th>                    <td>   -4.2000</td> <td>    8.337</td> <td>   -0.504</td> <td> 0.615</td> <td>  -20.568    12.168</td>
</tr>
<tr>
  <th>Thriller</th>                  <td>   12.5738</td> <td>    8.679</td> <td>    1.449</td> <td> 0.148</td> <td>   -4.466    29.613</td>
</tr>
<tr>
  <th>Buena</th>                     <td>   -1.8495</td> <td>    7.996</td> <td>   -0.231</td> <td> 0.817</td> <td>  -17.549    13.850</td>
</tr>
<tr>
  <th>Focus</th>                     <td>    0.9425</td> <td>   10.159</td> <td>    0.093</td> <td> 0.926</td> <td>  -19.004    20.889</td>
</tr>
<tr>
  <th>Fox</th>                       <td>  -33.2774</td> <td>    6.633</td> <td>   -5.017</td> <td> 0.000</td> <td>  -46.301   -20.254</td>
</tr>
<tr>
  <th>Lionsgate</th>                 <td>    5.3337</td> <td>    7.419</td> <td>    0.719</td> <td> 0.472</td> <td>   -9.233    19.901</td>
</tr>
<tr>
  <th>Paramount</th>                 <td>    0.4899</td> <td>    7.463</td> <td>    0.066</td> <td> 0.948</td> <td>  -14.162    15.142</td>
</tr>
<tr>
  <th>Relativity</th>                <td>  -20.4926</td> <td>    9.998</td> <td>   -2.050</td> <td> 0.041</td> <td>  -40.122    -0.864</td>
</tr>
<tr>
  <th>Sony</th>                      <td>   -9.7875</td> <td>    6.106</td> <td>   -1.603</td> <td> 0.109</td> <td>  -21.776     2.201</td>
</tr>
<tr>
  <th>Universal</th>                 <td>    5.7016</td> <td>    6.910</td> <td>    0.825</td> <td> 0.410</td> <td>   -7.865    19.268</td>
</tr>
<tr>
  <th>Warner</th>                    <td>  -17.2487</td> <td>    6.220</td> <td>   -2.773</td> <td> 0.006</td> <td>  -29.461    -5.036</td>
</tr>
<tr>
  <th>Weinstein</th>                 <td>  -26.5169</td> <td>   10.417</td> <td>   -2.546</td> <td> 0.011</td> <td>  -46.970    -6.064</td>
</tr>
<tr>
  <th>April</th>                     <td>   -9.6908</td> <td>    8.208</td> <td>   -1.181</td> <td> 0.238</td> <td>  -25.807     6.425</td>
</tr>
<tr>
  <th>August</th>                    <td>   -1.4786</td> <td>    7.741</td> <td>   -0.191</td> <td> 0.849</td> <td>  -16.677    13.720</td>
</tr>
<tr>
  <th>December</th>                  <td>    0.6170</td> <td>    8.522</td> <td>    0.072</td> <td> 0.942</td> <td>  -16.115    17.349</td>
</tr>
<tr>
  <th>February</th>                  <td>   -2.9690</td> <td>    8.364</td> <td>   -0.355</td> <td> 0.723</td> <td>  -19.392    13.454</td>
</tr>
<tr>
  <th>July</th>                      <td>   -2.9574</td> <td>    8.296</td> <td>   -0.357</td> <td> 0.722</td> <td>  -19.245    13.330</td>
</tr>
<tr>
  <th>June</th>                      <td>   13.2540</td> <td>    8.294</td> <td>    1.598</td> <td> 0.111</td> <td>   -3.031    29.539</td>
</tr>
<tr>
  <th>March</th>                     <td>   -8.5856</td> <td>    8.185</td> <td>   -1.049</td> <td> 0.295</td> <td>  -24.655     7.484</td>
</tr>
<tr>
  <th>May</th>                       <td>   -2.0330</td> <td>    8.865</td> <td>   -0.229</td> <td> 0.819</td> <td>  -19.438    15.372</td>
</tr>
<tr>
  <th>November</th>                  <td>    3.1109</td> <td>    8.144</td> <td>    0.382</td> <td> 0.703</td> <td>  -12.879    19.100</td>
</tr>
<tr>
  <th>October</th>                   <td>   -7.9429</td> <td>    7.811</td> <td>   -1.017</td> <td> 0.310</td> <td>  -23.279     7.393</td>
</tr>
<tr>
  <th>September</th>                 <td>   -8.3969</td> <td>    7.952</td> <td>   -1.056</td> <td> 0.291</td> <td>  -24.011     7.217</td>
</tr>
<tr>
  <th>const</th>                     <td>  -95.8902</td> <td>   17.285</td> <td>   -5.547</td> <td> 0.000</td> <td> -129.828   -61.952</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>160.829</td> <th>  Durbin-Watson:     </th> <td>   1.998</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td> 534.067</td> 
</tr>
<tr>
  <th>Skew:</th>          <td> 1.030</td>  <th>  Prob(JB):          </th> <td>1.07e-116</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 6.642</td>  <th>  Cond. No.          </th> <td>1.47e+08</td> 
</tr>
</table>
  
The 'Month Genre Density' has a statistically significant (p>0.10) effect on domestic box office gross sales, of US$2 million. Metis recommends Luther management evaluate if a potential loss of by releasing on schedule would materially affect their financial capacity to repay the debt. On the other hand, based on the regression results Luther should consider releasing the film in June, a month earlier. Data shows that films released in June earn about US$13 million higher.

## Other Ideas & Results  
1. Density count based on high budget movies (budget >US$100 million) and simple density count (just the number of movies released in the same time frame) do not have a statistically significant effect on domestic box office gross
2. Movie ratings were considered but eventually discarded because of the focus is on policy levers. Assuming that movie ratings and domestic box office gross are positively related, it would be difficult for Luther to influence ratings - the movie is already ready for release, it is what is is. It would also be improper to influence ratings in any artificial way post-release.
3. Attempted to explore effects of movie posters on domestic box office gross. Due to the lack of "resources", poster data was scraped and reduced to three values - the average RGB values of each pixel. As expected, the RGB variables does not affect box office performance. Reducing the poster to RGB variables excludes other important aspects of the posters. But it was an interesting exercise.
