---
title: "[Colab] 로컬파일 업로딩 & 다운로딩"
categories: "Colab"
Tags: [colab, python, 파일 업로드]
---



### 1. 업로딩

```python
from google.colab import files

uploaded = files.upload()

for fn in uploaded.keys():
  print('name: {name}, length: {length}'.format(name=fn, length=len(uploaded[fn])))
```

- upload함수를 호출한 후 로컬 파일탐색기를 통해서 업로드하고자 하는 파일을 선택할 수 있다.



### 2. 다운로딩

```python
with open('example.txt', 'w') as f:
  f.write('download this file')
  
files.download('example.txt')
```

- 작업한 파일명을 download함수의 매겨변수로 주어 호출하면 해당 파일을 다운로드한다.
