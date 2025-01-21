# 제5회 세종특별자치시 빅데이터 분석 아이디어 공모전


<img src="https://github.com/maango97/sejong-bigdata-contest/blob/main/%EC%A0%9C%EC%B6%9C%EB%AC%BC%20%ED%91%9C%EC%A7%80.png" width="600" height="320"/>

- 주제 : **세종시 폭염 저감을 위한 쿨페이브먼트 최적 입지 선정**
- 기간 : 2024.08~2024.09(3인)
- [발표 자료 PDF](https://github.com/maango97/sejong-bigdata-contest/blob/main/%E1%84%8E%E1%85%AC%E1%84%8C%E1%85%A9%E1%86%BC%20%E1%84%8C%E1%85%A6%E1%84%8E%E1%85%AE%E1%86%AF%E1%84%86%E1%85%AE%E1%86%AF.pdf)


## 분석 개요


- **문제 정의**
  - 2050년까지 세종시는 도심지를 중심으로 폭염, 열대야 일수가 크게 증가할 것으로 전망됨
  - 쿨페이브먼트란? 노면 온도를 낮추기 위해 특수 재료를 사용한 포장 기술
  - 쿨페이브먼트의 효과를 극대화하기 위해서는 **보행량이 많은** 골목에 그 입지를 선정하는 것이 중요함
  - 클러스터링을 이용한 최적 입지 선정을 통해 폭염으로 인한 세종시 시민들의 불편을 줄이는 것을 목표로 함

- **데이터 수집과 전처리**
  - 출퇴근 인구 : 동별 종사자 데이터, 동별 상업지역 위치
  - 정류장 이용 인구 : 버스 정류장 별 이용자수 데이터(2024.03~2024.08, 6개월치), 버스 정류장 위치
  - 통학 인구 : 초, 중, 고, 대, 특수 학교 위치, 학생 수 데이터
  - 주거 인구수와 도로 정비 수준에 따라 보행량이 많을 것으로 추정되는 도심과 부도심을 기준으로 데이터 필터링

- **클러스터링**
  - 보행량이 많은 지역이 군집화에서 더 큰 영향을 미치도록 K-Means 클러스터링에 가중치를 부여하여 클러스터링 수행
  - 가중치의 역할 : 데이터 포인트에 적용하여 중요한 지점이 더 많이 반영되도록 함

- **고민의 흔적들**
  - 클러스터링 시 동별 통근 인구가 단일 점으로 집중되어 군집 분석의 왜곡이 발생하는 현상
  
      - 해결 방법 : **동 별 상업지역을 100mx100m 크기의 그리드로 나눠서 계산**(동별 종사자 수를 균일하게 분포시켜 군집의 왜곡 방지)
  
  - 클러스터링을 통해 생성된 54개의 군집 중 최종 후보 입지군 선정 기준
  
      - 해결 방법 : 지름 627m의 원을 생성해 그 원이 커버하는 유동인구수를 고려함. 여기서 **627m는 세종시 동일 노선 내 버스 정류장 간 평균 거리**임. 버스 이용량이 많은 세종시 특성상 **627m 거리 내에서는 사람들이 버스에서 내려 걸어갈 가능성이 높으므로 도보권이라 판단**함


## 환경


- Anaconda-Jupyter Notebook
