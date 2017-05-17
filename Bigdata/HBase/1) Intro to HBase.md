## HBase
HDFS에 구현한 distributed column-oriented NoSQL 데이터베이스이다.
HBase는 대규모 데이터셋에 실시간으로 랜덤 엑세스가 필요할 때 사용할 수 있는 Hadoop library이다.
HBase는 Hadoop의 번들로 제공되며, 어도비, 트위터, 야후 등에서 실사용된다.


## HBase의 특성
 - cluster에 분산된 HBase 테이블들은 region에 의해서 sharding 된다. 그리고 data가 증가할수록 region에 의해 자동으로 수평분할된다. 

## HBase vs HDFS
 - HDFS는 분산 파일 시스템으로 각 파일에 대한 빠른 레코드 검색을 지원하지 않는다. 
 - HBase는 HDFS의 상위에서 덩치가 큰 테이블에 대해서 빠른 레코드 검색, 수정을 지원한다. 

## Data Load from HDFS to HBase

## 참고자료
 - [Apache: HBase Architecture](http://hbase.apache.org/0.94/book/architecture.html)
 - [Apache: HBase Reference Guide](http://hbase.apache.org/book.html)
 - [Cloudera: Importing Data Into HBase](https://www.cloudera.com/documentation/enterprise/5-9-x/topics/admin_hbase_import.html)