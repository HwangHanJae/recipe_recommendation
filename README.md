# 재료기반 맞춤 레시피 추천 시스템

## 프로젝트 배경 및 목적
### 배경
<img width=700 src = "https://user-images.githubusercontent.com/60374463/196422065-814aeb5a-ba28-42d7-94dc-16fa262462ef.png">
<!--![image](https://user-images.githubusercontent.com/60374463/196422065-814aeb5a-ba28-42d7-94dc-16fa262462ef.png)-->

- 1인가구의 증가로 혼자 외식을 하는 인원들이 증가하고 있습니다.
- 혼자 식사하는 경우 부적절한 식습관이 발생되기 쉽고 건강상 좋지 않은 결과를 가져오게 됩니다.
- 건강에 대한 관심과 집밥에 대한 수요가 증가했습니다.
- 1인가구의 경우 요리 후에 재료가 남는 문제와 부담도 존재합니다.

### 목적
- 1인가구도 재료를 남기지 않고 경제적이면서 건강한 집밥을 해먹을 수 있도록 합니다.
- 가격, 재료 등 사용자의 조건에 맞춘 레시피 검색 및 추천 서비스 제공합니다.

## 워크플로우
<!--![image](https://user-images.githubusercontent.com/60374463/196422396-ad4e7895-1c09-4e09-96dc-488a87b69590.png)-->
<img width=700 src = "https://user-images.githubusercontent.com/60374463/196422396-ad4e7895-1c09-4e09-96dc-488a87b69590.png">
여기서 DS 파트를 담당했습니다.

## 데이터 출처
- [농식품 빅데이터 거래소] 만개의 레시피
- [크롤링] 만개의 레시피
- [농식품 빅데이터 거래소] 농수축산물 일자별 도소매 가격
## 추천시스템

### 과정
- [코사인 유사도를 구하기 위한 텍스트 전처리 과정](DS/recommendation_system/cosine_similarity_ingredient_preprocessing.ipynb)
- [코사인 유사도를 구하고 데이터 프레임을 만드는 과정](DS/recommendation_system/make_cosine_similarity.ipynb)
1. (CKG_MTRL_CN - 재료 내용)컬럼 대신 레시피 일련번호를 기준으로 크롤링한 데이터를 사용
  - 원본 컬럼(CKG_MTRL_CN)은 텍스트로 되어 있음
  - 구분자를 '|'으로 사용하기 때문에 데이터를 분리하고, 전처리하는 과정이 어렵고 시간이 오래걸릴것이라 판단
  - [크롤링 과정](DS/ingredient_crawling.py)
2. 데이터 수 줄이기
  - 전체 데이터를 사용하여 코사인유사도를 구할 때 Memory Error가 발생하여 데이터 수를 줄여서 진행할 수 있도록 함
3. 양념 부분을 제외한 재료 부분만 추출
4. 공백, 소괄호, 중괄호, 특수문자 등 불필요한 단어 제거
5. 행은 레시피, 열은 재료로 구성된 데이터 프레임 생성
6. 코사인 유사도를 사용하여 추천시스템 구축 및 결과 데이터 프레임 생성
### 결과
<!--![image](https://user-images.githubusercontent.com/60374463/196422584-91dc72a2-59be-4358-9276-89d8286b0389.png)-->
<img width=700 src = "https://user-images.githubusercontent.com/60374463/196422584-91dc72a2-59be-4358-9276-89d8286b0389.png">

Worst Case의 경우 토마토스파게티가 양념 재료 분류가 되어있었는데 양념 부분이 제거되면서 재료가 파스타면만 남는 등 추천시스템을 적용하기 어려운 데이터가 존재합니다.

## 회고
### 아쉬운점
- 실제 사용자 데이터를 구하지 못하여 사용자를 기반으로 추천을 진행하지 못한점
- 추천시스템의 정량적인 평가지표를 사용하지 못한점
- Worst Case와 같은 경우에 대한 처리가 부족한 점

### 배운점

- 코사인 유사도를 이용하여 콘텐츠 기반으로 추천 시스템을 구축한 점
- DE, DA 다른 직군과의 협업을 통하여 서비스에 추천시스템을 적용시킨 점


