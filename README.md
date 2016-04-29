# Project Luther

## Situation 
LutherFilms, a movie production company, plans to release a film in July 2016. However, they found out that there will be a number of similar movies that will be released in the same month ("density"). Luther took out a high-yield debt to fund the production and is worried that the competition might affect its box office sales and be unable to pay back the debt. The alternative is to delay the release of the film, but this would delay box office cash flows that will be used to pay the interest.

The managers at Luther Films reached out to Metis, a consultancy, to help them on this issue. With a board meeting in two days, Luther managemet asked Metis to come back with a recommendation by the next day. 

## Methodology
Given the time limits (and budgetary constraints), Metis decided to scrape the web for data and perform a linear regression to determine whether density will materially affect Luther's box office revenues.

## Data & Assumptions
**Data**: Movies from 2009-2015  
**Data Source**: Boxofficemojo  
**Webpages scraped**: ~4,400  
**Features**: Movie density within a week and month by same genre and number of high budget production films  
**Filters**: Through preliminary analysis, budget is the strongest (statistically significant) predictor of box office revenues. As such, only movies with domestic box office gross and production budget of more than US$1 million are included. Removed foreign films(naively) by filtering out 'Foreign' genre. Only considered complet cases (drop all observations with null values in any parameter).
**Variable Scaling**: Subtract mean method for "# days in release", "max # of theaters"
**Final Data Set # of Observations**: ~730

## Model
The goal is to focus on the value and statistical significance of movie density so 100% of the data is used to estimate the model. 
```
adj. dom. gross =  1 + adj. budget + # days in release + max # of theaters (C) + (max # of theaters (C))^2 + density + genre + distributor + month
```
OLS and elastic net regressions were evaluated. Both produced the similar R-squared values and p-values for the density coefficients. OLS is the chosen final model due. It is more interpretable and less biased without lost of model fit.   
  
Severe multillineraity was detected in the variable "max # of theaters" and square. Centering (scaling the variable by subtracting the mean) brough VIF down from over 100 to 6. The VIF of "adj. budget" is 7 and the variable is retained as a predictor since removing it will affect R-squared materially and centering the variable does not address multcollinearity. 
  
OLS results:  
<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>dom_gross_adj_2015</td> <th>  R-squared:         </th> <td>   0.733</td> 
</tr>
<tr>
  <th>Model:</th>                    <td>OLS</td>        <th>  Adj. R-squared:    </th> <td>   0.719</td> 
</tr>
<tr>
  <th>Method:</th>              <td>Least Squares</td>   <th>  F-statistic:       </th> <td>   52.90</td> 
</tr>
<tr>
  <th>Date:</th>              <td>Thu, 28 Apr 2016</td>  <th>  Prob (F-statistic):</th> <td>2.93e-173</td>
</tr>
<tr>
  <th>Time:</th>                  <td>22:33:43</td>      <th>  Log-Likelihood:    </th> <td> -3767.4</td> 
</tr>
<tr>
  <th>No. Observations:</th>       <td>   732</td>       <th>  AIC:               </th> <td>   7609.</td> 
</tr>
<tr>
  <th>Df Residuals:</th>           <td>   695</td>       <th>  BIC:               </th> <td>   7779.</td> 
</tr>
<tr>
  <th>Df Model:</th>               <td>    36</td>       <th>                     </th>     <td> </td>    
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
  <th>const</th>                     <td>   54.3642</td> <td>    9.311</td> <td>    5.838</td> <td> 0.000</td> <td>   36.082    72.646</td>
</tr>
<tr>
  <th>adj_budget</th>                <td>    0.3105</td> <td>    0.051</td> <td>    6.119</td> <td> 0.000</td> <td>    0.211     0.410</td>
</tr>
<tr>
  <th>month_genre_density_count</th> <td>   -2.2124</td> <td>    1.172</td> <td>   -1.888</td> <td> 0.059</td> <td>   -4.513     0.089</td>
</tr>
<tr>
  <th>Action</th>                    <td>    5.2021</td> <td>    7.945</td> <td>    0.655</td> <td> 0.513</td> <td>  -10.397    20.801</td>
</tr>
<tr>
  <th>Adventure/Fantasy</th>         <td>  -27.0834</td> <td>    9.578</td> <td>   -2.828</td> <td> 0.005</td> <td>  -45.889    -8.278</td>
</tr>
<tr>
  <th>Animation</th>                 <td>  -24.8590</td> <td>    8.684</td> <td>   -2.863</td> <td> 0.004</td> <td>  -41.910    -7.808</td>
</tr>
<tr>
  <th>Comedy</th>                    <td>   10.7520</td> <td>    7.721</td> <td>    1.393</td> <td> 0.164</td> <td>   -4.407    25.911</td>
</tr>
<tr>
  <th>Drama</th>                     <td>    6.0831</td> <td>    7.557</td> <td>    0.805</td> <td> 0.421</td> <td>   -8.755    20.921</td>
</tr>
<tr>
  <th>Family</th>                    <td>  -31.1875</td> <td>   10.298</td> <td>   -3.028</td> <td> 0.003</td> <td>  -51.407   -10.968</td>
</tr>
<tr>
  <th>Horror</th>                    <td>    7.5307</td> <td>    8.220</td> <td>    0.916</td> <td> 0.360</td> <td>   -8.608    23.670</td>
</tr>
<tr>
  <th>Romance</th>                   <td>    7.8763</td> <td>    9.218</td> <td>    0.854</td> <td> 0.393</td> <td>  -10.222    25.975</td>
</tr>
<tr>
  <th>Sci-Fi</th>                    <td>   -8.2112</td> <td>    8.360</td> <td>   -0.982</td> <td> 0.326</td> <td>  -24.625     8.203</td>
</tr>
<tr>
  <th>Thriller</th>                  <td>    9.2760</td> <td>    8.729</td> <td>    1.063</td> <td> 0.288</td> <td>   -7.862    26.414</td>
</tr>
<tr>
  <th>Buena</th>                     <td>   -3.4803</td> <td>    8.064</td> <td>   -0.432</td> <td> 0.666</td> <td>  -19.313    12.353</td>
</tr>
<tr>
  <th>Focus</th>                     <td>    3.1190</td> <td>   10.247</td> <td>    0.304</td> <td> 0.761</td> <td>  -16.999    23.237</td>
</tr>
<tr>
  <th>Fox</th>                       <td>  -33.7165</td> <td>    6.698</td> <td>   -5.034</td> <td> 0.000</td> <td>  -46.867   -20.566</td>
</tr>
<tr>
  <th>Lionsgate</th>                 <td>    5.5432</td> <td>    7.493</td> <td>    0.740</td> <td> 0.460</td> <td>   -9.169    20.255</td>
</tr>
<tr>
  <th>Paramount</th>                 <td>    0.7589</td> <td>    7.537</td> <td>    0.101</td> <td> 0.920</td> <td>  -14.039    15.557</td>
</tr>
<tr>
  <th>Relativity</th>                <td>  -21.3363</td> <td>   10.095</td> <td>   -2.114</td> <td> 0.035</td> <td>  -41.157    -1.515</td>
</tr>
<tr>
  <th>Sony</th>                      <td>  -10.5908</td> <td>    6.165</td> <td>   -1.718</td> <td> 0.086</td> <td>  -22.695     1.514</td>
</tr>
<tr>
  <th>Universal</th>                 <td>    6.6864</td> <td>    6.974</td> <td>    0.959</td> <td> 0.338</td> <td>   -7.006    20.379</td>
</tr>
<tr>
  <th>Warner</th>                    <td>  -17.2133</td> <td>    6.281</td> <td>   -2.740</td> <td> 0.006</td> <td>  -29.546    -4.880</td>
</tr>
<tr>
  <th>Weinstein</th>                 <td>  -27.0233</td> <td>   10.521</td> <td>   -2.569</td> <td> 0.010</td> <td>  -47.679    -6.367</td>
</tr>
<tr>
  <th>April</th>                     <td>   -7.2751</td> <td>    8.271</td> <td>   -0.880</td> <td> 0.379</td> <td>  -23.515     8.965</td>
</tr>
<tr>
  <th>August</th>                    <td>   -0.4428</td> <td>    7.815</td> <td>   -0.057</td> <td> 0.955</td> <td>  -15.788    14.902</td>
</tr>
<tr>
  <th>December</th>                  <td>    4.3634</td> <td>    8.554</td> <td>    0.510</td> <td> 0.610</td> <td>  -12.431    21.158</td>
</tr>
<tr>
  <th>February</th>                  <td>   -2.0568</td> <td>    8.446</td> <td>   -0.244</td> <td> 0.808</td> <td>  -18.639    14.525</td>
</tr>
<tr>
  <th>July</th>                      <td>   -1.3089</td> <td>    8.367</td> <td>   -0.156</td> <td> 0.876</td> <td>  -17.737    15.119</td>
</tr>
<tr>
  <th>June</th>                      <td>   15.0652</td> <td>    8.364</td> <td>    1.801</td> <td> 0.072</td> <td>   -1.357    31.487</td>
</tr>
<tr>
  <th>March</th>                     <td>   -5.9978</td> <td>    8.242</td> <td>   -0.728</td> <td> 0.467</td> <td>  -22.179    10.183</td>
</tr>
<tr>
  <th>May</th>                       <td>   -2.0075</td> <td>    8.953</td> <td>   -0.224</td> <td> 0.823</td> <td>  -19.587    15.571</td>
</tr>
<tr>
  <th>November</th>                  <td>    6.3878</td> <td>    8.184</td> <td>    0.781</td> <td> 0.435</td> <td>   -9.680    22.456</td>
</tr>
<tr>
  <th>October</th>                   <td>   -4.8583</td> <td>    7.862</td> <td>   -0.618</td> <td> 0.537</td> <td>  -20.294    10.578</td>
</tr>
<tr>
  <th>September</th>                 <td>   -5.9986</td> <td>    8.015</td> <td>   -0.748</td> <td> 0.454</td> <td>  -21.734     9.737</td>
</tr>
<tr>
  <th>max_no_theaters_C</th>         <td>    0.0593</td> <td>    0.004</td> <td>   14.646</td> <td> 0.000</td> <td>    0.051     0.067</td>
</tr>
<tr>
  <th>theater_squared_C</th>         <td> 1.617e-05</td> <td> 1.85e-06</td> <td>    8.751</td> <td> 0.000</td> <td> 1.25e-05  1.98e-05</td>
</tr>
<tr>
  <th>in_release_days_C</th>         <td>    0.6255</td> <td>    0.055</td> <td>   11.463</td> <td> 0.000</td> <td>    0.518     0.733</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>167.691</td> <th>  Durbin-Watson:     </th> <td>   2.026</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td> 588.081</td> 
</tr>
<tr>
  <th>Skew:</th>          <td> 1.056</td>  <th>  Prob(JB):          </th> <td>1.99e-128</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 6.850</td>  <th>  Cond. No.          </th> <td>2.87e+07</td> 
</tr>
</table>  
  
The 'Month Genre Density' has a statistically significant (p < 0.10) effect on domestic box office gross sales, of US$2.2 million. Metis recommends Luther management evaluate if a potential loss of by releasing on schedule would materially affect their financial capacity to repay the debt. On the other hand, based on the regression results Luther should consider releasing the film in June, a month earlier. Data shows that films released in June earn about US$15 million higher.

## Other Ideas & Results  
1. Density count based on high budget movies (budget >US$100 million) and simple density count (just the number of movies released in the same time frame) do not have a statistically significant effect on domestic box office gross
2. Movie ratings were considered but eventually discarded because of the focus is on policy levers. Assuming that movie ratings and domestic box office gross are positively related, it would be difficult for Luther to influence ratings - the movie is already ready for release, it is what is is. It would also be improper to influence ratings in any artificial way post-release.
3. Attempted to explore effects of movie posters on domestic box office gross. Due to the lack of "resources", poster data was scraped and reduced to three values - the average RGB values of each pixel. As expected, the RGB variables does not affect box office performance. Reducing the poster to RGB variables excludes other important aspects of the posters. But it was an interesting exercise.
