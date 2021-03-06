## 데이타 수집 장치

1. DAQ(IBA, Simense 상품) 
 - 5ms, 20ms, 50ms등의 Micro Sec 단위로 대용량의 데이터를 수집할 때 쓰인다.
 - 1분 단위로 파일을 떨어뜨림 File(Multi Row), TC(Single Row) 형태로 받는다.
 - TC Net 데이터
1. HSDAQ 포스코ICT DAQ
1. OPC
 - 1초 단위로 데이터 수집
1. EAI(PC)
 - 데이터 서비스 부의 사상은 모두 IFM을 통해서 데이터를 수집하는 걸로 정했기 때문에,   EAI -> IFM을 보내서 IFM을 통해서 수신한다.
1. CMS
 - 설비관리 시스템


어떤 수집장치를 써야 하는지는 의사결정이 필요하다 왜냐하면 모두 돈에 연관되어 있다. 
DAQ, OPC는 SW가 필요하고 장치 설치할때마다 License비용이 들어간다. 

기술해석은 Tag 기준으로 후판에서 5000개 Tag를 수집한다. 
후판공장 전체로는 40만개 정도의 Tag가 수집된다. 
그러면 도대체 몇개의 Tag를 수집해야 하는가 ? HMI에서 사용하는 Tag갯수로 하기로 결정.
이게 의미가 있다고 판단. 그래서 20% 수준인 8만개 수집하기로 결정. 2단계로 내려가서 최종 9만개로 결정

DD 한개당 정의해야 할 속성이 23개

9만개에 대해서 DD에 표준화 작업이 필요

엔지니어 입장에서 쓸모가 있는 데이터를 기준으로 A(필수), B(필요할 것 같음), C(쓸모없다) 등급으로 분류

IFM 에서 Filtering을 하게 된 이유는 무엇일까 ?
A,B등급만 TC를 정의하고 나중에 A,B등급 항목에 대한 항목 변경이 발생하면, TC수정에 대한 비용이 발생하므로, 한번에 A,B,C등급을 전체 다 받은 후 IFM에서 Filtering 하게 되면 TC변경에 대한 비용이 들어가지 않으므로 이렇게 결정되었다.

TC에 대한 Layout은 IRMS에 있음.

Standard Number(snum) 은 이번 Smart Factory 하면서 신규 추가된 속성이다. 

IFM에서 Filtering을 하기위한 절차는 무엇인가 ?
DD에 Snum 항목의 Value가 정의되면, SNum이 있는 항목이 A,B등급 항목으로 수집대상이 되며
IFM에 별도의 테이블이 존재(DD정보 동기화)하여, 해당 테이블을 통해 수집대상 여부를 체크한다. 

한태호 팀장에게 공유받은 자료
한태호 팀장은 OPC, DAQ등에 대한 수집장치에 대한 정보는 모두 공유해 줄 것임
- 포2열연SF플랫폼_DB테이블 항목 분석.xlxs 자료 참조

IFM 및 IT기술서비스 팀 입장에서는 backbone에 대한 기능이 모두 완결 되어 있는데, 그렇다면 데이터서비스부의 Role은 무엇일지에 대한 고민이 생김.
IFM 및 IT기술서비스는 Biz에 대한 Code를 포함하고 싶지 않아 한다. 
어떤 데이터를 저장할지 말지에 대한 결정은 결국 Biz의 개념으로 데이터 서비스부의 역할

IFM은 국제표준단위가 존재하는 것에 대해서만 단위 변환을 해준다. 
하지만 일부에 대해서는 단위 변환을 하는 경우도 있음
IFM 업무 담당 이인 부장

Kafka Queue에 데이터 저장

Message 유형 구분
- Micro 데이터: A,B,C,D
- Macro 데이터: E ~ J
 환경 에너지 등 Biz Domain별로도 구분짓기 위해 Msg Type을 구분했지만, 나중에 보니 데이터 자체로는 구분짓는게 별 의미가 없고, Micro vs Macro 의 구분만이 유의미 한 것으로 보임

- A: DAQ, OPC 고속주기성
- B, C: 기술해석 Micro 데이터(기술해석은 없어지는 데이터 시스템이기 때문에 기술해석 데이터 모두 수용)
- D: 조업설비 시계열 데이터
    - 재료에 Mapping되기 어려운 데이터(제강, 연주)
 - I: 대표적인 Macro 데이터로 수집대상이 되는 데이터
 - J: event 성(변경점), 정렬을 위해 사용되는 부가정보들을 제공한다. 
Micro데이터와 Macro데이터의 구분은 ?
Micro데이터 ? 기본적으로 시계열로 들어와야 한다.(시간정보, TagId, 값)
Macro데이터 ?

Queue에 대한 Naming Rule, Queue를 물리적으로 구분하기 위한 기준들에 대한 고민들도 필요했음

전문에는 공통부분이 있다.(Default 영역)
- 조업구분, 공장공정코드, MicroData설비번호(데이터 서비스 부에서 부여)
- Asset코드
    - 지역, 설비, 조립품, 부품 으로 분류가 되어 있음
    - CMS에서 수집되는 항목에 대해서는 Asset 코드가 존재하지만, 나머지는 없음.
      그래서 Asset코드를 어떻게 셋업해야 하는지 고민이 많음
    - Asset코드는 사용자 관점에서 Asset단위로 Micro데이터를 조회하고 싶을때 filter 조건으로 활용가치가 있다. 

- IBA는 공통부분이 없으므로 IFM에서 생성
- 기술해석에서 올라오는 데이터가 정합성이 불일치 하는 경우 다수 존재(사소구분이 틀리든지) -> 데이터 서비스 부 로직에서 Dafault영역 재부여

MicroData설비번호는 왜 필요한가 ? 
- 정렬을 수행하기 위해서는 정렬을 수행하기 위한 정렬단위가 필요하다. 그 단위를 구분짓기 위해 필요한 항목
- 정렬단위를 분류화하기 위해서 꼭 맞는 항목이 존재하지 않으므로 만들어짐


Redis 저장 데이터
TC로 받은 데이터는 deliminator를 붙여서 String을 만들어 준다. 
- 정렬전: 정렬대상, 정렬미대상 영역은 Redis의 Port번호로 구분이 된다. 
 - 정렬대상
  정렬전 데이터는 Tag별 Value뿐만 아니라 Value에 대한 Meta정보가 추가됨으로 Resource가 증가
 . 6시간
 - 정렬 미대상: 정렬 후 Port로 바로 저장되서 Flume을 통해 Hadoop 저장

- 정렬후: 작업완료 event를 수신 받아서, 정렬전의 데이터를 추출해서 정렬 모듈 수행 후 다시 Redis에 저장
 . 2시간
 . Hue에서 조회를 하면 data 디렉토리가 정렬 후 데이터가 저장되는 partition 이다. 
 . data/ m25 / 8 -> column 형태로 저장된 데이터
 . data / m25 / Tb_m25_s -> row 형태로 저장된 데이터

- 전문 원본데이터는 Redis 거치지 않고 Flume -> Hadoop 에 바로 저장
    -> 이 원본데이터이 왜 필요했는지 ? 최초 구축시 데이터가 데이터 서비스 부의 로직을 통해 제대로 저장되는지 비교 확인할때 필요
    -> 데이터 유실시를 대비하기 위한 백업화면
    - 원본데이터는 최초에 조회할 수 있는 화면이 존재하지 않았는데 활용개선 Project를 진행하면서 원본데이터 조회 화면 생성
    - 원본데이터는 File Format으로 저장
    - 원본데이터는 3개월 저장
    - 가공이 없으므로 A,B,C 등급 항목 모두 저장
    - Hue에서 보면 partition 이 raw_data / M23 / 3W / tc 코드 / 년/ 월 / 원본파일.raw -> 팟캐이가 아님
    - 원본데이터를 Backup을 통해 정렬 모듈을 실행하는 기능은 현재 없음

 - 정렬 후 데이터는 Flume을 통해 Hadoop 에 저장 

현재까지 Proj 진행순서
 - 광양 후판 -> 활용개선 -> 포항 2열연 (현재) ->..... 

Hadoop은 File System 이다. 
Hadoop에 저장된 File을 SQL을 통해서 조회하고 싶은 Needs가 있어서 Impala에 구조 등록

Flume은 대량의 데이터를 처리해주는데, 유리하지만 
Tuning이 잘 되지 않으면 휴지 후 동시에 대량의 TC를 수신하는 경우 등의 케이스에 Flume이 Kill 되는 현상이 발생하기도 한다. 그렇기 때문에 Tuning이 잘 되어 Alive 상태가 유지될 수 있도록 하는 것이 중요.

Flume agent

Kafka Queue는 RTP가 Kill되도 file이 삭제 되지 않는다. 
Flume은 내부 Queue를 사용하는데 RTP 가 Kill되면 File이 삭제 그래서 현재 Kafka Queue로 변환하는 작업을 진행하지만, 데이터 size가 달라지는 현상이 발생하는 상태임

Hadoop의 partition이 최초로 잘 나누어지지 안았을 경우에는 성능이 안나와서, Partition을 최대한 늘려서 사용하게 됨

### 화면

가장 주안점은 어떻게 사용자가 데이터에 가장 편리하게 접근할 수 있을가에 대한 고민을 통해 지속 발전

그룹내 Tag수가 수천개일 경우에는 어떻게 편리성을 증대시킬 수 있을까 ?
Grouping의 단위 및 Depth를 추가 ? 어떻게 ? 
계속 고민이 되는 부분이다.

시계열 Micro Data 트렌드 조회 화면
- 정렬과 상관없이 Micro 데이터를 시간 축으로 조회
- MES와는 조회조건의 차이가 있고, 동일할 수 없다. 
    -> 그렇기 때문에 조업, 공장, 공정을 어떻게 분류해야 하는지 Prj하면서 의사결정이 되어져야 한다. 

전장길이정렬
- 재료의 길이단위로 보여줄 수 있는 화면

가열로 화면은 현업 요청으로 Biz Logic 이 녹아있는 화면도 있다. 

활용개선 프로젝트.. 
최초에는 Micro데이터만 관심이 있었는데, 설비과제를 진행하다 보니 의미가 있는 Macro데이터도 관리가 필요하다는 Needs가 발생해서 그러한 부분의 개선을 진행한 프로젝트
ex ) 광양_후판_후판최종검사실적

Impala에 구조 등록
Impala에서 I 키워드가 들어간 테이블은 Macro 실적
Macro 든 Micro든 Impala에 구조를 등록해야 한다. 

Main문서
*어플리케이션설계서.ppts -> 포스코ECM
수집,정렬에 대한 사상이 담겨져 있는 문서

### 정렬
과연 모든 재료에 대해서 Cyclic data(시계열)를 Segment Data(재료별)로 바꿔야 하는지가 고민이 었음

김남일 PCP 입장에서는 정렬이 가능한지 불가능한지를 어떻게 구분할 수 있는지 ?
정렬을 해서는 안되는 것들에 대해서 정렬을 수행하고 있지 않은가 ? 혹은 그 반대 
정렬에 대한 검증이 필요한데, 계측기가 투입이 안됨으로 인해 정렬에 대한 검증을 할 수 없는것에 대한 고민이 있다. 

재료동일점 맵핑
- 현업의 길이방향 정렬시 일정 간격으로 데이터를 조회하고 싶다. 
하지만 특정포인트의 Micro데이터가 없는 경우 데이터를 만들어 주어야 하는데 이를 재료 동일점 맵핑이라고 한다. 
- 연주는 5cm 단위로 데이터 생성

메시지 유형
- S Type
    - 재료번호 및 길이방향 위치 부여한 데이터
    - T_M25_S
- Z Type
    - 재료동일점 Mapping된 데이터
    - T_M25_Z

길이방향 정렬이 가능하기 위한 조건 세가지로 아래의 조건 값에 대한 Setup 필요
1. Metal in tag(Micro)
 - TC Net에 존재
 - 재료가 물리면 1, 없으면 0
 - 재료 Inout 시점

2. 속도항목이 있어야 한다.(Micro)
- 최초에는 속도를 사용하지 않음, 최초에는 Mill Length를 사용했었는데 하지만, 이 Mill Length는 만들어낸 값이라 정합성이 맞지 않기 때문에 속도를 사욯하게 되었음

3. 재료의 길이에 대한 기준길이가 있어야 한다.(Macro) 
 - path가 끝날때마다 폭, 두께, 중량에 대한 값을 받아서 기준길이를 구하게 된다.
 - 해당 기준길이는 MES로 I/F 되는 값이므로 신뢰성은 있다고 볼 수 있음 

작용점
- 재료 길이/폭방향에 대해 제품의 형상 및 품질에 영향을 줄 것으로 예상되는 설비상 Point를 지칭하는 자체 용어

결론
냉각을 하는 경우 물을 분사하는데, 이러한 경우 작용점이 무한하다고 판단하게 되며 이런경우 정렬 불가

제강 공정과 같이 재료의 형상이 없는 경우 정렬 불가 

정렬 수행 로직
- Metal In Flag의 값이 1이 되는 순간 부터 Roll 속도를 적산하여 이론상의 재료위치를 구한다. 
- Metal In Flag의 값이 0이 되면 이론상의 전체 길이 적산이 가능
- 이론상의 길이를 기준길이와 비교하여, 길이 비율에 따른 길이방향 위치를 재조정한다. 

후판의 경우는 이론상의 길이와 기준길이의 편차가 4% 정도 발생
이론상의 길이뿐만 아니라 기준길이 자체도 계산에 의한 결과이므로 정합성이 100% 맞다고 볼수는 없다. 그러므로 계측기가 있어야지 기준길이에 대한 정합성이 확보 가능

TagMeta 테이블이 생길 수 밖에 없던 사유
현업은 모든 항목에 대해서 정렬을 해달라고 요청을 했지만, 데이터를 뜯어보니 결국 정렬이 가능한 데이터와 불가능한 데이터가 있을 수 밖에 없다. 
정렬을 위해선 필수의 속성이 필요한데, 이러한 속성에 대한 정보를 관리하는게 Tag Meta 테이블이다. 

Event Traking 대상인 경우에는 RDB에 저장되는 Event 정보를 Mix해서 같이 보여줘야 한다. 

후판의 경우에는 Dummy path(압연이 끝난후 설비를 통과시키는 path) 인 경우에는 재료동일점 Mapping을 수행하지 않는다. 


Day2

## Micro Data 정렬 개요
데이터를 분석하기 위해서는 대표 실적이 필요하고, 그와 관련되 Micro 데이터들이 필요하다고 생각. 후판의 Macro, Micro 데이터를 살펴보면.

Micro 재료대표실적 - PC에서 수신
주요 작업 Event 일시를 수신받아서 정렬의 기준으로 활용한다. 


Macro 재료연속실적, 시계열실적 - OPC, DAQ

후판의 RM같은 경우는 24시간 중에 1.5시간 정도만 부하 데이터 발생
그래서 무부하 데이터를 저장하지 말까 고민도 했었지만, 그런 요구사항이 현업으로 부터 없는 상태에서 현재는 무부하 데이터도 모두 관리하는 상황

## 부하, 무부하 데이터
부하: 의미 있는 일을 하는 동안에 발생하는 실적들
무부하: 일이 없을 경우에 발생하는 실적

부하, 무부하 를 판단하는 기준은 특정 Tag(Metal IN Flag)를 참조해서 값이 있는 경우 부하, 없는 경우 무부하를 체크하고, 각 설비별로 해당 Tag가 존재 한다. 
물론 그 값이 맞냐 틀리냐의 문제는 존재한다. 

후판의 경우는 설비단위로 Micro Data

정렬이 이상적으로 수행되기 위해서는 설비단위로 Micro 데이터를 수신받는게 가장 좋다. 
하지만 현실적으로 현재 수신되는 Micro 데이터는 설비단위로 분류된 경우도 있지만, 그렇지 않은 경우도 존재 한다. (CMS 같은 경우는 진동에 관한 데이터를 한개의 TC에 전체 공정의 정보를 모두 송신)

가능하다면 TC를 분류하는 형태로 요청해서 실현되면 좋지만, 
현실적으로 불가능한 경우에는 데이터 서비스 영역에서 해당 Troubleshooting을 수용해서 해결하는 방안도 고려되어 개발되고 있다. 

정렬 처리 Process
완료 Event 수신 -> 정렬 대상이 존재하는지 체크 -> delay time 에 충족하는지 체크 -> 충족하면 정렬 수행
-> 충족하지 않으면 정렬 수행 않고 종료

-> 정렬 모듈에 awake event를 발생시켜서 -> 정렬 모듈 재기동 -> 정렬 대상 존재하는지 체크

정렬에 필요한 조건 체크 수행을 한다. 
1. 정렬에 필요한 A, B, C 전문이 모두 필요한데, 예를들면
 - A -10:30, B - 10: 30, C - 9:30 이면 C의 10: 30 분실적이 수신될때까지 정렬은 Wait Status에 머문다. 
2. 추가적인 조건은 무엇이 있을까 ?
 정렬에 필수적인 3가지 조건 항목의 값이 존재 해야 한다. 
3. Multi 작용점인 경우에도 불가

정렬에 delay time이 필요한 이유는 ? 
작업완료실적 Event를 수신하고 나서 곧바로 정렬을 수행하게 되면, Redis에 정렬전 TC 데이터가 모두 안들어 와 있는 경우가 있을 수 있다. 이유는 Spout, Bolt에 Queuing 상태로 남아 있어 Redis에 정렬전 데이터가 저장이 안되어 있는 경우 발생해서, 각 정렬모듈 별로 Delay Time을 셋업할 수 있는 기준을 관리하고 정렬수행 체크 모듈에서 사용한다. 

정렬을 개발하면서 가장 고민이 되었던 부분이 
과연 정렬의 대상이 되는 데이터는 무엇인가가 고민이 었음. 

예를들면, 환경데이터 (온도, 습도, 기압) 등의 데이터는 동일 시점에 연계되는 재료의 매수는 RM, FM 기타 모든 설비를 포함해서 1:N의 관계 에 있는데, 과연 이러한 데이터를 각 재료별 맵핑을 해주어야 하나라는게 고민이었음
결국 1:N의 데이터는 화면상에서 참조정보로 보여주는 정도로 하는것으로 View를 제공하고 있음

현재는 연주와 Roll에 대한 정렬에 대한 개념은 어느정도 정립이 되어 있는데, Tension(장력)이 발생하는 장치에 대해서는 과연 길이방향정렬이 필요한가 ? 아니면 특정 작용점에 대한 장력에 대한 Trend만 보면 가능할까 ? 
정렬이 필요한지 말지에 대한 고민들이 된다라는 것.. 

재료변경점은 재료변경점을 관리하는 테이블이 있음(Parent-child Relation)
변경점이 발생하는 Event들을 조사를 해보니, 어느정도 공통되는 부분이 있다고 판단이 되었고, 특정 Event케이스에 대해서는 변경점 TC에 대해서 공통 레이아웃으로 수신받도록 포항에 작업했음.. 

Micro Data 연계구분
cardinality 특성을 구분하는 항목이다. 
Micro Data의 모든 Tag에는 해당 항목의 값이 있어야 한다. 
B 유형만 재료맵핑이 가능하다. 

MicroDAta정합성구분
Tag 속성에 Min, Max 항목이 정의 되어 있어 틀이 만들어 졌지만, 결국 기준이 없기 때문에 SetUp의 어려움이 있다. Null값이 많음. 
Min, Max 값의 셋업이 플젝을 진행하면서 데이터를 채워나갈 필요가 있음

MicroData재료번호정합성 구분
Over한 것도 있음
? 기술해석에서 수집하는 데이터 모두 재료번호가 맵핑되어 있는데에 반해  charge1 -> charge2를 작업이 연속된다고 가정할때 charge1과 charge2 사이의 발생데이터를 모두 charge1으로 잘못 맵핑을 하고 있다. 
기술해석에서 발생하는 데이터의 정합성 체크를 위해서 활용되는 것으로 판단 됨.

L은 부하
U 무부하 데이터

MicroData길이위치산정방법구분: 재료의 특정위치를 찾아가기 위한 방법 정의
5번: 기술해석에서 한번의 path당 45개의 실적이 동시에 올라온다. (3000개)
이때 맵핑되는 작업완료 실적이 모두 동일하기 때문에 길이방향정렬은 실적시간이 필요한데, 그데이터가 없기 때문에 시간을 나누어 동일한 소요시간으로 가정하여 정렬을 실시한다. 

MicroData정렬방법 구분
재료동일점 Mapping 에 대한 방법 구분
거의 A를 사용하고 있음

Message 유형구분
Tabe설계 2단계.xls 파일에 모든 DB,기준, Redis, Hadoop에 대한 구현체를 정의하고 있음
In-Memory Key 체계
A-D는 받을때 Redis Key를 만들어서 Tag 단위로 저장하는데 A,B가 차이가 나는 부분이 Key는 동일하지만 Value 값이 서로 다르다. 

Redis에 저장되는 데이터 Set은 Value저장형태가 sorted Set인 경우에 Score를 주고 TTL 값을 관리
정렬 전에는 TTL을 참조해서 Buffering개념으로 데이터를 무제한 소유
정렬 후에는 s format으로 데이터를 변환해서 재저장하고 2시간(어떻게 2시간인지 알지 ?) 후에 저장되도록 TTL값 변경 ? 혹은 다른 값 ? 

String Type과 Sorted Set의 차이. 

K,L은 Micro DATa -> 정렬을 안하는 놈
column wise 저장 
곧바로 Hadoop으로 저장

Macro 데이터는 Column wise 저장( 항목이 deliminator로 구분해서 저장되는 데이터이고 각 값의 tag는 IRMS를 통해서 찾아갈 수 있다)

Cloumn Wise 저장 I, K, L
TB_M24_I_TC
TB_M24_S

Row Wise Data의 포맷

MicroData발생구분
2열연에 Analog Data와 Digital 데이터를 구분해달라는 요구사항
Analog: 0,1 이외의 값을 갖는 데이터
Digital: 0,1

광의로 보면 정렬이란게 꼭 재료번호맵핑, 길이방향정렬뿐만 아니라 Digital, Analog의 파형을 구분하는 것 조차도 정렬이라고 볼수있고, 
재료동일점 맵핑에도 해당 값이 사용된다. 

디지털과, 아날로그는 데이터의 전후 관계가 계단식인지 곡선인지를 구분하기 위해 필요함 -> 어디에 쓰일까 정확히 ? 

RDB가 어디에 쓰이는지 ? 
정렬Request 가 발생해서, 완료되기까지의 정렬에 대한 전반적인 정보들이 저장된다. 
정렬이 정상적으로 수행되었는지 Monitoring 및 원인분석을 하기 위해 사용

데이터 서비스 영역 입장에서는 작업지시 작업실적을 관리하는 테이블

Table설계 화면에서 Table일람
기준Table유무, RTP사용유무, NRTP사용유무

최초에 정렬 수집을 위해서 RDB가 만들어 졌지만, 비즈과제가 신규로 추가되는 경우가 생겨서 사용자 관점의 테이블 추가


코일공정 PosRame 확산 및 Customizing 방안

포항 2열연은 재료 Traking 기능이 필요
정비플랫폼을 확인해 보니 Traking이 필요하다고 판단

PC에서 발생한 완료일시 Event를 받는 경우 시간이 틀어졌을 경우 방법이 없음

포항 2열연에서 프로젝트를 하다보니 Asset 코드가 정의되어 있고 이게 의미가 있다. 
확산을 하게 되면 EAM을 통해서 Asset 코드를 받아서 Asset별로 Tag를 분류를 하는것이 좋다.

HOPES 는 PDS 
향후에는 HOPES를 없앨수도 있는데 포항 2열연은 HOPSE 데이터를 모두 가져오도록 되어 있다. 

코일 공정 확산 시 추가 개발 기능
- Scale 실적 국제표준단위 변환 기능
TC NET에서 발생하는 데이터들은 모두 Range의 값을 가지고 생성되는데, 각 장치별 각기다른 Scale로 값을 변환해서 사용하기 때문에
표준화해서 데이터의 저장이 필요.
항목표준화 시 같이 요구를 해야 한다. 

- 재료 Tracking 기능
qkftodgks tlfwjrdp eogo wjswkdrlfl 정렬을 않더라도 재료 매핑할 수 있는 기능

연연속 압연 전장길이 정렬 기능
- FM에서는 RM에서 발생한 재료들을 이론상으로 99개 재료들을 연연속 접합 할 수 있는데, FM에서 발생한 실적이 어느재료에 속한지 구분하기 위한 
METAL IN Tag가 모두 1이므로 MIF로 구분을 할 수 없어 다른 Tag가 필요한데, 이때 접합부 위치를 표시하는 Tag를 활용한다. 

IBA 가변구조 허용
IBA Address 기준 항목 매핑 기능 개발
- 왜 ? 신규항목이 만들어지는데 기존 포맷의 제일 뒤가 아닌 중간에 삽입되는 경우가 존재하는데, 이럴경우 문제의 소지가 있음
- 발생처에서 하는 것들을 제약하는 것이 문제가 되기 때문에, 수신측에서 가변적으로 변경된 레이아웃을 대응해서 수신할 수 있도록 기능을 개선하는 것이 필요

소급적용 기능을 공식적으로 만들 필요가 있음
- 왜 ? 비표준 항목이 표준화가 되었을 경우 현업 입장에서는 데이터가 너무 없으므로 과거 데이터 복원을 원하는데, 이럴 경우 Hadoop의 데이터를 DML을 통해서 넣어는 수작업이 필요
- 이를 자동화 하면 좋을 것 같음

변경점 관리
포항 2열연에서 보니 코일박스가 있음
코일박스는 접합을 할때에만 쓰임 코일박스에 따라서 변경점의 특성이 서로 다를 수 있음
(Head/Tail만 바뀌는 경우, 상하가 동시에 바뀌는 경우가 있을 수 있으며 이는 설비를 확인을 해야한다. )

기준테이블

기준 SEtup 대상 은 왜 MAster 업무기준이 아니고, Table 인지
EasyAccess 의 성능 문제 일까 ?

Master 업무기준
현재 프로그램상에 정의, 업무기준 흉내 -> 소스안 데이터 형태
마스터 업무기준에 사용되는 항목들의 표준화가 안되는 문제
연결이 끊기는 현상 등등


업무기준 SEtup 원장.xls
