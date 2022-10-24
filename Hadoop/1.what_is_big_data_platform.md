## 빅데이터의 정의  
기존의 데이터 처리 응용 소프트웨어로는 수집, 저장, 분석, 처리하기 어려울 정도의 방대한 양의 데이터  
데이터로부터 가치를 추출하고 결과를 분석하는 기술   
<br>

## 플랫폼의 정의
동일한 제품을 일정한 품질로 만드는 프로세스와 그 제품을 만드는 장치   
<br>

## 빅데이터 플랫폼의 정의
기업 내에 많은 사용자들이 데이터를 처리하고 분석을 쉽게 할 수 있는 환경을 제공해주는 시스템
- 빅데이터 플랫폼 요구사항
  1. 데이터 수집, 처리 및 저장
  2. 데이터 발견, 검색, 보안 제공
  3. 데이터 분석 및 ML 지원
<br>

## 빅데이터 아키텍처 개요

### 1. Data Sources
비지니스 데이터와 운용 데이터가 생성되는 단계
  - 데이터베이스
  - 이벤트 컬렉터
  - 로그
  - API
  - 파일
  - 오브젝트 스토리지
  - 기타
<br>


### 2. Data Ingestion and Processing
데이터 소스로부터 데이터를 수집하여 추출하고 변형하고 적재하는 단계

#### 2-1 배치형 데이터 수집(Flume, Scoop, Fluentd)
  - 데이터 베이스
  - 파일
#### 2-2 스트리밍형 데이터 수집(Kafka, Amazon Kinesis)
  - 애플리케이션 이벤트
  - 로그
  - 센서 데이터
#### 2-3 스트림 처리(Flink, Spark, Kafka)
실시간으로 데이터를 처리에 주로 사용
- 실시간성이 보장되야 할 때
- 데이터가 여러 소스로부터 들어올 때
- 데이터가 가끔 들어오거나 지속적으로 들어올 때
- 가벼운 처리를 할 때
> 사기거래 탐지, 이상탐지, 실시간알림, 비지니스 모니터링, 실시간 수요/공급 측정, 실시간 기능
- 일반적인 플로우  
1. 데이터를 모은다
2. 데이터 베이스에서 읽고 처리
3. 다시 데이터 베이스에 담는다

#### 2-4 배치 처리(MapReduce, Spark, Hive)
대량의 데이터를 처리에 주로 사용  
배치당 처리하는 데이터의 수가 달라지면서 리소스를 비효율적으로 사용하게 된다.
- 실시간성을 보장하지 않아도 될 때
- 데이터를 한번에 처리할 수 있을 때
- 무거운 처리를 할 때 ex) ML DL
> 매월 다음 14일의 수요 공급을 예측, 매월 월급 지급, 매일 아침 크롤링, 매주 새로운 데이터로 ML학습
- 일반적인 플로우
1. 데이터가 들어올때(ingest)
2. 쿼리/처리 후 state 업데이트
3. 데이터 베이스에 담는다  

[Reference: Batch Processing과 Stream Processing](https://yoo-young.tistory.com/m/73)


#### Lambda Architecture vs Kappa Architecture
  - Lambda Architecture  
  batch processing, realtime stream processing이 결합된 구조
    - 장점
      - 속도, 안정성이 우수하다.
      - 확장이 용이하다.
    - 단점
      - 중복 모듈이 많아진다.
      - 같은 코드가 batch layer, stram layer에 중복된다.
      - batch, stream에서 재처리를 할 수도 있다.
      
  - Kappa Architecture  
  realtime stream processing만 이용하는 구조
    - 장점
      - 리소스 절감 (batch layer가 없음)
      - 데이터 생성 / 처리하는 부분이 단일화 되어 시스템 이해가 쉽다.
    - 단점
      - 중복 이벤트 처리나, 이벤트 상호 참조 혹은 순서 관련 처리에 대한 설계가 필요함
      - 장애 발생시, 데잍 재생 관련 부분 처리의 어려움  

[Reference: lambda 아키텍처 vs kappa 아키텍처](https://seungdols.tistory.com/m/921)
<br>


### 3. Storage

#### 3-1. Data Warehouse(BigQuery, Redshift, Snowflake)
데이터 분석을 위하여 서로 다른 시스템에 데이터가 모델링이 되어있는 데이터 베이스   
정형화된 데이터가 들어가 있으며 리포팅이나 분석에 최적화
- 통합 
데이터는 원본 소스에 관계없이 항상 동일한 방식으로 추출되고 변환된다.
- 비휘발성
데이터 웨어하우스는 실시간으로 업데이트되지 않는다. 데이터의 예약 및 시간 업로드를 통해 업데이트되어 일시적인 변경의 영향으로부터 데이터를 보호한다.
- 확장 기능
데이터 웨어하우스는 스토리지 공간에 대한 증가하는 수요를 충족하기 위해 쉽게 확장할 수 있다.

#### 3-2. Data Lake
데이터가 raw 형태로 저장되기 때문에 다양한 유형의 데이터를 저장 가능  
추가 변환이 필요
  - Hudi, Delta Lake, Iceberg
  - Parquet, ORC, Avro
  - S3, HDFS  

[Reference: Data Warehouse Vs Data Lake](https://doqtqu.tistory.com/m/292)
<br>

### 4. Data Analytics and Prediction
데이터 분석가가 insight를 도출하기위한 인터페이스를 제공
#### 4-1. Machine Learning(Spark, Mahout, Amazon SageMaker)
현재 및 과거 데이터를 분석하여 미래 이벤트를 예측하는 분석 방법
#### 4-2. Interactive Query Engine(Trino, Impala)  
#### 4-3. Realtime Analytics(Druid, Pinot, Clickhouse)  

<br>

### 5. Output
데이터 분석결과를 보여주고 데이터 모델을 어플리케이션에 적용하는 단계  
데이터 기반 의사 결정, 비지니스 의사 결정 도와주기  
데이터의 도움을 받아 프로덕트를 향상시킴
#### 5-1. Visualization(Tableau, Superset, Redash)
수많은 데이터들을 이해하기 쉽게 시각적으로 표현하여 전달
#### 5-2. Application

<br>

### 6. Workflow Management(Airflow, Luigi, Azkaban, Oozie)
- 정해진 업무를 원할하게 진행하기 위한 구조
- 다수의 업무 시스템에 내장되어 있어 매일 매일의 태스크를 관리하는데 이용
- 이 구조가 정기적인 배치 처리의 실행에도 유용하여 데이터 처리 현장에서 자주 이용
