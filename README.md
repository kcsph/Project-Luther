# Project Luther (WIP)

## Situation
Metis Films, a movie production company, is about to release a film titled "Luther" in July 2016. However, they found out that there will be a number of similar movies that will be released in the same month ("density"). Metis took out a high-yield debt to fund the production and is worried that the competition might affect its box office sales and be unable to pay back the debt. The alternative is to delay the release of the film, but this would delay box office cash flows that will be used to pay the interest.

The managers at Metis Films reached out to McKennSo (MKS), a consultancy, to help them on this issue. With a board meeting in two days, the Metis managemet asked MKS to come back with a recommendation by the next day. 

## Methodology
Given the time limits (and budgetary constraints), MKS decided to scrape the web for data and perform a linear regression to determine whether density will materially affect Luther's box office revenues.

## Data & Assumptions
*Data*: Movies from 2011-2015  
*Data Source*: Boxofficemojo  
*Webpages scraped*: ~3,500  
*Features*: Movie density within a week and month by same genre and number of high budget production films  
*Filters*: Through preliminary analysis, budget is the strongest (statistically significant) predictor of box office revenues. As such, only movies with domestic box office gross and production budget of more than US$1 million are included. Removed foreign films(naively) by filtering out 'Foreign' genre.     
*Final Data Set # of Observations*: ~600

## Model
The goal is to focus on the value and statistical significance of movie density. 
Domestic Box Office Gross (Adj. 2015)  = Budget + Genre + Distributor + Days in Release + Week Genre Density + Month Genre Density + Week High Budget Density + Month High Budget Density   
```python
lm1 = smf.ols('dom_gross_adj_2015 ~ budget + genre + distributor + in_release_days + week_genre_density_count + month_genre_density_count + week_budget_density_count + month_budget_density_count',data=DF3)
fit1 = lm1.fit()
fit1.summary()
```
  
## Results  
The 'Month Genre Density' has a statistically significant (p>0.05) effect on domestic box office gross sales, of ~US$5 million. MKS recommends Metis management evaluate if a potential loss of US$5 million by releasing on schedule would materially affect their financial capacity to repay the debt. 
<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>dom_gross_adj_2015</td> <th>  R-squared:         </th> <td>   0.642</td>
</tr>
<tr>
  <th>Model:</th>                    <td>OLS</td>        <th>  Adj. R-squared:    </th> <td>   0.593</td>
</tr>
<tr>
  <th>Method:</th>              <td>Least Squares</td>   <th>  F-statistic:       </th> <td>   12.94</td>
</tr>
<tr>
  <th>Date:</th>              <td>Sun, 24 Apr 2016</td>  <th>  Prob (F-statistic):</th> <td>1.64e-71</td>
</tr>
<tr>
  <th>Time:</th>                  <td>12:31:22</td>      <th>  Log-Likelihood:    </th> <td> -2940.8</td>
</tr>
<tr>
  <th>No. Observations:</th>       <td>   543</td>       <th>  AIC:               </th> <td>   6016.</td>
</tr>
<tr>
  <th>Df Residuals:</th>           <td>   476</td>       <th>  BIC:               </th> <td>   6304.</td>
</tr>
<tr>
  <th>Df Model:</th>               <td>    66</td>       <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>       <td>nonrobust</td>     <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
                     <td></td>                       <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th> <th>[95.0% Conf. Int.]</th> 
</tr>
<tr>
  <th>Intercept</th>                              <td>  -80.0826</td> <td>   31.095</td> <td>   -2.575</td> <td> 0.010</td> <td> -141.183   -18.982</td>
</tr>
<tr>
  <th>genre[T.Adventure]</th>                     <td>  -71.1888</td> <td>   24.445</td> <td>   -2.912</td> <td> 0.004</td> <td> -119.223   -23.155</td>
</tr>
<tr>
  <th>genre[T.Animation]</th>                     <td>  -44.5544</td> <td>   12.852</td> <td>   -3.467</td> <td> 0.001</td> <td>  -69.809   -19.300</td>
</tr>
<tr>
  <th>genre[T.Comedy]</th>                        <td>    3.2431</td> <td>    9.621</td> <td>    0.337</td> <td> 0.736</td> <td>  -15.663    22.149</td>
</tr>
<tr>
  <th>genre[T.Concert]</th>                       <td>   20.2212</td> <td>   43.497</td> <td>    0.465</td> <td> 0.642</td> <td>  -65.249   105.691</td>
</tr>
<tr>
  <th>genre[T.Crime]</th>                         <td>  -16.0071</td> <td>   19.976</td> <td>   -0.801</td> <td> 0.423</td> <td>  -55.259    23.245</td>
</tr>
<tr>
  <th>genre[T.Documentary]</th>                   <td>    4.1127</td> <td>   36.077</td> <td>    0.114</td> <td> 0.909</td> <td>  -66.777    75.002</td>
</tr>
<tr>
  <th>genre[T.Drama]</th>                         <td>  -12.9652</td> <td>   11.214</td> <td>   -1.156</td> <td> 0.248</td> <td>  -35.001     9.070</td>
</tr>
<tr>
  <th>genre[T.Family]</th>                        <td>  -58.5014</td> <td>   19.587</td> <td>   -2.987</td> <td> 0.003</td> <td>  -96.988   -20.014</td>
</tr>
<tr>
  <th>genre[T.Fantasy]</th>                       <td>  -66.7273</td> <td>   19.193</td> <td>   -3.477</td> <td> 0.001</td> <td> -104.441   -29.014</td>
</tr>
<tr>
  <th>genre[T.Foreign]</th>                       <td>  -16.8291</td> <td>   37.312</td> <td>   -0.451</td> <td> 0.652</td> <td>  -90.145    56.487</td>
</tr>
<tr>
  <th>genre[T.Historical]</th>                    <td>   -5.9562</td> <td>   38.119</td> <td>   -0.156</td> <td> 0.876</td> <td>  -80.859    68.947</td>
</tr>
<tr>
  <th>genre[T.Horror]</th>                        <td>    1.2068</td> <td>   13.505</td> <td>    0.089</td> <td> 0.929</td> <td>  -25.331    27.744</td>
</tr>
<tr>
  <th>genre[T.Music]</th>                         <td>    0.8918</td> <td>   43.633</td> <td>    0.020</td> <td> 0.984</td> <td>  -84.846    86.630</td>
</tr>
<tr>
  <th>genre[T.Musical]</th>                       <td>   -3.8105</td> <td>   23.191</td> <td>   -0.164</td> <td> 0.870</td> <td>  -49.380    41.759</td>
</tr>
<tr>
  <th>genre[T.Period]</th>                        <td>  -45.7743</td> <td>   31.435</td> <td>   -1.456</td> <td> 0.146</td> <td> -107.542    15.993</td>
</tr>
<tr>
  <th>genre[T.Romance]</th>                       <td>   38.3183</td> <td>   21.992</td> <td>    1.742</td> <td> 0.082</td> <td>   -4.895    81.532</td>
</tr>
<tr>
  <th>genre[T.Romantic]</th>                      <td>  -34.1531</td> <td>   21.213</td> <td>   -1.610</td> <td> 0.108</td> <td>  -75.835     7.529</td>
</tr>
<tr>
  <th>genre[T.Sci-Fi]</th>                        <td>  -24.5098</td> <td>   11.451</td> <td>   -2.140</td> <td> 0.033</td> <td>  -47.010    -2.010</td>
</tr>
<tr>
  <th>genre[T.Sports]</th>                        <td>  -31.4270</td> <td>   26.227</td> <td>   -1.198</td> <td> 0.231</td> <td>  -82.961    20.107</td>
</tr>
<tr>
  <th>genre[T.Thriller]</th>                      <td>   -4.6661</td> <td>   13.712</td> <td>   -0.340</td> <td> 0.734</td> <td>  -31.609    22.277</td>
</tr>
<tr>
  <th>genre[T.War]</th>                           <td>  -34.7196</td> <td>   31.008</td> <td>   -1.120</td> <td> 0.263</td> <td>  -95.650    26.211</td>
</tr>
<tr>
  <th>genre[T.Western]</th>                       <td>  -63.4269</td> <td>   36.542</td> <td>   -1.736</td> <td> 0.083</td> <td> -135.231     8.377</td>
</tr>
<tr>
  <th>distributor[T.Anchor Bay Films]</th>        <td>   58.8934</td> <td>   65.168</td> <td>    0.904</td> <td> 0.367</td> <td>  -69.159   186.946</td>
</tr>
<tr>
  <th>distributor[T.Bleecker Street]</th>         <td>   36.9227</td> <td>   65.024</td> <td>    0.568</td> <td> 0.570</td> <td>  -90.848   164.693</td>
</tr>
<tr>
  <th>distributor[T.Broad Green Pictures]</th>    <td>   37.6348</td> <td>   65.130</td> <td>    0.578</td> <td> 0.564</td> <td>  -90.343   165.613</td>
</tr>
<tr>
  <th>distributor[T.Buena Vista]</th>             <td>   61.2590</td> <td>   28.917</td> <td>    2.118</td> <td> 0.035</td> <td>    4.438   118.080</td>
</tr>
<tr>
  <th>distributor[T.CBS Films]</th>               <td>   58.6016</td> <td>   35.108</td> <td>    1.669</td> <td> 0.096</td> <td>  -10.383   127.587</td>
</tr>
<tr>
  <th>distributor[T.Clarius Entertainment]</th>   <td> 2.817e-13</td> <td> 1.84e-13</td> <td>    1.533</td> <td> 0.126</td> <td>-7.93e-14  6.43e-13</td>
</tr>
<tr>
  <th>distributor[T.FilmDistrict]</th>            <td>   32.1628</td> <td>   33.525</td> <td>    0.959</td> <td> 0.338</td> <td>  -33.712    98.037</td>
</tr>
<tr>
  <th>distributor[T.Focus Features]</th>          <td>   28.9736</td> <td>   30.148</td> <td>    0.961</td> <td> 0.337</td> <td>  -30.266    88.214</td>
</tr>
<tr>
  <th>distributor[T.Fox]</th>                     <td>   17.1631</td> <td>   28.000</td> <td>    0.613</td> <td> 0.540</td> <td>  -37.857    72.183</td>
</tr>
<tr>
  <th>distributor[T.Fox Searchlight]</th>         <td>  -30.8096</td> <td>   33.303</td> <td>   -0.925</td> <td> 0.355</td> <td>  -96.250    34.630</td>
</tr>
<tr>
  <th>distributor[T.Freestyle Releasing]</th>     <td>   35.0142</td> <td>   49.395</td> <td>    0.709</td> <td> 0.479</td> <td>  -62.046   132.074</td>
</tr>
<tr>
  <th>distributor[T.High Top Releasing]</th>      <td>   63.8457</td> <td>   65.739</td> <td>    0.971</td> <td> 0.332</td> <td>  -65.329   193.020</td>
</tr>
<tr>
  <th>distributor[T.IFC]</th>                     <td> -125.8740</td> <td>   65.198</td> <td>   -1.931</td> <td> 0.054</td> <td> -253.986     2.238</td>
</tr>
<tr>
  <th>distributor[T.Kenn Viselman Presents]</th>  <td>  103.2165</td> <td>   67.100</td> <td>    1.538</td> <td> 0.125</td> <td>  -28.633   235.066</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate]</th>               <td>   68.5659</td> <td>   29.546</td> <td>    2.321</td> <td> 0.021</td> <td>   10.510   126.622</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate/Summit]</th>        <td>   34.2091</td> <td>   31.329</td> <td>    1.092</td> <td> 0.275</td> <td>  -27.351    95.769</td>
</tr>
<tr>
  <th>distributor[T.Newmarket]</th>               <td>   44.9943</td> <td>   64.713</td> <td>    0.695</td> <td> 0.487</td> <td>  -82.164   172.153</td>
</tr>
<tr>
  <th>distributor[T.Open Road Films]</th>         <td>   52.4708</td> <td>   31.188</td> <td>    1.682</td> <td> 0.093</td> <td>   -8.813   113.755</td>
</tr>
<tr>
  <th>distributor[T.Oscilloscope Pictures]</th>   <td>    7.3349</td> <td>   73.405</td> <td>    0.100</td> <td> 0.920</td> <td> -136.903   151.573</td>
</tr>
<tr>
  <th>distributor[T.Paramount]</th>               <td>   52.7879</td> <td>   28.443</td> <td>    1.856</td> <td> 0.064</td> <td>   -3.102   108.678</td>
</tr>
<tr>
  <th>distributor[T.Paramount (DreamWorks)]</th>  <td>   62.9789</td> <td>   37.145</td> <td>    1.695</td> <td> 0.091</td> <td>  -10.009   135.967</td>
</tr>
<tr>
  <th>distributor[T.Picturehouse (II)]</th>       <td>   76.2690</td> <td>   64.835</td> <td>    1.176</td> <td> 0.240</td> <td>  -51.129   203.667</td>
</tr>
<tr>
  <th>distributor[T.Quaker Media]</th>            <td>   76.1058</td> <td>   68.762</td> <td>    1.107</td> <td> 0.269</td> <td>  -59.008   211.220</td>
</tr>
<tr>
  <th>distributor[T.Relativity]</th>              <td>   24.2851</td> <td>   29.849</td> <td>    0.814</td> <td> 0.416</td> <td>  -34.368    82.938</td>
</tr>
<tr>
  <th>distributor[T.Roadside Attractions]</th>    <td>  -35.3819</td> <td>   44.957</td> <td>   -0.787</td> <td> 0.432</td> <td> -123.720    52.956</td>
</tr>
<tr>
  <th>distributor[T.Rocky Mountain Pictures]</th> <td>   60.9970</td> <td>   64.688</td> <td>    0.943</td> <td> 0.346</td> <td>  -66.113   188.107</td>
</tr>
<tr>
  <th>distributor[T.STX Entertainment]</th>       <td>   52.4486</td> <td>   50.500</td> <td>    1.039</td> <td> 0.300</td> <td>  -46.783   151.680</td>
</tr>
<tr>
  <th>distributor[T.Samuel Goldwyn]</th>          <td>   31.9182</td> <td>   44.988</td> <td>    0.709</td> <td> 0.478</td> <td>  -56.480   120.317</td>
</tr>
<tr>
  <th>distributor[T.Sony / Columbia]</th>         <td>   39.2951</td> <td>   28.673</td> <td>    1.370</td> <td> 0.171</td> <td>  -17.047    95.637</td>
</tr>
<tr>
  <th>distributor[T.Sony / Screen Gems]</th>      <td>   75.7988</td> <td>   31.199</td> <td>    2.429</td> <td> 0.015</td> <td>   14.493   137.104</td>
</tr>
<tr>
  <th>distributor[T.Sony Classics]</th>           <td>  -68.9076</td> <td>   35.651</td> <td>   -1.933</td> <td> 0.054</td> <td> -138.960     1.145</td>
</tr>
<tr>
  <th>distributor[T.Summit Entertainment]</th>    <td>   54.7580</td> <td>   35.023</td> <td>    1.563</td> <td> 0.119</td> <td>  -14.060   123.576</td>
</tr>
<tr>
  <th>distributor[T.TriStar]</th>                 <td>   51.6532</td> <td>   31.064</td> <td>    1.663</td> <td> 0.097</td> <td>   -9.386   112.692</td>
</tr>
<tr>
  <th>distributor[T.Universal]</th>               <td>   65.1649</td> <td>   28.437</td> <td>    2.292</td> <td> 0.022</td> <td>    9.287   121.043</td>
</tr>
<tr>
  <th>distributor[T.Warner Bros.]</th>            <td>   41.1792</td> <td>   28.124</td> <td>    1.464</td> <td> 0.144</td> <td>  -14.083    96.441</td>
</tr>
<tr>
  <th>distributor[T.Warner Bros. (New Line)]</th> <td>   47.9761</td> <td>   31.175</td> <td>    1.539</td> <td> 0.124</td> <td>  -13.281   109.233</td>
</tr>
<tr>
  <th>distributor[T.Weinstein / Dimension]</th>   <td>   27.1424</td> <td>   37.792</td> <td>    0.718</td> <td> 0.473</td> <td>  -47.118   101.403</td>
</tr>
<tr>
  <th>distributor[T.Weinstein Company]</th>       <td>   13.8256</td> <td>   30.747</td> <td>    0.450</td> <td> 0.653</td> <td>  -46.591    74.242</td>
</tr>
<tr>
  <th>distributor[T.Well Go USA]</th>             <td>   42.4388</td> <td>   65.198</td> <td>    0.651</td> <td> 0.515</td> <td>  -85.673   170.550</td>
</tr>
<tr>
  <th>budget</th>                                 <td>    0.8880</td> <td>    0.074</td> <td>   12.027</td> <td> 0.000</td> <td>    0.743     1.033</td>
</tr>
<tr>
  <th>in_release_days</th>                        <td>    0.9975</td> <td>    0.081</td> <td>   12.389</td> <td> 0.000</td> <td>    0.839     1.156</td>
</tr>
<tr>
  <th>week_genre_density_count</th>               <td>   -1.6746</td> <td>    4.140</td> <td>   -0.405</td> <td> 0.686</td> <td>   -9.809     6.460</td>
</tr>
<tr>
  <th>month_genre_density_count</th>              <td>   -4.5458</td> <td>    2.280</td> <td>   -1.994</td> <td> 0.047</td> <td>   -9.025    -0.066</td>
</tr>
<tr>
  <th>week_budget_density_count</th>              <td>   -1.2606</td> <td>    3.433</td> <td>   -0.367</td> <td> 0.714</td> <td>   -8.006     5.485</td>
</tr>
<tr>
  <th>month_budget_density_count</th>             <td>    0.6641</td> <td>    1.602</td> <td>    0.415</td> <td> 0.679</td> <td>   -2.483     3.811</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>466.278</td> <th>  Durbin-Watson:     </th> <td>   1.249</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td>26965.360</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 3.346</td>  <th>  Prob(JB):          </th> <td>    0.00</td> 
</tr>
<tr>
  <th>Kurtosis:</th>      <td>36.868</td>  <th>  Cond. No.          </th> <td>1.69e+18</td> 
</tr>
</table>


