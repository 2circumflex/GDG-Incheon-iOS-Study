# Subscripts

## 서브스크립트는..
* 컬렉션, 리스트, 시퀀스의 멤버 요소에 접근하기 위한 단축키(shortcuts)
* 클래스, 구조체, 열거형에 서브스크립트를 정의할 수 있음
* 값을 저장하고 가져오기 위한 접근자 메서드를 따로 구현하지 않고 [ ]를 사용해서 속성에 접근

```
let someArray = ["김병주", "임규", "이한형", "Seonju Park", "james", "이로운", "권오철", "영보스", "박정연(Jay)", "영구스"]
var name = someArray[0]	// 김병주

let someDictionary = ["kr": "한국", "us": "미국"]
var korea = someDictionary["kr"]	// 한국
```

## 서브스크립트 문법
* 인스턴스 이름 뒤에 [ ] 붙이고, [ ]안에 하나이상의 값을 써서 사용
* subscript 키워드를 써서 서브스크립트를 정의
* 인스턴스 메서드처럼 하나 이상의 파라미터를 입력하고 값을 리턴하는 형태
* 계산 프로퍼티처럼 read-write, read-only

```
subscript(index: Int) -> Int {
    get {
        // return an appropriate subscript value here
    }
    set(newValue) {
        // perform a suitable setting action here
    }
}
```

* 읽기전용 서브스크립트

```
subscript(index: Int) -> Int {
    // return an appropriate subscript value here
}
```

## 서브스크립트 옵션
* 파라미터 개수를 제한하지 않음
* 파라미터, 리턴 타입은 어떤 타입이든 가능
* 변수(Variable) 파라미터, 가변 인자(Variadic) 파라미터 사용 가능
* in-out 파라미터는 사용할 수 없고, 기본 파라미터 값을 지정할 수 없음
* 서브스크립트 오버로딩
	- 중괄호 [ ] 사이에 전달되는 파라미터를 통해 실행할 서브스크립트를 결정
	- 서브스크립트 오버로딩의 대상은 파라미터의 수와 자료형이고 리턴형은 포함되지 않음
	- 여러개의 서브스크립트를 구현할 때 파라미터의 수와 자료형이 일치하는 경우가 존재하지 않도록 주의

```
// 잘못된 서브스크립트 구현
class MyClass {
    subscript(index: Int) -> String {
        return "Swift Study"
    }
    
    subscript(index: Int) -> Double {
        return 0.0
    }
}

var myClass = MyClass()
var firstProduct = myClass[0]	// 에러


// 서브스크립트의 파라미터 자료형 변경
class MyClass {
    subscript(index: Int) -> String {
        return "Swift Study"
    }
    
    subscript(index: UInt) -> Double {
        return 0.0
    }
}

var myClass = MyClass()
var firstProduct = myClass[0]	// "Swift Study"
var d: Double = myClass[0]		// 0.0
```

## 예제

TimesTable 구조체 읽기 전용 서브스크립트 구현 예 (정수의 n배)


```
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
println("six times three is \(threeTimesTable[6])")
// prints "six times three is 18"
```

Matrix 구조체의 서브스크립트는 두개의 정수 파라미터를 가짐
```
struct Matrix {
    let rows: Int, columns: Int
    var grid: [Double]
    init(rows: Int, columns: Int) {
        self.rows = rows
        self.columns = columns
        grid = Array(count: rows * columns, repeatedValue: 0.0)
    }
    func indexIsValidForRow(row: Int, column: Int) -> Bool {
        return row >= 0 && row < rows && column >= 0 && column < columns
    }
    subscript(row: Int, column: Int) -> Double {
        get {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            return grid[(row * columns) + column]
        }
        set {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            grid[(row * columns) + column] = newValue
        }
    }
}
```
## 참고
* Objective-C 개발자를 위한 Swift
* [Apple - The Swift Programming Language (Subscripts)](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Subscripts.html#//apple_ref/doc/uid/TP40014097-CH16-ID305)





