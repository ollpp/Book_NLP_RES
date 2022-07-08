# Book NLP Recommend Service

</br>
</br>

## 프로젝트 개요
1. 음원, 동영상, 드라마, 영화, 도서 등 다양한 상품군에서 소비자를 향한 추천 서비스가 늘어나고 있다.
2. 사용자 데이터를 수집하여 사용자의 니즈를 보다 정확히 판단하고, User-Item 기반 추천 시스템을 통한 매출 증가를 목표로 서비스 개발 진행
</br>
</br>

## 필요한 데이터셋 소개

  - 모델 학습 및 서비스 구현에 필요한 데이터 : https://drive.google.com/file/d/1Qunmj9LLO_3JfzHsIid4LXzBFwjM4T2f/view?usp=sharing
  - `book_table.csv` : book_data.py 를 통해 책 정보를 크롤링한 초기 데이터셋
  - `book_table_after.csv` : book_table.csv 파일에서 키워드 추출 분석 결과를 추출한 데이터셋
  - `review_table.csv` : reveiw.py 를 통해 리뷰 정보를 크롤링한 초기 데이터셋
  - `review_table_after.csv` : review_table.csv 파일에서 감성 분석을 실시한 결과를 반영한 데이터셋
  - `book_emotion.csv` : book_data.py 를 통해 크롤링 후 키워드추출 및 감정분석 결과를 합친 책 데이터셋
  - `_mat.csv` : 책의 특성들간 코사인 유사도를 구한 후 matrix 형태로 저장한 파일 (추천 알고리즘 RES_final.ipynb 에서 사용)
  - `sentiment_model.h5` : Pre_trained Bert 모델에 크롤링 및 한국어 대화 데이터셋을 Fine_tunning 하여 학습한 모델
  - 한국어 감정 정보가 포함된 단발성 대화 데이터 셋 : https://aihub.or.kr/aihubdata/data/view.do?currMenu=120&topMenu=100&aihubDataSe=extrldata&dataSetSn=270
    
  
</br>
</br>

## 서비스 설명
1. 디렉토리 구조
  - book_res_nlp
    - modeling_note : NLP 및 추천 시스템 구현 파일
      - `NLP_modeling.ipynb` : 키워드 추출/감성 분석 모델링
      - `RES_final.ipynb` : 추천 시스템 알고리즘 모델링
    - static
    - templates
    - `book_data.py` : 책 정보 크롤링 실행 파일
    - 'chrome_confirm.py` : 크롬 버전 확인 파일
    - 'db_controll.py` : Cloud DB 접속 정보
    - `review.py` : 리뷰 정보 크롤링 실행 파일
    - `view.py` : 웹 서비스 실행 파일

</br>

2. 서비스 구현 방식
    1. 웹 서비스
        - 원하는 레포지토리에 다운을 받은 후, 다음 코드를 실행시켜 필요한 패키지들을 다운받는다.
          - `pip freeze > requirements.txt`
        - view.py 파일내 `11~15` 줄의 경로를 사용자에 맞게 파일을 위치시킨 후 설정해준다. 
        - `flask run` 을 통해 웹 서비스를 실행시킨다.
    2. 크롤링 서비스
        - `book_data.py` : 추가 크롤링을 원할 때 사용
        - `review.py` : 추가 크롤링을 원할 때 사용
    3. 모델링
        - `NLP_modeling.ipynb` : Pre_trained Bert model 을 사용하여 키워드 추출, 감성 분석 label 코드 
        - `RES_final.ipynb` : labeling 된 추가 정보를 활용한 5권의 책 추천 알고리즘 코드
        
        </br></br>

## 결론
1. 사회/비즈니스적 예상 활용
    1. 챗봇 시스템을 추가 구현한다면 사용자 접근성을 높일 수 있을것으로 예상
    2. 위 서비스를 사용하는 사용자를 대상으로 광고를 추가하여 추가 수익 가능
2. 추가 방향성/기술적 측면 제언
    1. 충분한 대화 데이터셋을 확보할 수 있다면, 챗봇 시스템으로 모델링을 진행하여 보다 사용자 접근성 높인 서비스 구현
    2. 사용자 DB 정보를 확보할 수 있다면, 성능이 더 좋은 추천시스템을 구현하여 성능을 향상
    
</br></br>

## 참고 자료
- [https://trading-for-chicken.tistory.com/19](https://trading-for-chicken.tistory.com/19) (chromedriver 자동 업데이트)
- [https://velog.io/@shchae04/Python-4Day](https://velog.io/@shchae04/Python-4Day) (크롤링 사용법)
- [https://github.com/ollpp/publicservant_AI](https://github.com/ollpp/publicservant_AI) (Bert 사전학습)
- [https://velog.io/@seolini43/KOBERT로-다중-분류-모델-만들기-파이썬Colab](https://velog.io/@seolini43/KOBERT%EB%A1%9C-%EB%8B%A4%EC%A4%91-%EB%B6%84%EB%A5%98-%EB%AA%A8%EB%8D%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-%ED%8C%8C%EC%9D%B4%EC%8D%ACColab) (감정 분석)