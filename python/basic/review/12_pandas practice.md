# pandas practice

-문제해결을 통한 practice





---

### 문제1

- card.csv데이터의 NUM 컬럼을 인덱스로 생성 후 이를 일자로 간주합니다. 

​	일자별 총 지출 금액을 구한 뒤 '총합'으로 마지막 컬럼에 추가해주세요.  단, 천단위 구분기호는 제거 후 숫자 컬럼으로 변경하세요.



1. 파일을 불러온 뒤 NUM을 인덱스로 지정

```python
import pandas as pd 
pd.read_csv('./data/card.csv', encoding = 'cp949') #파일 불러오기

card = card.set_index('NUM')

#NUM을 인덱스로 지정
        식료품       의복     외식비       책값 온라인소액결제     의료비
NUM                                                  
1    19,400  143,000   8,600   29,000   5,600  19,200
2    22,200  120,400   7,000   26,000   3,300  13,000
3    24,600   88,500   7,500   22,000   7,500  16,600
4    22,300  124,800   7,700   78,000   3,900  28,100
```

 

2. 천단위 구분기호 제거 후 숫자 컬럼으로 변경하기

```python
f1 = lambda x: int(x.replace(',',''))
#lambda 코드 자체만 출력할 경우 함수로 저장만 됨, applymap으로 매핑 필요
#applymap : 2차원 데이터프레임에 함수를 적용하기 위해 사용

card = card.applymap(f1)
print(card)
       식료품      의복    외식비      책값  온라인소액결제    의료비
NUM                                              
1    19400  143000   8600   29000     5600  19200
2    22200  120400   7000   26000     3300  13000
3    24600   88500   7500   22000     7500  16600
4    22300  124800   7700   78000     3900  28100
#천단위구분기호가 제거된 정수임을 확인
```



3. 일자별 총합을 구해 새로운 컬럼 생성하기

```python
card['총합'] = card.sum(axis=1) 
#axis를 1로 지정하여 행 원소들의 총합을 구한 뒤, 이를 '총합'컬럼으로 저장


      식료품      의복    외식비      책값  온라인소액결제    의료비      총합
NUM                                                      
1    19400  143000   8600   29000     5600  19200  224800
2    22200  120400   7000   26000     3300  13000  191900
3    24600   88500   7500   22000     7500  16600  166700

#총합 컬럼이 생성되었음을 확인
```



cf. 특정 컬럼만 천단위구분기호를 없애 정수로 변환하는 방법은?

```python
#####1
f2 = lambda x: int(x.replace(',',''))
card['식료품'].applymap(f2)

#AttributeError: 'Series' object has no attribute 'applymap'
#1차원 데이터 셋에는 applymap 적용이 불가능함

card['식료품'] = card['식료품'].map(f2)
#map은 가능

#---> applymap (x)    map (o)

-------------------------------------------------------------

#####2
card['의복'] = card['의복'].str.replace(',','')

25    253000
26    139300
27    122900
28    134200
29     93800
30    163100
Name: 의복, dtype: object
#','는 치환되었지만 dtype=object

card['의복'] = card['의복'].str.replace(',','').astype('int')


26    139300
27    122900
28    134200
29     93800
30    163100
Name: 의복, dtype: int32
#astype 이용하여 정수로 변경
#astype은 문자열에 사용이 불가능하며, array, Series, DataFrame에만 적용 가능

---------------------------------------------------------------


#####3
card['책값'].replace(',','')

26     33,000
27     26,000
28     21,000
29     30,000
30     30,000
Name: 책값, dtype: object
#replace만 사용할 경우 적용되지 않음
#값 치환 메서드 ---> 정확히 일치하는 값만 변경 또는 삭제함 

ex
card['책값'].replace("30,000",'')

26     33,000
27     26,000
28     21,000
29           
30           
Name: 책값, dtype: object
#'30,000'에 해당하는 29,30 인덱스 값들이 치환되었음을 확인
```

---



---

### 문제2

- 일자별로 각 품목별 지출 비율(%)을 출력하세요
  - 천단위구분기호 제거 후 정수로 변환하였다고 가정

```python
#solution 1: 각 행의 값을 전체 합으로 나누어 하나하나 구하기
card.iloc[0,:]

식료품         19400
의복         143000
외식비          8600
책값          29000
온라인소액결제      5600
의료비         19200
Name: 1, dtype: int64

card.iloc[0,:].sum()        
#224800    #1일의 지출 총합

(card.iloc[0,:] / card.iloc[0,:].sum())*100

식료품         8.629893
의복         63.612100
외식비         3.825623
책값         12.900356
온라인소액결제     2.491103
의료비         8.540925
Name: 1, dtype: float64
        
-------------------------------------------------------------------

#solution 2: apply 메서드를 이용해 각 일자별로 적용
f2 = lambda x: (x/x.sum())*100
card.apply(f2,axis=1)
            식료품         의복        외식비         책값   온라인소액결제        의료비
NUM                                                                 
1     8.629893  63.612100   3.825623  12.900356  2.491103   8.540925
2    11.568525  62.741011   3.647733  13.548723  1.719646   6.774362
3    14.757049  53.089382   4.499100  13.197361  4.499100   9.958008

#한번에 출력 가능
```

- 결과 해석
  - 의복비의 일자별 지출 비율이 전체 구성의 50% 이상으로 압도적으로 높음
  - 의견: 의복비 비중을 줄일 필요성이 있음

---



---

### 문제3 

- 각 품목에 해당하는 구매 포인트를 확인한 후, point 컬럼을 생성하세요.
  - 구매금액 50000원 미만: 구매금액의 1%
  - 구매금액 50000원 이상 100000원 미만: 구매금액의 3%
  - 구매금액 100000원 이상: 구매금액의 5%

```python
#solution 1: for문 + if문

result = []

for i in df1['주문금액']:
    if i < 50000:
        result.append(i * 0.01)
    elif i < 100000:
        result.append(i * 0.02)
    else:
        result.append(i * 0.05)
        
print(result)
#값이 매우 많아 지저분하게 출력됨

print(np.round(result,2))
[6211.6  1687.44  404.78 1046.52 1495.02 1148.92 1746.18  400.47 1799.54
  382.31  354.32 1169.44  421.11 1125.14 1791.66 1189.6  1056.64 1276.16
 1299.8  1146.   1323.56 5535.7  1431.96 1013.   5034.85 1251.76 1338.24
 ...
 #반드시 numpy를 이용해야 배열 전체에 적용됨
 
df1['point'] = np.round(result,2)
df1
 
      회원번호         가입일        첫구매일       최종구매일    주문금액    point
0      20  2015-05-13  2015-06-02  2019-06-18  124232  6211.60
1      20  2015-05-14  2015-06-04  2019-06-18   84372  1687.44
2      13  2015-05-14  2015-05-31  2019-06-18   40478   404.78
 
#point 컬럼이 추가되었음을 확인
```

 

```python
#solution 2: np.where(벡터 연산이 가능한 조건 연산 함수)

# in sql : select * from db_name where 조건절
# np.where(조건, 참일 때의 값 리턴, 거짓일 때의 값 리턴)

#첫번째 조건이 거짓이면 새로운 조건 추가
df1['point'] = np.where(df1['주문금액']<50000,  #조건1
         df1['주문금액']*0.01,   #조건1이 참일 때의 조건
         np.where(df1['주문금액']<100000,  #조건2
                  df1['주문금액']*0.02,    #조건2가 참일 때의 조건
                  df1['주문금액']*0.05))   #조건2가 거짓일 때의 조건

#회원번호별 총 주문금액과 포인트 금액 확인
df1.groupby('회원번호')[['주문금액','point']].sum()

         주문금액     point
회원번호                   
10    2569733  67784.94
11    1258669  26722.91
12    1807532  41064.37
```

---



---

### 문제4

- DataFrame의 특정 컬럼(Y) 값을 서로 다른 숫자로 변경 

```python
df2 = DataFrame({'Y':['a','a','b','b','c','a','a','b'],
           'X1': [1,2,3,4,4,6,3,5],
           'X2': [10,30,43,34,43,43,94,32]})

df2
   Y  X1  X2
0  a   1  10
1  a   2  30
2  b   3  43
3  b   4  34
4  c   4  43
5  a   6  43
6  a   3  94
7  b   5  32

#sol 1: 정수 인덱스를 이용해 하나씩 치환
df2['Y'].replace({'a':0,'b':1,'c':2})
0    0
1    0
2    1
3    1
4    2
5    0
6    0
7    1
Name: Y, dtype: int64

#sol 2: 자동변환함수 이용
from sklearn.preprocessing import LabelEncoder

m_lb = LabelEncoder()
m_lb.fit_transform(df2['Y'])
#array([0,0,1,1,2,0,0,1])


```

---



---

### 문제5

- df2에서 X1이 5 이상일 경우, X1의 평균(최빈값, 중앙값, 최소값)으로 수정

```python
#sol 1
df2['X1'][df2['X1']>=5]
# 5    6
# 7    5
# Name: X1, dtype: int64


#sol2
df2.loc[df2['X1']>=5,'X1']
# 5    6
# 7    5
# Name: X1, dtype: int64


m1 = df2['X1'].mean() #평균
m2 = df2['X1'].median() #중앙값

m3 = df2['X1'].mode()   #최빈값
0    3
1    4
dtype: int64

m4 = df2['X1'].mode()[0] #최빈값 중 가장 첫번째 값(여러개일 경우)
m5 = df2['X1'].min()
m6 = df2['X1'].max()

import statistics as stat
stat.mode(df2['X1']) #여러개의 최빈값 중 하나의 상수만을 리턴
#3.0

df2.loc[df2['X1']>=5, 'X1'] = m3 #최빈값 여러개
  Y   X1  X2
0  a  1.0  10
1  a  2.0  30
2  b  3.0  43
3  b  4.0  34
4  c  4.0  43
5  a  NaN  43
6  a  3.0  94
7  b  NaN  32


df2.loc[df2['X1']>=5, 'X1'] = m4
   Y  X1  X2
0  a   1  10
1  a   2  30
2  b   3  43
3  b   4  34
4  c   4  43
5  a   3  43
6  a   3  94
7  b   3  32
#정상 수정 되었음을 확인
```

---

