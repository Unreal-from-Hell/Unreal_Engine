# 언리얼 C++ 정리

## virtual 함수
- BeginPlay : 게임이 시작되거나 스폰되었을 때 한번만 호출되는 함수  
- Tick : 액터가 활성화 되어 있는 동안 계속해서 호출 -> PrimaryActorTick.bCanEverTick로 활성화 여부 결정
- PlayerTick : PlayerController의 Tick 함수  DeltaTime 인자를 통해 현재 틱에서 다음틱으로 넘어간 시간이 측정 가능
- PostInitProperties : 오브젝트에서 변수가 초기화될 때 호출되는 함수  
- PostEditChangeProperty : 변수가 수정될 때 호출되는 함수  
- SetUpPlayerInputComponent : 플레이어의 입력을 받는 함수 -> BindAxis(매핑명칭 , this , 발동할함수) , BindAction(매핑명칭 , 입력결정 , this , 발동할함수)
- GetCapusleComponent : 캡슐을 불러오는 함수
->InitCapsuleSize(넓이 , 높이)
- ACharacter::Jump : 캐릭터 위로 뛰는 함수
- ACharacter::StopJumping : 캐릭터의 점프가 멈추는 함수

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
- bStartWithTickEnabled : 생성자에서만 호출해야하며 원하는 시점에 Tick을 활성화 할 수 있도록 하는 함수
- UKismetMathLibrary::Vsize : 벡터의 길이를 반환

## 변수
- FRotationMatrix : 행렬 컨테이너
- FVector : X, Y, Z으로 구성된 3차원 공간의 벡터입니다.(자료구조 Vector아님!)
->GetSafeNormal : 벡터의 정규화(단위벡터)된 복사본을 가져와 길이에 따라 안전한지 확인합니다. 벡터 길이가 너무 작아 안전하게 정규화할 수 없는 경우 기본적으로 0 벡터를 반환합니다.
- FRotator : Roll : X pitch : Y  Yaw : Z로 구성된 회전을 위한 컨테이너
- FHitResult : 충돌 지점(point of impact) 및 해당 point의 표면(surface) normal과 같은 trace의 한 번의 hit 정보를 포함하는 구조체입니다.

## 매크로
- UE_LOG(LogTemp , 경고난이도 , TEXT) : 출력로그를 출력할수있음(Fatal , Error , Warning , Dispaly)
- UPROPERTY() : 언리얼 변수 설정 지정을 위해 필요한 매크로  
EditAnyWhere : 블루프린트 원본과 레벨에 배치된 양쪽 모두에서 편집가능  
VisibleAnyWhere : 프로퍼티창에서 보이지만 편집은 불가능  
BlueprintReadWrite : 블루프린트에서 읽기와 수정이 모두가능  
BlueprintReadOnly : 블루프린트에서 읽기만 가능  
Edit/visible : 편집 or 보기만  
Defaults/Instance : 클래스설계도 or 인스턴스에서만  
Transient : 프로퍼티가 휘발성 프로퍼티로 저장되지 않음  
Category : 편집툴, 패널 에서 프로퍼티를 카테고리로 묶어서 보여줌 -> Category = "ABC | DEF  일 경우 ABC 하위의 DEF로됨
meta : metadata라고 하며 에디터 관련 다양한 기능을 구현할 수 있음  
->(AllowPrivateAccess = "true") : private일 경우 에디터에서 보이지않지만 AllowPrivateAccess를 true로 할경우 보임  
->UIMin / UIMax : 에디터에서 조정할 수 있는 숫자 범위 지정 명령어  
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
->Attach 할때 SpringArmComponent::SocketName을 넣어줘야 스프링암 소켓에 붙어짐  
->bUsePawnControlRotation : 캐릭터의 컨트롤러의 회전을 따라 갈지 설정 
->bDoCollisionTest : 카메라가 벽을 뚫지 않게 만드는 옵션
- 액터 컴포턴트 (class UActorComponent) : Actor에 추가할 수 있는 재사용 가능한 동작을 정의하는 구성 요소의 기본 클래스입니다.
->GetVelocity : 속도를 벡터로 반환
- 캐릭터 컴포넌트 (class ACharacter) : 폰 컴포넌트에서 충돌 방향 매쉬 같은 것을 추가적으로 가진 클래스 입니다.
->PlayAnimMontage : 몽타주를 실행시켜주는 함수
- 캐릭터 무브먼트 컴포넌트(class UCharacterMovementComponent) : 서브 오브젝트로 달린 액터 (또는 캐릭터)에 일정한 형태의 이동을 제공합니다  
->orientRotationtoMovement : 캐릭터가 가속되고 있는 방향으로 회전  
->bUseControllerRotation(roll,pitch,yaw) : 폰이 컨트롤러의 pitch yaw roll을 가져갈지 결정  
->BrakingDecelerationWalking : 미끄러짐 방지 설정  
->IsFalling : 캐릭터가 공중에 있는지 확인 하는 함수
->GetCurrentAcceleration : 캐릭터의 가속도를 얻는함수
- 플레이어 컨트롤러 컴포넌트(class APlayerController) : Pawn과 그것을 제어하려는 사람 사이의 인터페이스로서, 플레이어의 의지를 대변하는 클래스이다  
->bShowMouseCursor : 게임 내에서 마우스가 보일지 결정 옵션  
->DefaultMouseCursor = EMouseCursor::(Default) : 마우스 커서를 설정하는 함수  
->StopMovement : 컨트롤러가 현재 수행중인 이동을 중단하는 함수  
-> GetHitResultUnderCursor(ECC , trace , HitResult) : 마우스 커서 위치에 트레이스를 쏴서 그 결과를 가져오는 함수 
ECC 검색 후 추가예정

## 딜리게이트
- 함수 포인터의 직접 접근이 아닌 대리자를 통한 함수 호출 방식 
호출할 함수나 이를 포함하는 객체가 없어져도 대리자가 체크해 안전하게 처리할 수 있음. 
동일한 형을 가진 함수 여러 개를 대리자가 묶어서 관리하고, 필요할 때 동시에 모두 호출하는 것이 가능함.
DECLARE_DELEGATE_

## 직렬화
- FArchive : 언리얼엔진에서 사용하는 직렬화

## 애니메이션 블루프린트
- 스테이트에일리어스 : 스테이트 에일리어스에 체크 되어 있는 스테이트에서 애니메이션을 진행중이여도 조건에 만족하면 해당 스테이트에일리어스 즉시 발동이됨
- 블랜드스페이스 : 여러개의 에니메이션을 섞을 수 있으며 다양한 변수를 지정해 변수에 맞게 설정이 가능\
- 애디티브 :  애니메이션 간의 차이를 계산하여 만들어지는 애니메이션을 말한다.
- 몽타주 : 나의 애셋에 들어있는 애니메이션을 합쳐 선택적으로 재생할 수 있도록 해주는 유연한 툴입니다
- 슬롯 : 애니메이션을 목적에 맞게 사용할 수 있는 노드 upper 같은 경우는 상단의 애니메이션만 사용

## AI
- AI 언리얼에서 사용하기 위해 : Build.cs 파일에 "NavigationSystem", "AIModule", "Niagara"를 추가해야함
- UAIBlueprintHelperLibrary::SimpleMoveToLocation(controller , Location)  : Location 방향으로 폰을 자동으로 이동시켜주는 함수 

## 나이아가라
- UNiagaraFunctionLibrary::SpawnSystemAtLocation : 해당위치에 나이아가라를 생성해주는 함수