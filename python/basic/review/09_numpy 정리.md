# numpy 정리 #



```python
###numpy를 이용하지 않고 시각화하기

import matplotlib.pyplot as plt #모듈 호출

#시각화할 데이터를 담을 빈 리스트 생성
t = []
p2 = []
p3 = []

#for문을 이용해 데이터 담기
for i in range(0,50,2): #2 간격으로 0~49까지의 숫자 반복
    t.append(i/10) 		#반복할 숫자/10 값을 리스트 t에 담기
    p2.append((i/10) ** 2)  #반복할 숫자/10을 제곱한 값을 p2에 담기
    p3.append((i/10) ** 3)  #반복할 숫자/10을 세제곱한 값을 p3에 담기
    
plt.plot(t,t,'r--',t,p2,'bs',t,p3,'g^') #plt.plot(x,y,형식문자열)
plt.show()



###numpy를 이용하여 데이터 시각화하기
import matplotlib.pyplot as plt
import numpy as np
t = np.arange(0.,5.,0.2) #0.2간격으로 0.~5.미만 까지의 실수를 생성
plt.plot(t,t,'r--',t,t**2,'bs',t,t**3,'g^') #위와 동일

#plt.plot() 옵션
#color
#b:파랑 g:초록 r:빨강 c:청록 y:노랑 k:검정 w:흰색 
#marker
#.:점 o:원 v:역삼각형 ^:삼각형 s:네모 +:플러스

plt.show()


#numpy를 이용했을 때 for문을 이용할 때보다 코드가 간결해짐
```









```python
import numpy as np
print(np.sqrt(2)) #2의 제곱근 출력
print(np.pi) #원주율 출력
print(np.sin(0)) #sin
print(np.cos(np.pi)) #cos

a = np.random.rand(5) 
print(a)              #0,1사이 n개의 실수를 5개 반환
					  #random은 서브 라이브러리
    			      #randint는 정수 반환
print(type(a))        #numpy.ndarray

-------------------------------------------------

print(np.random.choice(6,10))  #5까지의 숫자를 10개 랜덤 선택(중복O)
print(np.random.choice(10,6,replace = False)) #9까지의 숫자 6개 랜덤 선택(중복X)  ******
print(np.random.choice(6,10,p=[0.1,0.2,0.3,0.1,0.2,0.1])) #확률을 설정하는 p속성, 합은 1이 되어야 한다
      
```





```python
###for문을 이용한 버블차트

import matplotlib.pyplot as plt
import random

x = []
y = []
size = []   #시각화를 위한 3개의 빈 리스트 생성

for i in range(200): #0~200미만
    x.append(random.randint(10,100)) #x에 10과 100사이의 정수 랜덤추출 
    y.append(random.randint(10,100)) #y에 10과 100사이의 정수 랜덤추출
    size.append(random.randint(10,100)) #size=산점도의 버블 크기
    
plt.scatter(x,y,s=size,c=x,cmap='jet',alpha=0.7) 
#cmap='jet' : color map 중 낮은 부분인 파랑, 높은 부분인 빨강까지의 범위를 의미
#alpha=투명도
plt.colorbar() #컬러바도 함께 출력됨
plt.show()


###numpy를 이용한 버블차트

import matplotlib.pyplot as plt
import numpy as np

x = np.random.randint(10,100,200) #10에서 100까지의 정수 200개 랜덤 추출
y = np.random.randint(10,100,200)
size = np.random.rand(len(x))*100 #x의 크기만큼의 실수를 만들고 100을 곱한 값을 size로 지정

plt.scatter(x,y,s=size,c=x,cmap='jet',alpha=0.7)
plt.colorbar()
plt.show()

#반복횟수의 감소로 실행속도는 증가
```



```python
###numpy 기능

import numpy as np
a = np.array([1,2,3,4])
print(a)
#[1 2 3 4]  #리스트와 비슷하지만 원소를 구분하는 ','이 없음

print(a[1],a[-1])
# 2 4    
print(a[1:])
#[2,3,4]  #리스트와 마찬가지로 인덱싱&슬라이싱 가능

a = np.array([1,2,'3',4])
print(a) 
#['1','2','3','4']  #array에는 한가지 타입만 저장 가능, 따라서 모두 string으로 바뀜

a = np.zeros(10)
print(a)
#[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]  #모두 0으로 이루어진 크기 10의 배열 생성
a = np.ones(10)
print(a)
#[1. 1. 1. 1. 1. 1. 1. 1. 1. 1.] #모두 1로 이루어진 크기 10의 배열 생성

#a = np.twos(10)은 안됨, 다른 숫자 배열은 만들 수 없을까?
a = np.zeros(10) + 2
print(a)
#[2. 2. 2. 2. 2. 2. 2. 2. 2. 2.]

a = np.zeros(10) + 5 
print(a)
#[5. 5. 5. 5. 5. 5. 5. 5. 5. 5.] #가능!


a = np.eye(3)
print(a)
#[[1. 0. 0.]
#[0. 1. 0.]
#[0. 0. 1.]]     #3X3의 단위 배열 생성 (항등 행렬)

###0과 1이 아닌 연속된 숫자로 데이터를 생성
print(np.arange(3)) #0부터 3미만의 정수까지의 배열
#[0 1 2]

print(np.arange(3, 7))  #3에서 6까지의 정수배열
#[3 4 5 6]

print(np.arange(3,7,2))  #3에서 6까지의 간격 2인 배열
#[3,5]

a = np.arange(1,2,0.1)  #1이상 2미만의 간격 0.1인 실수 배열
print(a)
#[1.  1.1 1.2 1.3 1.4 1.5 1.6 1.7 1.8 1.9]

b = np.linspace(1,2,11) #1부터 2까지 11개의 구간으로 나누어진 실수 배열 *****
print(b)
#[1.  1.1 1.2 1.3 1.4 1.5 1.6 1.7 1.8 1.9 2. ]

##a는 간격을 지정, b는 특정 개수의 구간을 지정

a = np.arange(-np.pi,np.pi,np.pi/10)
print(a)

b = np.linspace(-np.pi,np.pi,20)
print(b)

#마찬가지

a = np.linspace(1,2,11) #1부터 2까지 11개의 구간으로 나누어진 실수 배열
print(np.sqrt(a)) #1의 제곱근 ~ 2의 제곱근의 값을 11개의 구간에 나누어 배열

##배열에 연산 or 함수를 적용하면 배열의 모든 값이 한번에 계산된다
##따라서 대량의 데이터에 대한 작업이 용이해진다

```



```python
import matplotlib.pyplot as plt
import numpy as np
a = np.arange(-np.pi, np.pi, np.pi/100)
plt.plot(a, np.sin(a)) # 특정 구간의 sin()함수의 모습을 쉽게 시각화
plt.show()

plt.plot(a, np.cos(a))
plt.plot(a+np.pi/2, np.sin(a)) #함수의 평행이동도 구현 가능
plt.show()
```



```python
#mask = 어떤 조건에 부합하는 데이터만 선별적으로 저장하는 기능

a = np.arange(-5,5)
print(a)
#[-5 -4 -3 -2 -1  0  1  2  3  4]
print(a<0) #배열 전체에 조건을 적용
#[ True  True  True  True  True False False False False False]
print(a[a<0]) #다시 배열에 적용 시 조건에 부합하는 데이터만 출력
#[-5 -4 -3 -2 -1]

#mask를 변수에 넣어서 사용 가능
mask1 = abs(a) > 3 #a에서 절댓값이 3보다 큰 원소를 mask1에 저장
print(a[mask1]) #[-5 -4  4]

#여러 마스크를 연결해 사용 가능
mask1 = abs(a) > 3
mask2 = abs(a) % 2 == 0 #a에서 절댓값이 짝수인 원소
print(a[mask1+mask2]) #두 조건 중 하나라도 해당하는 원소
print(a[mask1*mask2]) #두 조건 모두에 해당하는 원소

x = np.random.randint(-100, 100, 1000) # 1000개의 랜덤값 추출
y = np.random.randint(-100, 100, 1000)

mask1 = abs(x) > 50   #절대값이 50보다 큰 값
mask2 = abs(y) > 50

x=x[mask1+mask2]
y=y[mask1+mask2]    #mask 1, 2 중 하나라도 만족하는 값 저장


size = np.random.rand(len(x)) * 100 
plt.scatter(x, y, s=size, c=x, cmap='jet', alpha=0.7)
plt.colorbar()
plt.show()
```

