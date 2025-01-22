# CovidMonitor😷
<br>

## Table of Contents

1. [**Project**](#1-project)  
  1.1 [Project Background and Overview](#11-project-background-and-overview)  
  1.2 [Team Members](#team-members-️)  
  1.3 [Stack](#12-stack)  

2. [**Data Overview**](#2-data-overview)  
  2.1 [Table - Covid19SidoInfState](#21-database-structure)  
  2.2 [Data Set](#22-table-covid19sidoinfstate)  
  2.3 [Data Flow](#23-data-set)  
  2.4 [Data Source](#24-data-flow)
  2.5 [Data Source](#25-data-source)

3. [**Data Visualization Using Kibana**](#3-data-visualization-using-kibana️)  
  3.1 [Data Valid](#31-data-vaild)  
  3.2 [Kibana Visualize](#32-kibana-visualize)  

4. [**Connection Process**](#4-connection-process)  

5. [**TroubleShooting**](#5-troubleshooting)

6. [**Review**](#5-review)

# 1. Project
<br>

## 1.1. Project Background and Overview

### 🦠 Real-Time Respiratory Disease Tracking System

#### **Project Background**
독감 및 감기 등 호흡기 질환이 유행하고 있는 상황에서, 병원 데이터를 활용하여 **실시간 환자 발생 추이**를 추적할 수 있는 시스템을 구축합니다.

#### **Project Goal**
- 다양한 변수(나이대, 성별, 지역 등)에 따른 **감염 추이**를 한눈에 파악할 수 있습니다.
- **Kibana**를 활용하여 실시간 데이터를 시각화하고, 데이터 값만 변경하여 유행 상황을 쉽게 확인할 수 있습니다.

#### **Expected Outcomes**
이 프로젝트는 병원 데이터를 통해 **정확한 분석**을 제공하고, **유행 예측 및 대응**에 유용한 정보를 제공합니다.

<br>

<p align="center">
  <img src="https://github.com/user-attachments/assets/b807512a-ca97-470e-b8fc-d09ace3449d2" width="600">
</p>

<br>

## Team Members 🖥️

| <img src="https://github.com/kcklkb.png" width="200px"> | <img src="https://github.com/SuGeunJee.png" width="200px"> | <img src="https://github.com/PleaseErwin.png" width="200px"> | <img src="https://github.com/unoYoon.png" width="200px"> |
| :---: | :---: | :---: | :---: |
| [김창규](https://github.com/kcklkb) | [지수근](https://github.com/SuGeunJee) | [서소원](https://github.com/PleaseErwin) | [윤원호](https://github.com/unoYoon) |

<br>



## 1.2. Stack


<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>기술 스택</title>
    <style>
        table {
            width: 60%; /* 테이블 너비 최적화 */
            border-collapse: collapse;
            margin: 20px auto; /* 테이블 가운데 정렬 */
        }
        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #000000; /* 기본 배경색 추가 */
            color: white; /* 글씨 색상을 흰색으로 설정 */
        }
    </style>
</head>
<body>
    <table>
        <tr>
            <th>Category</th>
            <th>Technology</th>
        </tr>
        <tr>
            <td>Analytics Engine</td>
            <td><img src="https://img.shields.io/badge/Elasticsearch-52B54B?style=for-the-badge&logo=Elasticsearch&logoColor=white" alt="Elasticsearch"></td>
        </tr>
        <tr>
            <td>Database</td>
            <td><img src="https://img.shields.io/badge/Mysql-4479A1?style=for-the-badge&logo=Mysql&logoColor=white" alt="Mysql"></td>
        </tr>
        <tr>
            <td>OS</td>
            <td><img src="https://img.shields.io/badge/ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white" alt="Ubuntu"></td>
        </tr>
        <tr>
            <td>IDE</td>
            <td><img src="https://img.shields.io/badge/dbeaver-382923?style=for-the-badge&logo=dbeaver&logoColor=white" alt="DBeaver"></td>
        </tr>
        <tr>
            <td>Data Ingestion Tool</td>
            <td><img src="https://img.shields.io/badge/logstash-005571?style=for-the-badge&logo=logstash&logoColor=white" alt="Logstash"></td>
        </tr>
    </table>
</body>
</html>



# 2. Data Overview📰

<br>

## 2.1. Database Structure

### DataBase Connection Information
- **Host**: 192.168.0.114
- **Port**: 3306
- **Username**: covid
- **Database**: COVID

## 2.2. Table [Covid19SidoInfState]
<br>


![테이블](https://github.com/user-attachments/assets/8e60333f-a85b-46bd-b080-43b77eba7215)


<br>
<br>

## 2.3 Data Set
| 번호 | 변수명       | 설명                                                                 | 예시                  |
|------|--------------|----------------------------------------------------------------------|-----------------------|
| 1    | seq          | 각 데이터 항목의 고유 식별자.                                         | 23893                 |
| 2    | stdDay       | 데이터가 수집된 기준 날짜 또는 시간.                                | 2023년 04월 20일 00시 |
| 3    | gubun        | 데이터가 속한 지역 또는 범주를 구분하는 명칭.                       | 합계 (전체 지역을 포함한 총합) |
| 4    | gubunCn      | `gubun`의 중국어 표기.                                               | 首尔                   |
| 5    | gubunEn      | `gubun`의 영어 표기.                                                 | Seoul               |
| 6    | deathCnt     | COVID-19로 인한 누적 사망자 수.                                     | 34401                 |
| 7    | incDec       | 하루 동안 발생한 신규 확진자 수의 증감.                             | 14094                 |
| 8    | isolClearCnt | 격리에서 해제된 사람 수.                                            | 0                     |
| 9    | qurRate      | 검사 대비 확진자 비율. 특정 기간 동안 시행된 검사 수 대비 확진자 수의 비율을 나타냄. | 60343                 |
| 10   | defCnt       | 전체 확진자 수.                                                     | 31039863              |
| 11   | isolIngCnt   | 현재 격리 중인 사람 수.                                             | 0                     |
| 12   | overFlowCnt  | 오버플로우 수, 데이터 오류나 예외를 나타낼 때 사용되는 값.            | 22                    |
| 13   | localOccCnt  | 특정 지역에서 발생한 확진자 수.                                     | 14072                 |
| 14   | createDt     | 데이터가 DB에 생성된 날짜와 시간.                                        | 2023-04-20 04:32:41.0 |
| 15   | updateDt     | 데이터가 마지막으로 수정된 날짜와 시간.                             | 2023-04-20 04:32:41.0  |
| 16   | timestamp    | 데이터가 DB에 생성된 날짜와 시간.                             | 2023-04-20 04:32:41.0  |

<br>

## 2.4 Data Flow
<br>

- MySQL에서 Logstash를 거쳐 Elasticsearch로 데이터가 흐르는 과정

![MySQL ↔ Logstash_ JDBC Driver 활용 및 Elasticsearch 프로세스 과정 - visual selection](https://github.com/user-attachments/assets/5e35298d-3fb9-429c-94bf-f310148a4514)

## 2.5 Data Source

## Data Source

The data used in this project is sourced from **[KDX](https://kdx.kr/data/view/25918)**, a platform providing public data related to COVID-19 statistics.
<br>
<br>
<br>

# 3. Data Visualization Using Kibana👁️

## 3.1 Data Vaild

<br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/77fb4b43-2032-497c-ba39-77e63cfbf0e9" width="70%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/f917c8a3-0703-44d6-8045-d887d628f810" width="70%">
</p>


```sql
SELECT SUM(incDec) 
FROM Covid19SidoInfState 
WHERE gubun = '강원';

-> MySQL을 통한 지역 '강원' 확진자 수 검증 
```

## 3.2 Kibana Visualize

<div align="center">

  <br>
  <img src="https://github.com/user-attachments/assets/f18c2ff5-2f84-4142-9b22-5d72783bd5f6" alt="전체 확진자 수">
  <br>
  <strong>전체 확진자 수</strong>
  <br><br><br>

  <img src="https://github.com/user-attachments/assets/477ef09e-d1a5-4aa1-8c65-23c5cffdfc24" alt="지역별 사망자 수">
  <br>
  <strong>지역별 확진자 수</strong>
  <br><br><br>

  <img src="https://github.com/user-attachments/assets/e574b5e4-7c74-43c2-88b5-60355cf8d853" alt="월별 확진자 수">
  <br>
  <strong>월별 확진자 수</strong>
  <br>
</div>

<br>

<br>


# 4. Connection Process
**`covid.conf`**

```
input {
  jdbc {
    jdbc_validate_connection => true
    jdbc_driver_class => "com.mysql.cj.jdbc.Driver"
    jdbc_driver_library => "C:\02.devEnv\ELK\logstash-7.11.1\logstash-core\lib\jars\mysql-connector-j-8.2.0.jar"
    jdbc_connection_string => "jdbc:mysql://192.168.0.114/COVID"
    jdbc_user => "covid"
    jdbc_password => "covid"
    
    # false 타임스탬프 사용 / true 숫자 사용
    use_column_value => false

    # 마지막 처리 상태 저장
    record_last_run => true

    # 새로 추가되는 데이터를 구분하기 위해 트래킹할 컬럼 지정
    tracking_column => timestamp

    tracking_column_type => "timestamp"

    # 마지막 컬럼값 기록 여부
    clean_run => false

    last_run_metadata_path => "C:\02.devEnv\ELK\logstash-7.11.1\inspector-index.dat"

    #sql_last_value는 마지막 레코드 중 설정된 필드값
    statement => "SELECT seq,stdDay,gubun,gubunCn,gubunEn,deathCnt,incDec,isolClearCnt,qurRate,defCnt,isolIngCnt,overFlowCnt,localOccCnt,createDt,updateDt 
                  FROM Covid19SidoInfState 
                  WHERE timestamp > DATE_ADD(:sql_last_value, INTERVAL 9 HOUR)"
    schedule => "*/1 * * * *"
  }
}
filter {
  # 데이터를 직접 추가하여 필드 값을 설정
  mutate {
    remove_field => ["ecs", "host", "@version", "agent", "log", "tags", "input", "message"]
  }
  # null 값 처리 및 기본값 설정
  mutate {
    gsub => [
      "stdDay", "", "기본값", # null값을 "기본값"으로 설정
      "gubunEn", "", "기본값"
    ]
  }
  
  # 데이터 파싱 지원
  grok {
    match => { "stdDay" => "(?<year>\d{4})년 (?<month>\d{2})월" }
  }
  mutate {
    add_field => { 
      "stdYearMonth" => "%{year}-%{month}"
      "stdYear" => "%{year}년"
    }
    remove_field => ["year", "month"]  # 임시 필드 제거
  }

  date {
    match => ["createDt", "yyyy년 MM월 dd일 HH시"]
    timezone => "Asia/Seoul"
    locale => "ko"
    target => "createDt"
  }

  date {
    match => ["updateDt", "yyyy년 MM월 dd일 HH시"]
    timezone => "Asia/Seoul"
    locale => "ko"
    target => "updateDt"
  }

  # 숫자 타입으로 변환
  mutate {
    convert => {
      "seq" => "integer"
      "deathCnt" => "integer"
      "incDec" => "integer"
      "isolClearCnt" => "integer"
      "defCnt" => "integer"
      "isolIngCnt" => "integer"
      "overFlowCnt" => "integer"
      "localOccCnt" => "integer"
    }
  }
}

output {
  stdout {
    codec => rubydebug  # 콘솔에 출력하여 결과 확인
  }
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "covid28"
  }
}
```
**CSV → MySQL (database) → JDBC driver (for Logstash) → Logstash (data transfer) → Elasticsearch (data storage) → Kibana (data visualization)**
<br>

![image](https://github.com/user-attachments/assets/e6088f82-2cb7-4759-8cc2-199f84f3a845)

**ElasticSearch & logstash를 통한 data 값 확인**
<br>


# 5. TroubleShooting💥
<br>

### 이슈 1. Logstash add_field 문제 해결 트러블슈팅

```
     add_field => { # seq,stdDay,gubun,gubunCn,gubunEn,deathCnt,incDec,isolClearCnt,qurRate,defCnt,isolIngCnt,overFlowCnt,localOccCnt,createDt,updateDt
      "seq" => "%{[message][0]}"
      "stdDay" => "%{[message][1]}"
      "gubun" => "%{[message][2]}"
      "gubunCn" => "%{[message][3]}"
      "gubunEn" => "%{[message][4]}"
      "deathCnt" => "%{[message][5]}"
      "incDec" => "%{[message][6]}"
      "isolClearCnt" => "%{[message][7]}"
      "qurRate" => "%{[message][8]}"
      "defCnt" => "%{[message][9]}"
      "isolIngCnt" => "%{[message][10]}"
      "overFlowCnt" => "%{[message][11]}"
      "localOccCnt" => "%{[message][12]}"
      "createDt" => "%{[message][13]}"
      "updateDt" => "%{[message][14]}"
    }
```
**문제 상황**

- Logstash에서 add_field를 사용해 message 필드 데이터를 추출하려 했으나, Elasticsearch(ES)에 실제 값이 아닌 "%{[message][14]}" 같은 문자열이 저장됨.

**원인 분석**

1. 필드 참조 방식 오류

   - "%{[message][0]}" 같은 표현은 동적 변수 참조 방식이지만, message가 제대로 파싱되지 않으면 문자열 그대로 저장됨.
2. message 필드 구조화 문제

    - message가 단순 문자열이면 [message][0], [message][1]처럼 배열 인덱스로 접근할 수 없음.
mutate 또는 csv 플러그인으로 먼저 분리해야 함.

3. 데이터 파싱 실패

    - message가 분리되지 않아 add_field가 값을 제대로 참조하지 못함.

**해결 방법**
- add_field를 제거하여 잘못된 데이터 저장 방지.
- csv 또는 split 필터로 message를 개별 필드로 변환한 후 올바른 필드 매핑 적용.

<br>

***
### 이슈 2. ES시간 UTC기준으로 시간 비교 불가 트러블슈팅


![캡처2](https://github.com/user-attachments/assets/fa8c29a0-9aa7-4976-aa6b-92f2b1f447c1)



**문제 상황**

- 마지막으로 ElasticSearch에 입력된 시간과 db에 신규로 입력된 시간을 비교하여 신규데이터들만 들어갈 수 있도록 스케줄링하려고 하였으나 비교가 불가.


**원인 분석**

- ElasticSearch 서버 시간은 UTC기준으로 신규 입력된 데이터는 한국시간이라 상이함.


**해결 방법**

- statement 내 select 시 서버시간 + 9시간하여 한국시간과 맞춰 시간 비교가 가능하도록 변경했습니다.
<br><br>
***

### 이슈 3. Kibana 시각화 트러블슈팅

**문제상황**

- 날짜별 확진자 그래프를 시각화하기 위하여 Kibana Horizontal axis에 stdday를 입력하였으나, 대부분이 Other로 표시되어 시각화에 이용할 수 없음.

![Image](https://github.com/user-attachments/assets/a1126ccd-d51d-4f94-bb88-576ed6681e7e)

**원인 분석**
- Kibana에서는 100개의 행만 지원하기 때문에 92%가 Other로 분류됨.
- stdday 데이터가 연/월/일/시 통째로 keyword로 인식됨.

**해결 방안**
- stdYearMonth / stdYear 필드를 가공해서 시각화에 사용함

![Image](https://github.com/user-attachments/assets/3daae49d-6f24-49d4-b2ae-c33f5dd0e917)
<br>


# 6. Review


### 💡 김창규


이번 프로젝트로 JDBC를 사용하여 MySQL과 Logstash, Elasticsearch 간의 연결을 설정하고 데이터를 입력 및 시각화하는 경험을 쌓을 수 있었습니다. 필터링과 시각화까지 포함된 전체적인 흐름을 구현하면서, 데이터 파이프라인을 구성하는 데 있어 중요한 기술적 요소들을 배울 수 있는 좋은 기회였습니다. 프로젝트를 진행하면서, 실시간 데이터의 수정과 삭제까지 포함하는 고도화가 필요하다는 점을 느꼈으며, 실시간으로 변동되는 데이터를 반영하고 싶다고 느꼈습니다.

### 💡 서소원

mysql에서 logstash를 거쳐 ElasticSearch까지 이어지는 파이프라인 구축 과정을 경험할 수 있었다. 도구 실행 방법과 같은 기초만 아는 상태였는데 막상 부딪히면서 공부하니 많은 것을 배운 것 같다. Kibana에서 시각화의 자유도를 높이기 위해서는 데이터의 전처리가 중요함을 느꼈고, logstash의 필터링과 스케줄 등의 편리함을 체감하니 이래서 데이터 자동화 작업을 하는구나 싶었다.

### 💡 윤원호

이번 프로젝트를 통해 MySQL 데이터를 Logstash를 사용하여 Elasticsearch에 매핑하고 저장하는 과정을 진행했습니다. 
특히, 필터를 통해 대용량 데이터를 처리하는 방법을 사용하였습니다.
이후 MySQL 명령어를 통해 데이터를 삭제하는 부분에서 어려움이 있었지만, 
실시간 API 데이터를 받아와 CRUD 작업을 처리할 수 있도록 하는 것이 최종 목표입니다.

### 💡 지수근
이번 프로젝트를 통해 ELK(Elastic Search, Logstash, Kibana)의 연동 과정을 학습할 수 있었습니다. 이 과정에서 단순히 CSV 파일을 Filebeats로 읽어오지 않고, Logstash의 JDBC driver를 통해 MySQL DB와 연동하는 과정에서 많은 문제가 있었습니다. 가장 큰 어려움은 Logstash에서 MySQL의 데이터를 읽어올 때 UTC 기준으로 시간이 저장되어, KST와 9시간의 Timezone 차이가 발생하는 것이었습니다. 이를 해결하기 위해 SQL 쿼리에서 DATE_ADD 함수를 사용하여 9시간을 보정하는 방법을 적용했습니다. 또한, 1분 주기의 스케줄링으로 실시간 데이터 동기화를 구현하였으나, 매번 전체 데이터가 중복 저장되는 문제가 있었고, 이를 last_run_metadata를 활용하여 마지막 실행 시점 이후의 데이터만 가져오도록 개선할 수 있었습니다. 이러한 과정을 통해 단순히 데이터 연동을 넘어서, 실제 운영 환경에서 발생할 수 있는 시간대 처리, 증분 데이터 동기화와 같은 실질적인 문제들을 고려해서 프로그램을 개발하는 것이 필수적이라고 느꼈습니다.
