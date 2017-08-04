### 환경설정하기
- quad 설정.. layer floor로(카메라로부터 raycast를 사용할 것이고, 이때 이 바닥만 점검하게 할것이기 때문에)
- Lights 설정
- backgroundMusic 설정


### 게임 케릭터
- model 설정
- GetAxis vs GetRawAxis: 
- GetAxis는 -1 ~ 1 사이의 값 중 하나를 반환.
- GetRawAxi는 -1, 0, 1 세개의 값 중 하나만 반환.

- Turning, Animating 소스코드 확인하기
```Csharp
void Turn() {

    Ray camRay = Camera.main.ScreenPointToRay (Input.mousePosition);

    RaycastHit floorHit;

    if (Physics.Raycast (camRay, out floorHit, camRayLength, floorMask)) {

        Vector3 playerToMouse = floorHit.point - transform.position;

        playerToMouse.y = 0f;

        Quaternion newRotation = Quaternion.LookRotation (playerToMouse);

        playerRigidbody.MoveRotation (newRotation);

    }

}

void Animating(float h, float v) {

    bool isMoving = (h != 0f || v != 0f);

    anim.SetBool ("IsMoving", isMoving);

}
```


#### 애니메이션 설정
- Asset 하위 디렉터리에 Animation디렉터리 생성
- Animation 디렉터리에 Animator Controller 생성
- 사용될 애니메이션들을 컨트롤러에 추가해준다
- parameter를 통해서 애니메이션간의 전환을 설정


#### 씬에서 물리적 존재감 부여하기

##### rigidboy
- player에 add component physics > rigidbody(강체) 컴포넌트 추가
- 시간이 지나도 느려지지 않도록 해야하므로 Drag, Angular Drag infinity로 설정
- Constrains를 사용해서 플레이어 케릭터가 방향이 바뀌더라도 앞으로 쓰러지거나 굴러 떨어지지 않도록설정.
- y position을 고정해서 점프하거나 바닥 아래로 가라앉지 못하도록 설정
- x, z rotation을 고정해서 케릭터가 y축으로만 돌아볼 수 있도록 설정

##### Collider
- add component physics > Capsule Collider 추가해서 충돌을 감지할 수 있도록

### 스크립트 설정
```C#

```
