
### 목적
* 모듈로 분리하여 의존성 관리
	* 테스트 용이
* Preview를 활용한 개발 생산성 향상
* 추후 데모앱을 통한 빌드 속도 향상

### 방법
* 프로젝트 root에 Module 폴더 생성
	* 네이밍은 Module로 감싸고 있으니 Module 빼기
* Resource 빼기
	* UIFont, UIColor
* 빠른 작업(preview 로딩)을 위해서 Module용 Project 생성


### 이슈
* UIFont, UIColor 리소스 관리
	* Resource라는 패키지로 분리
	* 접근하기 위해서는 import 해줘야 하는데 기존에 접근하고 있는 부분이 너무 많다.
		* @_exported: 브릿지 헤더 느낌인데 정확히 확인해보자.

* add package 하면 독립적으로 실행할 수 없는 증상
	* 프로젝트에 포함해서 Preview를 돌려봤지만 로딩 속도가 느리다.
	- target 새로 만드는 방법 도전
		- unit 테스트 타겟을 추가해봤지만 preview를 지원하지 않는다.
	- project 새로 만드는 방법
		- Project를 새로 만드니 확실히 빠르다.

* Duplicate symbol 이슈
	* 그냥 꼬인듯... 이번에는 다시 생성하는 식으로 했는데 다음에도 먹힐지는 모르겠다...
	* 다시 생성해서 해결했던 이슈인데 또 발생했다.
	* 중복된 심볼이 있다는데...
	* Resource를 중복으로 참조하고 있어서 그런가? 
		* 근데 이건 어쩔 수 없는데? 그리고 이전에는 잘 됐는데?

* 스토리보드로 관리되고 있는 Color 이슈


