# InterViewProject

* 왜 Objective-C 에서 Swift 인가
  * 문법 구조상 널 포인트 에러에 대해 컴파일 단계에서 걸러줘 개발자의 실수를 막아 준다.
  * 다양한 비동기 통신 API(Rx, Combine) 들을 사용 하기가 힘들다.
  * Swift UI 프레임워크를 사용할 수 없다.

* 메소드 스위즐링이 무엇인가?
  * 런타임이 호출해야하는 메소드나 함수의 구현을 런타임에 결정 하는 기법
  * dynamic dispatch : Objective-C에서 사용하는 메소드 스위즐링 기법으로 런타임시 클래스의 특정 메소드나 프로퍼티를 호출 할때 해당 객체에 메세지를 보내는 방식으로 구현 되어 있다.  
  * dynamic 키워드 : Swift 에서 Objective-C 런타임을 쓸게라고 알려주는 키워드
    
* ARC 는 어느 시점에 작동하는가
  * 컴파일 시점에 레퍼런스 카운트를 추적하여 0 이 되는 시점에 릴리즈 코드를 자동으로 넣어 준다.

* strong이 무엇인가?
  * 메모리 관리 기법에 사용되는 키워드로 이 키워드로 지정된 객체는 메모리에 할당 받을 시 자동으로 레퍼런스 카운트 1이 증가한다.

* weak 이 무엇인가?
  * 메모리 관리 기법에 사용되는 키워드로 이 키워드로 지정된 객체는 메모리에 할당 받을 시 레퍼런스 카운트를 증가 시키지 않는다. Optional 이며 메모리 해제시 데이터는 nil 이 된다. 순환참조로 인해 발생될 메모리 릭을 방지 하기 위해 사용된다.
  
* unowned 는 무엇인가?
  * 메모리 관리 기법에 사용되는 키워드로 이 키워드로 지정된 객체는 메모리에 할당 받을 시 레퍼런스 카운트를 증가 시키지 않는다. Non Optional 이며 메모리 해제시 데이터는 남아있다. 순환참조로 인해 발생된 메모리 릭을 방지 하기 위해 사용된다.

* 메모리 릭 해결 방법
  * XCode memory graph
  * Instrument Leak 도구
  * deinit 을 통한 로그 체크

* Escaping Closure 란 무엇인가?
  * 메소드 파라미터로 전달받은 closure 를 메소드 라이프 사이클에서 끝내지 않고 메소드 밖에서 외부로 전달 하고 싶을 때 사용

* 클래스와 Struct 차이
  * 클래스는 참조타입이고 Struct 는 값 타입이다. 참조타입의 경우 대입 연산시 메모리를 참조하게 되어 원본역시 값이 바뀌며 값 타입의 경우 대입 연산시 값을 복사하게 되어 원본 값이 바뀌지 않는다.
  
* Autolayout priority
  * 오토레이아웃의 제약사항에 대한 우선순위를 말하며 상황에 따라 제약사항들이 부딛힐 때가 있는데 이를 우선순위를 설정하여 충돌을 방지한다. 
 
* content hugging priority
  * 컨텐츠의 고유 사이즈가 스스로 감싸 안아 커지기를 거부한다. priority 가 높을 수록 높이, 폭이 커지는 것을 우선적으로 막는다.

* content compression resistance priority
  * 컨텐츠의 고유 사이즈가 스스로 감싸 안아 작아지기를 거부한다. priority 가 높을 수록 높이, 폭이 작아지는 것을 우선적으로 막는다.

* 어플리케이션 라이프 사이클
  * not running
  * inactive
  * active
  * background
  * suspended
  
* FallThrough
  * swift 의 스위치 케이스문에서 사용되며 이 키워드가 있는 코드 위치까지 케이스에 걸리지 않더라도 무조건 실행
  
* 프로토콜
  * 개발자가 구현하고자 하는 세계를 코드로 규약화 해놓은 타입
  * extension 가능
  * 구조체, 열거형, 클래스형 에서 채택 가능

* Delegate
  * 객체를 참조하고 있는 다른 객체에게 변화 탐지 권한을 넘겨주어 객체의 변화 탐지를 알려주는 디자인 패턴
   
* Defer 블럭
  * 함수 종료 직전에 실행되는 블럭이며 보통 리소스 정리, 스레스 세이프 한 코드를 작성하기 위해 사용된다.
  
* NSArray 와 Array 차이
  * NSArray는 여러 타입을 수용 할 수 있지만 Array는 불가능하다.
  
* GCD : 운영체제에서 스레드를 직접 관리하는 C 기반의 스레드 API, 작업단위는 클로져이며 DispatchQueue가 이 Block 들을 관리한다.
  * DispatchQueue
    * Serial Dispatch Queue : 한 큐에 여러 Task를 넣어 처리
    * Concurrent Dispatch Queue : 여러 스레드에 여러 Task를 시스템이 알아서 넣으며 이를 분산하여 처리
    * sync : 작업을 다른 쓰레드에서 하도록 시킨 후 작업이 끝나길 기다리고 다음일 을 진행
    * async : 작업을 다른 쓰레드에서 하도록 시킨 후 작업이 끝나길 기다리지 않고 다음일 을 진행

* GCD 이전의 멀티스레딩 클래스
  * NSOperationQueue
  * NSThread

* 옵셔널
  * 널이 될 수 도 있는 타입
  * 케이스 some, none

* 옵셔널을 벗기는 방법
  * 옵셔널 바인딩 : if let, guard let 구문을 통해 있으면 사용하고 없으면 사용 하지 않는다.
  * 옵셔널 체이닝이란?
    * 상위 프로퍼티로 부터 하위 프로퍼티 까지 옵셔널을 연속적으로 확인하고 중간에 하나라도 nil이 발견되면 nil이 된다.
    
* 앱 개발에 사용 해본 디자인 패턴 : 프로그램이나 어떤 특정한 것을 개발하는 중에 발생했던 문제점들을 정리해서 상황에 따라 간편하게 적용해서 쓸 수 있는 것을 정리하여 특정한 "규약"을 통해 쉽게 쓸 수 있는 형태로 만든 것
  * Observer 패턴
  * 델리게이트 패턴
  * KVO 패턴
  * 싱글턴 패턴
  * Responder Chain : 하위 뷰 부터 상위 뷰 까지 동작에 대한 책임을 묻는 디자인패턴
  * 퍼사드 패턴 : 여러 복잡한 서브 클래스가 존재하고 클라이언트 클래스는 이를 직접 접근하지 않고 퍼사드에 접근하여 필요한 것을 사용하는 디자인 패턴
  * 빌더 패턴 : 복잡한 객체의 생성을 그 객체의 표현과 분리하여, 생성 절차는 항상 동일하되 결과는 다르게 만드는 패턴

    ``` swift
    let labelView: UILabel = {
       let label = UILabel()
       label.text = "린생"
       label.textColor = .black
       label.font = .systemFont(sizeOf: 20)
       return label    
    }()
    ```
    
    ``` swift
    class Director {
        func makeLabel(builder: Builder) -> UILabel {
            let build = builder
            build.setText(with: "린생")
            build.setTextColor(with: .black)
            build.setFontSize(with: 40)
            return build.label
        }
    }
    //일반
    let label1 = director.makeLabel(builder: ConCreateBuilder())
    //체이닝형태
    private let label2: UILabel = ConCreateBuilder()
        .setText(with: "린생 2")
        .setTextColor(with: .red)
        .setFontSize(with: 30)
        .label
    ```
* 앱 아키택쳐
  * MVC : Model, View, Controller 3개 구조로 나누고 사용자 액션 > 컨트롤러 > 
