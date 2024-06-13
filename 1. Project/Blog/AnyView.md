
# AnyView

- 함수에서 서로 다른 type의 view를 리턴해야하는 경우
	* 변수로 전달할때도 쓰일 수 있음
    
- AnyView는 성능상 안 좋아서 사용을 권장하지 않음    
    - 왜? 어떻게 안 좋은거야?
	    1. 불필요한 랩핑으로 불필요한 뷰 트리의 깊이 증가
	    2. SwiftUI가 뷰를 비교하고 변경 사항을 감지하는데 방해를 받을 수 있음
		    * SwiftUI는 뷰의 타입과 상태를 기반으로 효율적으로 업데이트를 수행
		    * 아마 믿고 패스할 수 없겠지?

### 대안책

- 함수일때는 @ViewBuilder 사용
- 변수일때는 generic 사용

https://safe.menlosecurity.com/https://www.swiftbysundell.com/articles/avoiding-anyview-in-swiftui/