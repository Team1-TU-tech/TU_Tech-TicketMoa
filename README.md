# TU_Tech-TicketMoa

## 전체 목차


- [기술스택](#기술스택)
- [개발기간](#개발기간)
- [Features](#Features)
  - [API](#API) #######넘버링하기########
  - [OCR](#OCR)
  - [ML](#ML)
  - [SPARK](#SPARK) #####추가하기#####
- [Contributors](#Contributors)
- [License](#License)
- [문의](#문의)
  
<br></br>

## 기술스택
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat&logo=FastAPI&logoColor=FFFFFF"/> <img src="https://img.shields.io/badge/Python-3.11-3776AB?style=flat&logo=Python&logoColor=F5F7F8"/> <img src="https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=MongoDB&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Amazon%20S3-569A31?style=flat&logo=Amazon%20S3&logoColor=ffffff"/> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=Docker&logoColor=white"/> <img src="https://img.shields.io/badge/Apache%20Kafka-231F20?style=flat&logo=Apache%20Kafka&logoColor=white"/> <img src="https://img.shields.io/badge/Numpy-013243?style=flat&logo=numpy&logoColor=F5F7F8"/> <img src="https://img.shields.io/badge/Scikitlearn-F7931E?style=flat&logo=scikitlearn&logoColor=F5F7F8"/>    <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=F5F7F8"/>    
<br></br>

## 개발기간
`2024.11.14 ~ 2025.1.2(50일)`
<br></br>

=======================================================================================
# **Features**
# API
## 개요
- docker-compose를 활용하여 FastAPI 실행, 공연 정보 제공 
- 사용자가 다양한 공연에 대한 정보를 검색, 조회, 추천할 수 있도록 지원
- 사용자 경험을 향상시키기 위해 실시간 로그 데이터 분석 및 머신러닝 기반 추천 기능 제공
<br></br>

## 목차
- [API Features](#API-Features)
- [Logging](#Logging)
- [실행 요구 사항](#실행-요구-사항)
<br></br>

## API Features

![image](https://github.com/user-attachments/assets/ce4fc0a2-a098-4de2-8b38-a8d0eef3fa61)

### search
- 공연 제목, 카테고리, 날짜, 아티스트 이름, 지역으로 공연 정보 검색
- 검색 시 로그 생성 후 Kafka를 통해 S3에 업로드
### detail
- MongoDB에 저장된 공연 정보를 `id` 기준으로 조회
- 조회 시 로그 생성 후 Kafka를 통해 S3에 업로드
### banner
- 현재 날짜를 제외한 가장 가까운 공연 11개를 추출하여 메인 화면 배너에 표시
### popular
- S3에 저장된 로그 데이터를 분석
- 고유 `id`를 기준으로 조회 수를 집계한 뒤, 가장 많이 조회된 공연을 내림차순으로 정렬하여 MongoDB에 저장
- 저장된 데이터 중 인기 순으로 상위 8개의 공연 데이터를 추출
### this_weekend
- 현재 날짜를 기준으로 이번 주 주말(토요일 및 일요일)에 관람할 수 있는 공연 데이터를 추출
### auth
- **JWT 인증 방식**을 기반으로 자체 로그인 및 로그아웃 
  - 로그인: 사용자 정보 검증 후 `Access Token` 과 `Refresh Token` 을 발급
  - 로그아웃: 클라이언트 측에서 토큰 삭제(localStorage 처리) 방식으로 동작. 서버에서는 로그아웃 로그 생성을 위해 토큰 검증을 통해 사용자 ID를 추출
- 로그인/로그아웃 시 로그 생성 후 Kafka를 통해 S3에 업로드
### sign_up
- check-id: 사용자 ID 중복 여부를 MongoDB에서 조회
- signup: 사용자 정보를 검증하고 MongoDB에서 ID 중복 여부를 최종 확인한 뒤, 사용자 정보를 MongoDB에 저장
- 각 과정에서 발생하는 성공 또는 실패와 관련된 로그를 생성하여 Kafka를 통해 S3에 업로드
### kakao
- **카카오 API**를 사용하여 로그인, 로그아웃 및 사용자 정보를 관리
    - 로그인: 카카오 OAuth를 통해 사용자 인증 후 `Access Token`을 발급받고, MongoDB에 사용자 정보를 저장
    - 로그아웃: 카카오 로그아웃 API를 호출하여 사용자 세션을 종료
 - 로그인/로그아웃 시 로그 생성 후 Kafka를 통해 S3에 업로드
### recommendation
- ML 모델을 활용하여 MongoDB에 저장된 전체 데이터의 description을 분석한 후, 각 공연과 유사도가 가장 높은 공연 3개를 추출
- 추출된 데이터는 MongoDB에 저장
- 저장된 데이터에서 고유 `id`에 해당하는 공연과 유사도가 높은 상위 3개의 공연 정보를 함께 반환
### exclusive_main
- 단독 판매되는 공연을 예매처별로 4개씩 추출
### exclusive_all
- 예매처별 단독 판매되는 공연 전체 조회
<br></br>

## Logging
### 로깅 시스템
- 'Validate', 'Login_log', 'Logout_log', 'KakaoLogin_log', 'KakaoLogout_log', 'Signup_log', 'View_detail_log' , 'Search_log' 토픽에 대해 사용자 요청을 로깅
- 사용자가 검색 요청을 하면, 요청 정보를 카프카 프로듀서가 메시지로 큐에 저장
- 메시지에는 사용자 ID, 검색어, 타임스탬프, 디바이스 정보 등의 메타데이터 포함
### 메시지 처리 및 저장
- 카프카 컨슈머는 토픽별로 메시지를 처리
- 메시지는 다음 조건 중 하나를 만족하면 S3에 Parquet 형식으로 저장
  - 메시지가 1시간 동안 누적된 경우
  - 전체 메시지가 1000개 이상 누적된 경우
- 각 토픽별로 독립적으로 데이터를 처리하며, 저장 경로는 logs/{토픽명}/{타임스탬프}.parquet 형식으로 구성
### 장점
1. 효율적인 저장: Parquet 파일 형식을 사용해 저장 공간을 절약하고 분석 속도를 최적화
2. 확장성: 토픽별 배치 처리로 대규모 데이터도 성능 저하 없이 처리 가능
3. 안정성: 업로드 후 버퍼 초기화를 통해 중복 저장을 방지하고 데이터 무결성 유지
<br></br>

## 실행 요구 사항 
```bash
# 도커 빌드
docker compose build

# 도커 백그라운드 실행
docker compose up -d
```
### FastAPI 접속
[localhost:8000](https://localhost:8000)
### Kafka UI 접속
[localhost:8081](https://localhost:8081)
<br></br>

# OCR
## 개요
- 이미지에서 텍스트를 추출하는 OCR(Optical Character Recognition) 기능 제공
- `easyocr` 라이브러리를 사용하여 이미지를 처리하고 텍스트 추출
<br></br>

## 목차
- [기능설명](#기능설명)
- [이미지 전처리](#이미지-전처리)
- [실행 요구 사항](#실행-요구-사항)
<br></br>

## 기능설명
- 이미지를 로드하여 OCR을 사용해 텍스트를 추출
- 다양한 이미지 포맷 지원 (JPEG, PNG, TIFF 등)
- 추출된 텍스트를 파일로 저장하거나 콘솔에 출력
- 텍스트 추출 정확도 개선을 위한 기본 이미지 전처리 기능 제공
- 이미지 전처리 후 MongoDB에 데이터 적재
<br></br>

## 이미지 전처리
OCR의 정확도를 높이기 위해 이미지를 전처리할 수 있습니다. 다음과 같은 전처리 옵션을 사용할 수 있습니다:

- 이미지 크기 조정
- 이미지 분할 (큰 이미지의 경우)

```python
# 이미지 크기 조정
def resize_image(image, max_width=1000):
    width, height = image.size
    if width > max_width:
        new_height = int(max_width * height / width)
        return image.resize((max_width, new_height))
    return image

# 이미지 분할
def split_image(image, height_limit=1000):
    width, height = image.size
    parts = []
    for i in range(0, height, height_limit):
        box = (0, i, width, min(i + height_limit, height))
        parts.append(image.crop(box))
    return parts
```
<br></br>

# ML
## 개요
- 공연 데이터를 기반으로 유사한 공연을 추천하는 알고리즘 구현
- 주로 공연의 설명(description)과 시작일(start_date), 지역(region) 등의 정보를 활용하여 유사한 공연을 찾아 추천
<br></br>

## 목차
- [기능설명](#기능설명)
- [get_top_similar_performances 함수](#get_top_similar_performances-함수)
<br></br>

## 기능설명
- **공연 데이터 분석**: 주어진 공연 데이터에서 중요한 특성(설명, 지역, 날짜 등)을 기반으로 공연을 분석합니다.
- **유사도 계산**: 각 공연 간의 유사도를 계산하여 유사한 공연들을 추천합니다.
- **추천 시스템**: 공연 설명을 벡터화하고, 코사인 유사도를 이용해 유사한 공연들을 추천합니다.
- **지역 및 날짜 필터링**: 유사 공연 추천 시, 지역과 날짜 기준으로 필터링하여 정확도를 높입니다.
<br></br>

## get_top_similar_performances 함수
```python
def get_top_similar_performances(cosine_sim: np.ndarray, performances, top_n=3, threshold=0.98, days_limit=90)
```
- `cosine_sim (np.ndarray)`: 공연 간의 코사인 유사도 행렬입니다. 각 원소는 두 공연 간의 유사도를 나타냅니다.
- `performances`: 공연들의 정보가 포함된 리스트입니다. 각 공연은 딕셔너리 형태로, 최소한 start_date(공연 시작일)와 region(지역) 키를 포함해야 합니다.
- `top_n (int, 기본값=3)`: 각 공연에 대해 추천할 유사한 공연의 수를 제한합니다. 기본값은 3개로 설정되어 있습니다.
- `threshold (float, 기본값=0.98)`: 유사도 임계값입니다. 이 값보다 낮은 유사도를 가진 공연만 추천됩니다. 이유는 1은 자기자신을 의미하며 0.98~0.99 의 경우 지역만 다르고 같은 공연을 나타냅니다.
- `days_limit (int, 기본값=90)`: 기준 공연과 유사한 공연의 종료일이 기준 공연의 시작일로부터 90일 이내인 경우만 추천합니다.
<br></br>
이 알고리즘을 사용하려면 다음과 같은 Python 패키지가 필요합니다:
```bash
pip install numpy pandas scikit-learn gensim konlpy
```
<br></br>

================================================================

## Contributors
`Mingk42`, `hahahellooo`, `hamsunwoo`, `oddsummer56`
<br></br>

## License
이 애플리케이션은 TU-tech 라이선스에 따라 라이선스가 부과됩니다.
<br></br>

## 문의
질문이나 제안사항이 있으면 언제든지 연락주세요:
<br></br>
- 이메일: TU-tech@tu-tech.com
- Github: `Mingk42`, `hahahellooo`, `hamsunwoo`, `oddsummer56`

