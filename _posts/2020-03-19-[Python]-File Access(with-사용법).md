---
Tag: python, with
---



- 파일에 액세스하기 위해 open 함수를 호출해야 하는데 사용 후 반드시 close해주어야 한다.

- open 함수를 사용하는 2가지 방법

  

### 1. try & finally 구문 사용

```python
try:
	file = open("경로")
  file.write('try & finally 구문을 사용한 방법')
finally:
	file.close()
```

- 사용 후 반드시 close함수를 호출하기 위해 finally 구문 사용.



### 2. with 사용법 (권장)

```python
with open('경로') as file:
  file.write('with 구문을 사용한 방법')
```

- with 코드블럭이 종료되면서 내부적으로 exit함수를 호출하여 close하므로 따로 호출하지 않아도 됌.
