
https://medium.com/@vladislavshkodich/mastering-swiftui-are-you-really-as-good-as-you-think-40a4953f7e88

"SwiftUI View가 왜 struct고 Equatable을 채택하고 있는지 알고 있니?"
"빌드하는 동안 init이 얼마나 호출되는지 알고 있니"

# [왜 Struct인가?]
* swiftui는 view가 여러번 재구성되는 구조로 설계되었다.

### '언제 view가 재구성되는가?'
	* State가 바뀔때
	* State만 바뀌고 State가 View에 적용되지 않았을때는 View가 재구성되지 않는다. 

### ObservableObject는?
	* 얘는 적용된 부분이 없어도 viewModel 값이 바뀌면 그냥 View가 재구성됨
	* 근데 "@Observable" 은 달라...



# [Swiftui가 뷰를 그리는 방법]
* 
* 1. 새로운 상태로 새로운 View를 그린다.
	* 기존 뷰와 비교해서 다르면 쓰고 아니면 버린다.
* 2. body를 호출해 계층 구조와 뷰가 변경된 부분이 있는지 확인


### body 안에서 복잡한 작업을 피하라

* ForEach 를 두고 map, filter 같은 작업 하는거
	* 왜냐하면 body가 여러번 호출될 수 있기 때문이야
'''swift
// Avoid such things ...  
var body: some View {  
List {  
ForEach(model.values.filter { $0 > 0 }, id: \.self) {  
Text(String($0))  
.padding()  
.debugBackground()  
}  
}  
}
'''

### body 안의 내용을 다른 뷰로 쪼개라 (!!)

* body를 비교하는데 쪼개면 변경사항을 줄일 수 있다.
* **서브뷰로 쪼개면 body를 호출할 필요 없이 해당 뷰를 생성만 하면 된다.**
	* **생성하면 1. 상태 체크 2. body 호출 인데**
	* **다른 변경이 없는 다른 서브뷰들은 상태 체크에서 다른게 없으니 끝나서 불필요한 body 호출을 줄일 수 있다.**


### 애니메이션을 줄 때는...

* 분기문이 아니라 뷰 안에서
	* 분기문은 swiftui가 같은 뷰라고 인식하지 못해



# [SwiftUI가 뷰를 비교하는 방법]

### memcmp, Equality, Reflection

* fast, medium, slow
* Equatable을 채택하면 이걸로 비교 가능


# [ 새 줄 요약]

1. 비교를 최소화 하자
	* ObservableObject대신 @Observable 사용
2. body 호출을 최소화 하자
	* view를 분리해서 불필요한 body 호출을 줄이자.
1. 비교시 성능을 빠르게 하자.
	* Equatable을 채택해서 Swiftui의 비교 성능을 올리자.
