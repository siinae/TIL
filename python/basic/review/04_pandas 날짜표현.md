# 파이썬 pandas 날짜표현 #



###  

```python
import pandas as pd
from pandas import Series, DataFrame

#현재 날짜
d1 = datetime.now()

datetime.strptime(d1, '%y/%m/%d')
#datetime.datetime(2021, 12, 30, 8, 4, 844995)
#문자열을 datetime객체로 바꿈, 벡터 연산 불가

##datetime.strftime ==> datetime을 문자열로

s1 = Series(['2022/01/01','2022/01/02','2022/01/03'])
 '''
 0    2022/01/01
1    2022/01/02
2    2022/01/03
dtype: object
'''
#datetime.strptime(s1, '%Y/%m/%d')
#TypeError: strptime() argument 1 must be str, not Series
#Series는 벡터 연산이 불가능하다.


#해결방법 -> map!
s1.map(lambda x: datetime.strptime(x,'%Y/%m/%d'))


#pd.to_datetime ==> 벡터 연산
s1
'''
0    2022/01/01
1    2022/01/02
2    2022/01/03
dtype: object  
'''
s2 = pd.to_datetime(s1)
s2
'''
Out[25]: 
0   2022-01-01
1   2022-01-02
2   2022-01-03
dtype: datetime64[ns]  --> 변함
'''

s2 = pd.to_datatime(s1, infer_datetime_format=True)
#infer_datetime_format=날짜or시간 포맷 추정해서 파싱하기

#날짜 포맷 변경
#datetime.strftime(string, format time)
#날짜 포맷 변경 한 후 return 데이터 타입은 무조건 문자!

datetime.strftime(d1, '%Y')  #연도 리턴 '2021'
a = datetime.strftime(d1, '%y')  #연도 리턴 '21'
type(a)
#str

#날짜 연산
#1) offset 
#일반적으로 동일 오브젝트 안에서 처음부터 주어진 요소나 지점까지의 변위차를 나타내는 정수형

from pandas.tseries.offsets import Day, Hour, Second
d1 + Day(100)
#Timestamp('2022-04-09 20:18:38.309739')

# 2) timedelta :날짜와의 차이
from datetime import timedelta
d1 + timedelta(100)
#datetime.datetime(2022, 4, 9, 20, 18, 38, 309739)

# 3) DateOffset 
d1 + pd.DateOffset(months = 4)
#Timestamp('2022-04-30 20:18:38.309739')

# 5. 날짜 - 날짜
d1 - datetime.strptime(d2, '%Y/%m/%d')
#datetime.timedelta(days=-3, seconds=47517, microseconds=1223)

d3 = d1 - datetime.strptime(d2, '%Y/%m/%d')
d3.days
#-3
d3.seconds
#47517

```

---











