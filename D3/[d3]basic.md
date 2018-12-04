## SVG는 무엇인가 ?

## <rect>
직사각형을 그릴 수 있는 속성

|x|직사각형 좌측상단의 x축 좌표|
|-|-|
|y|직사각형 좌측상단의 y축 좌표|
|width|직사각형의 너비|
|height|직사각형의 높이|
|rx|굴곡의 x축 반지름|
|ry|굴곡의 y축 반지름|

모서리가 둥근 직사각형의 svg 표현식으로, rx 및 ry의 값이 동일한 경우 가장 보기 좋다.
~~~
<svg width="500px" height="500px">
  <rect x="0" y="0" width="200" height="50" rx="10" ry="10">
</svg>
~~~

## <path>
path는 숫자와 글자를 사용해 그림이 그려지는 경로를 표현하는 d라는 속성값을 지닌다. 

d 속성에서 사용하는 문자는 대문자(absolute), 소문자(relative)로 표현될 수 있다. 
- M: move to의 약어로 path의 시작점
  - M 0 30: 좌측에서 0px, 위에서 30px 떨어진 곳에서 path가 시작됨을 의미한다. 
- q:
  - q 50 -50 100 0: 시작점에서 50 px 떨어진 지점에 높이가 50dls 최고점 지정, 100px 지점에서는 원점
- l: line to의 약어
  - l -100 0: 좌측에서 시작하는 길이가 100 인 선을 그려라

## svg 요소 투명도 조정
|opacity|0부터 1사이의 값을 가짐(0:투명, 1:불투명)|
|-|-|
|fill-opacity|fill 투명도 지정|
|stroke-opacity|stroke 투명도 지정|

## svg 출력 순서
svg는 레이어란 개념이 없지만 선언되는 순서에 따라 출력한다. 요소 2개가 겹친다면 나중에 코딩된 요소가 앞 위치에서 보이게 된다. 

## 그룹요소
<g> 태그를 통해서 요소를 그룹화할 수 있다. 
그룹화한 svg 요소는 css를 동시에 적용시키기에 유리하다. 

~~~
<g class="group">
  <text></text>
  <rect/>
</g>
~~~

## stroke 속성
|stroke|stroke의 색상 설정|
|-|-|
|stroke-width|stroke의 너비 설정|
|stroke-opacity|stroke의 투명도 설정|
|stroke-linecap|끝모양설정(butt, round, square)|
|stroke-dasharray|마디의 길이를 지정하면서 점선 형태 설정(5 10: 5px마디 10px간격)|

## transform / transition
transform을 이용하면 svg요소를 움직이거나 회전시킬 수 있다. transform 에서 사용하는 변환속성은 다음과 같다.
대괄호 안에 있는 인자는 선택사항이다. 
|translate(tx,[ty]|svg 요소의 좌표를 재설정 하는데 사용한다. |
|-|-|
|rotate(angle[cx,cy]|요소를 angle에서 설정한 각도만큼 시계방향으로 회전한다. cy, cy를 통해 회전점의 좌표를 설정할 수 있다.|
|scale(sx,[sy]|요소의 크기를 가로 sx배, 세로 sy배만큼 조절할 수 있다. 정의되지 않은 경우 sx와 같은 값으로 설정된다. |

## x축 범위 설정
domain에는 실제 데이터의 범위를 지정하고, range에는 화면에 뿌려지는 구간의 범위를 px단위로 넣어준다. 
domain 과 range는 배열 1개를 인자를 받고 배열 안에 두개의 원소로 시작과 끝의 범위를 기술한다. 
