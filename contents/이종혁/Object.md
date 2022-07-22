# 객체의 생성과 소멸

### 객체

1. 정적 객체
> 한 번 맵에 배치되면 움직임이 없는 객체

2. 동적 객체
> 동적으로 생성되었다가 소멸되는 객체
> * ex) 스폰(spawn), 리스폰(respawn)

### 스폰(spawn)
> 액터를 생성하는 것

* Locator를 사용하여 위치 좌표를 설정해주어야 한다


### Locator
> 마우스로 움직여 조정할 수 있다

* 스폰 지점, 이동 중계 지점 등 위치 정보를 제공하는 등의 다양한 기능
* TargetPoint, PlyaerStart 액터 등에 사용할 수 있다
> TargetPoint: 액터를 스폰할 위치를 지정할 때 사용 

<br>

### 액터 스폰하기
* SpawnActor를 이용
* Class, SpawnTransform을 지정해주어야 한다
* GetActorTransform을 이용하여 액터의 transform 추출 가능

> Class: 생성할 액터 타입   
> Transform: transform matrix로 Location, Rotation, Scale을 포함한다

<br>

### 액터의 소멸
> 필요 없는 액터들은 자원을 낭비하지 않도록 제거해야 한다.

1. Destroy Actor
* 총알이 벽에 맞으면 총알 액터를 제거
* 벽에 맞지 않고 날아간다면 ? -> 언젠가 제거 되어야 함

2. Lifespan(수명) property
* 액터에 있는 lifespan property에 시간을 설정
> 설정된 시간이 지나면 자동으로 소멸된다, defalut = 0 (수명 없음)

* 표창, 총알 등 공간을 날아다니는 액터에는 꼭 설정하기
* 깨진 물체, 시체, 래그돌 등에서 설정하기
> 게임에서 더 이상 기능을 상실하게 되면 특정 시간 후에는 사라지게 하는 것이 좋다

3. Kill Z property
* `월드 세팅` 패널에서 맵 마다 설정하는 property
* 설정한 z 위치보다 아래로 내려간 액터를 소멸시킴
    > 무한 낙하 방지 용도, defalut = -10km 


<br>

### Pawn의 리스폰

* Pawn이 소멸되어도 Playercontroller는 사라지지 않고 연결만 절단된다(Unpossess)
    > Pawn이 리스폰 되었을 때 Playercontroller를 다시 연결해주어야 함(Possess)

***하나의 controller는 하나의 pawn만 소유(possess)할 수 있다.***
    > 다른 pawn을 소유하고 싶으면 기존의 pawn을 unpossess한 이후에 가능하다

<br>

### 이벤트 바인딩(call back)
> 아직 발생하지 않은 사건에 대해서 이벤트를 적용하는 방법

<br>

### 흐름 제어 노드

1. DoOnce
> 최초 한 번만 실행하도록 하는 노드


2. Sequence
> 실행 핀에 연결된 노드를 순차적으로 실행하도록 하는 노드




