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

# Function

- 여러 개의 타입을 리턴하고자할 땐 Tuple 을 사용함
    
    ```swift
    func plus(num1: Int, num2: Int) -> (String, Int) {
    	return ("결과값은", num1 + num2)
    }
    
    let sum = plus(num1: 10, num2: 20)
    ```
    
- argument label을 안쓰고 싶을 때
    
    ```swift
    func plus(_ num1: Int, _  num2: Int) -> Int {
    	return num1 + num2
    }
    
    let sum = plus(10, 20)
    ```
    

# Closure

- function과 굉장히 유사함.
- 이름이 없음

```swift
let myScore = { (a: Int) -> String in
	return "\(a)점"
}
myScore(20)
```

- 축약
    - 바로 `return` 문이 실행될 경우 `return` 생략 가능
    
    ```swift
    let myScore2 = { (a: Int) -> String in
    	"\(a)점"
    }
    ```
    
    - 리턴 값의 타입이 추론될 수 있기 때문에, 반환 타입 생략 가능
    
    ```swift
    let myScore3 = { (a: Int) in
    	"\(a)점"
    }
    ```
    
    - 클로저의 리턴값을 받는 변수의 타입을 지정함으로써, 클로저 내부를 간결하게 할 수 있음
    
    ```swift
    let myScore4: (Int) -> String = { a in
    	"\(a)점"
    }
    ```
    
    - `$` 사용 (`in`을 생략할 수 있음)
    
    ```swift
    let myScore5: (Int, Int, Int) -> String = {
    	"\($0 + $1 + $2)점"
    } 
    ```
    
- 사용하는 이유
    - 함수를 다른 함수의 매개변수로 사용해야할 때 혹은 일회용 함수를 만들어 사용해야할 때 클로저를 유용하게 쓸 수 있다.
    - 참고
    	[Swift4 : 클로저: Closure: #표현방식: #왜필요해?: #효율적: #간결성: #생략](https://the-brain-of-sic2.tistory.com/23)
    
- `.sort()`
    
    ```swift
    var names = ["Chris", "Alex", "Ewa"]
    
    names.sort { (lhs, rhs) => Bool in
    	return lhs > rhs
    }
    
    names.sort{ $0 < $1 }
    names.sort() { $0 < $1 }
    names.sort(by: { $0 < $1 } )
    names.sort(by: < )
    ```
    

# enum

- 분류 시 사용

```swift
enum BookType {
	case comics(title: String, price: Int, year: Int)
	case fiction(title: String, price: Int, year: Int)
	case workbook(title: String, price: Int, year: Int)
}
```

- `switch ... case`
- `if case`
- `case let`

- `extension`
    
    ```swift
    extension BookType {
    	var typeName: String {
    		case .comics: 
    			return "comics"
    		default:
    			""
    	}
    }
    ```
    

# Class

```swift
class MyInfo {

	init(gender: GenderType) {
		self.genderType = gender
	}

	enum GenderType {
		case male
		case female
	}
	var genderType: GenderType

	var name = ""
	var age = 0

	func isAdult() -> Bool {
		if age > 19 {
			return true
		}
		return false
	}
}

var myInfo = MyInfo(gender: .female)

```

- `private` 으로 설정해두면 외부에서 값 확인 및 변경 불가
    
    ```swift
    private var genderType: GenderType
    ```
    

### 상속

```swift
class GameInfo { }

class Soccer: GameInfo { }
class Baseball: GameInfo { }
```

- override

```swift
class Baeball: GameInfo {
	override func presentScore() -> String {
		// 새로운 로직
	}
}
```

- `final` : 오버라이딩 불가

```swift
class GameInfo {
	final func presentScore() -> String {
		return "점수"
	}	
}
```
