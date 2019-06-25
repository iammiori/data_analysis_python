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
  - 두 talbe 을 marge 함

### 3. 데이터 전처리
- 평점 dataset 이라서, 별도의 정규화나, PCA 필요없음

### 4. 알고리즘 적용
- 데이터가 너무 많아, 10000 개로 한정 (아니면, jupyter memory error 뜸)
- collaborative filtering 중 item based 로 Pearson 상관계수 사용


### 5. 결과 해석 및 시각화
![co](https://user-images.githubusercontent.com/46439995/60074444-e0c0df80-975d-11e9-9fe8-cc5588d33460.PNG)

- watched 에 영화 이름만 바꿔주먼, 모든 상관관계를 다 구해, 영화를 5개 까지 추천해줌 (head() 때문에)

-------------------------------------------------------------------------------------------




