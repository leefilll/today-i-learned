## Initializations

## 구조체의 Initializer

```swift
struct SizeStruct {
  var width: Double
  var height: Double

  init(width: Double, height: Double) {
    self.width = width
    self.height = height
  }

  init(value: Double) {
    // self.width = value
    // self.height = value
    self.init(width: value, height: value)
  }
}
```

- `self.init()`을 사용하면 코드의 유지보수성이 높아짐
- 구조체의 초기화 함수에는 `convenience` 키워드를 붙일 수 없음

### Memberwise Initializer

구조체의 경우 초기화되지 않은 프로퍼티가 있어도, 생성자를 생략할 수 있음.

```swift
struct SizeStruct {
  var width: Double
  var height: Double
}

let size = SizeStruct(width: 10.0, height: 10.0)
```

- 프로퍼티 변수가 기본값을 갖고 있어도 초기화를 명시적으로 해줄 수 있음
- 단, 프로퍼티가 변수(`var`)가 아닌 상수(`let`)로 선언되었고 기본값을 갖고 있다면 `Memberwise init`으로 해당 프로퍼티를 초기화할 수 없음.
- 구조체에서 명시적으로 init()을 구현하면 `Memberwise init`을 사용할 수 없음.
  단, 확장하여 생성자를 추가하면 둘 다 사용 가능

```swift
struct SizeStruct {
  var width: Double
  var height: Double
}

extension SizeStruct {
  init(value: Double) {
    self.width = value
    self.height = value
  }
}

let size = SizeStruct(width: 10.0, height: 10.0)
// let size = SizeStruct(value: 10.0)
```

## 클래스의 Initializer

클래스에서 생성자는 두 가지로 나누어짐

- **Designated Initializer**: 지정 생성자(메인 생성자)
- **Convenience Initializer**: 간편 생성자

```swift
class SizeClass {
  var width: Double
  var height: Double


  // Designated Initializer
  init(width: Double, height: Double) {
    self.width = width
    self.height = height
  }

  // Convenience Initializer
  convenience init(value: Double) {
    self.init(width: value, height: value)
  }
}
```

- 클래스에서 선언할 수 있는 Designated Initializer의 수는 제한이 없음.
- Convenience Initializer에서는 Designated Initializer와 다르게 모든 프로퍼티를 초기화시켜야 하는 것은 아님. 필요한 것들만 초기화 시키고 Designated Initializer를 호출하는 방식(`self.init()`)으로 구현.
- Convenience Initializer에서는 반드시 `self.init()`을 호출 해야함

### Initializer Delegation

초기화 코드 `init`에서 중복을 최대한 제거함
모든 속성을 효율적으로 초기화하기 위해 사용함

- **Delegate Up**: 슈퍼 클래스의 Designated Initializer를 호출하는 것
  > 동일 클래스에 있는 다른 Designated Initializer를 호출하는 것은 불가능함
- **Delegate Across**: 동일 클래스 계층에 있는 다른 Designated Initializer를 호출하는 것(Convenience Initializer)

### Initializer Inheritance

```swift
class Figure {
  var name: String

  init(name: String) {
    self.name = name
  }
}

class Rectangle: Figure {
  var width: Double
  var height: Double

  init(name: String, width: Double, height: Double) {
    self.width = width
    self.height = height
    super.init(name: name)
  }

  override init(name: String) {
    width = 0.0
    height = 0.0
    // self.name = name <- 컴파일 에러 발생
    super.init(name: name)
  }
}
```

- initializer을 오버라이드하기 위해서는 서브클래스의 모든 프로퍼티가 초기화되어야 함
- 서브 클래스에서 지정 생성자는 슈퍼 클래스의 생성자를 무조건 호출해야 함(`super.init()`)
- 슈퍼 클래스의 프로퍼티 초기화는 슈퍼 클래스의 생성자에 맡겨야 함(명시적 할당 불가능)
- 간편 생성자의 경우 동일한 계층의 다른 생성자를 호출하기 때문에 슈퍼 클래스의 생성자를 호출할 수 없고, 오버라이딩이 불가능함

### Required Initializer

서브 클래스에서 동일한 생성자를 반드시 구현하도록 하고 싶을 때 사용하는 필수 생성자

```swift
class Figure {
  var name: String

  required init(name: String) {
    self.name = name
  }
}

class Rectangle: Figure {
  var width: Double = 0.0
  var height: Double = 0.0

  init() {
    super.init(name: "unknown")
  }

  required init(name: String) {
    super.init(name: name)
  }
}
```

- 슈퍼 클래스의 생성자에 `required` 키워드를 붙임
- 서브 클래스에서 반드시 동일한 생성자를 구현해야 함
- 만약, 서브 클래스의 모든 프로퍼티가 초기화되어 있고 생성자가 따로 없다면 구현하지 않아도 됨. 자동으로 슈퍼 클래스의 생성자를 이용하기 때문.
- 하지만, 생성자를 갖게 될 경우 생성자를 더이상 상속받지 않기 때문에 슈퍼 클래스의 필수 생성자도 추가로 구현해주어야 함

### Failable Initializer

상단의 초기화 방식은 모두 Nonfailable Initializer을 이용한 방식
초기화에 실패할 경우 런타임 에러가 발생함

```swift
struct Coordinate {
  let x: Double
  let y: Double

  init?(x: Double, y: Double) {
    guard x >= 0.0, y >= 0.0 else { return nil }
    self.x = x
    self.y = y
  }
}

let success = Coordinate(x: 1.0, y: 1.0) // Optional<Coordinate>
let fail = Coordinate(x: -1.0, y: 0.0) // nil
```

- 파일의 경로를 확인하여 인스턴스를 생성하는 등 초기화 방식에 이용할 수 있음
- 실패 시, nil을 리턴하고 초기화 성공 시 옵셔널 인스턴스를 리턴
