# react-addons-perf

## 사용하기
~~~
import Perf from 'react-addons-perf'; // ES6
var Perf = require('react-addons-perf'); // ES5 with npm
~~~

## 측정하기
1. start(): 측정 시작
1. stop(): 측정 끝
1. getLastMeasurements(): 가장 마지막 측정 결과 가져오기
~~~
Perf.start();
// ....
Perf.stop();

const measurements = Perf.getLastMeasurements();
~~~

## 결과 확인 메소드
- printInclusive(): 전체 소요 시간 출력
- printExclusive(): 컴포넌트가 마운트 되는 시간 제외하여 출력 (props 처리, componentWillMount(), componentDidMount() 등)
- printWasted(): 실제 렌더링이 없는 컴포넌트에서 소비된 시간 (ex - Diff 결과 차이가 없어 실제 DOM 변화가 없음)
- printOperations(): DOM 조작에 관한 로그

## 사용방법
- Component mount time = printInclusive() - printExclusive()
- rintOperations()는 React가 실제로 DOM을 생성하거나 업데이트하는 로그를 나타낸다. 예상치 못한 DOM 접근/수정 등을 확인할 수 있다.