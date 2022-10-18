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

### 1. Data Source

  - 데이터베이스
  - 이벤트 컬렉터
  - 로그
  - API
  - 파일
  - 오브젝트 스토리지
  - 기타
<br>


### 2. Data Ingestion and Processing

#### Data ingestion(Flume, Scoop, Fluentd)
  - 데이터 베이스
  - 파일
#### Event Streaming(Kafka, Amazon Kinesis)
  - 애플리케이션 이벤트
  - 로그
  - 센서 데이터
#### Stream Processing(Flink, Spark, Kafka)

#### Batch Processing(MapReduce, Spark, Hive)

<br>


### 3. Storage

#### Data Warehouse(BigQuery, Redshift, Snowflake)

#### Data Lake
  - Hudi, Delta Lake, Iceberg
  - Parquet, ORC, Avro
  - S3, HDFS

### 4. Data Analytics and Prediction

#### Machine Learning(Spark, Mahout, Amazon SageMaker)

#### Interactive Query Engine(Trino, Impala)

#### Realtime Analytics(Druid, Pinot, Clickhouse)


### 5. Output

#### Visualization(Tableau, Superset, Redash)

#### Application

### 6. Workflow Management(Airflow, Luigi, Azkaban, Oozie)
