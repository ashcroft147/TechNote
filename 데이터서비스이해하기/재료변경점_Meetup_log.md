### 18.01.24

# 수평적통합 시스템 개발의 주된 목적 ?
 - 주편이 나온시점부터 재료의 형태 및 위치가 어떻게 변해가는지를 추적하고자 하는게 이 시스템 개발의 주된 목적임을 상기

# PPT문서에서 표기한 표현 관련
 - '입측회전'의 의미는 ? 
    -> Head / Tail이 바뀌는 것을 의미하는 것으로 타인이 이해하기 쉬운 표현으로 변경 필요 

 - 발생가능 재료변경점은 ? 
    -> 기 정의된 Event발생구분 값으로 표기하는것으로 변경

# 1열연 압연에는 Crop절단이 있을 것으로 판단됨
 - 현재까지 분석한 결과만으로 변경점을 판단할 기준항목이 없기 때문에 당연히 발생하는 재료변경점을 없는것으로 가정하면 안된다. 
    -> 가장 중요한 가치는 이상적인 모델의 구현이 어떻게 되어야 하는지를 이해하고 먼저 해결해 나가야 함
 - 재료변경점이 발생하는 포인트를 실제에 맞게 찾는것이 중요하고, 값을 어떻게 만들어 주는지는 그 다음 단계에 고민이 필요한 문제임.
 - 만약 실적 테이블에 crop절단 실적이 없다면 이 값을 어떻게 만들어 낼까 ?
    -> 2열연의 경우에는 Default 값이 올라옴. 그렇다고 하면 1열연의 경우도 Default 값을 할지 혹은 다른 방법이 있을지 데이터를 찾는 방안 강구 필요

# 데이터의 신뢰성의 문제는 여러가지 원인에 의해서 발생할 수 밖에 없음
 - 정상 조업인 경우/ 매뉴얼로 처리 하는 경우 / 장애처리에 의한 백업 처리를 하는 경우 등
 - 결국 신뢰성의 문제는 발생가능한 케이스에 대해 최대한 고려함으로써, 100%의 신뢰도를 갖춘 시스템이 아닌 점차 신뢰도를 높이는 시스템 개발을 해나가는 노력이 필요함
   이를위해, 발생가능한 케이스에 대한 수용성이 높은 로직을 개발하는 것이 필요

# 열연정정작업의 경우를 보면, 해당 공정이 압연 혹은 기타 다른 길이가 늘어날만한 재료변경 이벤트가 없는데도 재료길이 변화가 있는 경우는 어떻게 해야하는지
 - 늘어나는 경우 : Tension Reel 에 의한 당김으로 길이가 늘어났을 수도 있다 -> 이것이 일정한 비율인지 / 혹은 비선형적인 값을 갖는지에 대한 통계분석 필요
 - 줄어드는 경우 : 가열 후 팽창했다가 상온으로 가는 경우 수축이 되는 경우 / 계측의 실수 등등 -> 마찬가지로 통계분석 필요

# 재료변경지점에 대한 상세한 위치값을 알지 못하는 경우 Evnet 발생 구분 코드별 대응 방안
 - Event 구분이 3인 경우 : 비례식 
 - Event 구분이 4인 경우 : 만약 잘려나간 길이를 알지 못하는 경우 centering을 통해 앞뒤로 잘려나간 길이를 계산
 - 위와같은 방법으로현재 수준에서 어느정도의 기준 수준으로 맞추는 것은 좋지만, 현재 개발하는 공장에서의 특이점 / 이상한점을 계속해서 발굴해내 원인을 분석하는 과정은 지속적으로 필요하다. 
   이상 및 특이점이 발견되는 현상에 대해서 패턴이 발견되지 않으면 통계분석이 우선 필요하고 그래야지만 현상 분석이 가능

# 운전모드 컬럼 추가가 될 예정
 - 실적이 아닌 백업으로 작업한 경우에는 데이터가 정합성이 맞지 않는 경우가 높을 수 있다. 
 - 이러한 정보를 기반으로 데이터 신뢰도에 대해서 현업에게 올바른 정보를 제공할 수 있다. 
 - 우선은 기본틀을 잡아놓는게 우선이고, 미세한 문제들은 기본틀이 진행되면서 차츰 해결해 나가는 방향으로 진행이 되어야 한다. 


# 재료변경점관리 모듈의 기동 관련
 - 이벤트 Trigger / 정주기의 복합된 형태로 기동되는 것을 고려해 보는 것이 좋겠다. 
    - 이벤트 Trigger : 이벤트 기반의 장점은 delay 최소화 및 재료검색 소요시간의 최소화 
    - 정주기의 역할: 재료변경점 미등록된 데이터의 백업 처리 (Nightly)

# 재료변경점 데이터의 하둡관리 방안 관련
 재료변경점 데이터를 Hadoop으로 저장하기 위한 시나리오는 다음의 경우가 있을 것이고, 가장 Simple하게 Hadoop으로 저장하는 신규 Route를 찾았으면 함
 - NRTP -> Hadoop
 - NRTP -> Kafka Queue -> Hadoop
 - NRTP -> Redis -> Flumn -> Hadoop
 
# 기준셋업 파일 Review에서 언급한 내용
 - "발생가능재료변경점" 항목에서 입측 / 출측의 개념은 불필요 할 것 같다. 설비정보를 알고 있으면 입측 / 출측 에 대한 정보는 자연스럽게 얻어진다. 
 - 길이항목의 경우에는 PosFrame은 mm 단위로 관리된다. 각 실적 항목 별 단위 변환이 필요한지 여부를 판단해서 단위변환 하는 로직을 만들어 준다. 
 - 업무기준을 성격별로 분할하는 것이 어떤가 (조업해석 테이블 마스터 기준 / 재료변경점 기준 )
 - 업무기준 항목 명은 표준항목이 필요없으므로 연산자 / 기준값 을 사용자가 인지가 편하도록 변경

# To-Do List
 - 정대웅 : NRTP 에서 하둡으로 가는 모듈 개발 설계
 - 박두환 : NRTP -> Hadoop -> View 까지 각 케이스 별 Performance Profiling
 - 구희준 / 김정현 : 회의내용 보완 및 설계 지속