# 블루프린트
## Get, Set
- 왼쪽 변수 탭에서 원하는 변수를 Ctrl + 좌드래그하면 Get, Alt + 좌드래그하면 Set
- 원하는 변수를 좌드래그해서 Get 또는 Set를 선택

## 사칙연산 키워드
- +
- -
- *
- /
- ++ or --

## 비교연산 키워드
- ==
- >
- >=
- <
- <=

## 논리연산 키워드
- and
- or
- not

## 키보드 이벤트
- keyboard 치고 원하는 키 이벤트 선택

## 디버깅
- 브레이크포인트: 원하는 곳 클릭 후 F9

## 흐름제어
### Branch, Sequence, Flip Flop
- Branch: True False 분기문
- Sequence: 순차적으로 실행
- Flip Flop: 번갈아가면서 실행

## Max, Min, Clamp
- Max: 들어온 두 값 중 큰값을 반환함
- Min: 들어온 두 값 중 작은값을 반환함
- Clamp: Max과 Min을 합친 기능

## For Loop, While Loop
- For Loop: for문. First Index에서 Last Index까지. With Break문이 따로 있음
- While Loop: While문

## Gate, MultiGate, Do Once, Do N
- Gate: 문처럼 열고 닫고 할 수 있음. Enter를 연결하는 이벤트가 실행 시 닫혀있으면 빠져나가지 못하고 열려있으면 빠져나감
- MultiGate: 게이트와 비슷하게 열고 닫지만 순차적으로 열리고 닫히며 리셋이라는 기능을 이용할 수 있다. 랜덤으로 여닫을 수도 있고 루프를 이용할 수도 있다.
- Do Once: 한번 실행되게 함. 리셋 가능
- Do N: 설정한 값만큼 실행되게 함. 리셋 가능

## Enum
- 열거형
- 컨텐츠브라우저 -> 추가 -> Blueprints -> Enumeration

## 함수
- 컨텐츠브라우저 -> 추가 -> Blueprint -> Blueprints Function Library

## 로컬 변수
- 함수 내부에서 선언된 지역 변수는 선언된 함수 내부만을 유효범위로 가진다
- 함수 호출 시 메모리가 할당되고 함수가 종료되면 메모리가 해제된다

## 복사와 참조
- 참조 전달 시 주소값이 매개변수로 넘어간다.
- 메모리와 관련하여 참조 전달에 관해 깊게 이해하고 있어야 한다

## 고급 디버깅
- call stack을 확인하면 지금 실행되고 있는 문장이 어디서 호출되어왔는지 알기 쉽다.

## 동적 배열 이론
- 동적 배열이 어떻게 메모리에 할당되는지 파악

## 배열
- 배열 사용 방법
- for each loop
- length
- get (copy & ref)
- add
- addunique
- shuffle
- swap

## Map
- add: 값을 추가함, 동일한 키 값으로 추가할 경우 가장 마지막의 값으로 덮어쓰여짐
- remove: 값을 삭제함
- find: 키값을 이용하여 찾는다. 결과로 값과 불리언결과를 반환한다.
- clear: 맵을 비운다
- is empty: 맵이 비어있는지 확인한다.
- length: 맵에 정보가 몇 개 있는지 확인한다.
- keys: 키값을 대상으로 무엇인가 할 때 사용
- value: 값을 대상으로 무엇인가 할 때 사용

