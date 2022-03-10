# Swift

> `safe type(엄격한 타입)`

- var(변수) / `let(상수)`

### Tuples (n쌍 형태)

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
