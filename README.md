# <img src="https://github.com/user-attachments/assets/1bab35d6-043c-4223-84da-bd03b03c26c8" alt="TicketMoa Logo" style="vertical-align: middle; width: 250px; height: auto;">  
## 공연 티켓 통합 사이트 
![image](https://github.com/user-attachments/assets/b7df3ace-5ff2-4892-a137-03f0e5f49314)

## 🗂️ 프로젝트 소개
### 주제 선정 이유
뮤지컬, 공연, 전시, 행사 등 다양한 플랫폼에 흩어져 있는 티켓 정보를 확인하는 과정이 복잡하고 불편하다는 점을 해결하고자 플랫폼 개발을 시작하게 되었습니다.
<br></br>
### 프로젝트 목적
사용자들이 분산된 티켓 정보를 한곳에서 확인하고 비교할 수 있는 환경을 제공함으로써 다양한 선택지를 쉽게 탐색할 수 있도록 돕고, 티켓 구매 과정을 보다 편리하게 만드는 것을 목표로 합니다.
<br></br>
### 주요 기능
**`사용자`를 위한 기능**
- 카테고리 검색: 뮤지컬/연극, 콘서트, 전시/행사
- 키워드 검색: 공연명, 아티스트명
- 지역/날짜 검색: 지역별, 기간별 검색
- 예매처별 단독 판매 티켓 정보 제공
- 추천: 주말을 위한 공연, 인기 공연, 유사 공연 추천
- 공연별 상세 정보 제공
- 검색 기록 확인 가능

**`관리자`를 위한 기능**
- 검색 기록 확인 가능
- 로그 데이터 기반 시각화 자료 제공
***************

## 📑 목차
- [기술스택](#기술스택)
- [개발기간](#개발기간)
- [시스템아키텍쳐](#시스템-아키텍쳐)
- [Features](#Features)
  
  - [React](#ReacT) 
  - [API](#API)
  - [OCR](#OCR)
  - [ML](#ML)
  - [Crawling](#Crawling)
  - [Airflow](#Airflow)

- [시연영상](#시연-영상)    
- [Contributors](#Contributors)
- [License](#License)
- [문의](#문의)
<br></br>

## ⚙️ 기술스택
### Data
<img src="https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=MongoDB&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Amazon%20S3-569A31?style=flat&logo=Amazon%20S3&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Apache%20Kafka-231F20?style=flat&logo=Apache%20Kafka&logoColor=white"/> <img src="https://img.shields.io/badge/Redis-FF4438?style=flat&logo=Redis&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Numpy-013243?style=flat&logo=numpy&logoColor=F5F7F8"/> <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=F5F7F8"/> <img src="https://img.shields.io/badge/Scikitlearn-F7931E?style=flat&logo=scikitlearn&logoColor=F5F7F8"/> <img src="https://img.shields.io/badge/Beautifulsoup-3776AB?style=flat&logo=Beautifulsoup&logoColor=#090a0a"/>
### Back
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat&logo=FastAPI&logoColor=FFFFFF"/>  <img src="https://img.shields.io/badge/Python-3.11-3776AB?style=flat&logo=Python&logoColor=F5F7F8"/>
### Front
<img src="https://img.shields.io/badge/React-61DAFB?style=flat&logo=React&logoColor=ffffff"/> <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=TypeScript&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=Bootstrap&logoColor=ffffff"/>
### Tools
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=Docker&logoColor=white"/> <img src="https://img.shields.io/badge/Amazon%20EC2-232F3E?style=flat&logo=amazonwebservices&logoColor=ffffff"/> <img src="https://img.shields.io/badge/NGINX-009639?style=flat&logo=NGINX&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Selenium-43B02A?style=flat&logo=selenium&logoColor=F5F7F8"/> <img src="https://img.shields.io/badge/Kakao-FFCD00?style=flat&logo=Kakao&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Google Chrome-4285F4?style=flat&logo=Google Chrome&logoColor=ffffff"/> <img src="https://img.shields.io/badge/GitHub-181717?style=flat&logo=GitHub&logoColor=ffffff"/>
<br></br>
## ⏳ 개발기간
**`2024.11.14 ~ 2024.12.31(48일)`**
<br></br>
## 🏗️ 시스템 아키텍쳐
![image](https://github.com/user-attachments/assets/b00fd4f6-dd14-4aa6-b126-bbe45f18875b)

## 🚀 Features
### React -> [repo 바로가기](https://github.com/Team1-TU-tech/react)
- TicketMoa의 front-end를 담당하는 application
- Nginx를 Load Balancer로 활용하여 가용성을 높임
<br></br>
### API -> [repo 바로가기](https://github.com/Team1-TU-tech/API)
- docker-compose를 활용하여 FastAPI 실행, 공연 정보 제공 
- 사용자가 다양한 공연에 대한 정보를 검색, 조회, 추천할 수 있도록 지원
- 사용자 경험을 향상시키기 위해 실시간 로그 데이터 분석 및 머신러닝 기반 추천 기능 제공
- `Validate`, `Login_log`, `Logout_log`, `KakaoLogin_log`, `KakaoLogout_log`,`Signup_log`, `View_detail_log` , `Search_log` 토픽에 대해 사용자 요청을 로깅
<br></br>
### OCR -> [repo 바로가기](https://github.com/Team1-TU-tech/ocr)
- 이미지에서 텍스트를 추출하는 OCR(Optical Character Recognition) 기능 제공
- `easyocr` 라이브러리를 사용하여 이미지를 처리하고 텍스트 추출
<br></br>
### ML -> [repo 바로가기](https://github.com/Team1-TU-tech/ml)
- 공연 데이터를 기반으로 유사한 공연을 추천하는 알고리즘 구현
- 주로 공연의 설명(description)과 시작일(start_date), 지역(region) 등의 정보를 활용하여 유사한 공연을 찾아 추천
<br></br>
### Crawling -> [repo 바로가기](https://github.com/Team1-TU-tech/crawling)
- Interpark / YES24 / Ticketlink 웹사이트에서 공연 티켓 정보를 크롤링하여, 다양한 공연의 티켓 정보를 수집하고 사용자에게 제공하는 기능을 구현
- 크롤링한 데이터는 특정 형식으로 저장되어, 후속 작업으로 티켓 검색 및 필터링 기능을 제공하거나, 다른 시스템에 연동할 수 있도록 활용
<br></br>
### Airflow -> [repo 바로가기](https://github.com/Team1-TU-tech/airflow)
- 구성: Docker Compose로 Apache Airflow와 Apache Kafka를 구성
- 데이터 수집: 3개 타겟 사이트에서 크롤링한 공연 데이터를 S3에 적재.
- 데이터 전처리: S3 데이터를 전처리하여 MongoDB에 저장.
- 추천 시스템: 유사 공연 추천 결과를 매일 배치 작업으로 생성하여 MongoDB에 저장.
- 중복 데이터 삭제: 매일 배치 작업으로 MongoDB 중복 데이터 삭제.
- 로그 기반 인기 공연 추출: S3 로그 데이터를 읽어와 인기 공연 추출 결과를 매일 배치 작업으로 생성하여 MongoDB에 저장.
***********

## 💻 시연 영상
### 사용자 페이지 - 회원가입, 로그인, 로그아웃
https://github.com/user-attachments/assets/eb0a4095-89a2-4e2f-8d45-c5bd505dd2a2

### 사용자 페이지 - 메인페이지 
https://github.com/user-attachments/assets/40b1c525-562f-43b6-88e3-58f1d7079b85

### 관리자 페이지
https://github.com/user-attachments/assets/f5aff28d-5b63-4b4c-a396-a3f4945cc075

## 🤝 Contributors
  | 역할 | 이름 | 책임 |
  |----|------|------|
  | PM | 김태민 | 프론트 |
  | AC | 정미은 | 데이터 ETL |
  | TL | 함선우 | 데이터 ETL |
  | AA | 오지현 | 백엔드 |

## ⚖️ License
이 애플리케이션은 TU-tech 라이선스에 따라 라이선스가 부과됩니다.
<br></br>
## 📩 문의
질문이나 제안사항이 있으면 언제든지 연락주세요:
- 이메일: TU-tech@tu-tech.com
- Github: `Mingk42`, `hahahellooo`, `hamsunwoo`, `oddsummer56`
