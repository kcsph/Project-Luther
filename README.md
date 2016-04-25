# Project Luther (WIP)

## Situation
Luther Films, a movie production company, is about to release a film in July 2016. However, they found out that there will be a number of similar movies that will be released in the same month ("density"). Luther took out a high-yield debt to fund the production and is worried that the competition might affect its box office sales and be unable to pay back the debt. The alternative is to delay the release of the film, but this would delay box office cash flows that will be used to pay the interest.

The managers at Luther Films reached out to Metis to help them on this issue. With a board meeting in two days, the Luther managemet asked Metis to come back with a recommendation by the next day. 

## Methodology
Given the time limits (and budgetary constraints), Metis decided to scrape the web for data and perform a linear regression to determine whether density will materially affect Luther's box office revenues.

## Data & Assumptions
*Data*: Movies from 2011-2015  
*Data Source*: Boxofficemojo  
*Webpages scraped*: ~3,500  
*Features*: Movie density within a week and month by same genre and number of high budget production films  
*Filters*: Through preliminary analysis, budget is the strongest (statistically significant) predictor of box office revenues. As such, only movies with domestic box office gross and production budget of more than US$1 million are included. Removed foreign films(naively) by filtering out 'Foreign' genre. Also naively dropped all null values. Dropped all movies with domestic gross of over US$600 million (domestic blockbusters), there's less than 5 movies that are blockbusters.  
*Final Data Set # of Observations*: ~500

## Model
The goal is to focus on the value and statistical significance of movie density. 
Domestic Box Office Gross (Adj. 2015)  = Budget + Genre + Distributor + Days in Release + Week Genre Density + Month Genre Density + Week High Budget Density + Month High Budget Density  
  
<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>dom_gross_adj_2015</td> <th>  R-squared:         </th> <td>   0.693</td>
</tr>
<tr>
  <th>Model:</th>                    <td>OLS</td>        <th>  Adj. R-squared:    </th> <td>   0.655</td>
</tr>
<tr>
  <th>Method:</th>              <td>Least Squares</td>   <th>  F-statistic:       </th> <td>   18.32</td>
</tr>
<tr>
  <th>Date:</th>              <td>Mon, 25 Apr 2016</td>  <th>  Prob (F-statistic):</th> <td>2.75e-82</td>
</tr>
<tr>
  <th>Time:</th>                  <td>13:39:53</td>      <th>  Log-Likelihood:    </th> <td> -2565.6</td>
</tr>
<tr>
  <th>No. Observations:</th>       <td>   493</td>       <th>  AIC:               </th> <td>   5241.</td>
</tr>
<tr>
  <th>Df Residuals:</th>           <td>   438</td>       <th>  BIC:               </th> <td>   5472.</td>
</tr>
<tr>
  <th>Df Model:</th>               <td>    54</td>       <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>       <td>nonrobust</td>     <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
                 <td></td>                    <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th> <th>[95.0% Conf. Int.]</th> 
</tr>
<tr>
  <th>Intercept</th>                       <td> -124.7355</td> <td>   49.429</td> <td>   -2.524</td> <td> 0.012</td> <td> -221.884   -27.587</td>
</tr>
<tr>
  <th>genre[T.Adventure]</th>              <td>  -70.1235</td> <td>   20.853</td> <td>   -3.363</td> <td> 0.001</td> <td> -111.107   -29.140</td>
</tr>
<tr>
  <th>genre[T.Animation]</th>              <td>  -45.3909</td> <td>   10.695</td> <td>   -4.244</td> <td> 0.000</td> <td>  -66.411   -24.371</td>
</tr>
<tr>
  <th>genre[T.Comedy]</th>                 <td>   -2.5684</td> <td>    7.878</td> <td>   -0.326</td> <td> 0.745</td> <td>  -18.053    12.916</td>
</tr>
<tr>
  <th>genre[T.Concert]</th>                <td>   21.3398</td> <td>   35.130</td> <td>    0.607</td> <td> 0.544</td> <td>  -47.705    90.384</td>
</tr>
<tr>
  <th>genre[T.Crime]</th>                  <td>  -29.9458</td> <td>   16.635</td> <td>   -1.800</td> <td> 0.073</td> <td>  -62.641     2.749</td>
</tr>
<tr>
  <th>genre[T.Documentary]</th>            <td>   -7.3785</td> <td>   29.160</td> <td>   -0.253</td> <td> 0.800</td> <td>  -64.690    49.933</td>
</tr>
<tr>
  <th>genre[T.Drama]</th>                  <td>  -28.3923</td> <td>    9.744</td> <td>   -2.914</td> <td> 0.004</td> <td>  -47.544    -9.241</td>
</tr>
<tr>
  <th>genre[T.Family]</th>                 <td>  -58.1201</td> <td>   15.870</td> <td>   -3.662</td> <td> 0.000</td> <td>  -89.311   -26.929</td>
</tr>
<tr>
  <th>genre[T.Fantasy]</th>                <td>  -57.9205</td> <td>   15.583</td> <td>   -3.717</td> <td> 0.000</td> <td>  -88.548   -27.293</td>
</tr>
<tr>
  <th>genre[T.Foreign]</th>                <td>  1.51e-12</td> <td> 6.07e-12</td> <td>    0.249</td> <td> 0.804</td> <td>-1.04e-11  1.34e-11</td>
</tr>
<tr>
  <th>genre[T.Historical]</th>             <td>  -37.4726</td> <td>   37.562</td> <td>   -0.998</td> <td> 0.319</td> <td> -111.297    36.352</td>
</tr>
<tr>
  <th>genre[T.Horror]</th>                 <td>   -3.2068</td> <td>   10.970</td> <td>   -0.292</td> <td> 0.770</td> <td>  -24.767    18.354</td>
</tr>
<tr>
  <th>genre[T.Music]</th>                  <td>   -3.8448</td> <td>   35.104</td> <td>   -0.110</td> <td> 0.913</td> <td>  -72.838    65.149</td>
</tr>
<tr>
  <th>genre[T.Musical]</th>                <td>  -11.9452</td> <td>   18.679</td> <td>   -0.639</td> <td> 0.523</td> <td>  -48.657    24.766</td>
</tr>
<tr>
  <th>genre[T.Period]</th>                 <td>  -34.6014</td> <td>   25.515</td> <td>   -1.356</td> <td> 0.176</td> <td>  -84.748    15.545</td>
</tr>
<tr>
  <th>genre[T.Romance]</th>                <td>   34.5790</td> <td>   17.948</td> <td>    1.927</td> <td> 0.055</td> <td>   -0.696    69.854</td>
</tr>
<tr>
  <th>genre[T.Romantic]</th>               <td>  -29.3192</td> <td>   17.818</td> <td>   -1.646</td> <td> 0.101</td> <td>  -64.338     5.700</td>
</tr>
<tr>
  <th>genre[T.Sci-Fi]</th>                 <td>  -32.0882</td> <td>    9.554</td> <td>   -3.359</td> <td> 0.001</td> <td>  -50.865   -13.312</td>
</tr>
<tr>
  <th>genre[T.Sports]</th>                 <td>  -33.5964</td> <td>   21.199</td> <td>   -1.585</td> <td> 0.114</td> <td>  -75.261     8.068</td>
</tr>
<tr>
  <th>genre[T.Thriller]</th>               <td>   -5.6373</td> <td>   11.267</td> <td>   -0.500</td> <td> 0.617</td> <td>  -27.781    16.506</td>
</tr>
<tr>
  <th>genre[T.War]</th>                    <td>  -21.8834</td> <td>   28.434</td> <td>   -0.770</td> <td> 0.442</td> <td>  -77.767    34.000</td>
</tr>
<tr>
  <th>genre[T.Western]</th>                <td>  -60.3573</td> <td>   34.873</td> <td>   -1.731</td> <td> 0.084</td> <td> -128.896     8.182</td>
</tr>
<tr>
  <th>distributor[T.Anchor]</th>           <td>   96.2259</td> <td>   67.447</td> <td>    1.427</td> <td> 0.154</td> <td>  -36.334   228.786</td>
</tr>
<tr>
  <th>distributor[T.Buena]</th>            <td>   76.5819</td> <td>   48.572</td> <td>    1.577</td> <td> 0.116</td> <td>  -18.881   172.044</td>
</tr>
<tr>
  <th>distributor[T.CBS]</th>              <td>   94.1578</td> <td>   51.077</td> <td>    1.843</td> <td> 0.066</td> <td>   -6.229   194.544</td>
</tr>
<tr>
  <th>distributor[T.FilmDistrict]</th>     <td>   67.6167</td> <td>   50.231</td> <td>    1.346</td> <td> 0.179</td> <td>  -31.107   166.340</td>
</tr>
<tr>
  <th>distributor[T.Focus]</th>            <td>   78.3083</td> <td>   49.397</td> <td>    1.585</td> <td> 0.114</td> <td>  -18.776   175.392</td>
</tr>
<tr>
  <th>distributor[T.Fox]</th>              <td>   53.7284</td> <td>   48.037</td> <td>    1.118</td> <td> 0.264</td> <td>  -40.684   148.141</td>
</tr>
<tr>
  <th>distributor[T.Freestyle]</th>        <td>   67.2104</td> <td>   58.235</td> <td>    1.154</td> <td> 0.249</td> <td>  -47.245   181.666</td>
</tr>
<tr>
  <th>distributor[T.High]</th>             <td>  102.4357</td> <td>   67.691</td> <td>    1.513</td> <td> 0.131</td> <td>  -30.603   235.475</td>
</tr>
<tr>
  <th>distributor[T.Kenn]</th>             <td>  143.8768</td> <td>   68.879</td> <td>    2.089</td> <td> 0.037</td> <td>    8.502   279.252</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate]</th>        <td>  108.8687</td> <td>   48.928</td> <td>    2.225</td> <td> 0.027</td> <td>   12.706   205.031</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate/Summit]</th> <td>   75.2624</td> <td>   49.480</td> <td>    1.521</td> <td> 0.129</td> <td>  -21.985   172.509</td>
</tr>
<tr>
  <th>distributor[T.Newmarket]</th>        <td>   99.0193</td> <td>   67.777</td> <td>    1.461</td> <td> 0.145</td> <td>  -34.188   232.227</td>
</tr>
<tr>
  <th>distributor[T.Open]</th>             <td>   89.6278</td> <td>   49.471</td> <td>    1.812</td> <td> 0.071</td> <td>   -7.602   186.857</td>
</tr>
<tr>
  <th>distributor[T.Oscilloscope]</th>     <td>   26.8523</td> <td>   74.719</td> <td>    0.359</td> <td> 0.719</td> <td> -120.000   173.704</td>
</tr>
<tr>
  <th>distributor[T.Paramount]</th>        <td>  100.9108</td> <td>   48.430</td> <td>    2.084</td> <td> 0.038</td> <td>    5.726   196.096</td>
</tr>
<tr>
  <th>distributor[T.Picturehouse]</th>     <td>  128.8769</td> <td>   67.880</td> <td>    1.899</td> <td> 0.058</td> <td>   -4.535   262.288</td>
</tr>
<tr>
  <th>distributor[T.Quaker]</th>           <td>  113.6918</td> <td>   69.872</td> <td>    1.627</td> <td> 0.104</td> <td>  -23.635   251.019</td>
</tr>
<tr>
  <th>distributor[T.Relativity]</th>       <td>   57.7786</td> <td>   48.805</td> <td>    1.184</td> <td> 0.237</td> <td>  -38.143   153.700</td>
</tr>
<tr>
  <th>distributor[T.Roadside]</th>         <td>   -1.0096</td> <td>   56.210</td> <td>   -0.018</td> <td> 0.986</td> <td> -111.484   109.464</td>
</tr>
<tr>
  <th>distributor[T.Rocky]</th>            <td>  114.4861</td> <td>   67.685</td> <td>    1.691</td> <td> 0.091</td> <td>  -18.541   247.513</td>
</tr>
<tr>
  <th>distributor[T.STX]</th>              <td>   86.0035</td> <td>   58.745</td> <td>    1.464</td> <td> 0.144</td> <td>  -29.455   201.462</td>
</tr>
<tr>
  <th>distributor[T.Samuel]</th>           <td>  110.7378</td> <td>   58.974</td> <td>    1.878</td> <td> 0.061</td> <td>   -5.170   226.645</td>
</tr>
<tr>
  <th>distributor[T.Sony]</th>             <td>   77.4993</td> <td>   48.205</td> <td>    1.608</td> <td> 0.109</td> <td>  -17.243   172.242</td>
</tr>
<tr>
  <th>distributor[T.Summit]</th>           <td>   95.4986</td> <td>   51.613</td> <td>    1.850</td> <td> 0.065</td> <td>   -5.942   196.939</td>
</tr>
<tr>
  <th>distributor[T.TriStar]</th>          <td>   86.5192</td> <td>   49.387</td> <td>    1.752</td> <td> 0.080</td> <td>  -10.546   183.585</td>
</tr>
<tr>
  <th>distributor[T.Universal]</th>        <td>  107.8650</td> <td>   48.402</td> <td>    2.229</td> <td> 0.026</td> <td>   12.736   202.994</td>
</tr>
<tr>
  <th>distributor[T.Warner]</th>           <td>   82.0786</td> <td>   48.212</td> <td>    1.702</td> <td> 0.089</td> <td>  -12.677   176.834</td>
</tr>
<tr>
  <th>distributor[T.Weinstein]</th>        <td>   61.5259</td> <td>   49.112</td> <td>    1.253</td> <td> 0.211</td> <td>  -34.998   158.050</td>
</tr>
<tr>
  <th>distributor[T.Well]</th>             <td>   74.7600</td> <td>   67.182</td> <td>    1.113</td> <td> 0.266</td> <td>  -57.280   206.800</td>
</tr>
<tr>
  <th>budget</th>                          <td>    0.6998</td> <td>    0.060</td> <td>   11.741</td> <td> 0.000</td> <td>    0.583     0.817</td>
</tr>
<tr>
  <th>in_release_days</th>                 <td>    1.1263</td> <td>    0.074</td> <td>   15.178</td> <td> 0.000</td> <td>    0.980     1.272</td>
</tr>
<tr>
  <th>month_genre_density_count</th>       <td>   -4.2578</td> <td>    1.554</td> <td>   -2.739</td> <td> 0.006</td> <td>   -7.313    -1.203</td>
</tr>
<tr>
  <th>month_budget_density_count</th>      <td>    1.4806</td> <td>    1.015</td> <td>    1.459</td> <td> 0.145</td> <td>   -0.513     3.475</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>107.660</td> <th>  Durbin-Watson:     </th> <td>   1.382</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td> 468.264</td> 
</tr>
<tr>
  <th>Skew:</th>          <td> 0.898</td>  <th>  Prob(JB):          </th> <td>2.08e-102</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 7.424</td>  <th>  Cond. No.          </th> <td>1.61e+18</td> 
</tr>
</table>
  
The 'Month Genre Density' has a statistically significant (p>0.05) effect on domestic box office gross sales, of ~US$4-5 million. Metis recommends Luther management evaluate if a potential loss of US$5 million by releasing on schedule would materially affect their financial capacity to repay the debt.   

##Next Steps 
1. Do exploratory data anlysis to: (1) adjust data filters, (2) check correlation and pair plots for directional relationship and fucntional forms  
2. Refine model
3. If there's time, explore other uses of the model (prediction)
