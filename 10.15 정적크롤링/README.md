# 10.15_정적 크롤링

>  beautifulsoup을 활용한 정적 크롤링

### 다음 뉴스기사 사이트에서 뉴스 제목과 신문사 크롤링하기.(exercise2_2)

```python
import requests
from bs4 import BeautifulSoup
title = []
co = []
urlstr = 'https://news.daum.net/ranking/popular/'
r = requests.get(urlstr)
r.encoding = "utf-8"
bs = BeautifulSoup(r.text, 'html.parser')
titleList = bs.select('.rank_news>ul>li>div.cont_thumb > strong > a')
coList = bs.select('div.cont_thumb > strong > span')

for titleDom in titleList:
    title.append(titleDom.string)
for coDom in coList:
    co.append(coDom.string)

print(len(title)) #길이 한번 체크해보기

for t,c in zip(title,co):
    print(t,c)
    
with open('C:/PyStexam/news.csv', "wt", encoding="utf-8") as f:
    f.write('newstitle, newscomname\n')  
    for i in range(len(title)):
        f.write(title[i]+","+co[i]+'\n')  
```

- with as 구문 안에서는 f라는 이름으로 오픈된 파일 이름을 사용하면 됨. 자동으로 close까지 이어짐





### 다음 영화 리뷰와 별점 크롤링하기(exercise2_3)

```python
import requests
from bs4 import BeautifulSoup
import re
for n in range(1,5):
    req = requests.get('https://movie.daum.net/moviedb/grade?movieId=131704&type=netizen&page='+str(n))
    html = req.text
    soup = BeautifulSoup(html, 'html5lib') 
    # html5lib 대신 html.parser를 사용하면 내용이 제대로 추출되지 않음
    point = soup.select('div.raking_grade > em')
    review = soup.select('div > p')
    movie_point = []
    movie_review = []
    for dom in point:
        movie_point.append(dom.text)
    for dom in review:
        movie_review.append(dom.text)
    
    commentLength = len(movie_point)  
    for i in range(commentLength):
        print(movie_point[i].strip() + ","+movie_review[i].strip())
    print("-----------------------------------------------------")
```

```python
#또 다른 풀이
import requests
from bs4 import BeautifulSoup
import re
n=1
while True:
    requ= requests.get('https://movie.daum.net/moviedb/grade?movieId=131704&type=netizen&page='+str(n))
    html = req.text
    soup = BeautifulSoup(html,'html5lib')
    point = soup.select('div.raking_grade > em')
    review = soup.select('div > p')
    if len(points) == 0:
        break
        
    movie_point = []
    movie_review = []
    
    for dom in points:
        movie_point.append(dom.text)
        
    for dom in reviews:
        content = dom.text.strip()
        content=re.sub("[\n\t]",' ',content)
        movie_review.append(content)
        
    commentLength = len(movie_point)
    for i in range(commentLength):
        print(movie_point[i].strip() + ","+movie_review[i].strip())
        n += 1 
```

