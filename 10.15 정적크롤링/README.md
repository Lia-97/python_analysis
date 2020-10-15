# 10.15_정적 크롤링

beautifulsoup을 활용한 정적 크롤링

다음 뉴스기사 사이트에서 뉴스 제목과 신문사 크롤링하기.

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

