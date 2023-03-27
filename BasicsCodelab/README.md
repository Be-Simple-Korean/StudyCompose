# Check
* MaterialTheme
  - Material 디자인 사양의 스타일 지정 원칙을 반영한 구성 가능한 함수
  - content로 하향 적용
* Surface
  - 요소를 감싸는 컨테이너 역할
  - 코드의 간결성 및 material요소
* by 
  - 속성위임
  - 코틀린 문법
  - 매번 .value값을 입력할 필요가 없음
* remember & rememberSaveable
  - 상태를 저장하여 불필요한 리컴포지션을 방지
  - rememberSaveable = 화면전환이나 프로세스 중단에도 상태를 저장
* animateDpAsState
  - 애니메이션이 완료될 때까지 애니메이션에 의해 객체의 value가 계속 업데이트되는 상태 객체를 반환
