# 메서드 치환, 삭제 / 정렬 #





---

### 01. replace 메서드 ### 

`replace(찾을 문자열, 바꿀 문자열) :치환`

- 기본 문자열 메서드
- 기본 파이썬 제공
- 문자열 호출 가능
- 벡터 연산(각 원소별 반복처리) 불가능
- 문자열 치환만 가능(숫자치환, NA 치환 불가능)

---







---

### 02. str.replace ###

`Series([리스트]).str.replace(찾을 문자열, 바꿀 문자열)`

- pandas 제공 --> Series 객체만 호출 가능
- 백터화 내장된 문자열 메서드
- 문자열 호출 가능
- 벡터 연산(각 원소별 반복처리) 가능
- 문자열 치환만 가능(숫자치환, NA 치환 불가능)
- 숫자로 구성된 Series 적용 불가

---







---

### 03. pandas replace ###

`df.replace(찾을 문자열, 바꿀 문자열)`

- pandas 제공
- 값 치환 메서드(단, 완전히 일치하는 값만 치환 가능)
- Series, DataFrame 호출 가능
- 숫자치환, NA 치환 가능
- 동시에 여러 대상 수정 가능

---







---

### 04. 리스트는 replace(), map() 호출 불가능 -->해결 방법은? ###



##### (1) 리스트 replace 호출하기  #####

```python
['abcd','abcde','aabb'].replace(',','')

#AttributeError: 'list' object has no attribute 'replace'
```



- 해결 방법 1: for문 이용

```python
outlist = []
for i in [abcd','abcde','aabb']:
          outlist.append(i.replace('a',''))
         
print(outlist)
          
##['bcd', 'bcde', 'bb']
```

- 해결 방법 2 : map 이용

```python
f1 = lambda x: x.replace('a','A')
list(map(f1,['abcd','abcde','aabb']))

#['Abcd', 'Abcde', 'AAbb']
```



But, 리스트로 map함수를 호출하면

```python
['abcd','abcde','aabb'].map(f1)

## AttributeError: 'list' object has no attribute 'map'
```

--> 해결 방법은?



##### (2) 리스트 map 호출하기 ######

```python
from pandas import Series, DataFrame
Series(['abcd','abcde','aabb']).map(f1)

# 0     Abcd
# 1    Abcde
# 2     AAbb
# dtype: object
```

- Series는 호출 가능 --> `method chaining!`

---







---

### 05. map 총정리 ###



```python
#testdata
df = DataFrame({'a':[2,5,3,6],'b':[71,23,25,59],'c':[493,112,190,506]})
```



##### (1) map 함수 ##### 

- 1차원 원소별 적용

- 다수의 인자 전달 시 각 인자의 크기 일치 필요

- numpy에서 사용

- Return `List`

  

##### (2)  map 메서드 #####

- 1차원(Series) 원소별 적용
- 다수의 인자 전달 시 각 인자의 크기 일치할 필요 X
- pandas에서 사용
- Return `Series`



##### (3) apply 메서드 

- 2차원 DataFrame 구조의 행별/열별 적용
- 주로 그룹 함수와 함께 사용
- Return Series 



##### (4) applymap 메서드

- 2차원 DataFrame 구조의 원소별 적용
- Return DataFrame

---







---

### 06. sort() ###

- Series, DataFrame 호출 가능



##### (1) sort_index()

```python
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

a = pd.read_csv('a.csv')
a.sort_index(ascending = True)  #오름차순 정렬
a.sort_index(ascending = False) #내림차순 정렬
a.sort_index(axis = 0)          #행 기준으로 열끼리 정렬
a.sort_index(axis = 1)			#열 기준으로 행끼리 정렬

```



##### (2) sort_value()

- Series, DataFrame 특정 컬럼 순서에 맞게 본문의 값(value)으로 정렬

```python
a.sort_values(by = 'name')  
#name 기준으로 오름차순(default)정렬

a.sort_values(by = ['name','salary'],ascending = [True, False]) 
#name(오름차순)에 따른 salary(내림차순) 정렬  
```



