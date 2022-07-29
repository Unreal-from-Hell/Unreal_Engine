# 트리거(Trigger)
> 오버랩 활용을 목적으로 하여 게임의 물리적인 움직임에는 간섭하지 않고 게임의 로직의 시발점이 되는 콜리전
> * 트리거 = 이벤트 박스


## 트리거를 사용한 인터랙션


### 인터랙티브 콘텐츠
* 상효작용적 요소를 가져야함
> 맵의 특정 장소에서 특별한 일이 발생, 장치/아이템과 상호작용


## 콜리전

### 게임에서의 충돌
* 두 자동차의 충돌 -> 물리적인 현상이 실제로 발생함
* 코스 위에 있는 아이템을 자동차로 부딪쳐서 아이템을 획득
* 자동차가 결승선에 도착

### UE4에서의 충돌
* 블록(Block): 물리적인 현상이 일어나는 경우
* 오버랩(Overlap): 물리적인 현상 없이 단순히 겹치는 것만 검출하는 경우 


### 트리거 활용 - 데스 트리거

간단한 플레이어 캐릭터의 사망 처리 준비
* 플레이어가 데미지를 조금이라도 받으면 사망한 것으로 출력

트리거를 레벨 블루프린트에서 사용
* 트리거를 레벨에 배치하고 액터와 오버랩되는 경우 데미지를 발생시킴

액터에 트리거 추가
* 여러 맵에서 활동이 가능하도록 액터 내에 트리거를 추가하기


### 액터 소멸

* 화염 트리거: 접촉하면 플레이어를 제거시킴
* 픽업 아이템: 접촉하면 자신이 제거되어야 함



### 픽업 아이템

* 코인: 각 스테이지에 여러 개 배치되어 있으며 획득하면 점수가 오름
* 두루마리: 각 스테이지에 하나 배치되어 있으며 획득하면 스테이지 클리어

### 픽업 아이템 생성

* 액터 소멸
> DestroyActor

* 액터 생성
> 액터를 템플릿을 기반으로 만들지 말고 가장 바닥부터 만들기

* 조건(if) 분기의 기본
> 분기 노드



## 실습 


## 1. 플레이어가 지속적으로 데미지를 입는 지역(데미지 존) 생성

### 레벨에 박스 트리거 추가하기

1. Fire 액터에 박스 트리거를 배치

2. 박스 트리거 선택 우클릭 -> 이벤트 추가 -> OnActorBeginOverlap
> 트리거 박스와 최초로 닿는 순간 발생

3. Apply Damamge 함수 호출 -> other actor를 -> damaged actor애 연결 


### 액터에 트리거 추가하기


1. fire 액터 선택 후 배치 -> 블루프린트/스크립투 추가 
2. 컴포넌트 추가 -> Box collision 추가
3. box collision 우클릭 -> 이벤트 추가 -> OnComponentBeginOverlap 
4. apply damage 함수 호출 -> other actor를 -> damaged actor에 연결


## 2. 맵에 배치할 코인과 두루마리를 만들고 플레이어가 획득할 수 있게 함


1. 코인, 스크롤 스태틱 메시를 선택 후 블루프린트/스크립트 추가 
2. box collision 추가
3. box collision 우클릭 -> 이벤트 추가 -> OnComponentBeginOverlap 
4. 객체를 소멸시키는 DestroyActor 함수 호출 -> 타깃: Self

### 처음부터 하나하나 만들기

1. 블루프린트 클래스 추가 -> Actor 상속 -> 컴포넌트 추가 -> Scene -> Scene 안에 컴포넌트 추가 -> 스태틱 메시 -> scroll 메시 추가
2. 컴포넌트 추가 -> box collision 추가 -> 우클릭 이벤트 추가 -> OnComponentBeginOverlap
3. 객체를 소멸시키는 DestroyActor 함수 호출 -> 타깃: Self 

> Scene 컴포넌트가 Root가 되도록 해야 한다.

***좌표계를 가지기 위해선 Scene 컴포넌트를 상속해야 함***
> Transform 정보를 가지고있음 


### 조건 분기

> 태그를 확인하여 동작 여부 판단

1. 디테일 -> Actor -> Tags -> "Player" 태그 추가
2. Actor Has Tag 함수 호출 -> OnComponentBeginOverlap의 other Actor를 타깃에 연결
3. branch 노드 생성 -> Actor Has Tag의 return을 Branch의 Condition에 연결
    > true/false를 구분하여 노드 연결 가능
4. OnComponentBeginOverlap -> Branch -> DestroyActor 연결

















