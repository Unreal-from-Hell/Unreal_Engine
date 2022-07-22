# 사용자 정의 이벤트

<br>

### 이벤트 종류
1. 표준 이벤트
 * BeginPlay, Tick, Collision 이벤트
2. 입력 이벤트
 * 축 입력, 액션 입력 이벤트
3. 사용자 정의 이벤트

<br>

## 이벤트 디스패처
> 이벤트를 정의하는 것과 통지하는 것을 함께 해결하는 방법


1. 이벤트 디스패처 추가
2. 생성한 이벤트 디스패처를 드래깅해서 배치(호출)
3. 이벤트가 발생하면 해야 하는 작업 흐름 구현
    > 다른 곳에서 해당 이벤트 디스패처를 이벤트 추가하여 해당 이벤트 발생으로 인한 작업 구현

<br>

## Gate open/close 실습하기

<br>

### GateClose Event 만들기

1. GateActor 블루프린트 에디터 열기
2. 빈 곳에 custom event(open) 추가하기
3. GateTimeline에 연결
4. custom event(close) 추가
5. GateTimeline의 Reverse에 연결하면 설정해둔 timeline을 역순으로 실행한다.

<br>

### 새 레벨 만들기
1. GateActor 배치하기
2. 레벨 블루프린트 에디터 열기
3. 'o' 키보드 입력 이벤트 배치
4. GateActor에 대한 레퍼런스 생성
5. custom event 호출

<br>

## 이벤트 디스패처 실습하기


1. 왼쪽의 이벤트 디스패처 추가하기
2. 드래그하여 블루프린트 에디터에 추가(호출)
3. switch timeline의 finished 핀을 이벤트 디스패처에 연결
4. 레벨 블루프린트 이벤트 추가 -> 이벤트 디스패처 추가
4. 레벨 블루프린트 에디터에서 이벤트 디스패처 이벤트에 GateActor의 custom event 연결

<br>


