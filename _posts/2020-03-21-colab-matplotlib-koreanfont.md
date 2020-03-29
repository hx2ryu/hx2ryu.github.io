---
title: "[Colab] matplotlib 한글폰트 설정"
categories: "Colab"
Tags: [python, colab, matplotlib, font]
toc: true
---



### 1.  폰트 설치

```python
!apt-get install fonts-nanum*
```



### 2. 라이브러리 추가

```python
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm
```



### 3. 폰트 설정

```python
path = '/usr/share/fonts/truetype/nanum/NanumBarunGothic.ttf'

fm.FontProperties(fname=path)
fm._rebuild()

plt.rc('font', family='NanumBarunGothic')
```

- 설정 후 한글폰트가 안나오면 런타임 재실행 후 `폰트설정 후 다시 확인`
  - 런타임 재실행: Runtime - Restart runtime... `(단축키: cmd+M.)`

