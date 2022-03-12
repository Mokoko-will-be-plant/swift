# Swift 문법 학습

> TIP

- 기본적으로 순서대로 코드가 실행된다.
- Safe Type 타입에 안전한 언어이다. (강타입)
- var httpError = (statusCode: 404, description: "not found") 등 표준으로 튜플을 이용해 사용한다.
-

## Playground

- 코드 테스트 하기 위한 파일 형태

## 변수, 상수

- let : 상수
- var : 변수

```swift
let guestName = "john"
var str: String = "Hello, playground"
var myAge: Int = 0

```

## 타입 추론 정의 (Type Annotations)

- String, Int, Double, Float 등으로 선언

```swift
/*
 주석을 달 수 있습니다.
*/
```

## Boolean

```swift
 var isOpen = false

 if !isOpen { // 느낌표나 isOpen == false 사용 가능

 } else {

 }
```

## Tuple

- n짝, n쌍이 있는 겨웅
- 짝에 맞게 사용된다.
- 항상 매칭되는 값이 있을 때만 사용된다.

> topTitle: (String, String)으로 타입이 정의됌 ex) topTitle.title 또는 topTitle.image

```swift
 var topTitle = (title: "메인화면", image: "mainIcon.png")
```

## Optional

- ?를 사용하여 옵셔널으로 타입을 정의한다.
- Null 대신 nil 사용

```swift
var myAge: Int? = 0
```

```swift
var a: Int? = 10
var b: Int? = 20

// 에러 발생 unwrapped or unwrapping
var c = a + b

// coalesce 쿼리싱을 사용하여 대체로 해결
var c = (a ?? 0) + (b ?? 0)

// force unwrapping 느낌표를 사용
// 값이 무조건 있는 상태로 변환한다. 예외상황 발생(조심)
var d = a! + b!

if a != nil {
	print(a!) // 이렇게 하는 이유는 a의 값이 있기 때문에 가능!
}

if var hasNumber = a {
	hasNumber = hasNumber + 2 // let이면 상수라 불가능!
	print(hasNumber)
}

// guard let
// guard var
// guard 개념은 함수 안에서 호출될 경우, 해당 값이 없을 때, 아래 코드를 실행하지 않도록 한다.

func testFunc() {
	guard var hasNumber = a else {
		return
	}
	hasNumber = hasNumber + 2
	print(hasNumber);
}

// 실행결과: a의 값이 있기 때문에, 12가 print됌. 만약 a가 없다면, 바로 리턴되어 아래가 실행되지 않음!
testFunc()

```

## Operators

- %(remainder Operator)
- truncatingRemainder(dividingBy: 2)를 두면, Int가 아니더라도 홀수 짝수를 구분 가능

```swift
let b: Double = 33

if b.truncatingRemainder(dividingBy: 2) == 0 {
	print("짝수");
} else {
	print("홀수");
}
```

## String

```swift
let myName = "name"

for character in myName {
	print(character)

	// 기대값은 n a m e 가 하나씩 출력
}

let isOn = true
isOn.description // "true"인 스트링 값 출력

let myNumber = 123
myNumber.description // "123"인 스트링 값 출력
String(myNumber) // 위와 같음

"my number is \(myNumber)" // 스트링 형태로 화면에 뿌려줄 때 사용! ${}와 비슷
```

- 스트링 함수
- .last()
- .lastDrop()
- .firstDrop()
- split(separator: ".")로 분리하면 배열로 쪼개서 나옴

## Collectin Type (Array / Set / Dictionary)

### Array

```swift
var myNames = Array<string>()
var myAges = [Int]()

myNames.append("kim")
myNames.append("lee")
myNames.append("jin")

// ** 중요 방어코드 **
// count로 number가 출력되기에 비교해서 사용할 수 있도록 한다!
let index = 2

if myNames.count > index {
	myNames[index]
}

myNames.append(contentsOf: ["hi", "hello"])
myNames = myNames + ["hi", "hello"]

myNames.remove(at: 3)
myNames.removeFirst()
myNames.removeLast()
myNames.removeAll()

myNames.insert("hahahaa", at: 1) // at에 따라 원하는 곳에 넣을 수 있음

for name in myNames {
	print(name + "님")
}

for (index, name) in myNames.enumerated() {
	print(index, name + "님")
}

```

### Set

> Tip

- 순서라는 개념이 없다.
- 교집합, 합집합 유리하다!
- 출력했을 때, 순서 보장 안되게 나온다.
- 중복된 값이 삽입이 되지 않는다.

```swift
var names = Set<String>()

names.insert("kim")
names.insert("lee")
names.insert("min")

var numbers1: Set = [1, 2, 3, 4, 5]
var numbers2: Set = [4, 5, 6, 7, 8]

// 교집합
numbers1.intersection(numbers2)
// {4, 5}

// 합집합
numbers1.union(numbers2)
// {8, 7, 6, 5, 1, 3, 4, 2}

// 합집합 - 교집합 (대칭차집합)
numbers1.symmetricDifference(numbers2)

// 여집합
numbers1.subtracting(numbers2)

```

### Dictionary

- Keys, Values로 사용됌 (순서는 없다)
- Key에 맞는 값들은 Optional이다. nil이 올 수 있다!!

```swift
var namesOfStreet = [String : Any]()

namesOfStreet["302ro"] = "1st Street"
namesOfStreet["303ro"] = "2st Street"
namesOfStreet["304ro"] = 3

var namesOfStreet = ["a" : 1, "b" : 2, "c" : 3]

namesOfStreet.keys

for dic in namesOfStreet {
	print(dic)
}
```

### Control Flow (흐름 제어)

```swift
// 0~4까지 출력 0...5는 0부터 5까지 출력
for index in 0..<5 {

}

let names = ["kim", "lee", "min"]
for index in 0..<names.count {
	print(index) // 0, 1, 2
}

let b = 100

switch b {
	case 1:
		print("1")
	case 2...5:
		print("2~5")
	default:
		print("other")
}

```

### Function

```swift
let a = 20
let b = 30

// _를 두면, 사용할 때, 키 값 생략 가능
func plus(_ num1: Int, _ num2: Int) -> (String, Int) {
	return ("결과값은", num1 + num2)
}

let p = plus(a, b)

var inputButtonType = "+"

// result가 결국 위와 같이 Int, Int -> Int 타입을 가지기 때문에, plus, minus, multiply를 리팩터링 가능
func displayCalc(result: ((Int, Int) -> Int)) {
	print("연산 결과", result(a, b))
}

if inputButtonType == "+" {
	displayCalc(result: plus)
} else if inputButtonType == "-" {
	displayCalc(result: minus)
} else if inputButtonType == "*" {
	displayCalc(result: multiply)
}

```

### Closure (클로저)

> 개념

- func과 유사
- 이름이 존재하지 않는다.
- in 이후에 statement 들어가 있음

```swift

// function
func myScore(a: Int) -> String {
	return "\(a)점"
}

let score = myScore(a: 40)
let score2 = myScore // 함수 호출을 안하면 리턴 값이 아닌, 함수의 타입만 대입이 된다.

// closure
let myScore2 = { (a: Int) -> String in
	return "\(a)점"
}

myScore2

// 축약 (생략)

- 한줄만 있는 경우에는 return 생략 가능
let myScore3 = { (a: Int) -> String in
	"\(a)점"
}

- return 타입 추론되어 -> String이 없어도 됌
let myScore4 = { (a: Int) in
	"\(a)점"
}

- return 타입 자동 추론되어 -> String이 없어도 됌
let myScore4 = { (a: Int) in
	"\(a)점"
}

- Int를 앞에 지정하면, 뒤에 안해도 된다.
let myScore5: (Int) -> String = { a in
	"\(a)점"
}

- 받는 parameter를 생략 가능하다.
let myScore6: (Int, Int, Int) -> String = {
	"\($0 + $1 + $2)점"
}

```

> 예시

```swift

// 조건 -> 찾는다 > 특정한 글자가 포함된 것을 찾는다.
// 조건 -> 찾는다 -> 입력한 글자로 시작하는 첫글자를 찾는다.

let names = ["apple", "air", "orange"]

let containsSomeText: (String, String) -> Bool = { name, find in
	if name.contains(find) {
		return true
	}
	return false
}

let isStartSomeText: (String, String) -> Bool = { name, find in
	if name.first?.description == find {
		return true
	}
	return false
}

func find(findString: String, condition: (String, String) -> Bool) -> [String] {
	var newNames = [String]()

	for name in names {
		if condition(name, findString) {
			newNames.append(name)
		}
	}

	return newNames
}

find(findString: "a", condition: containsSomeText)
// ["apple", "air", "orange"]
find(findString: "a", condition: isStartSomeText)
// ["apple", "air"]

```

```swift
names.sort{ $0 < $1 }
names.sort(by: { $0 < $1 } )
names.sort(by: < )
```

### enum

```swift
enum BookType {
	case fiction(title: String, price: Int, year: Int)
	case comics(title: String, price: Int, year: Int)
	case workbook(title: String, price: Int, year: Int)
}

extension BookType {
	var typeName: String {
		switch self {
			case .comics:
				return "comics"

			case .fiction:
			return "fiction"

			case .workbook:
			return "workbook"

		}
	}
}
var bookStyle: BookType?

var books = [BookType]()

func saveBook(book: BookType) {
	<!-- switch book {
		case .comics:
		case .fiction:
		default:

	}

	if book == .comics {

	} -->

	books.append(book)
}

saveBook(book: .comics(title: "aaa", price: 5000, year 2020))
saveBook(book: .comics(title: "bbb", price: 6000, year 2021))
saveBook(book: .comics(title: "ccc", price: 7000, year 2022))
saveBook(book: .fiction(title: "ddd", price: 7000, year 2023))
saveBook(book: .workbook(title: "eee", price: 4000, year 2024))

for book in books {

	if case let BookType.comics(title, _, _) = book {
		print(title, book.typeName);
	}
	<!-- switch book {
		case let .comics(title, price, year):
			print()

		case let .fiction(title, _, year):
			print()

		default:
			break
	} -->

}

```

### Class

```swift
// 항상 initialize가 되어야 한다. 안되면 에러 발생! 그래서 init 필요
class MyInfo {

	init(gender: GenderType) {
		self.genderType = gender
	}

	enum GenderType {
		case male
		case female
	}

	// 이부분!!
	var genderType: GenderType?

	// init할 때만 값을 넣을 수 있다. 업데이트도 안되고 접근도 안된다.
	private var genderType: GenderType?

	var name = ""
	var age = 0

	func isAdult() -> Bool {
		if age > 19 {
			return true
		}
		return false
	}
}

var myInfo = MyInfo(gender: .male)

// 상속

class GameInfo {
	var homeScore = 0
	var awayScore = 0

	// final을 해놓으면, override를 할 수 없다!
	final func presentScore() -> String {
		return homeScore.description + " : " + awayScore.description
	}
}

class Soccer: GameInfo {

}

class Baseball: GameInfo {
	override func presentScore() -> String {
		return homeScore.description + " 대 " + awayScore.description
	}
}
```

### Properties

```swift
class MyInfo {

	// stored property (저장)
	var name = ""
	var age = 0

	// lazy stored property
	// 만약에 이미지가 크다면 부하가 많이 걸린다.., 사용하려고 할 때 메모리에 올려서 사용!!
	lazy var myProfiles = [UIImage(named: "a"), UIImage(named: "a"), UIImage(named: "a")]

	// computed property (계산된) get만 하기 때문에 set get 생략 가능!
	var isAdult: Bool {
		if age > 19 {
			return true
		}
		return false
	}

	// email -> 보안 -> 암호화 된 값으로 사용한다. (항상)
	var _eamil = ""
	var email: String {
		get {
			return _eamil
		}
		set {
			_eamil = newValue.hash.description
		}
	}
}
```
