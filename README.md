# CovidMonitor😷
<br>

## Table of Contents

1. [**Project**](#1-project)  
  1.1 [Project Background and Overview](#11-project-background-and-overview)  
  1.2 [Team Members](#team-members-️)  
  1.3 [Stack](#12-stack)  

2. [**Data Overview**](#2-data-overview)  
  2.1 [Table - Covid19SidoInfState](#21-table-covid19sidoinfstate)  
  2.2 [Data Set](#22-data-set)  
  2.3 [Data Flow](#23-data-flow)  
  2.4 [Data Source](#24-data-source)  

3. [**Data Visualization Using Kibana**](#3-data-visualization-using-kibana️)  
  3.1 [Data Valid](#31-data-vaild)  
  3.2 [Kibana Visualize](#32-kibana-visualize)  

4. [**Connection Process**](#4-connection-process)  

5. [**Review**](#5-review)

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
### ✔️ Analytics Engine
<img src="https://img.shields.io/badge/Elasticsearch-52B54B?style=for-the-badge&logo=Elasticsearch&logoColor=white">

### ✔️ DataBase
<img src="https://img.shields.io/badge/Mysql-4479A1?style=for-the-badge&logo=Mysql&logoColor=white">

### ✔️ OS
<img src="https://img.shields.io/badge/ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white">

### ✔️ IDE
<img src="https://img.shields.io/badge/dbeaver-382923?style=for-the-badge&logo=dbeaver&logoColor=white">

### ✔️ Data Ingestion Tool
<img src="https://img.shields.io/badge/logstash-005571?style=for-the-badge&logo=logstash&logoColor=white">

<br>
<br>

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
| 14   | createDt     | 데이터가 생성된 날짜와 시간.                                        | 2023-04-20 04:32:41.0 |
| 15   | updateDt     | 데이터가 마지막으로 수정된 날짜와 시간.                             | null (수정된 시간이 없을 수도 있음) |

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
    #jdbc_connection_string => "jdbc:mysql://127.0.0.1:3306/fisa"
    jdbc_connection_string => "jdbc:mysql://192.168.0.114/COVID"
    jdbc_user => "covid"
    jdbc_password => "covid"
    
    # false 타임스탬프 사용, true 숫자 사용
    use_column_value => false

    record_last_run => true

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
  # 날짜 필드를 Elasticsearch에서 인식할 수 있도록 변환
  
  # 데이터 파싱 지원
  # grok {
  #   match => { "stdDay" => "(?<year>\d{4})년 (?<month>\d{2})월" }
  # }
  # mutate {
  #   add_field => { 
  #     "stdYearMonth" => "%{year}-%{month}"
  #     "stdYear" => "%{year}년"
  #   }
  #   remove_field => ["year", "month"]  # 임시 필드 제거
  # }


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
    # document_id => "%{id}"
    # doc_as_upsert => true
  }
}
```
**CSV → MySQL (database) → JDBC driver (for Logstash) → Logstash (data transfer) → Elasticsearch (data storage) → Kibana (data visualization)**
<br>

![image](https://github.com/user-attachments/assets/e6088f82-2cb7-4759-8cc2-199f84f3a845)

**ElasticSearch & logstash를 통한 data 값 확인**
<br>


# 5. Review

