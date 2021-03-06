---
title: "[Python] 서울 종합변원 상권분석 #1"
categories: 
 - "Data Analytics"
Tags: [python, 데이터 분석, 상권분석]
toc: true
---


### 1. 상권정보 파일데이터 다운

- [공공데이터 상권정보 링크](https://www.data.go.kr/dataset/15012005/fileData.do) 접속

- `상가(상권)정보_의료기관_201909` 파일 다운로드



### 2. 필요한 라이브러리 호출

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```



### 3. 폰트 설정

```python
# notebook을 실행한 브라우저에서 그래프를 보기 위함.
%matplotlib inline

# 폰트를 선명하게..
from IPython.display import set_matplotlib_formats
set_matplotlib_formats('retina')
```



- Colab 한글폰트 설정

```python
# 폰트 설치(나눔)
!apt-get install fonts-nanum*

# matplotlib 폰트매니저에 폰트 추가
import matplotlib.font_manager as fm

path = '/usr/share/fonts/truetype/nanum/NanumBarunGothic.ttf'

fm.FontProperties(fname=path)
fm._rebuild()

# 폰트 설정
plt.rc('font', family='NanumBarunGothic')
```



### 4. 파일데이터 불러오기

- [로컬파일 불러오기](https://hx2ryu.github.io/Colab-로컬-파일-업로딩-&-다운로딩/)

- [구글 드라이브 연동](https://hx2ryu.github.io/Colab-Google-Drive-연동하기/)

```python
df = pd.read_csv(file_path, low_memory=False)
```



### 5. 결측치

- NaN: Not a value

```python
# 결측치면 True
df.isnull()

# 결측치 수량
null_cnt = df.isnull().sum()
```



- 결측치 상위 10개 Column보기

```python
# DataFrame 생성
df_null_cnt = null_count.reset_index()

# 컬럼명 변경
df_null_cnt.columns = ['컬럼명', '결측치수']

null_cnt_top10 = df_null_cnt.sort_values(by='결측치수', ascending=False).head(10)
```

|      |           컬럼명 | 결측치수 |
| ---: | ---------------: | -------: |
|    2 |           지점명 |    89989 |
|   34 |           동정보 |    83929 |
|   28 |       건물부번지 |    80731 |
|   36 |           호정보 |    75784 |
|   35 |           층정보 |    47291 |
|   30 |           건물명 |    44882 |
|   23 |       지번부번지 |    19256 |
|    9 | 표준산업분류코드 |     4922 |
|   10 |   표준산업분류명 |     4922 |
|   11 |         시도코드 |      379 |



- 결측치 상위 10개 Column 제거하기

```python
drop_cols = null_cnt_top10['컬럼명'].tolist()
dropped_df = df.drop(columns=drop_cols, axis=1)
```



### 6. 통계값

- 특정 `컬럼`에 대한 통계값

```python
df[['위도', '경도']].describe()
```

|       |         위도 |         경도 |
| ----: | -----------: | -----------: |
| count | 91335.000000 | 91335.000000 |
|  mean |    36.624711 |   127.487524 |
|   std |     1.041361 |     0.842877 |
|   min |    33.219290 |   124.717632 |
|   25% |    35.811830 |   126.914297 |
|   50% |    37.234652 |   127.084550 |
|   75% |    37.507463 |   128.108919 |
|   max |    38.499659 |   130.909912 |

- 25%, 50% 75%에 해당하는 값이 아닌 다른 %의 값을 보고 싶은 경우 `percentiles` param 이용

```python
# 20%, 30%, 90%에 해당하는 값을 보고 싶다고 가정
df.describe(percentiles=[.20, .30, .90])
```



-  특정 `데이터타입`에 대한 통계값

```python
# 특정 데이터타입에 대한 통계값
df.describe(include='all') # 전체
df.describe(include='number') # 수치형 데이터
df.describe(include='object') # 문자열 데이터

# unique: 중복을 제거한 값, top: 가장 많이 등장한 데이터, freq: top 데이터의 빈도수
```

|        | 상호명 |   지점명 | 상권업종대분류코드 | 상권업종대분류명 | 상권업종중분류코드 |
| -----: | -----: | -------: | -----------------: | ---------------: | -----------------: |
|  count |  91335 |     1346 |              91335 |            91335 |              91335 |
| unique |  56910 |      858 |                  1 |                1 |                  5 |
|    top |   리원 | 장례식장 |                  S |             의료 |                S01 |
|   freq |    152 |       97 |              91335 |            91335 |              60774 |



- 그룹화한 수치 표현

```python
col_name_city = '시도명'

# 시도별 Row수
df[col_name_city].value_counts()
```

|      |   시도명   |  수   |
| :--: | :--------: | :---: |
|  0   |   경기도   | 21374 |
|  1   | 서울특별시 | 18943 |
|  2   | 부산광역시 | 6473  |
|  3   |  경상남도  | 4973  |
|  4   | 인천광역시 | 4722  |
|  5   | 대구광역시 | 4597  |

```python
# 시도별 비율
df[col_name_city].value_counts(normalize=True)
```

|      |   시도명   |  시도명  |
| :--: | :--------: | :------: |
|  0   |   경기도   | 0.234993 |
|  1   | 서울특별시 | 0.208266 |
|  2   | 부산광역시 | 0.071166 |
|  3   |  경상남도  | 0.054675 |
|  4   | 인천광역시 | 0.051915 |
|  5   | 대구광역시 | 0.050541 |



## Reference

- [[부스트코스] 파이썬으로 시작하는 데이터 사이언스](https://www.edwith.org/boostcourse-ds-510)

