# 차원 축소(주성분분석(PCA),다차원척도법(MDS)) #

---

### 01. 차원축소

- 분석의 대상이 되는 여러 변수의 정보를 최대한 유지하면서, 변수의 개수는 줄이는 탐색적 분석기법

- 하나의 완결된 분석기법으로 사용되기보다는 다른 분석과정을 위한 전 단계, 분석 수행 후 개선 방법, 또는 효과적인 시각화 목적으로 사용

- 저차원으로 학습할 경우, 회귀/분류/클러스터링 등의 머신러닝 알고리즘이 더 잘 작동함

---



---

### 02. PCA (주성분 분석) ###

- principal component analysis

- 측정된 변수들의 선형 조합(Linear Combination)에 의해 대표적인 주성분을 만들어 차원(Dimension)을 줄이는 방법



```python
1. data loading

from sklearn.datasets import load_iris #iris데이터 호출
iris_x = load_iris()['data']
iris_y = load_iris()['target']

iris_x #변수가 4개인 4차원
iris_y

2. 2차원 축소
from sklearn.preprocessing import StandardScaler as standard
m_sc = standard()  #standard scailing
m_sc.fit_transform(iris_x)  
iris_x_sc = m_sc.fit_transform(iris_x) #PCA적용 전 스케일링 변환

3. 주성분 갯수 설정 축소 작업
from sklearn.decomposition import PCA #decomposition:분해
m_pca2 = PCA(n_components) #주성분 개수 2개로 설정
iris_x_pca2 = m_pca2.fit_transform(iris_x_sc) #2차원으로 축소

4. 유도된 인공변수로 시각화
import mglearn

mglearn.discrete_scatter(iris_x_pca2[:,0],iris_x_pca2[:,1])
#첫번째, 두번째 컬럼만 선별하여 시각화

5. 3차원으로 축소
from sklearn.decomposition import PCA
m_pca3 = PCA(n_components = 3)
iris_x_pca3 = m_pca3.fit_transform(iris_x_sc)
#같은 과정 반복

from mpl_toolkits.mplot3d import Axes3D, axes3d
import matplotlib.pyplot as plt
#matplotlib의 2D 그래프에 3D 오브젝트를 그리도록 해주는 라이브러리

#도화지 그리기 & 축 그리기
fig1 = plt.figure() #도화지 
ax = Axes3D(fig1) #축

#step 1
#y == 0 인 데이터 포인트만 시각화
ax.scatter(iris_x_pca3[iris_y==0,0], #x 축 좌표
           iris_x_pca3[iris_y==0,1], #y 축 좌표
           iris_x_pca3[iris_y==0,2], #z 축 좌표
           c = 'b',
           cmap = mglearn.cm2,   	 #컬러맵
           s = 60,              	 #점 크기(size)
           edgecolors = 'k')    	 #black


#step 2. y==1 인 데이터 포인트만 시각화
ax.scatter(iris_x_pca3[iris_y==1,0], 
           iris_x_pca3[iris_y==1,1], 
           iris_x_pca3[iris_y==1,2],
           c = 'r',
           cmap = mglearn.cm2,   
           s = 60,              
           edgecolors = 'k')     

#step 3. y==2 인 데이터 포인트만 시각화
ax.scatter(iris_x_pca3[iris_y==2,0], 
           iris_x_pca3[iris_y==2,1], 
           iris_x_pca3[iris_y==2,2],
           c = 'y',
           cmap = mglearn.cm2,   
           s = 60,              
           edgecolors = 'k')     


6. 모델 적용 (KNN_최근접 이웃: 분류모델(지도학습), input data와 가장 거리가 가까운 k개의 관측치를 통해 input data의 Y값 결정)  

from sklearn.neighbors import KNeighborsClassifier as knn

m_knn1 = knn()
m_knn2 = knn()

from sklearn.model_selection import train_test_split

# train_x1, test_x1, train_y1, test_y1 = train_test_split(iris_x_pca2, iris_y)
# train_x2, test_x2, train_y2, test_y2 = train_test_split(iris_x_pca3, iris_y)

train_x1, test_x1, train_y1, test_y1 = train_test_split(iris_x_pca2, iris_y, random_state=0)
train_x2, test_x2, train_y2, test_y2 = train_test_split(iris_x_pca3, iris_y, random_state=0)

# random_state=0
# 초기값 설정 : seed 값 고정, 이 과정이 없을 경우 매번 데이터를 랜덤하게 뽑기 때문에 설명력이 계속 다르게 나옴 

m_knn1.fit(train_x1, train_y1)  #fit은 train data만 #KNeighborsClassifier()

#평가
m_knn1.score(test_x1, test_y1)  #0.8947368421052632

m_pca2.explained_variance_ratio_ #각 인공변수의 분산 설명력
#array([0.72962445, 0.22850762]) #72%, 22% --> 앞 변수가 중요한 변수!
sum(m_pca2.explained_variance_ratio_) #0.9581320720000164
#일반 분산설명력과 차이가 심할 경우 overfitting되었다고 함

m_knn2.fit(train_x2, train_y2)
m_knn2.score(test_x2, test_y2) #0.9736842105263158

m_pca3.explained_variance_ratio_ 
#array([0.72962445, 0.22850762, 0.03668922])
sum(m_pca3.explained_variance_ratio_) #0.9948212908928451
#거의 완벽!
```

---



---

### 03. MDS(다차원척도법) ##

- multidimensional scaling

- 개체들 사이의 유사성, 비유사성을 거리로 측정하여 2차원/3차원 공간상에 점으로 표현하는 기법

  (=상표를 비롯하여 상품이 가지고 있는 속성이나 응답자의 이상점과 같은 자극점들(stimuli)간의 복잡한 다차원 관계를 저차원인 2차원 평면이나 3차원 공간상에 단순한 구도로 시각화하여 나타내주는 기법)

- 개체들 사이의 집단화를 시각적으로 표현하는 분석방법

- 차원 축소과정에서 발생하는 오차(stress) 정의

- stress의 크기로 차원 축소에 대한 적합도 판단

- stress(0: 완벽, 5: 좋음, 10:보통, 20:나쁨)



```python
from sklearn.manifold import MDS #모듈 호출

1. data loading
from sklearn.datasets import load_iris #iris데이터 호출
iris_x=load_iris()['data']
iris_y=load_iris()['target']

2. scailing 정규화
from sklearn.proeprocessing import StandardScaler as standard 
m_sc=standard()
m_sc.fit_transform(iris_x)
iris_x_sc=m_sc.fit_transform(iris_x)
#여기까지 위와 동일

from sklearn.manifold import MDS
m_mds2 = MDS(n_components=2)
m_mds3 = MDS(n_components=3)

3. 데이터 변환
iris_x_mds1 = m_mds2.fit_transform(iris_x_sc)  #2차원으로 축소
iris_x_mds2 = m_mds3.fit_transform(iris_x_sc)  #3차원으로 축소


4. 유도된 인공변수 iris_x_mds1,2 확인

m_mds2.stress_  #235.36462064427394 --> 적합도 평가(.stress_)
m_mds2.embedding_ #변환된 데이터셋 값 #스트레스를 포함하는 데이터셋

#변환된 데이터 셋 값 points 변수에 담기
points = m_mds2.embedding_ 

5. 크루스칼 스트레스 계산

import numpy as np
from sklearn.metrics import euclidean_distances #metrics = 측정하다

DE = euclidean_distances(points) #오차를 포함하고 있는 임베딩값
DA = euclidean_distances(iris_x) #실제 거리

stress = 0.5*np.sum((DE-DA)**2)
stress1 = np.sqrt(stress/(0.5*np.sum(DA**2)))

stress   #3524.3828579930314
stress1  #0.18569671253464554   #적합도가 아주 좋음!

#3차원
m_mds3.stress_ #10.270914531347238
points = m_mds3.embedding_

#크루스칼(Kruskal) 스트레스 계산
import numpy as np
from sklearn.metrics import euclidean_distances

DE = euclidean_distances(points)
DA = euclidean_distances(iris_x)

stress = 0.5*np.sum((DE-DA)**2)
stress #3382.769730219763

stress2 = np.sqrt(stress/(0.5*np.sum(DA**2)))
stress2 #0.18192772682997418

```

---



​		