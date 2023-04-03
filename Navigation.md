# Compose Navigation

* 종속성 추가
  ~~~
  implementation "androidx.navigation:navigation-compose:{latest_version}"
  ~~~
* Navigation의 3요소
    * NavController
        * 항상 단일 NavHost 컴포저블에 연결
        * Compose에서 탐색을 사용할 때 중심이 되는 구성요소
        * 백스택 컴포저블 항목을 추적 / 스택 이동 / 백 스택 조작 사용 설정 / 대상 상태 간에 이동
        * rememberNavController()를 통해 인스턴스 생성
        * 항상 계층 구조 최상위 수준에서 만들고 배치 -> 모든 컴포저블이 액세스 하기 위해 = 상태 호이스팅
        * NavHost
            * 컨테이너 역할
            * 그래프의 현재 대상을 표시
            * 컴포저블 이동 시 NavHost의 콘텐츠가 자동으로 재구성
            * NavController를 이동 가능한 컴포저블 대상을 매핑하는 NavGraph에 연결
            * 가져올 수 있는 대상의 모음
            * NavGraph
                * 대상 추가하기
                    * NavHost의 후행람다로 연결될 컴포저블들을 composable() 확장 함수를 통해 추가
                  ~~~
                  NavHost(
                   navController = navController,
                  startDestination = Overview.route // 시작 경로
                  ){
                   composable(route = Overview.route) {
                    Overview.screen()
                  }}
                  ~~~
* 경로
    * 컴포저블의 경로를 정의
    * 올바른 위치로 이동하도록 컨트롤러를 안내
    * 각 컴포저블은 고유 경로가 있어야함.<br>
* 탐색 동작 실행
  * ~~~
     navConroller.navigate(route)
     ~~~
    * 후행 람다
      * launchSingleTop 
        * 백스택 위에 대상의 사본이 최대 1개만 있도록 설정
      * popUpTo(startDestination) { saveState = true }
        * 탭을 선택 했을 때 백 스택에 대규모 대상 스택이 빌드되지 않도록 그래프의 시작 대상을 팝업으로 만듭니다.
      * restoreState = true
        * 저장된 상태 복원 여부
* navController.currentBackStackEntryAsState()
  * 백스택에서 현재 대상의 실시간 업데이트를 State 형식으로 받아옴
  * destination:
    * 현재 화면을 반환
* 전달해야할 데이터가 많은경우 컴포저블을 직접 NavHost에 추가 = 데이터와 UI 분리
* 데이터 전달
  * 인수를 통해 전달
  * 전달시 경로(route)에 추가로 인수가 필요하다는것을 지정
  * route/{argument} 형식으로 인수를 경로와 함계 전달
  * arguments 매개변수를 정의함으로써 인수를 받아야한다는 사실을 알려줌
  * NavBackStackEntry
    * 백스택에 있는 항목의 현재 경로 및 전달된 인수에 관한 정보를 저장하는 클래스
    * NavBackStackEntry.arguments?.getString()으로 데이터 액세
* 딥링크
  * Manifestxml에서 data 추가
  * composable()의 매개변수로 딥링크 정의 
    ~~~ 
    val deepLinks = listOf(
       navDeepLink { uriPattern = "scheme://host/{$accountTypeArg}"}
    )
    ~~~