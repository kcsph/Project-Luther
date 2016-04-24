
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


```python
DF2.release_month = DF2.release_month.astype('category')
DF2.release_weekday = DF2.release_weekday.astype('category')
DF2.release_monthday = DF2.release_monthday.astype('category')
DF2.release_year = DF2.release_year.astype('category')
DF2.distributor = DF2.distributor.astype('category')
DF2.genre = DF2.genre.astype('category')
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
import matplotlib
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
```


```python
lm1 = smf.ols('dom_gross_adj_2015 ~ budget + genre + distributor + in_release_days + week_genre_density_count + month_genre_density_count + week_budget_density_count + month_budget_density_count',data=DF3)
fit1 = lm1.fit()
fit1.summary()
```




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




```python
lm2 = smf.ols('weekend_gross ~ budget + genre + distributor + in_release_days + week_genre_density_count + month_genre_density_count + week_budget_density_count + month_budget_density_count',data=DF3)
fit2 = lm2.fit()
fit2.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>      <td>weekend_gross</td>  <th>  R-squared:         </th> <td>   0.635</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.582</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   12.03</td>
</tr>
<tr>
  <th>Date:</th>             <td>Sun, 24 Apr 2016</td> <th>  Prob (F-statistic):</th> <td>5.42e-63</td>
</tr>
<tr>
  <th>Time:</th>                 <td>12:17:43</td>     <th>  Log-Likelihood:    </th> <td> -2165.1</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>   500</td>      <th>  AIC:               </th> <td>   4458.</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>   436</td>      <th>  BIC:               </th> <td>   4728.</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>    63</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
                     <td></td>                       <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th> <th>[95.0% Conf. Int.]</th> 
</tr>
<tr>
  <th>Intercept</th>                              <td>  -27.5987</td> <td>   20.938</td> <td>   -1.318</td> <td> 0.188</td> <td>  -68.750    13.553</td>
</tr>
<tr>
  <th>genre[T.Adventure]</th>                     <td>  -34.9940</td> <td>    8.942</td> <td>   -3.913</td> <td> 0.000</td> <td>  -52.569   -17.419</td>
</tr>
<tr>
  <th>genre[T.Animation]</th>                     <td>  -26.2062</td> <td>    4.597</td> <td>   -5.700</td> <td> 0.000</td> <td>  -35.242   -17.171</td>
</tr>
<tr>
  <th>genre[T.Comedy]</th>                        <td>   -2.2851</td> <td>    3.352</td> <td>   -0.682</td> <td> 0.496</td> <td>   -8.874     4.303</td>
</tr>
<tr>
  <th>genre[T.Concert]</th>                       <td>    5.4643</td> <td>   14.829</td> <td>    0.368</td> <td> 0.713</td> <td>  -23.681    34.609</td>
</tr>
<tr>
  <th>genre[T.Crime]</th>                         <td>  -15.5775</td> <td>    7.102</td> <td>   -2.193</td> <td> 0.029</td> <td>  -29.537    -1.618</td>
</tr>
<tr>
  <th>genre[T.Documentary]</th>                   <td>   -4.2775</td> <td>   12.291</td> <td>   -0.348</td> <td> 0.728</td> <td>  -28.435    19.880</td>
</tr>
<tr>
  <th>genre[T.Drama]</th>                         <td>  -12.6019</td> <td>    4.153</td> <td>   -3.035</td> <td> 0.003</td> <td>  -20.764    -4.440</td>
</tr>
<tr>
  <th>genre[T.Family]</th>                        <td>  -30.7411</td> <td>    6.732</td> <td>   -4.567</td> <td> 0.000</td> <td>  -43.972   -17.511</td>
</tr>
<tr>
  <th>genre[T.Fantasy]</th>                       <td>  -28.9395</td> <td>    6.586</td> <td>   -4.394</td> <td> 0.000</td> <td>  -41.884   -15.994</td>
</tr>
<tr>
  <th>genre[T.Foreign]</th>                       <td>  -17.7383</td> <td>   13.025</td> <td>   -1.362</td> <td> 0.174</td> <td>  -43.337     7.860</td>
</tr>
<tr>
  <th>genre[T.Historical]</th>                    <td>  -20.2450</td> <td>   16.843</td> <td>   -1.202</td> <td> 0.230</td> <td>  -53.349    12.859</td>
</tr>
<tr>
  <th>genre[T.Horror]</th>                        <td>   -1.6847</td> <td>    4.657</td> <td>   -0.362</td> <td> 0.718</td> <td>  -10.838     7.469</td>
</tr>
<tr>
  <th>genre[T.Music]</th>                         <td>   -3.8098</td> <td>   14.842</td> <td>   -0.257</td> <td> 0.798</td> <td>  -32.980    25.361</td>
</tr>
<tr>
  <th>genre[T.Musical]</th>                       <td>  -15.6750</td> <td>    7.987</td> <td>   -1.963</td> <td> 0.050</td> <td>  -31.373     0.023</td>
</tr>
<tr>
  <th>genre[T.Period]</th>                        <td>  -18.4432</td> <td>   10.749</td> <td>   -1.716</td> <td> 0.087</td> <td>  -39.570     2.684</td>
</tr>
<tr>
  <th>genre[T.Romance]</th>                       <td>   19.0683</td> <td>    7.556</td> <td>    2.524</td> <td> 0.012</td> <td>    4.218    33.918</td>
</tr>
<tr>
  <th>genre[T.Romantic]</th>                      <td>  -16.0784</td> <td>    7.528</td> <td>   -2.136</td> <td> 0.033</td> <td>  -30.873    -1.284</td>
</tr>
<tr>
  <th>genre[T.Sci-Fi]</th>                        <td>  -14.2201</td> <td>    3.978</td> <td>   -3.574</td> <td> 0.000</td> <td>  -22.039    -6.401</td>
</tr>
<tr>
  <th>genre[T.Sports]</th>                        <td>  -18.3245</td> <td>    8.954</td> <td>   -2.046</td> <td> 0.041</td> <td>  -35.924    -0.725</td>
</tr>
<tr>
  <th>genre[T.Thriller]</th>                      <td>   -6.9293</td> <td>    4.764</td> <td>   -1.454</td> <td> 0.147</td> <td>  -16.294     2.435</td>
</tr>
<tr>
  <th>genre[T.War]</th>                           <td>  -17.2917</td> <td>   12.011</td> <td>   -1.440</td> <td> 0.151</td> <td>  -40.897     6.314</td>
</tr>
<tr>
  <th>genre[T.Western]</th>                       <td>  -48.7126</td> <td>   14.795</td> <td>   -3.292</td> <td> 0.001</td> <td>  -77.791   -19.634</td>
</tr>
<tr>
  <th>distributor[T.Anchor Bay Films]</th>        <td>   23.2146</td> <td>   28.513</td> <td>    0.814</td> <td> 0.416</td> <td>  -32.824    79.254</td>
</tr>
<tr>
  <th>distributor[T.Bleecker Street]</th>         <td>-1.737e-13</td> <td>  1.9e-13</td> <td>   -0.916</td> <td> 0.360</td> <td>-5.46e-13  1.99e-13</td>
</tr>
<tr>
  <th>distributor[T.Broad Green Pictures]</th>    <td>-7.617e-16</td> <td> 2.28e-14</td> <td>   -0.033</td> <td> 0.973</td> <td>-4.55e-14   4.4e-14</td>
</tr>
<tr>
  <th>distributor[T.Buena Vista]</th>             <td>   27.7927</td> <td>   20.549</td> <td>    1.352</td> <td> 0.177</td> <td>  -12.595    68.181</td>
</tr>
<tr>
  <th>distributor[T.CBS Films]</th>               <td>   27.0147</td> <td>   21.564</td> <td>    1.253</td> <td> 0.211</td> <td>  -15.368    69.398</td>
</tr>
<tr>
  <th>distributor[T.Clarius Entertainment]</th>   <td>-3.212e-15</td> <td> 2.72e-14</td> <td>   -0.118</td> <td> 0.906</td> <td>-5.67e-14  5.03e-14</td>
</tr>
<tr>
  <th>distributor[T.FilmDistrict]</th>            <td>   19.0080</td> <td>   21.232</td> <td>    0.895</td> <td> 0.371</td> <td>  -22.721    60.737</td>
</tr>
<tr>
  <th>distributor[T.Focus Features]</th>          <td>   22.4713</td> <td>   20.933</td> <td>    1.073</td> <td> 0.284</td> <td>  -18.671    63.614</td>
</tr>
<tr>
  <th>distributor[T.Fox]</th>                     <td>   12.5703</td> <td>   20.323</td> <td>    0.619</td> <td> 0.537</td> <td>  -27.374    52.514</td>
</tr>
<tr>
  <th>distributor[T.Fox Searchlight]</th>         <td>   16.3732</td> <td>   22.332</td> <td>    0.733</td> <td> 0.464</td> <td>  -27.519    60.266</td>
</tr>
<tr>
  <th>distributor[T.Freestyle Releasing]</th>     <td>   18.5227</td> <td>   24.656</td> <td>    0.751</td> <td> 0.453</td> <td>  -29.936    66.981</td>
</tr>
<tr>
  <th>distributor[T.High Top Releasing]</th>      <td>   30.0498</td> <td>   28.621</td> <td>    1.050</td> <td> 0.294</td> <td>  -26.202    86.302</td>
</tr>
<tr>
  <th>distributor[T.IFC]</th>                     <td>-3.858e-15</td> <td> 1.21e-14</td> <td>   -0.319</td> <td> 0.750</td> <td>-2.76e-14  1.99e-14</td>
</tr>
<tr>
  <th>distributor[T.Kenn Viselman Presents]</th>  <td>   46.6353</td> <td>   29.195</td> <td>    1.597</td> <td> 0.111</td> <td>  -10.744   104.015</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate]</th>               <td>   33.3437</td> <td>   20.684</td> <td>    1.612</td> <td> 0.108</td> <td>   -7.309    73.996</td>
</tr>
<tr>
  <th>distributor[T.Lionsgate/Summit]</th>        <td>   22.3030</td> <td>   20.921</td> <td>    1.066</td> <td> 0.287</td> <td>  -18.815    63.421</td>
</tr>
<tr>
  <th>distributor[T.Newmarket]</th>               <td>   28.1277</td> <td>   28.584</td> <td>    0.984</td> <td> 0.326</td> <td>  -28.052    84.308</td>
</tr>
<tr>
  <th>distributor[T.Open Road Films]</th>         <td>   27.4449</td> <td>   20.891</td> <td>    1.314</td> <td> 0.190</td> <td>  -13.615    68.505</td>
</tr>
<tr>
  <th>distributor[T.Oscilloscope Pictures]</th>   <td>   31.6453</td> <td>   31.600</td> <td>    1.001</td> <td> 0.317</td> <td>  -30.461    93.752</td>
</tr>
<tr>
  <th>distributor[T.Paramount]</th>               <td>   25.6091</td> <td>   20.506</td> <td>    1.249</td> <td> 0.212</td> <td>  -14.695    65.913</td>
</tr>
<tr>
  <th>distributor[T.Paramount (DreamWorks)]</th>  <td>   21.3580</td> <td>   22.014</td> <td>    0.970</td> <td> 0.332</td> <td>  -21.908    64.624</td>
</tr>
<tr>
  <th>distributor[T.Picturehouse (II)]</th>       <td>   40.2826</td> <td>   28.615</td> <td>    1.408</td> <td> 0.160</td> <td>  -15.958    96.524</td>
</tr>
<tr>
  <th>distributor[T.Quaker Media]</th>            <td>   36.6347</td> <td>   29.474</td> <td>    1.243</td> <td> 0.215</td> <td>  -21.295    94.564</td>
</tr>
<tr>
  <th>distributor[T.Relativity]</th>              <td>   15.8611</td> <td>   20.621</td> <td>    0.769</td> <td> 0.442</td> <td>  -24.668    56.391</td>
</tr>
<tr>
  <th>distributor[T.Roadside Attractions]</th>    <td>    1.3885</td> <td>   23.778</td> <td>    0.058</td> <td> 0.953</td> <td>  -45.344    48.121</td>
</tr>
<tr>
  <th>distributor[T.Rocky Mountain Pictures]</th> <td>   32.0471</td> <td>   28.645</td> <td>    1.119</td> <td> 0.264</td> <td>  -24.252    88.346</td>
</tr>
<tr>
  <th>distributor[T.STX Entertainment]</th>       <td>   23.5514</td> <td>   24.779</td> <td>    0.950</td> <td> 0.342</td> <td>  -25.150    72.253</td>
</tr>
<tr>
  <th>distributor[T.Samuel Goldwyn]</th>          <td>   24.5725</td> <td>   23.791</td> <td>    1.033</td> <td> 0.302</td> <td>  -22.186    71.331</td>
</tr>
<tr>
  <th>distributor[T.Sony / Columbia]</th>         <td>   17.3730</td> <td>   20.484</td> <td>    0.848</td> <td> 0.397</td> <td>  -22.887    57.633</td>
</tr>
<tr>
  <th>distributor[T.Sony / Screen Gems]</th>      <td>   36.9919</td> <td>   20.938</td> <td>    1.767</td> <td> 0.078</td> <td>   -4.160    78.144</td>
</tr>
<tr>
  <th>distributor[T.Sony Classics]</th>           <td>   -7.5675</td> <td>   21.888</td> <td>   -0.346</td> <td> 0.730</td> <td>  -50.587    35.451</td>
</tr>
<tr>
  <th>distributor[T.Summit Entertainment]</th>    <td>   33.7934</td> <td>   21.802</td> <td>    1.550</td> <td> 0.122</td> <td>   -9.057    76.644</td>
</tr>
<tr>
  <th>distributor[T.TriStar]</th>                 <td>   24.3341</td> <td>   20.891</td> <td>    1.165</td> <td> 0.245</td> <td>  -16.726    65.394</td>
</tr>
<tr>
  <th>distributor[T.Universal]</th>               <td>   31.7607</td> <td>   20.445</td> <td>    1.553</td> <td> 0.121</td> <td>   -8.422    71.944</td>
</tr>
<tr>
  <th>distributor[T.Warner Bros.]</th>            <td>   22.2738</td> <td>   20.425</td> <td>    1.091</td> <td> 0.276</td> <td>  -17.869    62.417</td>
</tr>
<tr>
  <th>distributor[T.Warner Bros. (New Line)]</th> <td>   22.3457</td> <td>   20.895</td> <td>    1.069</td> <td> 0.285</td> <td>  -18.722    63.413</td>
</tr>
<tr>
  <th>distributor[T.Weinstein / Dimension]</th>   <td>   20.6797</td> <td>   22.015</td> <td>    0.939</td> <td> 0.348</td> <td>  -22.589    63.948</td>
</tr>
<tr>
  <th>distributor[T.Weinstein Company]</th>       <td>   17.8350</td> <td>   21.093</td> <td>    0.846</td> <td> 0.398</td> <td>  -23.621    59.291</td>
</tr>
<tr>
  <th>distributor[T.Well Go USA]</th>             <td>   20.0829</td> <td>   28.406</td> <td>    0.707</td> <td> 0.480</td> <td>  -35.747    75.913</td>
</tr>
<tr>
  <th>budget</th>                                 <td>    0.3006</td> <td>    0.026</td> <td>   11.532</td> <td> 0.000</td> <td>    0.249     0.352</td>
</tr>
<tr>
  <th>in_release_days</th>                        <td>    0.3240</td> <td>    0.033</td> <td>    9.836</td> <td> 0.000</td> <td>    0.259     0.389</td>
</tr>
<tr>
  <th>week_genre_density_count</th>               <td>   -0.9161</td> <td>    1.450</td> <td>   -0.632</td> <td> 0.528</td> <td>   -3.766     1.933</td>
</tr>
<tr>
  <th>month_genre_density_count</th>              <td>   -2.2978</td> <td>    0.813</td> <td>   -2.826</td> <td> 0.005</td> <td>   -3.896    -0.700</td>
</tr>
<tr>
  <th>week_budget_density_count</th>              <td>   -1.1662</td> <td>    1.231</td> <td>   -0.947</td> <td> 0.344</td> <td>   -3.587     1.254</td>
</tr>
<tr>
  <th>month_budget_density_count</th>             <td>    0.6449</td> <td>    0.556</td> <td>    1.161</td> <td> 0.246</td> <td>   -0.447     1.737</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>272.366</td> <th>  Durbin-Watson:     </th> <td>   1.351</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td>3383.531</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 2.088</td>  <th>  Prob(JB):          </th> <td>    0.00</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td>15.041</td>  <th>  Cond. No.          </th> <td>2.52e+17</td>
</tr>
</table>




```python

```


    ---------------------------------------------------------------------------

    ImportError                               Traceback (most recent call last)

    <ipython-input-11-6bf4f957f9b9> in <module>()
    ----> 1 import pandoc
    

    ImportError: No module named 'pandoc'



```python

```
