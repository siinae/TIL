# 파이썬 중간 정리2 (sort, groupby, merge, concat, api호출)

---

### 01. sort() ###

- pandas 정렬
- sort_index
- Series, DataFrame 호출 가능
- index, column 재배치

```python
import pandas as pd
import numpy as np
from pandas import Series, DataFrame

pd.read_csv('파일경로/파일명.csv')

import os
os.getcwd()  #current working directory

#원하는 피쳐만 가져오기
파일명.피쳐
파일명['피쳐']
--> 요청 결과를 Series로 출력


pd.read_csv('./score.csv')
'''
   no   name  math  eng
0   1  sinae   100   90
1   2  minsu    90   45
2   3  suhee    80   86
3   4   john    60   70
4   5   lena    90   47
5   6    jin   100   80
'''

score = pd.read_csv('./score.csv')
score.name
score['name']
'''
0    sinae
1    minsu
2    suhee
3     john
4     lena
5      jin
Name: name, dtype: object
'''

score.idx = score['no']
score.idx
'''
0    1
1    2
2    3
3    4
4    5
5    6
Name: no, dtype: int64
'''

score.iloc[:,1:]
'''
    name  math  eng
0  sinae   100   90
1  minsu    90   45
2  suhee    80   86
3   john    60   70
4   lena    90   47
5    jin   100   80
'''

score.set_index('name')
'''
       no  math  eng
name                
sinae   1   100   90
minsu   2    90   45
suhee   3    80   86
john    4    60   70
lena    5    90   47
jin     6   100   80
'''

score = score.set_index('name')


score.sort_index(ascending = True)
'''
       no  math  eng
name                
jin     6   100   80
john    4    60   70
lena    5    90   47
minsu   2    90   45
sinae   1   100   90
suhee   3    80   86
'''

score.sort_index(axis = 0)
'''
       no  math  eng
name                
jin     6   100   80
john    4    60   70
lena    5    90   47
minsu   2    90   45
sinae   1   100   90
suhee   3    80   86
'''

score.sort_index(axis = 1)
'''
       no  math  eng
name                
jin     6   100   80
john    4    60   70
lena    5    90   47
minsu   2    90   45
sinae   1   100   90
suhee   3    80   86
'''

score.sort_values(by = 'eng') 
'''
       no  math  eng
name                
minsu   2    90   45
lena    5    90   47
john    4    60   70
jin     6   100   80
suhee   3    80   86
sinae   1   100   90
'''

score.sort_values(by = 'eng', ascending = False)
'''
       no  math  eng
name                
sinae   1   100   90
suhee   3    80   86
jin     6   100   80
john    4    60   70
lena    5    90   47
minsu   2    90   45
'''


score.sort_values(by = ['name','math'])
'''
       no  math  eng
name                
jin     6   100   80
john    4    60   70
lena    5    90   47
minsu   2    90   45
sinae   1   100   90
suhee   3    80   86
'''


score.sort_values(by = ['name','math'],ascending = [True, False])
'''
       no  math  eng
name                
jin     6   100   80
john    4    60   70
lena    5    90   47
minsu   2    90   45
sinae   1   100   90
suhee   3    80   86
'''


```

---







---

### 02. groupby ###

- 그룹연산
- python pandas groupby

```python
a.groupby(by = None,      	   #그룹핑 기준 컬럼
               axis = 0,       #그룹핑 연산 방향
               level: None)    #멀티 인덱스일 경우, 특정 레벨의 값을 기준 컬럼으로 사용

#멀티인덱스
a.groupby(by = ['제품','판매처'])['수량'].sum()
a.groupby(by = ['제품','판매처'])['수량'],agg(['sum','mean'])
#aggregate : 종합한,총
#agg --> 여러 함수를 동시에 전달

a.groupby(by = ['제품','판매처'])['수량'],agg({'제품' :'sum','판매처': 'mean'})
#dict() 사용


a.groupby(level = 0).sum()
#level [0]에 해당하는 '제품'별 총합
```

---







---

### 03. merge   vs  concat

- merge
  - pd.merge(left =, right =, how = , on =)
  - 2개 이상의 DataFrame 객체 DBMS의 join 방식으로 결합
  - 참조 조건 사용
- concat
  - pd.concat(objs=, axis= )
  - 2개 이상의 DataFrame 객체를 결합

```python
import pandas as pd
import numpy as np
from pandas import Series, DataFrame


df1 = DataFrame(np.arange(1,7).reshape(2,3), columns=['A','B','C'])

df2 = DataFrame(np.arange(10,61,10).reshape(2,3), columns=['A','B','C'])


# concat
pd.concat([df1, df2])
'''
    A   B   C         #행의 결합(세로방향으로 합쳐짐) 
0   1   2   3
1   4   5   6
0  10  20  30
1  40  50  60
'''

pd.concat([df1,df2], axis = 0)
'''
    A   B   C         #동일결과
0   1   2   3
1   4   5   6
0  10  20  30
1  40  50  60
'''

pd.concat([df1,df2], axis = 1) 
'''
   A  B  C   A   B   C    #열의 결합
0  1  2  3  10  20  30   
1  4  5  6  40  50  60
'''
pd.concat([df1, df2], ignore_index=True)
#인덱스 무시

'''
    A   B   C         
0   1   2   3
1   4   5   6
2  10  20  30
3  40  50  60
'''


#join
#두 데이터프레임(테이블)의 참조조건 활용, 하나의 객체로 합치거나 데이터를 처리하는 것
# merge 수행

pd.merge(left,              #첫번째 데이터프레임
         right,             #두번째 데이터프레임
         how='inner',       #조인 방법(default = 'inner')
         on=,               #조인 컬럼(컬럼명이 서로 같을 때)
         left_on=           #첫번째 데이터프레임 조인(컬럼명이 서로 다를 때)
         right_on=)         #두번째 데이터프레임 조인(컬럼명이 서로 다를 때)
```

---







---

### 04. api 호출 ###

```python
import pandas as pd
import numpy as np
import requests
from openpyxl.workbook import Workbook
from bs4 import BeautifulSoup           #HTML과 XML 파일로부터 데이터를 뽑아내기 위한 파이썬 라이브러리

apikey = '할당받은 api key'
api = 'api주소'
#for문 이용
i = 0
for i in list_:
    url = api.format(list_, key = apikey)
    req = requests.get(url)
    re = req.text
    soup = BeautifulSoup(re, 'html.parser')
    
.
.
.

    
#웹 스크래핑
from bs4 import BeautifulSoup as bs
from pprint import pprint
import requests

html = requests.get("https://주소")    
print(html)

print(html.text)
soup = bs(html.text, 'html.parser')
print(soup)
.
.
.
```

---

