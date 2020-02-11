# Crawling top 100 ice cream shops in yelp
In the program, we crawled 10 webpages in yelp to find the 100 most popular ice cream shop in New York City and listed the information we need:
- [x] Ranking    
- [x] Name
- [x] Rating
- [x] Telephone
- [x] Address
- [x] District

Firstly, import the pakeages we need:
```
from bs4 import BeautifulSoup
import urllib.request
import pandas as pd
%matplotlib inline 
```
We need web address to get information. There are 10 pages in total, if we want it to automaticly crawl, we need a for loop to change url:
``` 
urllist=[]
for i in range(0,100,10):
    url = 'https://www.yelp.com/search?find_desc=Ice%20Cream&find_loc=New%20York%2C%20NY%2010023&start='
    url+=str(i)
    urllist.append(url)
parentlist=[]
```
For each page we crawl, find the htlm code and beautifulsoup to parser
```
soup=BeautifulSoup(ourUrl,'html.parser')
mains=soup.find_all('div',{'class':'lemon--div__373c0__1mboc largerScrollablePhotos__373c0__3FEIJ arrange__373c0__UHqhV border-color--default__373c0__2oFDT'})
```
The following code shows how to find rank information. The usual format is rank.name, if we just want rank information then we can judge where point is and extract information before point
```
rank=main.find('p').text
            if rank[1]=='.' or rank[2]=='.':
                rank1=rank.index('.')
                rank2=int(rank[0:rank1])
            else:
                rank2=None
```
After extract all the information we need, we use pandas to dataframe
```
tb=pd.DataFrame(data=parentlist,columns=['Rank','Name','Ratings','Num_review','Tel','Add','District'])
```
Also, we can use plot chart to show this
```
tb[tb['District']!=''].groupby('District').Ratings.mean().plot(kind='bar')
```
