# var, let(변수, 상수)

### 변수 및 상수 선언

- var : 변수
- let : 상수

### Swift 언어의 특징

- type safe language (강타입)

# Type Annotations

- `var str: String = "Hello, world"` 와 같이 **type annotating**이 가능함. 
- 그러나 기본적으로 타입추론이 이루어지기 때문에 `var str = "Hello, world"` 와 같이 작성해도 충분함.

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
# Operators

- 타입이 다르면 연산 불가
- `%` 를 사용하지 못하는 경우 `.truncateRemainder(devidingBy: )` 사용

# Unicode

- 값의 범위 비교 하는데에 주로 사용
- 16진수로 이루어져있음
- `"A" === "\u{41}"`
- `“z” === “\u{7a}”`

# String

- 줄바꿈 가능한 긴 문자열
    
    ```swift
    let myLongStr = 
	"""
	hi
	hello
	welcome
	"""
    ```
    
- `.description` 다른 타입의 값을 string 형태로 변환
    
    ```swift
    let isOn = false
    isOn.decription
    ```
    
- 문자열 안에서 변수 사용
    
    ```swift
    let myNumber = 123
    "my number is \(myNumber)"
    ```
    

# Array

- `var myNames = Array<String>()`
- `var myAges = [Int]()`
- 배열 값 조회의 방어코드 작성
    
    ```swift
    let index = 2
    if myNames.count > index {
    	myNames[index]
    }
    ```
    
- 배열 값 추가
    
    ```swift
    myAges.append(3)
    myAges.append(contentsOf: [41, 23])
    myAges = myAges + [41]
    myAges = myAges + [41, 23]
    
    myAges.insert(3534, at: 2)
    ```
    
- 배열 값 삭제
    
    ```swift
    myAges.remove(at: 0)
    myAges.removeAll()
    ```
    
- `.enumerated()` 인덱스와 값 둘 다 조회
    
    ```swift
    for (index, age) in myAges.enumerated() {}
    ```
    

# Set (집합)

- 순서(index) 개념 없음
- 중복 불가
- Array의 중복된 값을 없애고자 할 때 `Set()` 으로 type casting을 활용할 수 있음

- Set 연산
    
    ```swift
    var numbers1: Set = [1, 2, 3, 4, 5]
    var numbers2: Set = [4, 5, 6, 7, 8]
    
    // 교집합
    numbers1.intersection(numbers2)
    
    // 합집합
    numbers1.union(numbers2)
    
    // 합집합 - 교집합 (대칭차집합)
    numbers1.symmetricDifference(numbers2)
    
    // 여집합
    numbers1.subtracting(numbers2)
    ```
    

# Dictionary

- key: value
- 순서 개념 없음

```swift
var namesOfStreet = [String: Any]()

namesOfStreet["302ro"] = "1st Street"
namesOfStreet["305ro"] = 2
```

# Control Flow

- range로 돌리는 for문

```swift
for index in 0...5 {}
for index in 0..<5 {}
```
