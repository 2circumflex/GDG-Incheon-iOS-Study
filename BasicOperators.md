# Basic Operators
Swift는 대부분의 표준 C 연산자를 제공하고 일반적인 코딩 에러를 제거하기 위한 몇몇의 기능을 향상시켰습니다.

## Assignment Operator (할당 연산자)
* =

Swift는 C, Objective-C 와 다르게 할당 연산의 결과를 반환하지 않습니다.
의도된 equal to operator(==) 사용시, 실수하는것을 방지해 줍니다.
```
// Objective-C 코드
int x = 5;
int y = 7;
if (x = y) {		// x에 y값이 할당되고 x의 값이 리턴되서 참
    NSLog(@"같음");
} else {
    NSLog(@"다름");
}

// 같음
```

```
// Swift 코드
var x = 5
var y = 7
if x = y {		// 에러발생
    print("같음")
} else {
    print("다름")
}
```

튜플(tuple)을 할당할 경우, 그 요소는 한번에 여러개의 상수나 변수로 분해 될수있습니다.
```
let (x, y) = (1, 2)		// x = 1, y = 2
or
var (x, y) = (1, 2)		// x = 1, y = 2
```

## Arithmetic Operators (산술 연산자)
* +
* -
* *
* /

Swift 산술연산자는 기본적으로 값이 오버플로우되는 것을 허용하지 않습니다.
오버플로우 연산자를 통해 오버플로우 동작을 선택할수 있습니다.
```
var num: Int = Int.max
var overflowNum: Int = num + 1		// 에러

num = Int.min
var underflowNum: Int = num - 1		// 에러
```

덧셈 연산자는 문자열을 지원합니다.
```
var str = "hello, " + "world"

// hello, world
```

## Overflow Operator (오버플로우 연산자)
* &+
* &-
* &*

Swift는 정수계산을 위한 세개의 오버플로우 연산자를 제공합니다.
이 연산자들은 &(ampersand) 문자로 시작합니다.
```
var num: Int = Int.max
var overflowNum: Int = num &+ 1

num = Int.min
var underflowNum: Int = num &- 1
```


## Remainder Operator (나머지 연산자)
* %

Swift는 정수뿐만 아니라 실수도 나머지 연산을 지원합니다.
```
8 % 2.5

// 0.5
```

## Nil Coalescing Operator
* ??

옵셔널(Optional) 형식과 함께 사용할 수 있는 새로운 연산자.

a **??** b
a는 옵셔널 형식의 데이터 또는 표현식.
b는 a가 nil일 경우 리턴할 기본값 또는 표현식.

nil coalescing operator는 다음과 같은 코드로 표현 가능
```
a != nil ? a! : b
```
a가 nil이 아니면 a의 값을 강제추출(forced unwrapping), nil이면 b값 리턴.
a의 값이 nil이 아니면 b는 평가되지 않습니다. [short-circuit evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation)


```
let defaultColor = "red"
var userDefinedColorName: String?
// userDefinedColorName은 nil

var colorNameToUse = userDefinedColorName ?? defaultColor
// colorNameToUse = "red"

userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColor
// colorNameToUse = "green"
```

## Range Operators (범위 연산자)
* ... (Closed Range Operator)
* ..< (Half-Open Range Operator)

### (Closed Range Operator)
a...b
a에서 b까지의 범위를 정의(a와 b의 값을 포함).
a의 값이 b보다 크면 안됩니다.
```
for index in 6...5 {	// 에러
	//     
}
```
for-in 루프와 함께 사용하고자 하는 값 범위에서 반복할때 유용.
```
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}

// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

### (Half-Open Range Operator)
a..<b
a에서 b까지의 범위를 정의(b는 포함되지 포함 안됨)
0을 기반으로한 리스트 또는 배열을 작업할때 유용.
```
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i])")
}

// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```

## Basic Operator 목록

연산자|명칭|사용 방법
----|---|-------
=   | 대입 연산자<br>(Assignment Operator) | a = b
+<br>-<br>*<br>/<br> | 산술 연산자<br>(Arithmetic Operator) | a + b<br>a - b<br>a * b<br>a / b
&+<br>&-<br>&* | 오버플로우 연산자<br>(Overflow Operator) | a &+ b<br>a &- b<br>a &* b
%   | 나머지 연산자<br>(Remainder Operator) | a % b
++  | 증가 연산자<br>(Increment Operator)  | a\++<br>\++a
\-- | 감소 연산자<br>(Decrement Operator)  | a\--<br>\--a
`-`   | 단항 빼기 연산자<br>(Unary Minus Operator) | -a
`+`   | 단항 더하기 연산자<br>(Unary Plus Operator) | +a
==<br>!=<br>><br><<br>>=<br><= | 비교 연산자<br>(Comparison Operator) | a == b<br>a != b<br>a > b<br>a < b<br>a >= b<br>a <= b
?: | 삼항 연산자<br>(Ternary Conditional Operator) | a ? b : c
?? | (Nil Coalescing Operator) | a ?? b
...<br>..< | 범위 연산자<br>(Range Operator) | a...b<br>a..<b
!<br>&&<br>&#124;&#124; | 논리 연산자<br>(Logical Operator) | !a<br>a && b<br>a &#124;&#124; b
+=<br>-=<br>*=<br>/=<br>%=<br><<=<br>>>=<br>&=<br>^=<br>&#124;=<br>&&=<br>&#124;&#124;= | 복합 대입 연산자<br>(Compound Assignment Operator) | a += b<br>a -= b<br>a *= b<br>a /= b<br>a %= b<br>a <<= b<br>a >>= b<br>a &= b<br>a ^= b<br>a &#124;= b<br>a &&= b<br>a &#124;&#124;= b
