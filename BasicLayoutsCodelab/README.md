# Check list
* Modifier
  - heightIn = 컴포저블에 특정 최소 높이 지정
  - clip = 컴포저블의 모양을 조정
  - paddingFromBaseline = 레이아웃 상단에서 기준선까지 특정 거리가 유지되도록 패딩을 추가
* Image 컴포저블에 이미지 지정은 painter 파라미터 이용
* Icon, Image 컴포저블에 접근자를 위해 contentDescription은 필수
* Arrangement.spacedby 
  - 각 항목 사이에 간격 추가
* contentPadding
  - 기존 패딩을 유지하면서, 스크롤시 콘텐츠가 짤리지 않도록 함
* Spacer
  - 공간(여백)을 확보할 때 사용
* 목록에 들어갈 데이터가 적은 경우 = Column / 데이터가 많다면 Lazy
* rememberScrollState() 
  - 영구적인 ScrollState 인스턴스를 가지며, 스크롤의 현재 상태를 포함
* Scaffold
  - 바텀 내비게이션 적용시 bottombar 속성을 이용하여 적용
  - Material Design을 구현하는 앱을 위한 구성 가능한 최상위 수준 컴포저블을 제공
