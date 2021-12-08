## Clean Architectures

![Screen Shot 2021-12-08 at 3 38 47 PM](https://user-images.githubusercontent.com/38246878/145160775-d877bef3-b0fe-422c-9ab2-6d746b7584ab.png)

> Clean Architecture에서 가장 중요한 사항은 원 내부에 있는 레이어는 바깥의 레이어에 대해서 어떠한 의존성을 갖지 않는 것

![1*MzkbfQsYb0wTBFeqplRoKg-2](https://user-images.githubusercontent.com/38246878/145160949-a7448c1c-e450-49e4-b8a2-45c72cdcacb4.png)

### Domain Layer

Entities, Use Cases, Repository Interface가 포함됨

- Business Logic이 들어감
- 다른 어떠한 레이어에도 의존성을 갖지 않고 완전하게 고립(isolated)되어 있어야 함
- 필요하다면 다른 프로젝트에도 사용될 수 있어야 함
- 어떠한 외부 라이브러리 의존성을 갖지 않아야 함(UIKit, SwiftUI, RxSwift 등 포함)

### Presentation Layer

UI(UIViewController, SwiftUI Views) 및 ViewModel을 포함

- 각 뷰는 ViewModel(혹은 Presenter)에 의하여 Coordinated됨
- ViewModel은 하나 이상의 UseCase를 호출함
- Domain Layer에만 의존성을 가지고 있음

### Data Layer

Repository Implementations와 API, 하나 이상의 데이터소스를 포함

- Repository는 다른 데이터소스에서 데이터를 구성함
- 데이터소스는 네트워크를 통할 수도 있고, 로컬 데이터배이스로 이루어질 수도 있음
- Domain Layer에만 의존성을 가지고 있음

### Data Flow

![1*N3ypUNMUGv87qUL57JyqJA](https://user-images.githubusercontent.com/38246878/145161771-3901d791-027f-431a-913d-977d0c9d0944.png)

1. UI(View)에서 Presenter(ViewModel) 메소드 호출
2. ViewModel은 UseCase를 호출
3. UseCase는 데이터를 Repository에서 가져옴
4. 각 Repository는 네트워크나 로컬 데이터베이스(혹은 Cache)를 통해 데이터를 반환
5. 다시 UI로 데이터를 전달하고 UI는 데이터를 표출함

### 예시 프로젝트 설명

> 소스코드: https://github.com/kudoleh/iOS-Clean-Architecture-MVVM

- **Presentation Layer**

  - ViewModel을 포함
  - ViewModel은 UIKit이나 SwiftUI와 같은 UI 프레임워크를 포함하지 않음
  - UIKit을 나중에 SwiftUI로 바꾸는 작업이 이루어져도 ViewModel은 재사용 가능해야 함
  - UI는 비즈니스 로직과 애플리케이션 로직을 알 수 없으며, ViewModel은 접근함
    <br/>

- **Data Layer**

  - Repository를 포함하는데, Domain Layer의 Repository Interface를 채용함(의존성 역전 원칙, Dependency Inversion).
  - Response된 데이터를 맵핑하기 위하여 DTO(Data Transfer Object)를 활용함. 캐싱할 때 DTO 객체를 그대로 저장해주어도 됨.
  - Request 시에, 캐시에서 먼저 값을 리턴하고 Request를 날리도록 구현.
  - 데이터 저장소와 API는 완전히 다른 것으로 교체될 수 있도록 구현해야 함(예를 들어, Core Data에서 Realm으로)
    <br/>

- **MVVM**

![1*SWQ5UQ1XU8wSykwXnWpiNg](https://user-images.githubusercontent.com/38246878/145169746-cdf6216a-5e8f-4b8b-a5b3-6974ac577468.png)

- View와 ViewModel의 데이터 바인딩은 클로져, 델리게이트나 옵저버 패턴으로 구현

![1*XEIiznI1ngHpPoQe-0Z0nw](https://user-images.githubusercontent.com/38246878/145170399-ebb6f7b8-6e59-4321-b2f9-99eef9f0b8ad.png)

- ViewModel간의 통신은 델리게이트 패턴으로 구현
- Responder라고 칭하기도 함

### 기타 참고

- (Flow)Coordinator 패턴은 프레젠테이션 로직에 집중하는데, 이는 ViewController의 사이즈를 줄이고, 책임을 분리함. 예시에서 FlowCoordinator에 대한 강한 참조로 연결되어 있는 것은, 메모리에서 해제되지 않게 하기 위함임.

---

### References

- [Clean Architecture and MVVM on iOS](https://tech.olx.com/clean-architecture-and-mvvm-on-ios-c9d167d9f5b3)

- [Clean architecture with RxSwift](https://github.com/sergdort/CleanArchitectureRxSwift)

- [Clean Architecture for mobile: To be, or not to be](https://medium.com/globant/clean-architecture-for-mobile-to-be-or-not-to-be-2ffc8d46e402)
