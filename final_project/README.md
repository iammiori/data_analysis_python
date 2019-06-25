# data_analysis_python - final project 

## 1. EPL Market_value Predict

### 1. 문제정의
EPL(English Premier League) 이적시장 기간에 맞춰,  ‘A’ 축구구단은 구단 재산에 맞는 선수를 영 입하기 위해, 미리 시장가치를 예측해 보기로 하였다.  

### 2. 데이터 확보
* 사용 데이터 셋
  - [EPLdata_final](https://www.kaggle.com/mauryashubham/english-premier-league-players-dataset/downloads/english-premier-league-players-dataset-201718.zip/1)

### 3. 데이터 전처리
- club feature 과 nationality 는 big_club( bigclub : 1 / other : 0 ) 과 region (국가별로  수 부여) 으로 대체할 수 있기 때문에 drop 함
- fpl sel : string 형식이기 때문에, %를 0.01 로 계산해줘서, float형으로 변환
- position 도 string 이기 때문에, dummy variable 로 만들어주기위해, pd.get_dummies (pd = pandas) 사용
- NaN 값 확인 , 처리 (국적 feature 하나 비어있어서, 선수의 국적을 찾은다음 넣어줌)

### 4. 알고리즘 적용
- target variable : market_value
- input varibale : other feature
- **PCA** 를 통해 normalization 필수

- linear regression
- selection algorithm (정확도 높이기 위해, 변수 더 줄이기)

### 5. 결과 해석 및 시각화

![final_result](https://user-images.githubusercontent.com/46439995/60073761-41e7b380-975c-11e9-9eb8-57ad92a8e6c6.PNG)

![ols result](https://user-images.githubusercontent.com/46439995/60073845-7a878d00-975c-11e9-9965-524604aa2e58.PNG)


![final plot](https://user-images.githubusercontent.com/46439995/60073846-7c515080-975c-11e9-9f37-3cf5ed34cacc.PNG)

--------------------------------------------------------
## 2. 영화 추천 시스템 

### 1. 문제정의
‘B’는 영화 추천 사이트를 만들고자 한다. 처음 사이트를 만드는 거기 때문에, user의 수가 적을 거 같아서, 기존에 있던 데이터를 바탕으로 추천시스템을 만들고자 한다. 따라서, 새로 가입하는 user가 영화 한편이라도 본다면, 그 영화와 상관관계가 높은 영화를 추천해 주는 추천 시스템을 만들 것이다. (마치 넷플리스 처럼) 

### 2. 데이터 확보
* 사용 데이터 셋 (이중 movie, rating table)
  - [movielens-20m-dataset](https://www.kaggle.com/grouplens/movielens-20m-dataset )
  - 두 tabe 을 marge 함

### 3. 데이터 전처리
- 평점 dataset 이라서, 별도의 정규화나, PCA 필요없음

### 4. 알고리즘 적용
- 데이터가 너무 많아, 10000 개로 한정 (아니면, jupyter memory error 뜸)
- collaborative filtering 중 item based 로 Pearson 상관계수 사용


### 5. 결과 해석 및 시각화
![co](https://user-images.githubusercontent.com/46439995/60074444-e0c0df80-975d-11e9-9fe8-cc5588d33460.PNG)

- watched 에 영화 이름만 바꿔주먼, 모든 상관관계를 다 구해, 영화를 5개 까지 추천해줌 (head() 때문에)

-------------------------------------------------------------------------------------------
## 3. 쇼핑몰 고객 clustering

### 1. 문제정의
‘C’ 쇼핑몰 마켓팅 담당자는 여름방학시즌을 맞이하여, 고객에게 맞춤별 할인 쿠폰을 보냄으로써, 쇼핑몰의 판매량을 증가시키려 계획을 했다. 수입에 비해, Spending Score 이 높은 고객에게는 VIP로 생각을 해서, 할인율이 더 높은 쿠폰을 주고, Spending Score이 낮은 고객에게는 흥미를 끌 어, 쇼핑몰로 오게 할 마켓팅을 진행할 예정이다.  

### 2. 데이터 확보
* 사용 데이터 셋
  - [mall customer segmentaion data](https://www.kaggle.com/vjchoudhary7/customer-segmentation-tutorial-in-python)

### 3. 데이터 전처리
- genre (성별) feature 가 categorial 이므로 label encoder 를 써서 male 은 1 , female 으 0으로 바꿔줌
- nan 확인 -> 없었음
- id featrue 삭제
- normalization 필수 (데이터의 범위가 다르므로)

### 4. 알고리즘 적용
- k means 사용  
![kmeans](https://user-images.githubusercontent.com/46439995/60075220-c25be380-975f-11e9-9aeb-c65ce22fc928.PNG)
- 적절한 k를 구하기 위한 elbow method (k=5 가 적절하다 판단)

### 5. 결과 해석 및 시각화
- cluster 별 feature 분석 (histogram)
![cluster별 feature 분석](https://user-images.githubusercontent.com/46439995/60075391-27afd480-9760-11e9-92c5-37354a2fb10d.PNG)

- cluster scatter plot
![최종 plot](https://user-images.githubusercontent.com/46439995/60075452-4f9f3800-9760-11e9-8bfc-0c7cb4ec6e88.PNG)

이 그래프를 통해, 오렌지 색과 골드색, 즉 cluster 3과 cluster 4 에 속하는 고객은 spending score 이 높은 고객 집단이다. 특히 오렌지색의 cluster4는 Income 이 낮음에도 불구하고 spending score가 높은 집단이다. 따라서 두 집단에게는 VIP 전용 할인 쿠폰을 보낸다면, 더욱 쇼핑몰 이용 률이 높아지고 spending score가 더 높아질 거라 기대할 수 있다. 반면 cluster 1 은 income 은 많 으나, spending score이 낮은 집단이다. 이 집단에게는 ‘C’ 쇼핑몰에 오게끔 하는 것도 하나의 홍보 일 수도 있다. 따라서 cluster 1 집단이 관심있는 상품이 있다면, 이를 홍보를 함으로써, 쇼핑몰에 오게끔 해서 구매를 유도할 수 있을 것 같다. 따라서 고객별 관심 상품데이터를 같이 분석해, 마 켓팅에 활용하면, 영업에 도움이 되지 않을까 싶다. 


