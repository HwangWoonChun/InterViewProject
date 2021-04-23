# InterViewProject

# 초기화

* ~~initalize 방법~~
  * 지정 이니셜라이저(Designated Initializer) : 클래스의 모든 저장 프로퍼티를 초기화 한다.
  * 편의 이니셜라이저(Convenience Initializer) : 지정 이니셜라이저의 일부 매개 변수의 기본 값을 설정하여 초기화 한다.
  
    ``` swift  
    convenience init(name: name){
      self.init(name: name, age: 27) // 지정 이니셜라이저 호출
    }
    ```

# 스레드

* ~~프로세스, 쓰레드~~
  * 프로세스는 어떤 프로그램의 단위를 말한다.
  * 쓰레드는 프로세스 안에서의 작업 단위들을 말하며 자원을 서로 공유하며 기능을 수행한다.

* ~~NSOperationQueue, GCD 차이~~
  * 둘다 멀티 스레딩 처리를 위한 API
  * GCD : C 기반의 저수준 API / 재개 중지 취소 불가
  * NSOperation : Objc 기반의 고수준 API / 약간의 오버헤드 / 더 느려 / 재개 중지 취소 가능

* ~~블러킹, 넌블러킹(관점 : 제어권)~~
  * 블러킹 - 작업이 완료 되면 제어권을 넘겨 준다.
  * 넌블러킹 - 작업이 완료 되기 전에 제어권을 넘겨 준다.
  
* ~~Synchronous / Asynchronous (관점 : 처리 시간)~~
  * sync : 호출된 함수의 리턴 시점과 결과 반환 시점이 동일
  * aysnc : 호출된 함수의 리턴 시점과 결과 반환 시점이 동일 하지 않다.

* ~~세마포어와 뮤텍스~~
  * 세마포어는 공유 자원에 세마포어의 변수만큼의 프로세스(또는 쓰레드)가 접근
  * 반면에 뮤텍스는 오직 1개만의 프로세스(또는 쓰레드)만 접근

* ~~GCD : 운영체제에서 스레드를 직접 관리하는 C 기반의 스레드 API, 작업단위는 클로져이며 DispatchQueue가 이 Block 들을 관리한다.~~
  * DispatchQueue
    * Serial Dispatch Queue : 한 큐에 여러 Task를 넣어 처리
    * Concurrent Dispatch Queue : 여러 스레드에 여러 Task를 시스템이 알아서 넣으며 이를 분산하여 처리
    * sync : 작업을 다른 쓰레드에서 하도록 시킨 후 작업이 끝나길 기다리고 다음일 을 진행
    * async : 작업을 다른 쓰레드에서 하도록 시킨 후 작업이 끝나길 기다리지 않고 다음일 을 진행
    
# UI

* ~~오토레이아웃 코드로 짜는 방법 2가지 NSLAayoutcontraint ~~
  * NSLayoutConstraint : 제약사항을 직접 관리
  * NSLayoutAnchor : NSLayoutConstraint 를 쉽게 만들기 위한 팩토리 클래스, 직접 NSLayoutConstraint를 생성하기 보단 필요한 뷰에 속성을 통해 제약사항을 걸어 준다.

* ~~Autolayout priority~~
  * 오토레이아웃의 제약사항에 대한 우선순위를 말하며 상황에 따라 제약사항들이 부딛힐 때가 있는데 이를 우선순위를 설정하여 충돌을 방지한다. 
 
* ~~content hugging priority~~
  * 컨텐츠의 고유 사이즈가 스스로 감싸 안아 커지기를 거부한다. priority 가 높을 수록 높이, 폭이 커지는 것을 우선적으로 막는다.

* ~~content compression resistance priority~~
  * 컨텐츠의 고유 사이즈가 스스로 감싸 안아 작아지기를 거부한다. priority 가 높을 수록 높이, 폭이 작아지는 것을 우선적으로 막는다.

* ~~clipsToBounds vs maskToBounds~~
  * clipsToBounds : true일때 내용들과 서브뷰들은 뷰의 테두리를 기준으로 잘리게 된다. 기본값은  false
  * maskToBounds : true 일때 서브레이어들은 레이어의 테두를 기준으로 잘리게 된다. 기본값은 false
  
* ~~layer vs View~~
  * layer : 별도의 쓰래드에서 GPU 를 사용해 UI 를 직접 그림
  * view : 메인 쓰레드에서 CPU 를 사용해 UI 를 그림

* ~~다이나믹, 폰트~~
  * systemFont 대신 preferredFont 사용하면 시스템 설정에 지정된 폰트대로 다이나믹한 폰트 제공

# 객체 지향언어, 프로토콜 지향언어, 함수형 언어

* ~~객체 지향언어와 프로토콜 지향언어~~
  * 객체 지향언어는 상속을 통해 자기 자신이 가지지 않아도될 변수라던지 함수도 가지게 되어 무거워 질 수 있다. 하지만 프로토콜 지향언어는 상속이 없고 extension 을 통해 초기 구현이 가능해져 클래스 처럼 공통된 기능을 구현 할 수 가 있다. 이렇게 필요한 기능과 변수만 가지기 때문에 가볍다.

* ~~객체 지향언어~~
  * 캡슐화 : 변수와 함수를 하나의 단위로 묶는다.
  * 정보은닉 : 세부 구현을 외부에 비노출
  * 상속
  * 다형성(하나의 변수, 함수가 상황에 따라 다른의미로 해석 가능 - 오버라이딩, 오버로딩)
  
* ~~오버라이딩 : 상위 클래스 위에 자신의 메소드를 덮어쓰는 기술~~

* ~~오버로딩 : 같은 이름의 메서드 여러개를 가지면서 매개변수의 유형과 개수가 다르도록 하는 기술~~

* ~~함수형 프로그래밍~~
    * 함수형 프로그래밍은 계산을 수학적 함수의 조합으로 생각하는 방식을 말한다. 이것은 일반적인 프로그래밍 언어에서 함수가 특정 동작을 수행하는 역할을 담당하는 것과는 반대되는 개념으로, 함수를 수행해도 함수 외부의 값이 변경될 수 없다.

        ``` swift
        //명령형
        var i = 1;
        while i <= 1000 {
        }
        //선언형
        (1...100).forEach { i in
        }
        ```

# Swift

* ~~swift 의 type safety~~
  * Swift는 타입에 대해 철저한 언어이다. 다른 언어는 Int 를 쉽게 float 으로 형변환 없이 사용 할 수 있지만 Int 는 Int로서 사용해야 한다.
  * 타입추론 : 스위프트는 초기화 시 선언 없이 할당된 값을 통해 타입을 추론한다.

* oauth : 사원증을 이용해 출입할 수 있는 회사를 생각해 보자. 그런데 외부 손님이 그 회사에 방문할 일이 있다. 회사 사원이 건물에 출입하는 것이 로그인이라면 OAuth는 방문증을 수령한 후 회사에 출입하는 것에 비유할 수 있다. 역시 직접 서비스에 로그인한 사용자와 OAuth를 이용해 권한을 인증받은 사용자는 할 수 있는 일이 다르다. 서비스에 대한 허용 여부에 대해 묻는 경우가 많다.

  ``` swift
  ASWebAuthenticationSession
  ```

* ~~메타타입~~

  * 스위프트는 타입을 아주 중요하게 다루는 언어 어느 정도냐면 심지어 타입에도 타입이 있을 정도, 그리고 이 타입의 타입을 메타타입이라고 부른다. 타입 자체를 변수로 사용 하고 싶을때 유용하게 사용된다.

  * 메타타입은 2가지 방법으로 쓰인다.
    * 런타임 시 type(of:변수)
    * 컴파일 시 (원하는 타입의 이름).self 

* 그렇다면 컴파일과 런타임시에 클래스 접근이 어떻게 다른가?

  * 컴파일 시엔 개발자가 지정한 타입으로 설정되지만 런타임 시엔 메모리에 할당된 타입으로 설정 된다.

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
    
* ~~그렇다면 대문자 Self vs 소문자 self 는 무엇인가?~~
   * Self : 자기자신이 아니라 타입 그 자체를 말한다. 
   * self. : 타입 인스턴스에서 자기자신을 나타내는 프로퍼티 이다.

* ~~FallThrough~~
  * swift 의 스위치 케이스문에서 사용되며 이 키워드가 있는 코드 위치까지 케이스에 걸리지 않더라도 무조건 실행

* ~~Defer 블럭~~
  * 함수 종료 직전에 실행되는 블럭이며 보통 리소스 정리, 스레스 세이프 한 코드를 작성하기 위해 사용된다.
  
* ~~NSArray 와 Array 차이~~
  * NSArray는 여러 타입을 수용 할 수 있지만 Array는 불가능하다.

* ~~NSCache~~
  * 메모리에 캐싱하는 기능을 하는 클래스로 메모리가 부족할때 자동으로 버린다. key, value pattern 으로 구성되어 있다.

* ~~lazy~~
  * 변수를 사용하기 전까진 초기화 및 연산되지 않는다. 무조건 var 타입, 메모리 낭비를 막을 수 있다.

* ~~codable~~
  * json을 특정 타입으로 디코딩, 특정타입을 json으로 인코딩을 지원하는 프로토콜

* ~~assosiated Type~~
  * 프로토콜에서 사용되며 프로토콜에서 채택될 프로퍼티가 다양한 타입을 받도록 해주는 타입

    ``` swift
    protocol Type {
       associatedtype MyType
       var name: MyType { get }
    }
    ```
 
# 어플리케이션

* ~~bitcode~~
   * bitcode가 나오기 전까지는, 해당 앱이 실행될 수 있는 모든 환경, 예를들어 32-bit, 64-bit와 arm6/arm7/arm7s/arm64에 대해 바이너리를 생성하여 이를 하나의 파일로 합쳤다. 이를 fat binary 라고도 한다.
   * bitcode가 있다면? 앱스토어 제출시 fat binary를 만들지 않고, bitcode를 업로드 합니다. 앱스토어는 bitcode를 받아가지고 각 환경 별 바이너리를 생성합니다. 사용자는 환경에 딱 맞는 바이너리를 받는다.
   
* ~~어플리케이션 라이프 사이클~~
  * not running
  * inactive
  * active
  * background
  * suspended

# WWDC

* ~~WWDC2020~~
  * IOS 14 Widget 기능 추가
  
* ~~WWDC2019~~
  * Swift UI

# 메모리

* ~~Strong Reference Cycle(강력 순환 참조)~~
  * 두 클래스가 있다고 가정하자, A라는 클래스는 B 타입의 프로퍼티를, B라는 클래스는 A 타입의 프로퍼티를 가지고 있다고 할때, A, B 인스턴스를 메모리에 해제시 A, B의 인스턴스에 접근할 인스턴스가 없기 때문에 각 클래스가 들고 있는 프로퍼티에 누수가 발생한다. 해결방법은 weak 인데, 한번더 생각해보자.
  
* ~~TableViewDelegate 는 왜 weak?~~
  * ViewController 는 TableView에 대한 레퍼런스를 가지고 TableView는 delegate나 dataSource 를 통해 레퍼런스를 가진다. 둘다 스트롱 레퍼런스를 가지게되면 메모리 해제가 안된다. 그래서 weak

* ~~ARC 는 어느 시점에 작동하는가~~
  * 컴파일 시점에 레퍼런스 카운트를 추적하여 0 이 되는 시점에 릴리즈 코드를 자동으로 넣어 준다.

* ~~strong이 무엇인가?~~
  * 메모리 관리 기법에 사용되는 키워드로 이 키워드로 지정된 객체는 메모리에 할당 받을 시 자동으로 레퍼런스 카운트 1이 증가한다.

* ~~weak 이 무엇인가?~~
  * 메모리 관리 기법에 사용되는 키워드로 이 키워드로 지정된 객체는 메모리에 할당 받을 시 레퍼런스 카운트를 증가 시키지 않는다. Optional 이며 메모리 해제시 데이터는 nil 이 된다. 순환참조로 인해 발생될 메모리 릭을 방지 하기 위해 사용된다.
  
* ~~unowned 는 무엇인가?~~
  * 메모리 관리 기법에 사용되는 키워드로 이 키워드로 지정된 객체는 메모리에 할당 받을 시 레퍼런스 카운트를 증가 시키지 않는다. Non Optional 이며 메모리 해제시 데이터는 남아있다. 순환참조로 인해 발생된 메모리 릭을 방지 하기 위해 사용된다.

* ~~메모리 릭 해결 방법~~
  * XCode memory graph
  * Instrument Leak 도구
  * deinit 을 통한 로그 체크

* ~~interface builder 를 통한 변수는 weak? strong?~~
  * weak 시 removeFromSuperView() 함수를 호출 하게 되면 메모리에서 사라진다.
  * strong 시 removeFromSuperView() 함수를 호출 해도 메모리에 남아있는다. 

* autorelease pool
  * Non arc 환경에서 풀에 등록되었다가 풀이 없어지면 메모리 해제
  * Arc 에선 strong pointer life cycle에 의해 헤제

# class, struct

* ~~class func~~

  * 타입 메소드로 클래스 틀을 위한 메소드, 상속이 가능하다.

* ~~static func~~

  * 타입 메소드로 클래스 틀을 위한 메소드, 상속이 불가능하다.

* 접근제어자
 
  * open, public : open은 클래스만 / 모듈 외부에서도 접근이 가능하다.
  * internal : 모듈(프로젝트라고 생각하자)의 모든 소스파일에서는 접근이 가능하지만, 외부 모듈에선 사용되지 않도록 한다. 보통 프레임워크 에서 사용되며 기본적인 접근제어자 이다.
  * fileprivate : 하나의 파일내에서만 접근이 가능
  * private : 정의된 블록 내에서만 접근이 가능

* ~~final~~

  * Swift에서 final키워드를 사용하면 메소드, 프로퍼티, 서브스크립트가 오버라이드를 금지, 상속 방지

* ~~구조체와 클래스 속도~~

  * 어떻게 구성했냐에 따라 다를테지만, 구조체는 스택 영역에 할당되고(컴파일러 영역에 할당) 클래스는 힙 메모리영역에 할당된다.(런타임 영역에 할당) 되어 생성속도는 보통 구조체가 빠르다.

* ~~클래스와 Struct 차이~~

  * 클래스는 참조타입이고 Struct 는 값 타입이다. 참조타입의 경우 대입 연산시 메모리를 참조하게 되어 원본역시 값이 바뀌며 값 타입의 경우 대입 연산시 값을 복사하게 되어 원본 값이 바뀌지 않는다.

* ~~Swift ui는 왜 구조체를?~~

  * 프로토콜에 extension 이용 하기 때문에 상속이 필요 없다. 멀티 스레드 환경에서 구조체는 스레드 세이프 하다.

# 클로져

* 클로져
  * 클로저는 사용자의 코드 안에서 전달되어 사용할 수 있는 로직을 가진 중괄호“{}”로 구분된 코드의 블럭
  * 참조 타입이다.

* ~~Escaping Closure 란 무엇인가?~~
  * 메소드 파라미터로 전달받은 closure 를 메소드 라이프 사이클에서 끝내지 않고 메소드 밖에서 외부로 전달 하고 싶을 때 사용

* [weak self] 안써도 되는 케이스

  * ~~비 escaping closure~~

    * 강한 참조주기를 도입 할 위험이 없으므로 weak또는 사용을 요구하지 않는다.

  * ~~GCD, 애니메이션 호출~~
  
    * GCD는 일반적으로 참조주기의 위험을 초래하지 않기 때문에 쓰지 않는다. async 같은 경우는 바로 리턴 되기 때문에 클로저 내부에 [weak self]를 쓰지 않아도 된다.
    
    * 아래처럼 클로져를 self 프로퍼티에 저장 할 경우 [weak self] 를 사용해야 한다.
    
      ``` swift
      func leakyDispatchQueue() {
          let workItem = DispatchWorkItem { self.view.backgroundColor = .red } //weak self 필요
          DispatchQueue.main.asyncAfter(deadline: .now() + 1.0, execute: workItem)
          self.workItem = workItem // stored in a property
      }
      ```
      
    * 뷰컨트롤러를 백버튼으로 deinit 시키면서 테스트 한 케이스, 결론은 뷰컨트롤러의 라이프 사이클에 따라 사용 되지 않아도 된다.
      
      * 아래 케이스는 메인스레드 부분이 실행된다.

          ``` swift
                  DispatchQueue.global(qos: .userInitiated).async {
                      self.proArray.append("2")
                      self.proArray.append("3")
                      Thread.sleep(forTimeInterval: 10)

                      DispatchQueue.main.async {
                          self.proArray.removeLast()
                          print(self.proArray)
                      }
                  }
          ```

      * 아래 케이스는 메인스레드 부분이 실행되지 않는다.

          ``` swift
                  DispatchQueue.global(qos: .userInitiated).async { [weak self] in
                      self?.proArray.append("2")
                      self?.proArray.append("3")
                      Thread.sleep(forTimeInterval: 10)

                      DispatchQueue.main.async {
                          self?.proArray.removeLast()
                          print(self?.proArray)
                      }
                  }
          ```

    
* ~~[weak self] 써야되는 케이스~~
  
  * escaping closure + self 프로퍼티에 저장 되는 케이스
  
  * 클로져 안에 object 가 strong reference 를 유지
  

# ~~옵셔널~~

* 옵셔널
  * 널이 될 수 도 있는 타입
  * 케이스 some, none

* 옵셔널을 벗기는 방법
  * 옵셔널 바인딩 : if let, guard let 구문을 통해 있으면 사용하고 없으면 사용 하지 않는다.
  * 옵셔널 체이닝이란?
    * 상위 프로퍼티로 부터 하위 프로퍼티 까지 옵셔널을 연속적으로 확인하고 중간에 하나라도 nil이 발견되면 nil이 된다.

* nil == none

# 디자인패턴

* 앱 개발에 사용 해본 디자인 패턴 : 프로그램이나 어떤 특정한 것을 개발하는 중에 발생했던 문제점들을 정리해서 상황에 따라 간편하게 적용해서 쓸 수 있는 것을 정리하여 특정한 "규약"을 통해 쉽게 쓸 수 있는 형태로 만든 것

  * targetAction 패턴
    * 이벤트가 발생하면 해당 타겟을 찾아 액션을 하는 디자인 
      ``` swift
      func addTarget(_ target: Any?, 
              action: Selector, 
                 for controlEvents: UIControl.Event)

      //Example - view controller 내에서 IBOutlet 으로 연결된 button 객체
      button.addTarget(self, #selector(ViewController.touchActionMethod()), touch)
      ```

  * ~~Observer 패턴~~
    * Delegate : 객체를 참조하고 있는 다른 객체에게 변화 탐지 권한을 넘겨주어 객체의 변화 탐지를 알려주는 디자인 패턴
    * KVO 패턴
    
  * ~~싱글턴 패턴~~
    * 애플리케이션이 시작될 때 어떤 클래스가 최초 한번만 메모리를 할당하고(Static) 그 메모리에 인스턴스를 만들어 사용하는 디자인패턴, 
    * 해당 싱글톤 객체를 수정할 경우 싱글톤 객체를 사용하는 곳에서 사이드 이팩트 발생 확률이 생기게 되며
    * 멀티 쓰래드환경에서 동기화 처리 문제등이 생기게 된다.
    
  * ~~커맨드 패턴~~
    * 실행될 기능을 추상화, 캡슐화 하여 한 클래스에서 여러 기능을 실행 할 수 있도록 하는 디자인 패턴
    
  * ~~Responder Chain~~
    * 하위 뷰 부터 상위 뷰 까지 동작에 대한 책임을 묻는 디자인패턴
    
  * ~~퍼사드 패턴~~
    * 여러 복잡한 서브 클래스가 존재하고 클라이언트 클래스는 이를 직접 접근하지 않고 퍼사드에 접근하여 필요한 것을 사용하는 디자인 패턴
    
  * ~~빌더 패턴~~
    * Builder 패턴이란 여러 속성을 가진 복잡한 객체를 간결하게 생성하기 위해 사용한다.

  * ~~팩토리 메소드 패턴~~
    * 객체를 생성하기 위한 인터페이스를 정의하는데, 어떤 클래스의 인스턴스를 만들지는 서브클래스에서 결정하게 만든다. 즉 팩토리 메소드 패턴을 이용하면 클래스의 인스턴스를 만드는 일을 서브클래스에게 맡기는 것. 객체 생성 하는 코드를 분리하여 클라이언트 코드와 결합도(의존성)를 낮추어 코드를 건드리는 횟수를 최소화 하기 위한 패턴이다.
    
# 아키텍쳐

* 의존성 
  * 코드에서 두 클래스간의 관계를 말한다. 하나의 모듈이 바뀌면 의존한 다른 클래스 까지 변경이 이루어진다. 이렇게 되면 정확성이나 테스트가 힘들어진다.
  * 의존성 주입 : 내부가 아니라 외부에서 객체를 생성해서 넣어주는 것을 주입한다고 합니다.
  
* ~~앱 아키택쳐~~
  * MVC : Model, View, Controller 3개 구조로 나누고 컨트롤러가 뷰와 모델에 각각 변경사항 전달 하고 모델이 뷰 업데이트 하도록 
    * View - Model 의 높은 의존성 > 어플리케이션이 커질 수 록 복잡
    * 하나의 컨트롤러에 다양한 뷰와 모델이 존재 할 수 있어 Controller 에 Massive Code 가 많아 질 수 있다.
    
  * MVP : Model, View, Presenter 3개 구조로 나누고 프레젠터를 통해 뷰와 모델 업데이트
    * View - Model 의 의존성은 해결, View - Presenter 의 높은 의존성
  
  * MVVM : Model, View, ViewModel 3개 구조로 나누고 사용자 액션 > 뷰는 커맨드 패턴으로 뷰 모델에 액션 전달 > 뷰 모델은 모델에게 데이터 요청 > 모델은 뷰 모델에게 데이터 전달 > 뷰 모델은 데이터 가공 > 뷰는 뷰 모델과 데이터 바인딩하여 화면 갱신
    * 데이터 바인딩(델리게이트, KVO, Reacitve, Property Observer 등)을 통해 각 클래스는 의존성을 가지지 않는다.
    * 설계가 쉽지는 않다.

  * ReactorKit : Flux + Reactive Programming 컨샙이며, 사용자 액션 과 뷰 상태를 한 스트림으로 놓고 각각의 계층 view, action, reactor, state 에 옵저버가 전달 해주는 디자인 패턴이다.
    * View > Action > Mutate > Mutation > Reduce > State > View


# ~~RXSwift~~

* reactive programming
  * 비동기 데이터 스트림을 이용한 프로그래밍

* PublishSubject
  * PublishSubject는 .completed, .error이벤트가 발생할때까지, 즉 종료될때까지 subscribe한 이후부터 이벤트를 방출 합니다.

* BehaviorSubject
  * PublishSubject 와 동일 하지만 초기값을 가진다.

* ReplaySubject
  * ReplaySubject는 생성시 선택한 특정 크기만큼 일시적으로 캐시하거나 버퍼를 저장해서 최신 요소를 모두 방출합니다.

* PublishRelay
  * RxSwift인 Subject와는 다르게 Relay는 RxCocoa의 클래스 입니다. PublishSubject의 특성처럼 구독 이후의 발생하는 이벤트들만 알 수 있습니다.

* ~Subject vs ~Relay 
  * ~Subject 는 .completed, .error의 이벤트가 발생하면 subscribe가 종료되는 반면, 
  * ~Relay 는 .completed, .error를 발생하지 않고 Dispose되기 전까지 계속 작동하기 때문에 UI Event에서 사용하기 적절

* Observable vs Publisher
  * Publisher는 에러타입 까지 지정해줘야하지만 Observable은 그렇지 않다.

* RxSwift의 hot, cold
  * hot 생성과 동시에 이벤트 방출 / Variables, properties, constants, tap coordinates, mouse coordinates, UI control values, current time
  * cold 옵저버가 subscribe 하는 순간 방출 / Async operations, HTTP Connections, TCP connections, streams 

* RxSwift의 로그

* RxSwift의 6.1

# ~~기타~~

* 메소드 스위즐링이 무엇인가?

  * 런타임이 호출해야하는 메소드나 함수의 구현을 런타임에 결정 하는 기법
  * dynamic dispatch : Objective-C에서 사용하는 메소드 스위즐링 기법으로 런타임시 클래스의 특정 메소드나 프로퍼티를 호출 할때 해당 객체에 메세지를 보내는 방식으로 구현 되어 있다.  
  * dynamic 키워드 : Swift 에서 Objective-C 런타임을 쓸게라고 알려주는 키워드
