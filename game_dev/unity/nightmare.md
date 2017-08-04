### 플레이어 이동 설정

- 움직임
- 회전
- 애니메이션 설정

#### moving
```Csharp
	void Move(float h, float v) {

		Vector3 movement = new Vector3 (h, 0f, v).normalized * playerSpeed * Time.deltaTime;
		playerRigidbody.MovePosition (transform.position + movement);

	}
```

#### rotation
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
```

#### animation
```Csharp
	void Animating(float h, float v) {

		bool isMoving = (h != 0f || v != 0f);

		anim.SetBool ("IsMoving", isMoving);
	
	}
```

#### entire source code

```PlayerMovement.cs
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
	public float playerSpeed;

	Animator anim;
	Rigidbody playerRigidbody;

	float camRayLength;		//카메라에서 발사하는 광선의 길이(레이캐스트)
	int floorMask;			//quad와 카메라 레이캐스트의 충돌만 판정할 것이므로 quad의 레이어마스크 정보를 참조할때 쓴다.

	void Awake() {
		
		anim = GetComponent <Animator> ();
		playerRigidbody = GetComponent <Rigidbody> ();
		camRayLength = 100f;
		floorMask = LayerMask.GetMask ("Floor");
	}

	void FixedUpdate() {

		float h = Input.GetAxisRaw ("Horizontal");
		float v = Input.GetAxisRaw ("Vertical");
		WalkingProcess (h, v);
	
	}

	void WalkingProcess(float h, float v) {

		Animating (h, v);
		Move (h, v);
		Turn ();

	}

	void Move(float h, float v) {

		Vector3 movement = new Vector3 (h, 0f, v).normalized * playerSpeed * Time.deltaTime;
		playerRigidbody.MovePosition (transform.position + movement);

	}
		
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

}
```


### 카메라 설정

- target 설정
- 카메라와 타겟 사이의 오프셋(움직일 위치) 구하기
- 카메라 움직임 부드러움 정도 설정
- 각종 참조 설정해주고
- 매 프레임마다 카메라의 현재위치, 움직일 위치를 계산하고 Vector3.Lerp(cur, new, smoothing)함수를 이용해서 움직여준다

```CameraFollow.cs

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraFollow : MonoBehaviour {

    public Transform target;

    float smoothing;

    Vector3 offset;

    void Start() {

        offset = this.GetComponent <Transform>().position - target.position;

        smoothing = 5 * Time.deltaTime;

    }

    void FixedUpdate() {

        Vector3 newCamPosition = (target.position + offset);

        this.GetComponent <Transform>().position = Vector3.Lerp (this.GetComponent <Transform>().position, newCamPosition, smoothing);

    }

}
```

### 적 설정

- 애니메이션 설정
- 콜라이더 트리거 설정
- 네비게이션 설정
 
#### 네비게이션
- 주어진 환경속에서 물체를 피하거나 가로지르면서 길찾기

- 네비게이션: 레벨설정 가능(zombunny 설정 -> 네비게이션 레벨 설정 순서로 진행)
- nav mesh: 베이킹이라는 프로세스를 수행해서, 레벨의 어떤 부분을 탐색할 수 있는지 지정
- nav mash agent: 위의 환경 안에서, 이동하거나 가로질러 가는 컴포넌트 
- 정적 물체들을 계산해서, 단순화한 AI 경로를 도출해냄. 정적 오브젝트를 옮기는 경우에는, 베이킹을 다시 수행해 주어야 한다. 

### Canvas
- Health UI
- shift: pivot을 결정
- alt: position을 결정
