
# 1.0 Getting movie links for scraping


```python
# Get Soup
import requests
from bs4 import BeautifulSoup
import re
import dateutil.parser

##Page list 
pagelist2015 = ['http://www.boxofficemojo.com/yearly/chart/?page=1&view=releasedate&view2=domestic&yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=2&view=releasedate&view2=domestic&yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=3&view=releasedate&view2=domestic&yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=4&view=releasedate&view2=domestic&yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=5&view=releasedate&view2=domestic&yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=6&view=releasedate&view2=domestic&yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=7&view=releasedate&view2=domestic&yr=2015&p=.htm']
pagelist2014 = ['http://www.boxofficemojo.com/yearly/chart/?yr=2014&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=2&view=releasedate&view2=domestic&yr=2014&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=3&view=releasedate&view2=domestic&yr=2014&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=4&view=releasedate&view2=domestic&yr=2014&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=5&view=releasedate&view2=domestic&yr=2014&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=6&view=releasedate&view2=domestic&yr=2014&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=7&view=releasedate&view2=domestic&yr=2014&adjust_mo=&adjust_yr=2015&p=.htm']
pagelist2013 = ['http://www.boxofficemojo.com/yearly/chart/?yr=2013&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=2&view=releasedate&view2=domestic&yr=2013&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=3&view=releasedate&view2=domestic&yr=2013&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=4&view=releasedate&view2=domestic&yr=2013&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=5&view=releasedate&view2=domestic&yr=2013&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=6&view=releasedate&view2=domestic&yr=2013&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=7&view=releasedate&view2=domestic&yr=2013&adjust_mo=&adjust_yr=2015&p=.htm']
pagelist2012 = ['http://www.boxofficemojo.com/yearly/chart/?yr=2012&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=2&view=releasedate&view2=domestic&yr=2012&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=3&view=releasedate&view2=domestic&yr=2012&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=4&view=releasedate&view2=domestic&yr=2012&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=5&view=releasedate&view2=domestic&yr=2012&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=6&view=releasedate&view2=domestic&yr=2012&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=7&view=releasedate&view2=domestic&yr=2012&adjust_mo=&adjust_yr=2015&p=.htm']
pagelist2011 = ['http://www.boxofficemojo.com/yearly/chart/?yr=2011&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=2&view=releasedate&view2=domestic&yr=2011&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=3&view=releasedate&view2=domestic&yr=2011&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=4&view=releasedate&view2=domestic&yr=2011&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=5&view=releasedate&view2=domestic&yr=2011&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=6&view=releasedate&view2=domestic&yr=2011&adjust_mo=&adjust_yr=2015&p=.htm','http://www.boxofficemojo.com/yearly/chart/?page=7&view=releasedate&view2=domestic&yr=2011&adjust_mo=&adjust_yr=2015&p=.htm']
pagelist = pagelist2015 + pagelist2014 + pagelist2013 + pagelist2012 + pagelist2011
```


```python
##Find movie links based on page list
movielist = []
for page in pagelist:
    url = page
    response = requests.get(url,headers={'Microsoft Edge':'Metis data science student scraping project'})
    soup = BeautifulSoup(response.text)
    for x in soup.find_all('a'):
        try:
            if "/movies/?id" in x['href']:
                movielist.append(x['href'])
            else:
                continue
        except:
            continue
            
##Translate movie links into full html addresses
htmllist = []
for x in movielist:
    htmllist.append('http://www.boxofficemojo.com'+x+'&adjust_yr=2015&p=.htm')
```

    C:\Users\kennd\Anaconda3\lib\site-packages\bs4\__init__.py:166: UserWarning: No parser was explicitly specified, so I'm using the best available HTML parser for this system ("lxml"). This usually isn't a problem, but if you run this code on another system, or in a different virtual environment, it may use a different parser and behave differently.
    
    To get rid of this warning, change this:
    
     BeautifulSoup([your markup])
    
    to this:
    
     BeautifulSoup([your markup], "lxml")
    
      markup_type=markup_type))
    


```python
len(htmllist)
```




    3387



# 2.0 Scraping Script

## Import BeautifulSoup and scraping modules
from bs4 import BeautifulSoup
import requests
import re
url = 'http://www.boxofficemojo.com/movies/?id=fruitvale.htm'
response = requests.get(url,headers={'Microsoft Edge':'Metis data science student scraping project'})
soup = BeautifulSoup(response.text)

## 2.1 Subfunctions to extract data from movie webpages


```python
##Get movie title
def get_movie_title(soup):
    try:
        return soup.find('title').text.split('-')[0].split('(')[0].strip()
    except:
        return None

##Get movie domestic box office gross
def get_movie_domestic_gross(soup):
    try:
        return float(soup.find_all('b')[2].text.replace('$','').replace(',',''))/(10**6)
    except:
        return None
    
##Get movie distributor
def get_movie_distributor(soup):
    try:
        return soup.find(text=re.compile('Distributor')).findNextSibling().text
    except:
        return None
    
##Get movie release date
def get_movie_release_date(soup):
    try:
        datestring = soup.find(text=re.compile('Release Date')).findNextSibling().text
        date = dateutil.parser.parse(datestring)
        return date
    except:
        return None
        
##Get movie genre
def get_movie_genre(soup):
    try:
        return soup.find(text=re.compile('Genre:')).findNextSibling().text.split()[0]
    except:
        return None
    
##Get movie runtime
def get_movie_runtime(soup):
    try:
        runtime_string= soup.find(text=re.compile('Runtime')).findNextSibling().text.split()
        return float(runtime_string[0])*60 + float(runtime_string[2])
    except:
        return None

##Get movie MPAA rating
def get_movie_mpaa_rating(soup):
    try:
        return soup.find(text=re.compile('MPAA')).findNextSibling().text
    except:
        return None

##Get movie production budget
def get_movie_prod_budget(soup):
    try:
        prod_budget_string = soup.find(text=re.compile('Production Budget')).findNextSibling().text.replace('$','').replace(',','')
        if 'million' in prod_budget_string:
            return float(prod_budget_string.split()[0])
        else:
            return None
    except:
        return None

##Get movie opening weekend gross
def get_movie_weekend_gross(soup):
    if soup.find(text=re.compile('Wide\xa0Opening')):
        try:
            return float(soup.find(text=re.compile('Wide\xa0Opening')).findNext().text.replace('$','').replace(',',''))/(10**6)
        except:
            return None
    elif soup.find(text=re.compile('Opening\xa0Weekend')):
        try:
            return float(soup.find(text=re.compile('Opening\xa0Weekend')).findNext().text.replace('$','').replace(',',''))/(10**6)
        except:
            return None
    else:
        return None

##Get movie in release days
def get_movie_release_days(soup):
    try:
        return abs(float(soup.find(text=re.compile("In Release")).findNext().text.strip().split()[0]))
    except:
        return None
```

## 2.2  Combine subfunctions into one function


```python
def get_movie_data(soup):
    datalist = []
    datalist.append(get_movie_title(soup))
    datalist.append(get_movie_domestic_gross(soup))
    datalist.append(get_movie_distributor(soup))
    datalist.append(get_movie_release_date(soup))
    datalist.append(get_movie_genre(soup))
    datalist.append(get_movie_runtime(soup))
    datalist.append(get_movie_mpaa_rating(soup))
    datalist.append(get_movie_prod_budget(soup))
    datalist.append(get_movie_weekend_gross(soup))
    datalist.append(get_movie_release_days(soup))
    df.append(datalist)
```

## 2.3 Loop through links and combine into one data frame


```python
##Set df as master list
df = []
for link in htmllist:
    response = requests.get(link,headers={'Microsoft Edge':'Metis data science student scraping project'})
    soup = BeautifulSoup(response.text)
    get_movie_data(soup)
```

    C:\Users\kennd\Anaconda3\lib\site-packages\bs4\__init__.py:166: UserWarning: No parser was explicitly specified, so I'm using the best available HTML parser for this system ("lxml"). This usually isn't a problem, but if you run this code on another system, or in a different virtual environment, it may use a different parser and behave differently.
    
    To get rid of this warning, change this:
    
     BeautifulSoup([your markup])
    
    to this:
    
     BeautifulSoup([your markup], "lxml")
    
      markup_type=markup_type))
    


```python
import pandas as pd
DF = pd.DataFrame(df, columns = ['title','dom_gross_adj_2015','distributor','release_date','genre','runtime','rating','budget','weekend_gross','in_release_days'])
DF.drop_duplicates()
DF.shape
```




    (3387, 10)



### Checkpoint 1: Pickle


```python
##Pickle
import pickle
with open('my_data.pkl', 'wb') as picklefile:
    pickle.dump(DF, picklefile)
```


```python
##Take out of jar
import pickle
import pandas as pd
import numpy as np
import math
import matplotlib
import datetime
%matplotlib inline
with open("my_data.pkl", 'rb') as picklefile: 
    DF = pickle.load(picklefile)
```


```python
DF2 = DF[(DF.dom_gross_adj_2015>1) & (DF.budget>1)].reset_index(drop=True)
```


```python
def get_month(x):
    return x.month

def get_weekday(x):
    return x.isoweekday()

def get_monthday(x):
    return x.day

def get_year(x):
    return x.year

DF2["release_month"] = DF2["release_date"].apply(get_month)
DF2["release_weekday"] = DF2["release_date"].apply(get_weekday)
DF2["release_monthday"] = DF2["release_date"].apply(get_monthday)
DF2["release_year"] = DF2["release_date"].apply(get_year)
```


```python
##Create genre density count for each movie
##Very slow but no choice but to loop through the data frame
week_count_list = []
for current_row in range(DF2.shape[0]):
    week_count = 0.0
    current_DF = DF2.iloc[current_row,:]
    for compare_row in range(0,DF2.shape[0]):
        compare_DF = DF2.iloc[compare_row,:]
        try: 
            time_delta = abs((current_DF[3]-compare_DF[3]).days)
        except:
            time_delta = 0
        if time_delta <= 7 and (current_DF[4] == compare_DF[4]):
            week_count +=1
    week_count_list.append(week_count)
week_count_list = pd.Series(week_count_list)
```


```python
##Create genre density count for each movie
##Very slow but no choice but to loop through the data frame
month_count_list = []
for current_row in range(DF2.shape[0]):
    month_count = 0.0
    current_DF = DF2.iloc[current_row,:]
    for compare_row in range(0,DF2.shape[0]):
        compare_DF = DF2.iloc[compare_row,:]
        try: 
            time_delta = abs((current_DF[3]-compare_DF[3]).days)
        except:
            time_delta = 0
        if time_delta <= 30 and (current_DF[4] == compare_DF[4]):
            month_count +=1
    month_count_list.append(month_count)
month_count_list = pd.Series(month_count_list)
```


```python
##Create high budget density count for each movie
##Very slow but no choice but to loop through the data frame
budget_week_count_list = []
for current_row in range(DF2.shape[0]):
    week_count = 0.0
    current_DF = DF2.iloc[current_row,:]
    for compare_row in range(0,DF2.shape[0]):
        compare_DF = DF2.iloc[compare_row,:]
        try: 
            time_delta = abs((current_DF[3]-compare_DF[3]).days)
        except:
            time_delta = 0
        if time_delta <= 7 and compare_DF.budget >= 100:
            week_count +=1
    budget_week_count_list.append(week_count)
budget_week_count_list = pd.Series(budget_week_count_list)
```


```python
##Create high budget density count for each movie
##Very slow but no choice but to loop through the data frame
budget_month_count_list = []
for current_row in range(DF2.shape[0]):
    month_count = 0.0
    current_DF = DF2.iloc[current_row,:]
    for compare_row in range(0,DF2.shape[0]):
        compare_DF = DF2.iloc[compare_row,:]
        try: 
            time_delta = abs((current_DF[3]-compare_DF[3]).days)
        except:
            time_delta = 0
        if time_delta <= 30 and compare_DF.budget >= 100:
            month_count +=1
    budget_month_count_list.append(month_count)
budget_month_count_list = pd.Series(budget_month_count_list)
```


```python
DF2["week_genre_density_count"] = week_count_list
DF2["month_genre_density_count"] = month_count_list
DF2["week_budget_density_count"] = budget_week_count_list
DF2["month_budget_density_count"] = budget_month_count_list
DF2 = DF2[(DF2["release_year"] >= 2011) & (DF2["release_year"] < 2016)]
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-4-5a8031b77f74> in <module>()
    ----> 1 DF2["week_genre_density_count"] = week_count_list
          2 DF2["month_genre_density_count"] = month_count_list
          3 DF2["week_budget_density_count"] = budget_week_count_list
          4 DF2["month_budget_density_count"] = budget_month_count_list
          5 DF2 = DF2[(DF2["release_year"] >= 2011) & (DF2["release_year"] < 2016)]
    

    NameError: name 'week_count_list' is not defined



```python
DF2 = DF2[DF2['genre'] != 'Foreign']
DF2.release_month = DF2.release_month.astype('category')
DF2.release_weekday = DF2.release_weekday.astype('category')
DF2.release_monthday = DF2.release_monthday.astype('category')
DF2.release_year = DF2.release_year.astype('category')
DF2.distributor = DF2.distributor.astype('category')
DF2.genre = DF2.genre.astype('category')
DF2.distributor = DF2.distributor.apply(lambda x : x.split()[0])
DF2.rating = DF2.rating.astype('category')
```

### Checkpoint 2: Pickle


```python
##Pickle checkpoint
import pickle
with open('my_data2.pkl', 'wb') as picklefile:
    pickle.dump(DF2, picklefile)
```


```python
import pickle
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
with open("my_data2.pkl", 'rb') as picklefile: 
    DF2 = pickle.load(picklefile)
```

# 3.0 Exploratory Analysis

# 4.0 Regression model


```python
import statsmodels.formula.api as smf
```


```python
DF3 = DF2.copy()
DF3 = DF3.dropna()
DF3 = DF3[DF3['dom_gross_adj_2015']<600]
```


```python
lm2 = smf.ols('dom_gross_adj_2015 ~ budget + genre + distributor + in_release_days + month_genre_density_count + month_budget_density_count',data=DF3)
fit2 = lm2.fit()
fit2.summary()
```




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




```python
lm2 = smf.ols('weekend_gross ~ budget + genre + distributor + in_release_days + month_genre_density_count + month_budget_density_count',data=DF3)
fit2 = lm2.fit()
fit2.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>      <td>weekend_gross</td>  <th>  R-squared:         </th> <td>   0.620</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.574</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   13.26</td>
</tr>
<tr>
  <th>Date:</th>             <td>Mon, 25 Apr 2016</td> <th>  Prob (F-statistic):</th> <td>2.68e-63</td>
</tr>
<tr>
  <th>Time:</th>                 <td>13:40:05</td>     <th>  Log-Likelihood:    </th> <td> -2097.8</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>   493</td>      <th>  AIC:               </th> <td>   4306.</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>   438</td>      <th>  BIC:               </th> <td>   4537.</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>    54</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
                 <td></td>                    <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th> <th>[95.0% Conf. Int.]</th> 
</tr>
<tr>
  <th>Intercept</th>                       <td>  -25.3063</td> <td>   19.136</td> <td>   -1.322</td> <td> 0.187</td> <td>  -62.915    12.303</td>
</tr>
<tr>
  <th>genre[T.Adventure]</th>              <td>  -30.0480</td> <td>    8.073</td> <td>   -3.722</td> <td> 0.000</td> <td>  -45.914   -14.182</td>
</tr>
<tr>
  <th>genre[T.Animation]</th>              <td>  -21.8270</td> <td>    4.140</td> <td>   -5.272</td> <td> 0.000</td> <td>  -29.964   -13.690</td>
</tr>
<tr>
  <th>genre[T.Comedy]</th>                 <td>   -4.7107</td> <td>    3.050</td> <td>   -1.545</td> <td> 0.123</td> <td>  -10.705     1.284</td>
</tr>
<tr>
  <th>genre[T.Concert]</th>                <td>    3.5144</td> <td>   13.600</td> <td>    0.258</td> <td> 0.796</td> <td>  -23.215    30.244</td>
</tr>
<tr>
  <th>genre[T.Crime]</th>                  <td>  -14.8668</td> <td>    6.440</td> <td>   -2.309</td> <td> 0.021</td> <td>  -27.524    -2.210</td>
</tr>
<tr>
  <th>genre[T.Documentary]</th>            <td>   -5.2213</td> <td>   11.289</td> <td>   -0.463</td> <td> 0.644</td> <td>  -27.408    16.966</td>
</tr>
<tr>
  <th>genre[T.Drama]</th>                  <td>  -14.2782</td> <td>    3.772</td> <td>   -3.785</td> <td> 0.000</td> <td>  -21.692    -6.864</td>
</tr>
<tr>
  <th>genre[T.Family]</th>                 <td>  -27.6901</td> <td>    6.144</td> <td>   -4.507</td> <td> 0.000</td> <td>  -39.765   -15.615</td>
</tr>
<tr>
  <th>genre[T.Fantasy]</th>                <td>  -24.1414</td> <td>    6.033</td> <td>   -4.002</td> <td> 0.000</td> <td>  -35.998   -12.285</td>
</tr>
<tr>
  <th>genre[T.Foreign]</th>                <td> 2.967e-12</td> <td> 2.35e-12</td> <td>    1.262</td> <td> 0.208</td> <td>-1.65e-12  7.59e-12</td>
</tr>
<tr>
  <th>genre[T.Historical]</th>             <td>  -17.4553</td> <td>   14.541</td> <td>   -1.200</td> <td> 0.231</td> <td>  -46.035    11.124</td>
</tr>
<tr>
  <th>genre[T.Horror]</th>                 <td>   -1.5469</td> <td>    4.247</td> <td>   -0.364</td> <td> 0.716</td> <td>   -9.894     6.800</td>
</tr>
<tr>
  <th>genre[T.Music]</th>                  <td>   -6.5936</td> <td>   13.590</td> <td>   -0.485</td> <td> 0.628</td> <td>  -33.303    20.116</td>
</tr>
<tr>
  <th>genre[T.Musical]</th>                <td>  -15.5955</td> <td>    7.231</td> <td>   -2.157</td> <td> 0.032</td> <td>  -29.808    -1.383</td>
</tr>
<tr>
  <th>genre[T.Period]</th>                 <td>  -14.0467</td> <td>    9.878</td> <td>   -1.422</td> <td> 0.156</td> <td>  -33.460     5.367</td>
</tr>
<tr>
  <th>genre[T.Romance]</th>                <td>   19.8270</td> <td>    6.948</td> <td>    2.854</td> <td> 0.005</td> <td>    6.171    33.483</td>
</tr>
<tr>
  <th>genre[T.Romantic]</th>               <td>  -15.2377</td> <td>    6.898</td> <td>   -2.209</td> <td> 0.028</td> <td>  -28.795    -1.681</td>
</tr>
<tr>
  <th>genre[T.Sci-Fi]</th>                 <td>  -15.2228</td> <td>    3.699</td> <td>   -4.116</td> <td> 0.000</td> <td>  -22.492    -7.954</td>
</tr>
<tr>
  <th>genre[T.Sports]</th>                 <td>  -18.0979</td> <td>    8.207</td> <td>   -2.205</td> <td> 0.028</td> <td>  -34.227    -1.968</td>
</tr>
<tr>
  <th>genre[T.Thriller]</th>               <td>   -6.4349</td> <td>    4.362</td> <td>   -1.475</td> <td> 0.141</td> <td>  -15.007     2.138</td>
</tr>
<tr>
  <th>genre[T.War]</th>                    <td>  -17.1676</td> <td>   11.008</td> <td>   -1.560</td> <td> 0.120</td> <td>  -38.802     4.467</td>
</tr>
<tr>
  <th>genre[T.Western]</th>                <td>  -40.8809</td> <td>   13.500</td> <td>   -3.028</td> <td> 0.003</td> <td>  -67.414   -14.347</td>
</tr>
<tr>
  <th>distributor[T.Anchor]</th>           <td>   19.8838</td> <td>   26.111</td> <td>    0.762</td> <td> 0.447</td> <td>  -31.434    71.202</td>
</tr>
<tr>
  <th>distributor[T.Buena]</th>            <td>   23.2564</td> <td>   18.804</td> <td>    1.237</td> <td> 0.217</td> <td>  -13.700    60.213</td>
</tr>
<tr>
  <th>distributor[T.CBS]</th>              <td>   24.5929</td> <td>   19.773</td> <td>    1.244</td> <td> 0.214</td> <td>  -14.270    63.456</td>
</tr>
<tr>
  <th>distributor[T.FilmDistrict]</th>     <td>   17.7888</td> <td>   19.446</td> <td>    0.915</td> <td> 0.361</td> <td>  -20.430    56.008</td>
</tr>
<tr>
  <th>distributor[T.Focus]</th>            <td>   21.0805</td> <td>   19.123</td> <td>    1.102</td> <td> 0.271</td> <td>  -16.504    58.665</td>
</tr>
<tr>
  <th>distributor[T.Fox]</th>              <td>   14.0427</td> <td>   18.597</td> <td>    0.755</td> <td> 0.451</td> <td>  -22.507    50.593</td>
</tr>
<tr>
  <th>distributor[T.Freestyle]</th>        <td>   17.7593</td> <td>   22.545</td> <td>    0.788</td> <td> 0.431</td> <td>  -26.550    62.069</td>
</tr>
<tr>
  <th>distributor[T.High]</th>             <td>   26.4116</td> <td>   26.205</td> <td>    1.008</td> <td> 0.314</td> <td>  -25.092    77.915</td>
</tr>
<tr>
  <th>distributor[T.Kenn]</th>             <td>   42.0534</td> <td>   26.665</td> <td>    1.577</td> <td> 0.115</td> <td>  -10.354    94.461</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate]</th>        <td>   32.5618</td> <td>   18.941</td> <td>    1.719</td> <td> 0.086</td> <td>   -4.666    69.789</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate/Summit]</th> <td>   22.8153</td> <td>   19.155</td> <td>    1.191</td> <td> 0.234</td> <td>  -14.832    60.463</td>
</tr>
<tr>
  <th>distributor[T.Newmarket]</th>        <td>   26.7078</td> <td>   26.238</td> <td>    1.018</td> <td> 0.309</td> <td>  -24.861    78.277</td>
</tr>
<tr>
  <th>distributor[T.Open]</th>             <td>   24.9139</td> <td>   19.152</td> <td>    1.301</td> <td> 0.194</td> <td>  -12.727    62.554</td>
</tr>
<tr>
  <th>distributor[T.Oscilloscope]</th>     <td>   26.1285</td> <td>   28.926</td> <td>    0.903</td> <td> 0.367</td> <td>  -30.722    82.979</td>
</tr>
<tr>
  <th>distributor[T.Paramount]</th>        <td>   25.7269</td> <td>   18.749</td> <td>    1.372</td> <td> 0.171</td> <td>  -11.122    62.576</td>
</tr>
<tr>
  <th>distributor[T.Picturehouse]</th>     <td>   37.5340</td> <td>   26.279</td> <td>    1.428</td> <td> 0.154</td> <td>  -14.114    89.182</td>
</tr>
<tr>
  <th>distributor[T.Quaker]</th>           <td>   33.6478</td> <td>   27.050</td> <td>    1.244</td> <td> 0.214</td> <td>  -19.516    86.811</td>
</tr>
<tr>
  <th>distributor[T.Relativity]</th>       <td>   14.9772</td> <td>   18.894</td> <td>    0.793</td> <td> 0.428</td> <td>  -22.157    52.111</td>
</tr>
<tr>
  <th>distributor[T.Roadside]</th>         <td>    0.8988</td> <td>   21.760</td> <td>    0.041</td> <td> 0.967</td> <td>  -41.869    43.667</td>
</tr>
<tr>
  <th>distributor[T.Rocky]</th>            <td>   31.2191</td> <td>   26.203</td> <td>    1.191</td> <td> 0.234</td> <td>  -20.280    82.718</td>
</tr>
<tr>
  <th>distributor[T.STX]</th>              <td>   20.9348</td> <td>   22.742</td> <td>    0.921</td> <td> 0.358</td> <td>  -23.763    65.632</td>
</tr>
<tr>
  <th>distributor[T.Samuel]</th>           <td>   31.5744</td> <td>   22.831</td> <td>    1.383</td> <td> 0.167</td> <td>  -13.297    76.446</td>
</tr>
<tr>
  <th>distributor[T.Sony]</th>             <td>   20.5691</td> <td>   18.662</td> <td>    1.102</td> <td> 0.271</td> <td>  -16.109    57.247</td>
</tr>
<tr>
  <th>distributor[T.Summit]</th>           <td>   32.9248</td> <td>   19.981</td> <td>    1.648</td> <td> 0.100</td> <td>   -6.346    72.195</td>
</tr>
<tr>
  <th>distributor[T.TriStar]</th>          <td>   24.4041</td> <td>   19.119</td> <td>    1.276</td> <td> 0.202</td> <td>  -13.173    61.981</td>
</tr>
<tr>
  <th>distributor[T.Universal]</th>        <td>   30.9009</td> <td>   18.738</td> <td>    1.649</td> <td> 0.100</td> <td>   -5.926    67.728</td>
</tr>
<tr>
  <th>distributor[T.Warner]</th>           <td>   23.0873</td> <td>   18.664</td> <td>    1.237</td> <td> 0.217</td> <td>  -13.595    59.770</td>
</tr>
<tr>
  <th>distributor[T.Weinstein]</th>        <td>   18.6452</td> <td>   19.013</td> <td>    0.981</td> <td> 0.327</td> <td>  -18.722    56.013</td>
</tr>
<tr>
  <th>distributor[T.Well]</th>             <td>   12.5133</td> <td>   26.008</td> <td>    0.481</td> <td> 0.631</td> <td>  -38.603    63.630</td>
</tr>
<tr>
  <th>budget</th>                          <td>    0.2623</td> <td>    0.023</td> <td>   11.366</td> <td> 0.000</td> <td>    0.217     0.308</td>
</tr>
<tr>
  <th>in_release_days</th>                 <td>    0.2853</td> <td>    0.029</td> <td>    9.930</td> <td> 0.000</td> <td>    0.229     0.342</td>
</tr>
<tr>
  <th>month_genre_density_count</th>       <td>   -2.0766</td> <td>    0.602</td> <td>   -3.451</td> <td> 0.001</td> <td>   -3.259    -0.894</td>
</tr>
<tr>
  <th>month_budget_density_count</th>      <td>    0.5648</td> <td>    0.393</td> <td>    1.438</td> <td> 0.151</td> <td>   -0.207     1.337</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>183.286</td> <th>  Durbin-Watson:     </th> <td>   1.439</td> 
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td>1025.895</td> 
</tr>
<tr>
  <th>Skew:</th>          <td> 1.521</td>  <th>  Prob(JB):          </th> <td>1.70e-223</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 9.379</td>  <th>  Cond. No.          </th> <td>1.61e+18</td> 
</tr>
</table>


