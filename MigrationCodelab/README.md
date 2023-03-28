# Check list
* Compose에 대한 종속성을 추가하면 xml에서 ComposeView를 사용할 수 있음
* ComposeView에 액세스하여 setContent() 후 컴포저블 호출
* LiveData.observeAsState()
  * 컴포저블에서 LivaData 관찰 시 사용
  * LiveData를 State 객체로 표현
* pluralsStringResource() 
  * 복수형 string xml 데이터
  * quantity 데이터에 맞게 문자열 설정 및 가져오기
* Compose에서 Spanned를 지원하지 않기 때문에 HTML데이터를 표시하기 위해 AndroidView API 사용
* ViewCompositionStrategy
  * ComposeView가 프래그먼트의 뷰 수명주기를 따르도록 함
  * DisposeOnViewTreeLifecycleDestroyed를 사용하여 lifecycleOwner가 소멸되면 컴포지션을 삭제한다 
* MdcTheme 
  * styles.xml에서 색상을 선택 