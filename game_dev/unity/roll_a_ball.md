### 기본 내용 정리

- Update: 프레임을 렌더링 하기 전에 호출됨

- FixedUpdate: 물리 효과 계산을 수행하기 직전에 호출됨

- LateUpdate: 추적 카메라, 절차 애니메이션, 마지막으로 알려진 상태의 수집 등을 위해 가장 좋은 함수(update에서 모든 아이템들이 처리된 후에 이 함수가 처리됨)

- Rigidbody와 Collider가 포함된 게임 오브젝트는 동적인 것으로 간주됨 / 정적인 오브젝트를 움직였을때에는 유니티 엔진에서 모든 정적 오브젝트의 위치를 다시 계산해서 캐시에 담는데, 이는 리소스 소모가 심함. 큐브에 Rigidbody 컴포넌트가 없으므로 정적 오브젝트인데 회전을 시키고 있다..  rigidbody 컴포넌트를 추가해 줌으로써 최적화 수행

- kinematic 옵션: 물리력에 반응하지 않도록 설정하는 옵션.. Transform을 이용해서 이동, 회전 등을 수행하는건 여전히 가능

- collider: 물체간의 충돌에 관여. trigger로 설정해두면 충돌은 하지 않지만 겹치는지에 대한 판단을 해줄 수 있다
- rigidbody: 물체에 물리법칙을 적용or해제할때 사용

- 정적 오브젝트가 움직여서는 안됨
- 동적 오브젝트는 collider, rigidbody 둘다 갖고있음
- 표준 rigidbody는 물리력을 이용해서 움직임
- 키네마틱 rigidbody는 transform을 이용해서 움직임


### UI
- canvas 자식으로 배치됨.
- UI 오브젝트의 transform은 보통 게임 오브젝트의 transform과 다르게, Rect Transform 형태임.
