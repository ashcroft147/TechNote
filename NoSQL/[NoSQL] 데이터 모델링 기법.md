## NoSQL 데이터 모델
 1. Key/Value Store
  - Oracle Coherence, Redis
 
 2. Ordered Key/Value Store
  - 내부적으로 Key를 순서로 Sorting해서 저장
  - NoSQL은 Ordery by 기능이 없기때문에 Sorting해서 출력시 필요
  - Apache의 Hbase, Cassandra 
 
 3. Document Key/Value Store
  - Key를 사용하는 것은 동일하나 Value에 Document 라는 타입을 저장한다. 
  - Document는 XML, JSON, YAML 과 같은 구조화된 데이터 타입이다.
  - Sorting, Join, Grouping 등의 기능 제공
  - MongoDB,CouchDB,Riak 

## NoSQL과 RDBMS의 차이
 - NoSQL은 데이터를 저장하고, Key에 대한 Put/Get만 지원한다.
 - NoSQL에서는 Sorting, Join, Grouping, Range, Index에 대한 기능을 지원하지 않으므로 
   NoSQL Data Modeling Pattern을 통해서 구현할 수 있다.

## When embeded, When Reference
 - embeded
 ~~~
 {
     "sesseionId": "1",
     "speakers": [
         {
            embedded
         },
         {
            embedded
         }
     ]
 }
 ~~~
 - when ?
    - query(select, update) operation이 동시에 일어나는 경우의 data
    - 하위의 document가 상위 document에 의존적 인 경우의 data
        - 예를들어, 네 명의 가족이 음식을 주문하는 경우 각 구성원의 메뉴는(하위 document)는 주문에(상위 document) 의존적
    - 1:1 관계에 있는 data의 경우
        - 걸그룹의 멤버는 각각 profile을 반드시 갖고 있고, 이러한 1:1의 관계에 있는 sub object는 embeded되어야 한다.
    - Similar volatility: 비슷한 시점에 동시에 바뀌는 Data의 경우
        - 예를들어 email과, socialId 객체가 있다고 가정하면 이 둘은 거의 바뀌지 않고 바뀌는 주기가 비슷하다.

 - 성능은 ?
    - embeded document는 data를 가져오거나 put하는 경우 하나의 document에만 query를 실행하므로 더 좋은 성능을 낸다.

 - reference
 ~~~
 {
     "sesseionId": "1",
     "speakers": [{"id": 1}}, {"id": 2}}]
 },
 //reference
 {
    "id": 1, 
 },
 reference
 {
    "id": 2
 }
 ~~~

 - when ?
    - one-to-many의 관계에 있으면서 sub document로 있는 경우 그 데이터가 무한정 증가하는 경우
        - 예를들어, SNS의 댓글인 경우에 특정 document에 embeded 해버리면, comment가 증가할수록 Main document는 성능이 당연히 떨어질수 밖에 없다.
    - many-to-many의 관계
        - 예를들어, 여러 강사가 있고 각각의 강사가 여러개의 강좌를 강의한다고 하면 이런 경우 강사랑, 강좌는 서로 document를 분리하는게 낫다
    - 서로연관된 데이터지만 서로다른 volatility를 갖고 있는 데이터의 경우
    - 참조되는 document의 entity가 다른 document에 의해서 key entity로 사용되는 경우 분리 해야 한다. 

 - 성능은 ?
    - embeded 보다는 낮지만, database를 작게 관리할 수 있어 효율적이다.

 - embeded + referencing

## Normalized, Unnomalized
    - document내에 sub document가 있을때, sub document를 완전히 따로 분리해서 document를 구성할 수 있고(Normalize), 만약 자주 사용되는 entity 같은 경우에는 
    document에 entity를 구성해서 sub document를 읽으러 갈 필요 없게 할 수 있다.(Denomalize)

    - normalize
        - 장점: storage space를 아낄 수 있다.
    - denormalize
        - 장점: read speed가 올라간다.

## Homogeneous, Heterogeneous data

## 참고자료
 - ![조대협의 블로그](http://bcho.tistory.com/665)
 - ![MS Build](https://www.youtube.com/watch?v=-o_VGpJP-Q0)