# Swift

> `safe type(엄격한 타입)`

- var(변수) / `let(상수)`

## Tuples (n쌍 형태)

**_Tuples 예제_**

```
var httpError = (404, "not found")
httpError(Int, String)
httpError.0 = 404
httpError.1 = "not found"
```

```
var httpError = (status: 404, desc: "not found")
httpError.status = 404
httpError.desc = "not found"
```

- `nii` swift에서 표현하는 null
- ?로 표현하는 undefine은 타입 선언에 위치한다
```
# TypeScript
data?: TYPE

# Swift
data: TYPE?
```

## Optional

### unwrapping
> optional을 벗겨내는 것을 의미
<br>ex )
```
var a: Int? = 10
var b: Int? = 20

case 1. var c = a + b // err

case 2. var c = (a ?? 0) + (b ?? 0) // unwrapping을 사용하여 타입 에러를 해결

case 3. var c = a! + b! // force unwrap
!! 값이 무조건 있다고 가정하여 실행 (force unwrap) => 값이 없다면 심각한 에러 발생. 주의하여 사용할 것
```
***if let && if var***
> unwrapping 방식중 하나
><br>if문 안의 조건문의 값이 nil인가 아닌가를 체크하는 문법입니다.

조건문이 nill이 아니라면 해당 블럭이 실행되는 구조

***guard let && guard var***
> unwrapping 방식중 하나
><br>guard 안의 조건문이 true가 아니면 else문이 실행되는 문법
><br>일반적으로 칠드런에 사용
```
func testFunc() {
    guard let hasNumber = a else {
        return
    }
    print(hasNumber)
}
// 값이 없으면 바로 함수 종료, 있으면 함수 실행
```

## Operator

- 타입`Int`는 정수를 나타낸다<br>`Double`은 소수점을 나타낸다 (나누기, 곱하기에 유의)
- Int와 Double의 연산자는 당연히 불가능 <swift는 강타입 언어>


***remind operator***

- %
> 나머지를 구하는 연산자<br> `a%b` a를 b로 나누었을때 나오는 나머지

```
if a%2 == 0 {
    print("짝수")
} else {
    print("홀수")
}
```

- % 를 사용하지 못하는 경우(Double 등...)
> .truncateRemainder(devidingBy: N)를 사용

### Unicode
- 유니코드는 16진수이다. (1,2,3,4,5,6,7,8,9,a,b,c,d,e,f,g)
> "\u{30}" == "0"<br>"\u{30}" == "9"<br><br>"\u{41}" == "A"<br>"\u{7a}" == "z" // 대문자부터 시작하며 41 ~ 7a가 알파벳을 나타냄

적용 예시
```
var inputValue = "1~9"
if inputValue >= "\u{30}" && inputValue <= "\u{39}" {
    print("숫자다")
} else {
    print("숫자가 아니다")
}
```

- `.description`을 통해 String으로 표현 가능 (Boolean, Number ...)
> = String()

```
let Bool = true
Bool.description // "true"
```

- `.last` 마지막 string 값을 가져옴
- `.dropFrist` 첫 string값을 빼고 가져옴. (마지막도 가능)
- `.split(seperator: "~")`
> JS와 다르게 인자 안에 `seperator: `를 선언해줘야 하는듯?

## Collection (Array, Set, Dictionary)

### Array
- 선언
> var Arr = Array<Type>()
```
var StringArr = Array<String>()

// in TS
let StringArr: String[]
```
- 삽입
> `.append()`를 사용. (= `push( )` )<br>`apeend(contentsOf: [])`를 통해 다른 Array를 추가 // 같은 타입 한정 (타입에 유의)

- 분리
> `.remove(at: index)`를 사용<br>removeFirst, removeAll등 다양한 옵션 제공

- 배열 원소 개수
> `.count` (= `.length` )<br>
Arr.`count == 0` (= Arr`.isEmpty` )

- ARRAY`.enumerated`를 통해 배열의 index와 value를 동시에 가져올 수 있음

### Set
> 순서가 상관 없는 배열

- 선언

```
var name = Set<Type>()
```

- 삽입
> `.insert()`<br> ***같은 값은 중첩되어 들어가지 않음. 즉, Array를 Set 타입으로 변경하여 중복되는 원소 삭제 가능***

- 교집합 (.intersection)
> `Arr1.intersection(Arr2) // 배열 Arr1와 Arr2의 교집합

- 합집합 (.union)
> `Arr1.union(Arr2) // 배열 Arr1와 Arr2의 합집합

- 여집합 (.subtracting)
> `Arr1.subtracting(Arr2) // 배열 Arr1와 Arr2의 여집합

- 합집합 - 교집합 (대칭차집합 `.symmetricDifference()`)

### Dictionary
> var Dictionary = [Type : Type]()

- 선언
```
var namesOfStreet = `[String : String]()`
namesOfStreet["key 1"] = "value 1"
namesOfStreet["key 2"] = "value 2"
```
- value값을 다른 타입으로 덮어쓸 수 있다 (Optinonal도 따로 선언 안해도 사용 가능) <br>// 이 후 선언에서 nil을 주면 key에 nil이 지정 되는 것이 아니라 key자체가 사라지는 개념

- ${Dictionary}.keys
> key값들을 가져올 수 있다