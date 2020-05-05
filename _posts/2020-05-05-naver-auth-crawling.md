title: "[웹크롤링] 네이버 로그인 인증"
categories: "웹크롤링
tags: [python, 웹크롤링]
toc: true
---


### 1. 라이브러리 추가 및 유틸리티 설치

```python
from selenium import webdriver
```

- [크롬 드라이버 설치](https://chromedriver.chromium.org/downloads)
  - 설치시 크롬드라이버와 설치된 크롬의 버전 일치해야 함.
    - **ex) If you are using Chrome version `83`, please download ChromeDriver `83.0.4103.14`**



### 2. 구현

```python
chrome_driver_path = '크롬드라이버 설치된 위치'
login_url = 'https://nid.naver.com/'
id = '개인 아이디'
pw = '개인 패스워드'

driver = webdriver.Chrome(chrome_driver_path)
driver.get(login_url)

driver.find_element_by_id('id').send_keys(id)
driver.find_element_by_id('pw').send_keys(pw)

driver.find_element_by_css_selector('#frmNIDLogin > fieldset > input').click()
```

