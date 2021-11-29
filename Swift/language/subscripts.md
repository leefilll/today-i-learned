## Subscripts

collection이나, list, sequence에서 특정한 요소에 접근할 때 사용하는 문법

- class, struct, enum에서 정의
- 하나의 타입에 여러 개의 `subscript`를 정의할 수 있음(subscript overloading)
- `subscript`메소드에서 여러 개의 파라미터를 받을 수 있음
- `subscript`메소드의 파라미터와 반환값의 타입은 어떤 타입이든 사용 가능
- `subscript`메소드의 파라미터로 Variadic Params와 Default Params는 모두 사용할 수 있지만, in-out params는 사용할 수 없음.

### 형태

```swift
subscript(parameters) -> ReturnType {
  get {
    return expression
  }
  set(newValue) {
    statements
  }
}
```

- 만약, setter를 작성하지 않으면, read-only 연산 프로퍼티로 동작함

### 예시

```swift
struct Matrix {
  let rows, columns: Int
  var values: [Int]

  init(rows: Int, columns: Int) {
    self.rows = rows
    self.columns = columns
    self.values = Array(repeating: 0, count: rows * columns)
  }

  private func isValid(row: Int, column: Int) -> Bool {
    return row >= 0 && row < rows && column >= 0 && column < columns
  }

  subscript(row: Int, column: Int) -> Int {
    get {
      assert(isValid(row: row, column: column), "Index out of range")
      return values[row * column + column]
    }
    set {
      assert(isValid(row: row, column: column), "Index out of range")
      values[row * column + column] = newValue
    }
  }
}
```

### Type Subscripts

`static`으로 선언하여 타입 자체에 `subscript`메소드를 추가할 수 있음

```swift
enum Weekdays: String, CaseIterable {
  case monday, tuesday, wednesday, thursday, friday, saturday, sunday

  static subscript(index: Int) -> String {
    return Weekdays.allCases[index].rawValue
  }
}

let tuesday = Weekdays[1]
print(tuesday) // tuesday
```
