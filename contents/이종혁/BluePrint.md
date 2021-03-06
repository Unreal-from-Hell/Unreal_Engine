# Blue Print 
> 게임 스크립트 언어 

## 액터 이동 방법


### 액터란
* 게임 공간에 배치된 객체 
* 게임 세계에 배치할 수 있는 모든 것(좌표를 가짐)

###  액터의 모빌리티 프로퍼티(Mobility Property) 
액터를 게임 플레이 도중 어떤 방식으로 이동 또는 변화할 수 있도록 할지를 제어
> 빛과 그림자의 실시간 계산의 부하를 줄이기 위함

* 스태틱(Static): 게임 플레이 도중 어떤 식으로든 이동 또는 변할 수 없는 액터
* 스테이셔너리(Stationary): 게임 플레이 도중 이동하지는 못하지만 변할 수 있는 액터
* 무버블(Movable): 게임 플레이 도중 추가, 제거, 이동해야하는 액터

> 디폴트는 스태틱, 특별한 경우만 무버블로 하자

## 액터를 움직이는 여러가지 방법

### 1. 좌표를 매 프레임마다 변경해서 움직이기
* 가장 기본적이고 원시적인 방법
* 틱 이벤트(Tick Event) 사용
* 움직임이 복잡해지면 한계가 많음


### 2. 이동 컴포넌트에 파라미터를 전달해서 움직이기 
UE4에서 이동 컴포넌트(Movement Component)를 사용
* CharacterMovemnet: 캐릭터 이동 전용 컴포넌트
> 부모클래스인 Character에 포함되어 있음
* RotatingMovement: 회전 관련 컴포넌트
* ProjectileMovement: 발사체 관련 컴포넌트

### 3. 시퀀서로 결정한 좌표로 변경해서 움직이기 (시간의 흐름에 따라 key frame만 명시)
* 타임라인에서 특정 시간 위치에 키 프레임(Key Frame)을 배치함 중간의 위치와 방향은 자동 보정됨
* 정해진 애니메이션의 구현에 편리함
* UE4에서 정해진 시퀀스 기반으로 움직이기 위한 마티네(Matinee)와 타임라인(Timeline) 기능을 제공
> * 마티네: 에디터에서 컷신(시네마틱 영상)을 생성하고 재생하기 위한 구조
> * 타임라인: 키 프레임을 사용해 벡터와 스칼라 값을 변경해주는 기능


### 4. 물리 엔진을 사용해서 움직이기 
* 게임 객체에 물리 파라미터를 지정하고, 이를 기반으로 물리 엔진이 모든 제어를 처리하는 방법
> 이동 컴포넌트와의 차이점: 이동 컴포넌트는 게임 물리(게임 관련 활용이 편리), 물리엔진은 현실 물리(예측이 힘듦)

* 장점: 파라미터가 많이 필요하지 않고 편리하게 사용 가능
* 단점: 제거나 예측이 어려움
* UE4에서는 엔비디아의 PhysX가 통합되어 있다




## 블루프린트 스크립트의 기본


### 레벨 블루프린트
* 맵과 함께 저장됨
* 맵에 있는 액터에 쉽게 접근할 수 있음
* 스크립트 재사용 불가


### 레벨 블루프린트 열기 
> 블루프린트 -> 레벨 블루프린트 열기


### Hello world 출력하기
* BeginPlayEvent: 시작시 한 번만 발생
* PrintSting: 문자열 출력 노드 
> BeginPlayEvent의 실행 핀을 PrintString 노드에 연결




### 액터의 위치 추출하기
* TickEvent: 매 frame 마다 발생
* GetActorLocation: 액터의 현재 위치(벡터) 추출 노드
> 액터 선택 후 액터에 대한 레퍼런스(reference) 생성 -> GetActorLocation 함수 호출




### 액터 움직이기
* Vector 자료형, Vector 연산
* SetActorLocation: 액터 위치 지정 노드
> 벡터 연산 노드를 통해 SetActorLocation의 New Location에 연결

***움직이기 위해선 객체의 Mobility를 Movable로 해주기***




## 클래스 블루프린트


### 맵에 있는 액터를 클래스 블루프린트로 변환하는 방법
> 디테일 -> 블루프린트/스크립트 추가

* 액터 이동하기는 레벨 블루프린트에서와 동일하다

***클래스 블루프린트로 만들면 어떤 월드에 배치하더라도 해당 Action을 재사용할 수 있음***


## 하드웨어 입력 개요


### 입력 이벤트

디지털 입력 이벤트
* 누른 상태(on)와 누르지 않은 상태(off)의 두 가지 상태만 존재
* 키보드, 게임패드, 마우스 등

아날로그축 입력 이벤트
* 입력값이 여러 단계로 이루어져 있음
* 마우스의 이동 거리, 게임패드의 아날로그 스택 등
* 대부분 float 타입으로 입력의 정도를 표현
* 음수를 사용하여 반대 방향 입력
* 게임패드 트리거 입력: 양수만 존재


## pawn과 controller 


### Pawn
> Controller에 의해서 조작되는 액터

조작자: Controller라는 액터로 표현
* 사람 플레이어 또는 컴퓨터 플레이어(AI)


입력 이벤트 처리
* 일반적인 방법: Controller에서 H/W입력을 받고 이를 Pawn에 반영


### 카메라 회전

SpringArm 카메라 설정 값 Use Pawn Control Rotation 체크
> Controller의 회전 값으로 SpringArm을 회전시킴
> * 카메라가 항상 캐릭터 등을 바라보게 된다


## 입력 매핑

### 매핑
플레이어의 하드웨어 입력을 액터가 이해하고 활용할 수 있는 형태의 데이터로 변한
* 친근한 이름으로 매핑시킴

### 종류

액션 매핑: 디지털 입력 이벤트
* 점프, 슈팅, 오브젝트 상호작용 등 별도의 동작


축 매핑: 아날로그 축 입력 이벤트
* 걷기, 둘러보기, 탈것의 조향처럼 세기나 방향이 있는 것들


### 노드 명칭

액션 입력 이벤트, 축 입력 이벤트
* 카테고리: 입력 -> 액션 이벤트, 축 이벤트
> 표시: 입력 액션, 입력 축




### 위치
> 프로젝트 세팅 -> 엔진 -> 입력 -> 바인딩 -> 액션 매핑, 축 매핑



### 이동 이벤트 구현

1. 캐릭터 움직임
축 이벤트 노드 배치 -> Add Movement Input 노드에 연결
* MoveForward, MoveRight 입력 축 이벤트 

2. 이동속도 
Sprint 입력 액션 노드 배치 -> Character Movement 노드 -> Set Max Walk Speed의 타깃 선택 
* Sprint 입력 액션의 Pressed -> 스피드 증가, Released -> 원래 스피드로 복귀에 연결



### 카메라 움직임 구현

1. 위 아래 보기: LookUp 이벤트 입력 축 -> Add Controller Pitch Input에 연결

2. 좌우 보기: LookRight 이벤트 입력 축 -> Add Controller Yaw Input에 연결 

> SpringArm의 카메라 세팅의 Use Pawn Control Rotation 체크 



### MoveForward, MoveRight에
카메라 노드 -> Get Forward Vector의 타깃에 연결 -> Add MoveMent Input의 World Direction에 연결



### Camera Manager 생성 
PlayerController -> Player Camera Manager Class 의 + 선택하여 블루프린트 클래스 생성
> View Min, Max 제한 


## 메시


### 스켈레탈 메시와 캐릭터
> 뼈 구조를 가진 FBX 파일을 통해 캐릭터의 외형 변경 


### 스태틱 메시
 * 외형만 디자인


### 스켈레탈 메시 (스킨 메시)
* 관절(joint)를 사용하여 캐릭터 포즈를 결정하도록 디자인
> 관절(joint), 뼈(bone)


### 파일 포맷: FBX
> Maya, 3dsMax, Blender 등에서 제작하여 FBX 포맷으로 저장
> * import 시에 특별히 신경 쓸 필요 없이 축 문제 등이 거의 없다



## 메시 에디터 

스태틱 메시: 스태틱 메시 에디터

스켈레탈 메시: 에니메이션 에디터


### 애니메이션 에디터
* 스켈레톤 에디터
> 뼈대 구조를 편집

* 스켈레탈 메시 에디터
* 애니메이션 에디터
* 애니메이션 블루프린트 에디터
> 애니메이션의 동작을 블루프린트로 관리

* 피직스 데이터 
> 스켈레탈 메시의 콜리전 물리 등을 관리




## 스켈레탈 메시의 콜리전

### 콜리전

스태틱 메시
* 변형되지 않으므로 미리 만들어 놓을 수 있다
* 전체를 하나의 캡슐/박스 콜리전으로 만들 수 있음

스켈레탈 메시
* 메시가 변형되므로 콜리전을 미리 만들어 둘 수 없음
* 스켈레톤의 관절과 관절 사이에 캡슐 박스 콜리전을 추가해 애니메이션과 함께 움직이도록 함
> 이러한 애니메이션 대응 콜리전 데이터를 피직스 애셋(Physics Assest)이라고 함 

### 피직스 애셋
* 언리얼 에디터에서 작업해야 함
* 피직스 애셋은 필수가 아닌 선택
> CharacterMovement 컴포넌트: 캡슐을 사용해 지형과 접촉을 판정함

* 정교함이 필요한 경우에는 사용하는 것이 좋음
> 격투게임의 발차기 같은 경우 콜리전이 더 정교해야 함

***따라서, 콜리전 조합(지형 콜리전용 캡슐 콜리전 + 캐릭터 콜리전용 데이터)으로 운용하자***




### 피직스 애셋 생성

스켈레탈 메시 우클릭 -> 스켈레탈 메시 액션 -> 생성 -> 피직스 애셋 -> 생성
> 스켈레탈 메시 에디터에서 피직스를 연결








