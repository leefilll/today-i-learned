## First Class Citizen(일급 객체)

### 일급 객체란?

1. **상수와 변수에 할당할 수 있음**

```swift
var firstClassFunction: ((String) -> Void)

func sayHello(to name: String) {
  print("Hello \(name)")
}

firstClassFunction = sayHello(to:)
```

2. **함수의 인자로 전달할 수 있음**

```swift
UIView.animate(withDuration: 1.0, animations: {
  self.someButton.alpha = 0.0
})
```

3. **함수에서 반환값으로 사용할 수 있음**

```swift
func increment(by increment: Int) -> ((Int) -> Int) {
  return { $0 + increment }
}

let incrementByTen = increment(by: 10)
print(incrementByTen(5)) // 15
```
