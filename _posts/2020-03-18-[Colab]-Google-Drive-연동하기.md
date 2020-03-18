---
Date: 2020-03-18
Tag: colab, google drive
---



## [Colab] Google Drive 연동

- 연동하는 3가지 방법 중 마운팅하는 방법이 소스가 가장 간단해보여서 정리함.



```python
from google.colab import drive
drive.mount('/content/drive')
```

- colab에서 위 코드를 실행한 후 url에 접속하여 인증코드를 얻은 후 입력한다.



```python
with open('/content/drive/My Drive/test.txt', 'w') as f:
  f.write('Hello, world')
```

- 위 소스를 실행하면 연동된 구글 드라이버 최상위 루트에 **'test.txt'** 파일을 생성된다.

