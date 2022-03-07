# var, let(변수, 상수)

### 변수 및 상수 선언

- var : 변수
- let : 상수

### Swift 언어의 특징

- type safe language (강타입)

# Type Annotations

- `var str: String = "Hello, world"` 와 같이 **type annotating**이 가능함. 그러나 기본적으로 타입추론이 이루어지기 때문에 `var str = "Hello, world"` 와 같이 작성해도 충분함.

# Bool

```swift
var isOpen = false

if !isOpen {
	//
} else {
	//
}
```

# Tuples

- n짝, n쌍
- 하나의 tuple에 여러개의 값들을 넣어 묶을 수 있다. 모두 같은 타입일 필요는 없음

```swift
var topTitle = ("메인화면", "mainIcon.png")
topTitle.0
topTitle.1

var httpError = (statusCode: 404, description: "not found")
httpError.statusCode
httpError.description
```

- decompose 할 수 있음

```swift
var (statusCode, description) = httpError
var (statusCode, _) = httpError

// _를 생략해버리면 httpError tuple 자체가 statusCode란 변수에 할당되어버림.
var (statusCode) = httpError
```

# Optionals

- Int 타입의 `0`이나, String 타입의 `“”`는 존재하는 값이다.
  값이 존재하지 않아 `nil` 로 값이 할당될 가능성이 있는 변수는 `?` 를 이용하여 Optional을 부여한다.

```swift
var myAge: Int?
if myAge == nil {
	// alert 나이입력!
}
```

### unwrapping

- coalesce
- force-unwrap
  값이 분명히 존재한다는 확신이 있지않는 한 사용하지 않는 것을 권장함.
- if statement
  단순히 `nil` 인지 검증만 했을 때는 `Optional()` 타입으로 값을 전달받음 (unwrapping 되지 않음)
  if let, if var를 통해 unwrapping 했을 때, 값만 전달받음
- guard let, guard var
  `guard` 를 통과하지 못하면 `else { }` 을 실행한다. (보통 `return` 으로 함수 실행을 종료함)

```swift
var a: Int? = 10
var b: Int? = 20

// coalesce
var c = (a ?? 0) + (b ?? 0)

// force-unwrap
var d = a! + b!

// if statement
if a != nil { print(a!) }
if let hasNumber = a {}
if var hasNumber = a {}

// guard
function testFunction() {
	guard let hasNumber = a else {
		return
	}
	print(hasNumber)
}
```
