## JSON

> Codable 프로토콜은 내부적으로 Encoding 프로토콜과 Decoding 프로토콜을 합친 것

```swift
public typealias Codable = Decodable & Encodable
```

### JSON Encoding

`JSONEncoder`를 사용하되, `Encoding` 프로토콜을 채용하고 있어야함

```swift
struct EncodableStruct: Encodable {
  var name: String
  var number: Int
}

let instance = EncodableStruct(name: "Encoding", number: 10)

let encoder = JSONEncoder()

do {
  let jsonData = try encoder.encode(instance)
  // logic...
} catch {
  // error handling
}
```

### JSON Decoding

`JSONDecoder`를 사용하되, `Decoding` 프로토콜을 채용하고 있어야함

```swift
struct DecodableStruct: Decodable {
  var name: String
  var number: Int
}

let json = """
{
  "name": "Decoding",
  "number": 10,
}
"""

guard let jsonData = json.data(using: .utf8) else { fatalError() }

let decoder = JSONDecoder()

do {
  let decoded = try decoder.decode(DecodableStruct.self, from: jsonData)
  // logic...
} catch {
  // error handling
}
```

### CodingKeys

`JSONEncoder`와 `JSONDecoder`는 자동으로 프로퍼티 이름과 매핑해줌.
만약 프로퍼티 이름과 다르다면 직접 구현을 해주어야 함
이때, `CodingKeys` enum을 추가해주고 구현. 이 CodingKeys enum은 `CodingKey` 프로토콜을 채용해야 함

```swift
struct CodableStruct: Codable {
  var name: String
  var number: Int

  enum CodingKeys: String, CodingKey {
    case name
    case number = "integer"
  }
}

let json = """
{
  "name": "Codable",
  "integer": 10
}
"""
```

### Utility

```swift
encoder.outputFormatting = .prettyPrinted // 콘솔 출력 시 정리되어 출력
encoder.keyEncodingStrategy = .convertToSnakeCase // JSON으로 변환시 SnakeCase를 사용하도록 지정
encoder.dateEncodingStrategy = .iso8601 // Date 타입 포매팅
```

```swift
let dataFormatter = DateFormatter()
formatter.dateFormat = "yyyy/MM/dd"
encoder.dateEncodingStrategy = .formatted(dateFormatter)
// DateFormatter 객체를 이용할 수도 있음
```
