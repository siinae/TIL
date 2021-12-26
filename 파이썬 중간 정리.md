# 파이썬 중간 정리 #



---

### 01. 변수와 리스트 ###

1. 모듈 호출

- 모듈명.함수명

  ```python
  round(1.5)
  #2
  
  trunc(1.5)
  #NameError: name 'trunc' is not defined
  
  
  import math as ma
  ma.trunc(2.8) 
  #2
  ```

  

2.  모듈 내 함수 직접 호출

- 함수명만 사용 가능

  ```python
  from math import trunc
  trunc(2.8)
  #2
  ```



3. 산술연산

   ```python
   9 // 2
   
   #4
   #몫 정수 출력
   
   9 / 2
   
   #4
   #몫 실수 출력
   
   4 ** 2 
   #16
   #거듭제곱
   
   math.pow(4,2)
   #16.0
   #pow() : 거듭제곱 실수형으로 출력
   ```

   

4. 파이썬 기본 구조

   (1) 리스트

- 여러 상수의 동시 전달이 가능한 1차원 기본 자료구조

- 서로 다른 데이터 타입 허용

```python
a = [1,2,3,4]
type(a)
#list

a2 = [1,2,3,'4']
type(a2)
#list
```

​		

- 리스트 색인/수정/연산/확장

```python
a[-1]  #reverse indexing
#4 

a[0:1] # n:m --> n에서 m-1까지
#[1]

a[0,2]
a[[0,2]]
#TypeError: list indices must be integers or slices, not list
#여러 숫자 전달은 불가능

a[0] = 9  #수정
a
#[9,2,3,4]

a + 4 
# TypeError: can only concatenate list (not "int") to list
# 리스트와 정수(int) 연산 불가

a > 4
# TypeError: '>' not supported between instances of 'list' and 'int'
# 조건의 전달 불가

[1,2,5,2] + [4,2,6,2]  #확장
#[1,2,5,2,4,2,6,2]

a + [4]           #원소 추가
#[9,2,3,4,4]

a.append(7)       #원소 추가2
a
#[9,2,3,4,4,7]

del(a[0])  #첫번째 원소 삭제
a
#[2,3,4,4,7]

del(a)     #객체 삭제
a
##NameError: name 'a' is not defined

a2 = []    #리스트 내 모든 원소 삭제
a2
#[]
```



​	(2) 튜플

- 고정되어 변경이 불가능한 상수 전달
- 괄호를 하지 않아도 고정된 값이므로 튜플로 자동인식

```python
t = (1,2,3,4)
type(t) 
#tuple

t2 = 1,2,3,4
type(t2)
#tuple

t[0] = 9
#TypeError: 'tuple' object does not support item assignment
#수정 불가능
```

---







---

### 02. 문자열 처리 ###

- 함수와 메서드

  - 함수

    - 함수(대상) 

    - 인수 전달이 모두 괄호 안에서 진행 됨

  - 메서드:
    - 대상.메서드
    - 객체에서 호출 가능한 형태의 함수(값을 객체가 가지고 있음)

  - 메서드는 함수의 일부, 인수의 전달 방식이 다름

```python
###대소 치환
b = 'abcde' 				#string
b.upper() 					#대문자치환
'ABC'.lower() 				#소문자치환
'apple banana'.title()		#단어 첫글자 대문자 치환
#'Apple Banana'

###색인(문자열 추출)
'apple'[-3]
#'p'

###문자열 시작, 끝 여부 확인
b.startwith('a')     #a로 시작?
b.startwith('a',1)   #a가 두번째(1)에 있나?
b[1:].startwith('a') #b의 두번째가 a로 시작?
b.endswith('e')		 #e로 끝?

###앞뒤 공백 또는 문자 제거
'     abc   '.strip  #양쪽 공백 제거
#'abc'

'abc'.strip('a') 	 #문자 제거
#'bc'

'abaca'.strip('a')   #양쪽 끝의 문자 a만 제거(중간글자 삭제 불가)
#'bac'

###치환
'abcabc'.replace('ab','AB')

###문자열 분리
'a/b/c/d'.split('/')[0:2]
#['a','b']

###위치값 리턴
b.find('b')
#1

### Q. 전화번호에서 지역번호 추출
tel = '123)456-7890'
n = tel.find(')')
tel[0:n]
tel[:n]
#'123'

###포함횟수
'ahaaajaiea'.count('a')
#6

###형(type)확인
type(b)			#데이터 타입 확인
#str
a.isalpha()		#문자 확인
#True
a.isnumeric()	#숫자 확인
#False

###대소문자 확인
c = 'abCde'
c.isupper()
#False
c.islower()
#False

###문자열 결합
'a' + 'b'
'a' * 3
#'aaa'

###문자열 길이
len(b)
```

---







---

### 03. 조건문과 반복문 ###

1. 조건문(if문)

```python
d = 4
if d > 5:
    print('A')
else:
    print('B')

#리스트는 불가    
e = [1,3,5,7,8]
if e > 5:
    print('A')
else:
    print('B')
#TypeError: '>' not supported between instances of 'list' and 'int'
```



2. 반복문(for, while)

- 객체의 각 원소에 동일한 연산 처리를 진행할 경우
  - for문: 정해진 횟수, 대상이 있을 경우
  - while문: 조건에 따른 반복을 실행하는 경우

(1) for문

```python
f = [1,3,5,15,25]
for i in f:
    if i > 5:
        print('A')
    else:
        print('B')

### 위 리스트에서 각 원소에 10을 더해서 출력
f + 10      		 # 불가(리스트와 int 계산 불가능)


f = for i in f:      # for문의 결과를 바로 변수로 저장하는 것도 불가능
    print(i+10)

    
###그럼 어떻게? 
f2 = []
for i in f:
    f2.append(i+10)  

print(f2)
#[11,13,15,25,35]

f3 = [1,2,3]
f3.append(4)
f3
```



(2) while문

```python
while 조건:
    조건이 참일 때 반복 문장
    
    
###함수의 객체화
g = sum(i for i in range(1,101))
print(g)
    
###반복제어문
#1. continue : 특정 조건일 경우 반복문 스킵
#2. break : 특정 조건일 경우 반복문 종료(정지조건)
#3. exit : 특정 조건일 경우 프로그램 종료
#4. pass : 문법적으로 오류를 발생시키지 않기 위해 자리를 채우는 역할
#          협업할 때 주로 사용(코드 미입력시 잠시 pass해둠)



for i in range(1,11):
    if i == 5:
        continue
    print(i)
#1
#2
#3
#4
#6
#7
#8
#9
#10


for i in range(1,11):
    if i == 5:
        break
    print(i)
#1
#2
#3
#4



###1부터 100까지 누적합이 최초로 2000 이상이 되는 시점의 k값과 총 합을 출력하시오
# 1 + 2 + 3 + ...... + k >= 2000

vsum = 0
for i in range(1,101):
    vsum = vsum + i
    if vsum >= 2000:
        break
print(i,vsum)
#62,2016
```

---







---

### 04.사용자 정의 함수 ###

- input과 output의 관계를 내부에 정의
- def, lambda(축약형)

(1) def 방식

```python
#def 함수이름(인수1, 인수2, 인수3):
#	 함수 본문(for 등)
#    return 반환할 객체


#인수에 default 값(기본값) 선언

#(1)
def f_d(x = 1, y):
    return(x * y)
#SyntaxError: non-default argument follows default argument
#첫번째 인수에 기본값을 정의하면, 뒤에 나오는 인수도 기본값 정의해야 함


#(2)
def f_d(y,x = 1):
    return(x * y)

#에러 안남
#default 값을 갖는 인수를 맨 뒤에 배치하는건 가능

```



(2) lambda 

- 비교적 단순한 연산 및 리턴 시 사용

```python
###사용자 정의 함수 + map

map(func,             #적용할 함수
    interable)        #추가할 인수

f = lambda x: x * 10
h = [2,3,5,2]
map(f,h)
# <map at 0x16b252aa8b0>
#매핑된 값이 저장된 주소

list(map(f,h))
#[20,30,50,20]
```

---







---

### 05. 자료구조(numpy) ###

- numpy: 배열(array) 생성, 연산
  - 배열(array): 하나의 데이터 타입만 허용(int, float, str 등 ), 다차원 자료구조

```python
import numpy as np

###색인
a = np.array([[1,2,3],[4,5,6],[7,8,9]])
a[1,1]  
#5 
a[[1,2],[1,2]] 
#array([5,9]) 
#원하는 값은 [5,6,8,9]

###색인함수 (ix_()) 사용하여 해결
a[np.ix_([1,2],[1,2])]
#array([[5, 6],
#       [8, 9]])


a[:,0] > 5 #첫번째 컬럼 가져와서 5보다 큰 데이터만 출력
a[a2[:,0] > 5]
a[a2[:,0] > 5,:]
# array([[7, 8, 9]])
# 조건의 결과를 행 방향에 색인 값으로 전달(2차원)

a.dtype  #numpy 구성 데이터 타입
a.shape  #numpy 모양(shape) 알려줌 #(3,3)  #3행3열
a.shape[0]  #numpy 행의 수
a.shape[1]  #numpy 열의 수

a.reshape(1,9) #array 모양 변경
a.ndim #number,dimension  #array 차원

###연산
[1,2,3] + [4,5,6]  #list는 서로 원소끼리 연산 불가능, 확장으로 해석 됨
#[1,2,3,4,5,6]

#연산하려면? --> numpy 이용하기

np.array([1,2,3]) + np.array([4,5,6])
#array([5,7,9])
#사이즈 같아야 함

###형(데이터 타입)변환 메서드

a.astype('float')
# array([[1., 2., 3.],
#        [4., 5., 6.],
#        [7., 8., 9.]])   #실수형으로 변환

a.astype('int')
# array([[1, 2, 3],
#        [4, 5, 6],
#        [7, 8, 9]])   #정수형으로 변환

a.astype('str')
# array([['1', '2', '3'],
#        ['4', '5', '6'],
#        ['7', '8', '9']], dtype='<U11')  #문자형으로 변환

###np.where 함수
# if 문의 축약
# np.where(조건, 참인 값 반환, 거짓인 값 반환)

#sql문 기본형태: select * from db where

np.where(a2>5,'A','B')  #참이면 A, 거짓이면 B

###산술 연산 메서드

a.describe()  #오류(배열이기 때문에)--> pandas에서만 가능!
#AttributeError: 'numpy.ndarray' object has no attribute 'describe'


a.sum() #전체합
a.mean() #전체평균
a.var() #전체분산
a.std() #전체표준편차(평균에서 떨어진 정도)
a.min()  #전체 최소값
a.max() #전체 최대값

(a > 5).sum()  #a에서 5보다 큰 값의 총합(True=1,False=0)
(a > 5).any()  #True: a2에서 5보다 큰 값이 하나라도 있을 경우 True
(a > 5).all()  #False: a2에서 모두 5보다 클 경우만 True

a.sum(axis = 0)  
#서로 다른 행 원소끼리 더하기
#1행 첫번째+2행 첫번째+3행 첫번째끼리 더하기 #하나의 열처럼 더하는 것(열의 합)
#행=0, 행 기준/ 행 별 총합(서로 다른 행끼리, 세로방향 연산)
#array([12, 15, 18])


a.sum(axis = 1)  
#서로 다른 열 원소끼리 더하기
#1열 첫번째+..+3열 첫번째 #하나의 행처럼 더하기(행의 합)   
#열=1, 열 기준/ 열 별 총합(서로 다른 열끼리, 가로 방향 연산)
#array([ 6, 15, 24])

#[축 번호]
#2차원 : 행(0) 열(1)
#3차원 : 층(0) 행(1) 열(2)

###전치 메서드
# (1) T = 행과 열을 전치
np.arange(1,9)
#array([1, 2, 3, 4, 5, 6, 7, 8])
a = np.arange(1,9).reshape(4,2)
a
# array([[1, 2],
#        [3, 4],
#        [5, 6],
#        [7, 8]])
a.T
# array([[1, 3, 5, 7],
#        [2, 4, 6, 8]])


# (2) swapaxes: 두 축을 전달 받아서 두 축을 서로 전치, 전달 순서는 중요하지x
#axes=축
a.swapaxes(0,1)
a.swapaxes(1,0)

# (3) transpose
# 원본의 차원에 맞는 축번호를 인수에 차례대로 전달, 그리고 전치 전달되는 순서 중요
a

a.transpose(0,1)  #원본 그대로 출력
a.transpose(1,0)  #행과 열이 전치



###외부파일 입출력
# 1) 파일 불러오기
# np.loadtxt(fname,      #파일명
#            dtype,      #데이터타입
#            delimiter,  #구분자(필드 구분 기호)
#            skiprows,   #skip 할 행의 수
#            usecols,    #선택할 컬럼 위치(값)
#            encoding)   #인코딩 옵션

# 2) 파일 내려쓰기
# np.savetxt(fname,      # 파일명
#            X,          # 객체명
#            delimiter,  # 구분자
#            fmt,        # 출력형식(format)
#            header,     # 헤더 출력 여부(file 첫 문자열)
#            encoding)   # 인코딩 옵션

###fmt(포맷) 전달/변경 방식
# %s : 문자열
# %f : float(실수)
# %d : 정수
'%s' % 123
#'123'  --> 문자로 바꿈
'%f' % 123
#'123.000000' --> 실수로 바꿈
'%.2f' % 123
#'123.00' --> 실수형으로 바꾸는데 소수점 둘째자리까지 표현
'%d' % 123
#'123'
'%7d' % 123
#'    123' --> 앞 공백을 8로 줌
```

---







---

### 06. 자료구조(pandas) 1: Series ###

- pandas 메서드: 벡터화 내장(매 원소마다 반복 가능)
- Series
  - 1차원 자료 구조
  - 하나의 데이터타입 허용


```python
#pandas 메서드: 벡터화 내장(매 원소마다 반복 가능)
#Series, DataFrame

# 1) split

from pandas import Series, DataFrame

l1
# ['abc', 'def']
Series(l1)
# 0    abc
# 1    def
# dtype: object

s1 = Series(l1)

l2
#['a/b/c', 'd/e/f']
Series(l2)
# 0    a/b/c
# 1    d/e/f
# dtype: object
s2 = Series(l2)

s2.str.split('/')
# 0    [a, b, c]
# 1    [d, e, f]
# dtype: object

#2) 대소 치환
s1.str.upper()
s1.str.lower()
s1.str.title()  #camel형태 (낙타)


#3) replace
s1.str.replace('a','A')  
# 0    Abc
# 1    def
# dtype: object

s1.str.replace('a','')   
# 0     bc
# 1    def
# dtype: object

#천단위 구분기호 처리
s3 = Series(['1,200','3,000','4,000'])
s3.sum()
#'1,2003,0004,000' 
#문자열 결합으로 인식됨

s3.str.replace(',','').astype('int').sum()


s3 = Series(['1,200','3,000','4,000'])
s3 = s3.str.replace(',','')
sum(list(map(lambda x: int(x),s3)))


#4) startwith, endswith, contains
s1
# 0    abc
# 1    def
# dtype: object

s1.str.startswith('a')

s1[s1.str.startswith('a')]   #s1 각 원소에서 'a'로 시작하는 원소 추출

s1[s1.str.endswith('c')]     #s1 각 원소에서 'c'로 끝나는 원소 추출

s1[s1.str.contains('e')]     #s1 각 원소에서 'e'를 포함하는 원소 추출


#문자열 크기 len()
s1.str.len()
# 0    3
# 1    3
# dtype: int64

#count 포함 개수
Series(['aabbbb','abcdadd']).str.count('a')
# 0    2
# 1    2
# dtype: int64

#제거 함수(공백, 문자)
Series(['     cd     ', '            df      '])
# 0                 cd     
# 1                df      
# dtype: object
Series(['     cd     ', '            df      ']).str.strip()
# 0    cd
# 1    df
# dtype: object

Series(['     cd     ', '            df      ']).str.strip().str.len()
# 0    2
# 1    2
# dtype: int64

s1.str.strip('a') #문자열 제거
# 0     bc
# 1    def
# dtype: object

Series(['aaabaaabcd','abcdaa']).str.strip('a')
# 0    baaabcd     #중간값 삭제 불가--> 해결방법은? -> replace
# 1        bcd
# dtype: object

Series(['aaabaaabcd','abcdaa']).str.replace('a','')
# 0    bbcd
# 1     bcd
# dtype: object
#문자열 제거(중간값 삭제 가능)

#find(위치값 return)
s3 = Series(['abc@def.com','abcde@def.com'])
s3.str.find('@')
# 0    3
# 1    5
# dtype: int64

#이메일 아이디 추출
s3 = Series(['abc@def.com','abcde@def.com'])
s3
a  = s3.str.find('@')
a
s3.str[0:a]
# 0   NaN
# 1   NaN
# dtype: float64   --> 불가능--> a 값이 두개임

#pad : 문자열 삽입
s1.str.pad(5,           #총 자리수
           'Left',      #삽입 방향
           '!')         #삽입 글자

s1.str.pad(5,'left', '!')
# 0    !!abc
# 1    !!def
# dtype: object

s1.str.pad(5,'right', '!')
# 0    abc!!
# 1    def!!
# dtype: object

s1.str.pad()

s5 = Series(["I Love you", "You know"])
s5
s5.str.pad(20,'right','^')
# 0    I Love you^^^^^^^^^^
# 1    You know^^^^^^^^^^^^
# dtype: object

#문자열 결합
s4 = Series(['abc','def','123'])
s4.str.cat()
#'abcdef123'
s4.str.cat(sep='/')
# 'abc/def/123'

s5 = Series([['a','b','c'],['d','e','f']])
s5
# 0    [a, b, c]
# 1    [d, e, f]
# dtype: object

s5.str.join(sep='')  
# 0    abc
# 1    def
# dtype: object

s5.str.join(sep=',') 
# 0    a,b,c
# 1    d,e,f
# dtype: object

```

---







---

### 07. 자료구조(pandas) 2: DataFrame

- DataFrame
  - 2차원 자료구조(행과 열 구조)

```python
import numpy as np
import pandas as pd
from pandas import Series, DataFrame


#생성
d1 = {'name': ['sinae','bus'], 'sal': [900,1800]}
d1

df1 = DataFrame(d1)
df1
#     name   sal
# 0  sinae   900
# 1   bus  1800

#색인(indexing)  

d3 = DataFrame(np.arange(1,7).reshape(2,3), index = ['a','b'], columns = ['col1','col2','col3'])

#컬럼 선택
d3.col1
# a    1
# b    4
# Name: col1, dtype: int32

d3['col1']
# a    1
# b    4
# Name: col1, dtype: int32

# iloc, loc 
#iloc : positional indexing
#loc : label indexing
d3
d3.iloc[:,0]  #행은 전부, 열은 인덱스0만
# a    1
# b    4
# Name: col1, dtype: int32

d3.iloc[:,0:3]  #행은 전부, 열은 0~2인덱스
#    col1  col2  col3
# a     1     2     3
# b     4     5     6

d3.iloc[:,[0,2]]
#    col1  col3
# a     1     3
# b     4     6

d3.iloc[:,[0,-1]]
#    col1  col3
# a     1     3
# b     4     6

d3.loc[:,['col1','col3']]
#    col1  col3
# a     1     3
# b     4     6

#조건색인 처리
d3.loc[d3.col1 == 1, :]  #컬럼 1인거, 열은 전부
#   col1  col2  col3
# a     1     2     3

#기본 메서드
d3.dtypes  #각 컬럼별 데이터 타입 확인
# col1    int32
# col2    int32
# col3    int32
# dtype: object

d3.index
#Index(['a', 'b'], dtype='object')
d3.columns
#Index(['col1', 'col2', 'col3'], dtype='object')
d3.values
# array([[1, 2, 3],
#        [4, 5, 6]])

d3.columns = ['A','B','C']  #컬럼 이름 변경
d3
#    A  B  C
# a  1  2  3
# b  4  5  6

#연산
d3 + 10

d4 = DataFrame({'A': [10,40],'B': [20,30], 'C': [30,60]}, index = ['a','b'])
#     A   B   C
# a  10  20  30
# b  40  30  60

d5 = DataFrame({'A': [10,40],'B': [20,30]}, index = ['a','b'])
#     A   B
# a  10  20
# b  40  30

d3 + d5
#     A   B   C
# a  11  22 NaN
# b  44  35 NaN

d3.add(d5, fill_value = 0)
#     A   B    C
# a  11  22  3.0
# b  44  35  6.0

```

---

