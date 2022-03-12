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
ex )
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