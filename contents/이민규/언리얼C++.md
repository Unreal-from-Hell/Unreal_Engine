# 언리얼 C++ 정리

## virtual 함수
- BeginPlay : 게임이 시작되거나 스폰되었을 때 한번만 호출되는 함수  
- Tick : 액터가 활성화 되어 있는 동안 계속해서 호출 -> PrimaryActorTick.bCanEverTick로 활성화 여부 결정  
- PostInitProperties : 오브젝트에서 변수가 초기화될 때 호출되는 함수  
- PostEditChangeProperty : 변수가 수정될 때 호출되는 함수  
- SetUpPlayerInputComponent : 플레이어의 입력을 받는 함수 -> BindAxis(매핑명칭 , this , 발동할함수) , BindAction(매핑명칭 , 입력결정 , this , 발동할함수)

## 함수
- CreateDefaultSubobject<클래스>(TEXT("사용할 이름")) : C++의 New와 동일
- GetActorLocation : 현재 액터의 위치값을 가져옴
- SetActorLocation : 액터의 위치값 수정
- SetupAttachment(나의 루트이름) : 나의 루트 밑으로 상속되는 함수
- AddMovementInput(방향 , 이동값) : 액터 위치 업데이트
- GetActorForwardVector() : 엑터가 향하는 방향기준 x축 상의 좌표를 벡터로 반환
- GetActorActorRightVector() : 엑터가 향하는 방향기준 y축 상의 좌표를 벡터로 반환
- GetActorUpVector() : 액터가 향하는 방향기준 z축 상의 좌표를 벡터로 반환
- FRotationMatrix.GetScaledAxis(EAxis::X or Y or Z) : 행렬에서 이동 행렬을 뺀 순수하게 회전에 대한 행렬이면서 FVector로 반환

## 변수
- FRotationMatrix : 행렬 컨테이너
- FVector : X, Y, Z으로 구성된 3차원 공간의 벡터입니다.(자료구조 Vector아님!)
- FRotator : pitch : Y Roll : X Yaw : Z로 구성된 회전을 위한 컨테이너

## 매크로
- UE_LOG(LogTemp , 경고난이도 , TEXT) : 출력로그를 출력할수있음(Fatal , Error , Warning , Dispaly)
- UPROPERTY() -> 언리얼 변수 설정 지정을 위해 필요한 매크로  
EditAnyWhere : 블루프린트 원본과 레벨에 배치된 양쪽 모두에서 편집가능  
VisibleAnyWhere : 프로퍼티창에서 보이지만 편집은 불가능  
BlueprintReadWrite : 블루프린트에서 읽기와 수정이 모두가능  
BlueprintReadOnly : 블루프린트에서 읽기만 가능  
Transient : 프로퍼티가 휘발성 프로퍼티로 저장되지 않음  
Category : 편집툴, 패널 에서 프로퍼티를 카테고리로 묶어서 보여줌  
Edit/visible -> 편집 or 보기만  
Defaults/Instance : 클래스설계도 or 인스턴스에서만

- UFUNCTION() -> 언리얼 함수 설정 지정을 위해 필요한 매크로  
BlueprintCallable : 블루프린트에서도 사용 가능   
BlueprintImplementableEvent  : 블루프린트에서 이벤트 설정가능  
BlueprintNativeEvent  : C++과 블루프린트 협동으로 이벤트 가능  
Category : 필수

## 입력방식
- Action : 눌렀다가 때는 방식은의 간단한 것(한번)
- Axis : 마우스 같이 연속적인 값(계속)

## 컴포넌트
- 캡슐 컴포넌트(class UCapsuleComponen) : 인간형 폰의 충돌과 이동을 관리하는 루트 컴포넌트입니다. 
- 스켈레탈 메시 컴포넌트(class USkeletalMeshComponent) : 인간형 폰의 비주얼을 담당하는 컴포넌트입니다.
- 화살 컴포넌트(class UArrowComponent) : 편집을 위해 시선 방향을 가리키는 컴포넌트입니다. 
- 카메라 컴포넌트(class UCameraComponent) : 폰에 빙의한 플레이어의 화면을 렌더링할 카메라 컴포넌트입니다
- 스프링암 컴포넌트(class USpringArmComponent) : 카메라 구도를 쉽게 세팅할 수 있게 제공하는 컴포넌트입니다(삼각대라고 생각하면 편함)

## 딜리게이트
- 함수 포인터의 직접 접근이 아닌 대리자를 통한 함수 호출 방식 
호출할 함수나 이를 포함하는 객체가 없어져도 대리자가 체크해 안전하게 처리할 수 있음. 
동일한 형을 가진 함수 여러 개를 대리자가 묶어서 관리하고, 필요할 때 동시에 모두 호출하는 것이 가능함.
DECLARE_DELEGATE_

## 직렬화
- FArchive : 언리얼엔진에서 사용하는 직렬화