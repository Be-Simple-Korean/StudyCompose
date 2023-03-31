# Check list

* UI 상태 생성
    * 앱이 데이터 영역에 액세스하고 필요한 경우 비즈니스 규칙을 적용하며 UI에서 사용하는 UI 상태를 노출하는 프로세스
    * StateFlow API (UI 상태 생성 API)
        * MutableStateFlow로 변경 가능한 변수 생성, StateFlow로 읽기 전용 변수를 생성함으로써
          ViewModel을 통해서만 UI 상태를 수정할 수 있도록 설계
        * asStateFlow() = 변경 불가능한 flow로 만들기
        * init()으로 초기값 설정
        * 상태가 변경될때 UI를 업데이트 시켜주려면 collectAsStateWithLifeCycle() 추가
            * collectAsStateWithLifeCycle()
                * liftcycle.runtime.compose 종속성 추가
                * StateFlow에서 값을 수집하고 State API를 통해 최신 값을 표시
              ~~~ 
               by viewmodel.{StateFlow instance}.collectAsStateWithLifeCycle()
               ~~~
* 코루틴(Coroutine)
    * 안드로이드에서 비동기 작업을 수행하는데 권장되는 방법
    * 백그라운드에서 항목을 로드할때 코루틴 사용
* Compose의 부작용
    * 구성 가능한 함수의 범위 밖에서 발생하는 앱 상태에 관한 변경사항 = '부수 효과'
    * 일회성 이벤트(스낵바,화면 이동)에는 필요
* 앱 상태를 변경해야 하는 경우 부수 효과가 예측 가능한 방식으로 실행되도록 Effect API 사용이 필요
* Effect API
    * UI를 내보내지 않고, 컴포지션이 완료될 때 부수 효과 실행
    * LaunchedEffect
        * 컴포저블 범위내에서 정지 함수를 실행
        * 컴포지션 시작시 코루틴이 실행됨 / 종료시 코루틴이 취소됨.
        * 다양한 키를 매개변수로 받아 키중 하나가 변경되면 효과를 다시 시작
        * 한번만 트리거(사용)하려면 상수를 키로 사용
          ~~~ 
          LaunchedEffect(true){} 
          ~~~
        * rememberUpdatedState
            * 값이 들어올때마다 새로운 value값을 remember된 mutableState에 직접 apply 해줌
            * 상위 컴포저블 데이터가 바뀔때 하위에도 적용되야한다면 이를 사용
* ScaffoldState
  * DrawerState를 포함 -> 프로그래매틱 방식으로 open(), close()가 됨
    * open(), close()은 정지함수이기 때문에 코루틴 내에서 호출되어야 함.
      * 정지함수는 기본스레드에서 호출하기때문에 안전해야한다.
    * openDrawer()가 컴포저블 외부이기 때문에 코루틴을 실행하려면 rememberCoroutineScope() 사용 해야 함. 
* rememberCoroutineScope API
  * 컴포저블의 생명주기를 따르는 코루틴 스코프를 반환
* rememberSaveable
  * Saver를 직접 구현하고 커스텀하게 저장하는 로직 구현이 가능
  * Saver로 클래스의 인스턴스를 저장 및 복원하는 방법을 rememberSaveable에 알림
  * Saver는 객체를 Saveable 상태로 변환
  * Saver
    * save() = 원래 값을 저장 가능한 값으로 변환
    * restore() = 복원된 값을 원본 클래스의 인스턴스로 반환
    * Compose API 중 listSaver, mapSaver를 사용하여 코드의 양을 줄일 수 있음
* snapshowFlow API지
  * State 객체를 Flow 객체로 변환 
    * 데이터가 여러 개 일때, flow로 변환하여 filter를 거쳐 collect에서 수집후 처리
* LifecycleEventObsever
  * 모든 수명 주기 변경을 수신하고 수신자에게 디스패치할 수 있는 클래스
  * 구성 가능한 함수가 아닌 뷰에 액티비티의 수명 주기를 따르게 하기 위한 클래스
* DisposableEffect 
  * 키가 변경되거나 컴포저블이 컴포지션을 종료하면 정리되어야 하는 부작용을 위한 것
  * LocalLifeCycleOwner로 현재 lifecycle을 추가 
  * DisposableEffect에 매개변수로 넘긴 key중에 변경이 발생하면 key를 사용하여 관찰자를 onDispose 람다로 삭제하고 다시 추가
  * 이를 통해 메모리 누수 방지
* produceState
  * 컴포즈가 아닌 상태를 컴포즈 상태로 변환
  * 상태에 따른 분기처리
* derivedStateOf API
  * paramter로 넘긴 항목이 변경되면 상태가 변경된다.
