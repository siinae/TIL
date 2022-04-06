# 결측치 처리, 중복값 제거 #

- NaN값 처리 
  - 숫자형 결측값
  - 문자형 결측값





---

	### 01. pandas, numpy 호출 + Series 정의

```python
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

s1 = Series([1,2,3,np.nan])
s1

0    1.0
1    2.0
2    3.0
3    NaN
dtype: float64
    
s2 = Series(['a','b','c',np.nan])
s2

0      a
1      b
2      c
3    NaN
dtype: object
```

---



---

### 02. NaN값 수정 

- 평균 산출 시 -> NaN값을 제외하고 계산

```python
s1.mean()
#2.0
```

- fillna() 를 이용한 치환

```python
s1.fillna(0)  #NaN값을 0으로 치환


0    1.0
1    2.0
2    3.0
3    0.0
dtype: float64
```

- replace()를 이용한 치환

```python
s2.replace(np.nan, 'a')  #NaN값을 a로 치환

0    a
1    b
2    c
3    a
dtype: object
```

- s1 원소들의 null값 유무 확인 

```python
s1.isnull()

0    False
1    False
2    False
3     True
dtype: bool
```

- True인 경우 0으로 정의

```python
s1[s1.isnull()] = 0
s1

0    1.0
1    2.0
2    3.0
3    0.0
dtype: float64
```

---



---

### 03. NaN값으로의 수정

- Series s3정의

```python
s3 = Series(['서울','.','대전','.','대구','.','부산'])
s3

0    서울
1     .
2    대전
3     .
4    대구
5     .
6    부산
dtype: object

```

- '.'의 처리를 위해서는 값을 Nan으로 만든 뒤 결측치 처리를 이용해야 함 --> 문자형의 경우 최빈값으로 대체하는 경우가 많음

```python
S3 = S3.replace('.',np.nan)
s3

0     서울
1    NaN
2     대전
3    NaN
4     대구
5    NaN
6     부산
dtype: object
```

---



---

### 04. NaN값을 이전 값 or 이후 값으로 수정하기

```python
s3.fillna(method = 'ffill')

0    서울
1    서울
2    대전
3    대전
4    대구
5    대구
6    부산
dtype: object
-----------------------------
s3.ffill()

0    서울
1    서울
2    대전
3    대전
4    대구
5    대구
6    부산
dtype: object
```

---



---

### 05. NaN값을 가지는 행, 열 제거

- DataFrame 정의

```python
df1 = DataFrame(np.arange(1,17).reshape(4,4), columns = list('ABCD'))
df1

    A   B   C   D
0   1   2   3   4
1   5   6   7   8
2   9  10  11  12
3  13  14  15  16
```

- NaN값으로 바꾸기

```python
df1.iloc[0,0] = np.nan
#0번째 행 0번째 0 값인 1을 NaN으로 바꿈

df1.iloc[1,[0,1]] 
#1번째 행의 0,1번째 열 값 
A    5.0
B    6.0
Name: 1, dtype: float64

        
df1.iloc[2,[0,1,2]] = np.nan
df1.iloc[3,:] = np.nan
df1

     A    B    C     D
0  NaN  2.0  3.0   4.0
1  5.0  6.0  7.0   8.0
2  NaN  NaN  NaN  12.0
3  NaN  NaN  NaN   NaN

```

- dropna() 
  - default : dropna(how = 'any') 
    - NaN값이 하나라도 포함된 행을 제거
  - dropna(how = 'all')
    - 모두 NaN값인 행만 제거 

```python
df1.dropna()

     A    B    C    D
1  5.0  6.0  7.0  8.0
--------------------------
df1.dropna(how = 'any')

     A    B    C    D
1  5.0  6.0  7.0  8.0
--------------------------
df1.dropna(how = 'all')

     A    B    C     D
0  NaN  2.0  3.0   4.0
1  5.0  6.0  7.0   8.0
2  NaN  NaN  NaN  12.0

```

- 기본적인 결측값 처리 순서
  - np.nan으로 치환 
  - dropna(how = 'all') 이용하여 모두 결측값인 행 제거

```python
df1.dropna(thresh = 2)

     A    B    C    D
0  NaN  2.0  3.0  4.0
1  5.0  6.0  7.0  8.0

#NaN값이 2개 이상인 행 제거
-------------------------------------

df1.dropna(axis = 1, how = 'all')

#특정 컬럼이 모두 NaN으로만 구성되어 있는 경우 제거
-------------------------------------

df1.dropna(subset = ['C'])

     A    B    C    D
0  NaN  2.0  3.0  4.0
1  5.0  6.0  7.0  8.0

#C컬럼 원소 중 NA값이 있는 행 제거
```

---



---

### 06. 중복값 처리

- Series 정의

```python
s1 = Series([1,1,2,3,4])
s1

0    1
1    1
2    2
3    3
4    4
dtype: int64
    
s1.unique()

#array([1, 2, 3, 4], dtype=int64)
#중복되지 않게 출력
```

- 중복값 확인 및 제거(Series)

```python
#중복값 확인
s1.duplicated()

0    False
1     True
2    False
3    False
4    False
dtype: bool
#boolean값으로 변환되어 출력
#'ed'임에 주의

#중복값 제거
s1.drop_duplicates()

0    1
2    2
3    3
4    4
dtype: int64
#'es'임에 주의
```

- DataFrame 정의

```python
df2 = DataFrame({'A':[1,1,3,4],'B':[10,10,30,40]})
df2

   A   B
0  1  10
1  1  10
2  3  30
3  4  40

df3 = DataFrame({'A':[1,1,3,4],'B':[10,10,30,40],'C':[100,200,300,400]})
df3 

   A   B    C
0  1  10  100
1  1  10  200
2  3  30  300
3  4  40  400

```

- 중복값 제거(DataFrame)

```python
df2.drop_duplicates()

   A   B
0  1  10
2  3  30
3  4  40
#'es'임에 주의
--------------------------------------------------
df3.drop_duplicates()

   A   B    C
0  1  10  100
1  1  10  200
2  3  30  300
3  4  40  400
#0,1번째 인덱스의 1과 10이 겹치지만 제거되지 않음
#모든 컬럼의 값이 일치해야 제거!
--------------------------------------------------
df3.drop_duplicates(subset = ['A','B'])

   A   B    C
0  1  10  100
2  3  30  300
3  4  40  400
#컬럼 A,B에 중복된 값이 있는 경우 제거
--------------------------------------------------
df3.drop_duplicates(subset = ['A','B'],keep = 'last')

   A   B    C
1  1  10  200
2  3  30  300
3  4  40  400
#컬럼 A,B에 중복된 값이 있는 경우 제거하고, 마지막 값을 살림
#인덱스가 0이 아닌 1임을 확인
```

---

