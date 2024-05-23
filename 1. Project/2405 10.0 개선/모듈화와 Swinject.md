
나누는건 package로 나누면 된다.
package끼리 유연하게 상호작용하려면 의존성 주입이 필요하다.

기본은 protocol로 추상화 하는 것이다.

### HOW

* protocol로 정의
* AppDelegate에서 의존성 등록
	* 객체 구현해놓기 (근데 여기서 생성되는 의존성을 어떻게 관리...?)
* 사용부에서 가져다 쓰기


(참고: https://kevinabram1000.medium.com/a-simple-modular-architecture-with-dependency-injection-in-ios-372d56a9bed9)
