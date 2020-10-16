# 10.16_동적 크롤링

Web Element 객체 찾기

- 태그의 css 선택자로 찾기.(.find_element_by_css_selector())

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get('https://www.naver.com/') 
target=driver.find_element_by_css_selector("[name = 'query']")
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
```

- 태그의 id 속성 값으로 찾기(.find_element_by_id())

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get('https://www.naver.com/') 
target=driver.find_element_by_id('query')
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
```

- 태그의 class 속성 값으로 찾기(.find_element_by_class_name())

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get('https://www.naver.com/') 
target=driver.find_element_by_class_name('input_text')
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
```

