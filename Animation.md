# Animation
* animate*AsState
  * 간단한 값 변경 애니메이션
  * animateColorAsState()...
* AnimatedVisibility
  * 페이드 인 & 아웃으로 확장 및 축소시 사용
  * 가시성 애니메이션
  * enter = 시작 될 때 / exit = 끝날 때
    * slideInVertically 
      * 항목 높이의 절반만 사용하는게 default라 높이에 대한 set 필요 
      * initialOffsetY = entert 시 높이 지정,
      * targetOffsetY = exit 시 높이 지정(default = 0)
      * animationSpec
        * 애니메이션 추가 맞춤 설정   
        * tween()을 이용하여 시간 및 easing 설정
        * easing = 애니메이션을 부드럽게 하는것
* animateContentSize()
  * 크기 변경에 대한 애니메이션 
* InfiniteTransition
  * 애니메이션 반복
  * rememberInfiniteTransition()을 사용하여 인스턴스 생성
  * ~~~ 
    val alpha by infiniteTransition.animateFloat(
    initialValue = 0f,
    targetValue = 1f,
    animationSpec = infiniteRepeatable(
        animation = keyframes {
            durationMillis = 1000
            0.7f at 500
        },
        repeatMode = RepeatMode.Reverse
    ))
    ~~~  
    initialValue -> tagertValue로 반복<br>
    keyframes = 1초동안 실행 중 0.5초 내에 0~0.7f까지 진행, 나머지 0.5에서는 1f까지 진행
