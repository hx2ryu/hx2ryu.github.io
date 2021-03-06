---
title: "[Python] 서울 종합변원 상권분석 #2"
categories: 
 - "Data Analytics"
Tags: [python, 데이터 분석, ]
toc: true
---



### 7. 데이터 색인

##### 1) 조건 색인

-  유사의료업의 소분류명의 각 개수 알아보기

```python
df.loc[df['상권업종중분류명'] == '유사의료업', '상권업종소분류명'].value_counts()
```

| 상권업종소분류명 | 상권업종소분류명 |
| :--------------: | :--------------: |
|    치과기공소    |       1724       |
|     언어치료     |       664        |
|  유사의료업기타  |       629        |
|   척추교정치료   |       338        |
|      침구원      |       154        |
|      혈액원      |       130        |
|    응급구조대    |       125        |
|      접골원      |        9         |
|      제대혈      |        1         |



- 서울에 위치한 약국 정보 색인하기

```python
# 색인
df_seoul_pharmacy = df[(df['상권업종소분류명'] == '약국') & (df['시도명'] == '서울특별시')]

# 표
df_seoul_pharmacy.head(7)[['상호명', '상권업종소분류명', '시도명']]
```

|           상호명 | 상권업종소분류명 |     시도명 |
| ---------------: | ---------------: | ---------: |
|       이즈타워약 |             약국 | 서울특별시 |
|         진흥약국 |             약국 | 서울특별시 |
|       신세계약국 |             약국 | 서울특별시 |
|   메디팜한솔약국 |             약국 | 서울특별시 |
|           명약국 |             약국 | 서울특별시 |
| 21세기신천지약국 |             약국 | 서울특별시 |
|       우슬초약국 |             약국 | 서울특별시 |



##### 2. 텍스트 색인

```python
df_seoul_hospital = df.loc[(df['상권업종소분류명'] == '종합병원') & (df['시도명'] == '서울특별시')]

# 상호명에 '꽃배달/의료기/장례식장/상담소/어린이집'이 포함된 데이터의 인덱스 리스트
drop_row1 = df_seoul_hospital.loc[df_seoul_hospital['상호명'].str.contains('꽃배달|의료기|장례식장|상담소|어린이집')].index.tolist()

# 상호명이 '의원'으로 끝나는 데이터 색인 인덱스 리스트
drop_rows2 = df_seoul_hospital.loc[df['상호명'].str.endswith('의원')].index.tolist()

drop_all_rows = drop_row1 + drop_rows2

```



##### 3. 데이터 제거

```python
drop_all_rows = drop_row1 + drop_rows2
df_seoul_hospital = df_seoul_hospital.drop(drop_all_rows, axis=0) 
```

​	



### 8. 차트그리기

- 서울시 구별 의료기관 분포

```python
# seaborn으로 그리는 bar plot
plt.figure(figsize=(15, 4))
sns.countplot(data=df_seoul, x='시군구명')
```

![서울시 구별 의료기관 분포1](/assets/posting_src/seoul_district_barplot.png)



```python
# pandas로 위/경도를 이용한 산점도 그리기
df_seoul[['위도', '경도', '시군구명']].plot.scatter(x='경도', y='위도', figsize=(8, 7), grid=True)
```

![서울시 구별 의료기관 분포2](/assets/posting_src/seoul_district_scatterplot1.png)



```python
# seaborn으로 위/경도를 이용한 산점도 그리기
plt.figure(figsize=(9, 8))
sns.scatterplot(data=df_seoul, x='경도', y='위도', hue='시군구명')
```

![서울시 구별 의료기관 분포3](/assets/posting_src/seoul_district_scatterplot2.png)



## Reference

- [[부스트코스] 파이썬으로 시작하는 데이터 사이언스](https://www.edwith.org/boostcourse-ds-510)

