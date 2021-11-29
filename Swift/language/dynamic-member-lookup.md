## Dynamic Member Lookup

Dynamic Member Lookup은 파이썬과 같은 다른 언어와 호환성을 위해 도입된 문법

- Swift 4.2 부터 추가된 기능
- class, struct, enum, protocol에 사용 가능
- `subscript(dynamicMemberLookup:)` 메소드 구현 필수

### 구현

```swift
@dynamicMemberLookup
struct Person {
  var name: String
  var age: Int

  subscript(dynamicMemberLookup member: String) -> String {
    switch member {
      case "nameKey":
        return name
      case "ageKey":
        return age
      default:
        return "n/a"
    }
  }
}
```

- `subscript(dynamicMemberLookup:)`의 파라미터 타입은 `KeyPath` 혹은 `ExpressibleByStringLiteral`을 채택한 타입만 가능(FilePath, Selector, String, Substring 등)
- 만약 `KeyPath`와 멤버 이름을 둘 다 구현할 경우, `KeyPath`를 우선적으로 사용함

> 반드시 `subscript(dynamicMemberLookup:)`메소드를 구현해주어야 함

### 사용법

```swift
let person = Person(name: "Leefill", age: 30)

print(person.name) // Leefilll
print(person.age) // 30

print(person[dynamicMember: "nameKey"]) // Leefilll
print(person[dynamicMember: "ageKey"]) // 30

print(person.nameKey) // Leefilll
print(person.ageKey) // 30
```

### 한계점

dynamicMemberLookup을 사용하면, 다른 언어와의 호환성이 증가해 조금 더 유연하게 개발할 수 있음
그러나, 대상에 접근하는 시점이 런타임이기 때문에, 컴파일 타임에 오류를 잡아내기 힘듦

> Dynamic member lookup by member name can be used to create a wrapper type around data that can’t be type checked at compile time, such as when bridging data from other languages into Swift.
