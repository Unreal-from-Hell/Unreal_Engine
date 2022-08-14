# Unreal C++ Game Project 
> Unreal5 C++ 학습을 위한 게임 프로젝트

# 패치노트
- 08.14  
캐릭터 추가  
캐릭터 걷기 및 뛰기 추가

# 코드 
>08.14
- 캐릭터 코드
```c++
// Fill out your copyright notice in the Description page of Project Settings.
#include "MyCharacter.h"

// Sets default values
AMyCharacter::AMyCharacter()
{
	PrimaryActorTick.bCanEverTick = true;
}

// Called when the game starts or when spawned
void AMyCharacter::BeginPlay()
{
	Super::BeginPlay();
}

// Called every frame
void AMyCharacter::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}

// 이 부분이 캐릭터의 입력값을 받는 부분
void AMyCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

	PlayerInputComponent->BindAxis(TEXT("MoveFB") , this ,&AMyCharacter::MoveForWard);
	PlayerInputComponent->BindAxis(TEXT("MoveRL") , this ,&AMyCharacter::MoveRight);
}

void AMyCharacter::MoveForWard(float axisvalue)
{
	if(axisvalue == 0 )
		return;
	
	FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);
	AddMovementInput(Direction, axisvalue);
	
}

void AMyCharacter::MoveRight(float axisvalue)
{
	if(axisvalue == 0)
		return;
	
	FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);
	Controller->GetPawn()->AddMovementInput(Direction, axisvalue);
}
```

<br>
<img src='./Images/Game_Idle.png' width=400/>
<img src='./Images/Game_Run.png' width=400/>
<br>