## View Life Cycle

- ViewController의 생명주기
  1. `init()`
  2. `loadView()`
  3. `viewDidLoad()`
  4. `viewWillAppear()`
  5. `viewDidAppear()`
  6. `viewWillDisappear()`
  7. `viewDidDisappear()`
  8. `viewDidUnload`

### init()

- ViewController의 생성자

### loadView()

- ViewContoller의 `view` 프로퍼티가 요청되었는데 `nil`일 때 자동으로 호출됨
  이 메소드는 view를 생성하고, viewController의 `view`에 할당함
- ViewController와 관련된 Nib 파일이 있을 경우, view는 그 Nib 파일에서 할당됨

> 만약, 코드로 ViewController를 그리고 생성한다면, 이 메소드를 오버라이드해서 view 프로퍼티를 할당해주어야 함

```swift
  override func loadView() {
    let view = UIView()
    // ...
    self.view = view
  }
```

### viewDidLoad()

- viewController가 메모리에 로드된 이후에 호출
- 리소스 초기화, 초기 화면 구성
- 화면이 그려질 때 처음 한 번만 호출됨

### viewWillAppear()

- 뷰가 화면에 나타나기 직전에 호출됨
- navigation cycle에서 pop()시에도 호출됨

### viewDidAppear()

- 뷰가 화면에 나타난 직후에 호출됨

### viewWillDisappear()

- 뷰가 삭제되려는 것을 ViewController에 통지

### viewDidDisappear()

- ViewController에서 view가 제거되었음을 통지

## Navigation

> 한 화면에서 다른 화면으로 push한 이후, pop하였을 때 각 화면의 라이프 사이클 메소드 호출 순서
> **A 화면** -PUSH-> **B 화면** -POP-> **A 화면**

```bash
(A) viewDidLoad(_:)
(A) viewWillAppear(_:)
(A) viewDidAppear(_:)
# --- PUSH ---
(A) viewWillDisappear(_:)
(B) viewDidLoad(_:)
(B) viewWillAppear(_:)
(A) viewDidDisappear(_:)
(B) viewDidAppear(_:)
# --- POP ---
(B) viewWillDisappear(_:)
(A) viewWillAppear(_:)
(B) viewDidDisappear(_:)
(A) viewDidAppear(_:)
```
