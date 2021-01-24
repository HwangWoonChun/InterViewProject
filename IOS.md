# InterViewProject

* 메타타입
  * 인스턴스를 이용하여 클래스의 클래스 메소드, 클래스 프로퍼티에 접근하려면 type(of: instance) 를 함수로 접근 할 수 있는 데 이것을 메타타입이라 한다.

    ``` swift
    struct Medium {
        static let author = "naljin"
        func postArticle(name: String) {}
    }

    let blog: Medium = Medium()
    let something = type(of: blog) // Medium은 인스턴스의 타입, Medium.Type은 클래스, 구조체, 프로토콜의 그 자체의 유형
    ```
  * 메타타입은 2가지 방법으로 쓰인다.
    * 런타임 시 type(of:)
    * 컴파일 시 (원하는 타입의 이름).self 
    
  * 그렇다면 컴파일과 런타임시에 클래스 접근이 어떻게 다른가?

    ``` swift
    class SomeBaseClass {
        class func printClassName() {
            print("SomeBaseClass")
        }
    }
    class SomeSubClass: SomeBaseClass {
        override class func printClassName() {
            print("SomeSubClass")
        }
    }
    
    let someInstance: SomeBaseClass = SomeSubClass()
    //컴파일 시 엔 SomeBaseClass 이지만
    //런타임 시 엔 SomeSubClass 타입 이다.
    ```

* Strong Reference Cycle(강력 순환 참조)
  * 두 클래스가 있다고 가정하자, A라는 클래스는 B 타입의 프로퍼티를, B라는 클래스는 A 타입의 프로퍼티를 가지고 있다고 할때, A, B 인스턴스를 메모리에 해제시 A, B의 인스턴스에 접근할 인스턴스가 없기 때문에 각 클래스가 들고 있는 프로퍼티에 누수가 발생한다. 해결방법은 weak 인데, 한번더 생각해보자.
  
* TableViewDelegate 는 왜 weak?
  * ViewController 는 TableView에 대한 레퍼런스를 가지고 TableView는 delegate나 dataSource 를 통해 레퍼런스를 가진다. 둘다 스트롱 레퍼런스를 가지게되면 메모리 해제가 안된다. 그래서 weak

* [weak self] 써야되는 이유
  * 비 escaping closure : 강력한 참조주기를 도입 할 위험이 없으므로 weak또는 사용을 요구하지 않는다.
  * escaping closure : 클로저는 속성에 저장되거나 다른 클로저로 전달될때, 클로저 내부의 객체 self는 클로저 (또는 전달 된 다른 클로저)에 대한 강력한 참조를 유지합니다.
  * guard let self = self 의도에 따라 좋거나 나쁠 수있는 경우에 따라 할당 해제가 지연 될 수 있습니다. Guard let이 여기서 실제로하는 일은 self가 nil과 같은지 확인하고 그렇지 않은 경우 범위 기간 동안 self에 대한 일시적인 강력한 참조를 생성하는 것입니다.
  * GCD 호출은 나중에 실행되도록 저장되지 않는 한 일반적으로 참조주기의 위험을 초래하지 않습니다. 이러한 호출은 즉시 실행되기 때문에 [weak self] 없이도 메모리 누수가 발생하지 않습니다.

* 넌블러킹, 블러킹(함수의 자신)
  * 블러킹 - 호출된 함수가 자신의 작업을 모두 끝낼때까지 제어권을 가지고 있어 호출한 함수가 대기하도록 만듦
  * 넌블러킹 - 호출된 함수가 바로 return 해서 호출한 함수에게 제어권을 주어 다른 일을 할 수 있게 함
  
* Synchronous / Asynchronous (함수의 작업완료를 신경 씀)
  * sync : 동기는 함수를 호출하고 호출된 함수의 작업이 완료된 후의 return 을 기다리거나 return 을 받더라도 호출한 함수가 계속해서 작업완료 여부를 신경씀
  * aysnc : 동기는 함수를 호출할 때 callback 함수를 같이 전달해 작업이 완료되면 callback을 실행. 작업완료를 callback이 신경씀

* Self vs self

* 빌더 패턴을 왜 쓰는가
  * 생성자 인자로 너무 많은 인자가 넘겨 지는 경우 어떠한 인자가 어떤 값을 나타내는지 확인 하기 힘들다. 또 어떠한 인스턴스의 경우에는 특정 인자만 생성해야 하는 케이스가 있는데, 이런 가독성 문제를 해결하기 위함

  ``` swift
  public Student(id: String, name: String, address: String)
  let st = Studnent("","","","")

  let st = Student.builder()
            .id("")
            .name()
            .address()
  ```
  

* final을 쓰는 이유 : Swift에서 final키워드를 사용하면 메소드, 프로퍼티, 서브스크립트가 오버라이드를 금지, 상속 방지

* 구조체와 클래스 속도 : 어떻게 구성했냐에 따라 다를테지만, 구조체는 스택 영역에 할당되고(컴파일러 영역에 할당) 클래스는 힙 메모리영역에 할당된다.(런타임 영역에 할당) 되어 생성속도는 보통 구조체가 빠르다.

* Swift ui는 왜 구조체를?
  * 프로토콜에 extension 이용 하기 때문에 상속이 필요 없다. 멀티 스레드 환경에서 구조체는 스레드 세이프 하다.

* scene delegate
  * iOS 13 이상에서는 씬 델리게이트(scene delegate)가 앱 델리게이트의 일부 역할을 담당합니다. 중요한 것은 window의 개념이 scene 개념으로 대체된다는 것입니다. 앱에는 둘 이상의 scene이 있을 수 있으며 이제 scene은 앱의 사용자 인터페이스 및 콘텐츠의 배경으로 사용됩니다. 특히 재미있는 점은 scene이 있는 하나의 앱을 갖는 개념은 iOS 및 iPadOS에서 다중 창 앱을 빌드할 수 있습니다. 

* CPU VS GPU
  * CPU는 명령어가 입력된 순서대로 데이터를 처리하는 직렬(순차) 처리 방식에 특화된 구조를 가지고 있다. CPU가 단일 명령어를 빠르게 처리할 수 있는 비결도 이 때문이다. 반대로 GPU는 여러 명령어를 동시에 처리하는 병렬 처리 방식을 가지고 있다.

* 세마포어와 뮤텍스
  * 세마포어는 공유 자원에 세마포어의 변수만큼의 프로세스(또는 쓰레드)가 접근할 수 있습니다. 반면에 뮤텍스는 오직 1개만의 프로세스(또는 쓰레드)만 접근할 수 있습니다.

* 객체 지향언어와 프로토콜 지향언어
  * 객체 지향언어는 상속을 통해 자기 자신이 가지지 않아도될 변수라던지 함수도 가지게 되어 무거워 질 수 있다. 하지만 프로토콜 지향언어는 상속이 없고 extension 을 통해 초기 구현이 가능해져 클래스 처럼 공통된 기능을 구현 할 수 가 있다. 이렇게 필요한 기능과 변수만 가지기 때문에 가볍다.

* 객체 지향언어
  * 캡슐화, 정보은닉, 상속, 다형성(하나의 변수, 함수가 상황에 따라 다른의미로 해석 가능 - 오버라이딩, 오버로딩)
  
* 오버라이딩 : 상위 클래스 위에 자신의 메소드를 덮어쓰는 기술

* 오버로딩 : 같은 메소드의 매개변수에 따라 다르게 동작

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
  * targetAction 패턴 : 이벤트가 발생하면 해당 타겟을 찾아 액션을 하는 디자인 
  * Observer 패턴
  * 델리게이트 패턴
  * KVO 패턴
  * 싱글턴 패턴 : 애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴, 먼저 싱글톤이란 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 객체를 만들어 사용하는 디자인 패턴을 의미한다. 해당 싱글톤 객체를 수정할 경우 싱글톤 객체를 사용하는 곳에서 사이드 이팩트 발생 확률이 생기게 되며, 멀티 쓰래드환경에서 동기화 처리 문제등이 생기게 된다.
즉 생성자의 호출이 반복적으로 이뤄져도 실제로 생성되는 객체는 최초 생성된 객체를 반환 해주는 것이다.
  * 커맨드 패턴 : 실행될 기능을 추상화, 캡슐화 하여 한 클래스에서 여러 기능을 실행 할 수 있도록 하는 디자인 패턴
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
* 의존성 
  * 코드에서 두 클래스간의 관계를 말한다. 하나의 모듈이 바뀌면 의존한 다른 클래스 까지 변경이 이루어진다. 이렇게 되면 정확성이나 테스트가 힘들어진다.
  
* 앱 아키택쳐
  * MVC : Model, View, Controller 3개 구조로 나누고 사용자 액션 > 컨트롤러 모델 업데이트 > 컨트롤러 모델을 나타내줄 뷰 선택 > 뷰 갱신
    * View - Model 의 높은 의존성 > 어플리케이션이 커질 수 록 복잡
    * 하나의 컨트롤러에 다양한 뷰와 모델이 존재 할 수 있어 Controller 에 Massive Code 가 많아 질 수 있다.
    
  * MVP : Model, View, Presenter 3개 구조로 나누고 사용자 액션 > 뷰는 데이터를 Presenter 에게 요청 > Presenter 모델에게 데이터 요청 > 모델 Presenter에게 데이터 전달 > Presenter는 View 에게 데이터 전달 > View 갱신
    * View - Model 의 의존성은 해결, View - Presenter 의 높은 의존성
  
  * MVVM : Model, View, ViewModel 3개 구조로 나누고 사용자 액션 > 뷰는 커맨드 패턴으로 뷰 모델에 액션 전달 > 뷰 모델은 모델에게 데이터 요청 > 모델은 뷰 모델에게 데이터 전달 > 뷰 모델은 데이터 가공 > 뷰는 뷰 모델과 데이터 바인딩하여 화면 갱신
    * 데이터 바인딩(델리게이트, KVO, Reacitve, Property Observer 등)을 통해 각 클래스는 의존성을 가지지 않는다.
    * 설계가 쉽지는 않다.

  * ReactorKit : Flux + Reactive Programming 컨샙이며, 사용자 액션 과 뷰 상태를 한 스트림으로 놓고 각각의 계층 view, action, reactor, state 에 옵저버가 전달 해주는 디자인 패턴이다.
    * View > Action > Mutate > Mutation > Reduce > State > View

* clipsToBounds vs maskToBounds
  * clipsToBounds : true일때 내용들과 서브뷰들은 뷰의 테두리를 기준으로 잘리게 된다. 기본값은  false
  * maskToBounds : true 일때 서브레이어들은 레이어의 테두를 기준으로 잘리게 된다. 기본값은 false
  
* layer vs View
  * layer : 별도의 쓰래드에서 GPU 를 사용해 UI 를 직접 그림
  * view : 메인 쓰레드에서 CPU 를 사용해 UI 를 그림

* NSCache
  * 메모리에 캐싱하는 기능을 하는 클래스로 메모리가 부족할때 자동으로 버린다. key, value pattern 으로 구성되어 있다.

* @escaping
  * 함수 종료 시점에 함수 외부에 클로져를 전달 혹은 저장하기 위해 쓰이는 

* 다이나믹, 폰트
  * systemFont 대신 preferredFont 사용하면 시스템 설정에 지정된 폰트대로 다이나믹한 폰트 제공

* lazy
  * 변수를 사용하기 전까진 초기화 및 연산되지 않는다. 무조건 var 타입, 메모리 낭비를 막을 수 있다.

* CGAffineTransform
  * 뷰 프레임을 계산하지 않고 2D 그래픽을 그릴 수 있는 구조체

* anmiate option : duration(애니메이션 진행 시간 - 초 동안), delay(지연시간), usingSpringWithDamping, initialSpringVelocity
  * 진동 폭 : usingSpringWithDamping 0 에 가까울 수록 크다.
  * 진독 속도 : initialSpringVelocity 0 에 가까울 수록 크다.

* PublishSubject : PublishSubject는 .completed, .error이벤트가 발생할때까지, 즉 종료될때까지 subscribe한 이후부터 이벤트를 방출 합니다.

* BehaviorSubject : PublishSubject 와 동일 하지만 초기값을 가진다.

* ReplaySubject : ReplaySubject는 생성시 선택한 특정 크기만큼 일시적으로 캐시하거나 버퍼를 저장해서 최신 요소를 모두 방출합니다.

* PublishRelay : RxSwift인 Subject와는 다르게 Relay는 RxCocoa의 클래스 입니다. PublishSubject의 특성처럼 구독 이후의 발생하는 이벤트들만 알 수 있습니다.

* ~Subject는 .completed, .error의 이벤트가 발생하면 subscribe가 종료되는 반면, ~Relay는 .completed, .error를 발생하지 않고 Dispose되기 전까지 계속 작동하기 때문에 UI Event에서 사용하기 적절합니다.

* codable : json을 특정 타입으로 디코딩, 특정타입을 json으로 인코딩을 지원하는 프로토콜
