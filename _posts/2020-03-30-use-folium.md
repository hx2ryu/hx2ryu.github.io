---
title: "[Python] Folium을 이용한 지도 사용법"
categories: Python
tags: [python, folium, map]
toc: true
---



### 1. 필요한 라이브러리 추가

```python
import folium
```



### 2. 구현

##### 1) 위도/경도 값으로 간단한 맵 호출 

```python
# 서울시청 위/경도: 37.566664, 126.978413
latitude = '37.566664'
longitude = '126.978413'

folium.Map(location=[latitude, longitude])
```

![서울시청](/assets/posting_src/map1.png)



##### 2) 마커 표시하기

```python
# 서울시청 좌표: location_cityhall, 덕수궁 좌표: location_deoksugung
location_cityhall = [37.566664, 126.978413]
location_deoksugung = [37.565776, 126.975173]

m = folium.Map(location=location_cityhall, width='50%', height='50%', zoom_start=15)

# 마커 생성하여 맵에 추가
folium.Marker(
    location = location_cityhall,
    popup = 'Seoul City Hall',
    icon = folium.Icon(color='red', icon='info-sign')
).add_to(m)

folium.Marker(
    location = location_deoksugung,
    popup = '덕수궁',
    icon = folium.Icon(color='blue', icon='cloud')
).add_to(m)

# 맵 호출
m
```

![마커 표시](/assets/posting_src/map2.png)



##### 3. 맵에서 클릭한 곳에 마커 표시하기

```python
m.add_child(folium.ClickForMarker(popup='Here'))
```



##### 4. 맵 파일로 저장

```python
path = '/map.html'
m.save(path)
```

