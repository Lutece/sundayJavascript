## Chapter01 자바스크립트 프로그래밍 환경과 모델

### 1.1자바스크립트 환경
원래 자바스크립트는 웹 브라우저 안에서만 실행할 수 있는 프로그래밍 언어로 탄생했다.  
하지만 시간이 흐르면서 데스크톱, 서버 등에서도 자바스크립트 프로그래밍 환경이 제공되었다.

### 1.2 자바스크립트 프로그래밍 기초
#### 1.2.1 변수 선언과 초기화
기본적으로 자바스크립트 변수는 전역이며 정확하게 따지자면 사용하기 전에 꼭 변수를 선언 할 필요가 없다.  
선언하지 않고 자바스크립트 변수를 초기화하면 전역 변수가 된다.  

자바스크립트에서는 var라는 키워드, 변수명, 할당 표현식(선택 사항)을 이용해 변수를 선언한다.
```js
var number;
var name;
var rate = 1.2;
var greeting = "Hello world";
var flag = false;
```

#### 1.2.2 자바스크립트 산술, 수학 라이브러리 함수
자바스크립트는 표준 수학 연산자를 지원한다.
- `+` (더하기)
- `-` (빼기)
- `*` (곱하기)
- `/` (나누기)
- `%` (나머지)

자바스크립트는 제곱근, 절대값, 삼각 함수 등의 고급 함수 기능을 이용할 수 있도록 함수 라이브러리를 제공한다.  
수학 연산자는 표준 순서를 따르므로 연산자 순서를 바꾸려면 `괄호()`를 사용해야 한다.
```js
var x = 3;
var y = 1.1;

console.log((x + y) * (x - y));     // (출력값 7.789999999999999)

var z = (x + y) * (x - y);

console.log(z.toFixed(2));  // (출력값 7.79)
```

#### 1.2.3 조건문
조건문을 이용하면 불린 표현식의 결과에 따라 어떤 프로그래밍 문장을 수행할 것인지 결정할 수 있다.

##### if문
- 단순한 if문
- if-else문
- if-else if문
```js
var mid = 25;
var high = 50;
var low = 1;
var current = 13;
var found = -1;

//단순한 if문
if ( current < mid ){
    mid = ( current - low ) / 2;
}
console.log(mid);   // (출력값 6)

//if-else문

if ( current < mid ){
    mid = ( current - low ) / 2;
} else {
    mid = ( current + high ) / 2;
}
console.log(mid);   // (출력값 31.5)

//if-esle if문
if ( current < mid ){
    mid = ( current - low ) / 2;
} else if ( current > mid ){
    mid = ( current + high ) / 2;
} else {
    found = current;
}
console.log(mid);   // (출력값 6)
```
##### switch문
if문 외에 switch문이라는 조건문도 사용된다.  
swtich문은 조건식(대표값)을 다양한 값과 비교하여 분기하는 경우에 유용하다.
```js
putstr("Enter a month number");
var monthNum = readline();
var monthName;
switch (monthNum) {
    case "1":
        monthName = "January"
        break;
    case "2":
        monthName = "February"
        break;
    case "3":
        monthName = "March"
        break;
    case "4":
        monthName = "April"
        break;
    case "5":
        monthName = "May"
        break;
    case "6":
        monthName = "June"
        break;
    case "7":
        monthName = "July"
        break;
    case "8":
        monthName = "August"
        break;
    case "9":
        monthName = "September"
        break;
    case "10":
        monthName = "October"
        break;
    case "11":
        monthName = "November"
        break;
    case "12":
        monthName = "December"
        break;
    default:
        console.log("Bad input");
}
```
자바스크립트의 switch문은 다른 프로그래밍 언어의 switch문과는 조금 다르다.  
가장 큰 차이 중 하나는 자바스크립트의 테스트 대상 표현식에는 모든 데이터형을 사용할 수 있는 반면 C++, 자바 등에서는 테스트 대상에 사용할 수 있는 데이터형이 정해져 있다.

#### 1.2.4 반복문

##### while문
어떤 조건이 참일 때 반복적으로 명령 집합을 실행하는 문
```js
var number = 1;
var sum = 0;
while (number < 11){
    sum += number;
    ++number;
}

console.log(sum);   // (출력값 55)
```
##### for문
명령 집합을 일정 횟수만큼 반복할 때는 for문을 사용한다.
```js
var number = 1;
var sum = 0;
for ( var number = 1; number < 11; number++){
    sum += number;
}

console.log(sum);   // (출력값 55)
```

배열의 요소에 잡근할 때도 for문을 자주 사용한다.
```js
var numbers = [3, 7, 12, 22, 100];
var sum = 0;
for (var i = 0; i < numbers.length; ++i){
    sum += numbers[i];
}

console.log(sum);   // (출력값 144)
```

#### 1.2.5 함수
자바스크립트는 값을 반환하는 함수와 반환하지 않는 함수(값을 반환하지 않는 함수를 서브프로시저 또는 void 함수라 한다.)를 모두 지원한다.
```js
//값을 반환하는 함수
function factorial( number ){
    var product = 1;
    for ( var i = number; i >= 1; --i ){
        product *= i;
    }
    return product;
}

console.log(factorial(4));  // (출력값 24)
console.log(factorial(5));  // (출력값 120)
console.log(factorial(10));  // (출력값 3628800)

//자바스크립트의 서브프로시저(또는 void 함수)
function curve( arr, amount ){
    for ( var i = 0; i < arr.length; ++i){
        arr[i] += amount;
    }
}

var grades = [77, 73, 74, 81, 90];
curve(grades, 5);
console.log(grades);    // (출력값 [82, 78, 79, 86, 95])
```
자바스크립트의 모든 함수 파라미터는 값으로 전달되며 레퍼런스 전용 파라미터는 없다.  
하지만 배열처럼 객체 레퍼런스를 함수 파라미터로 사용할 때는 위 예제에서 보여주는 것처럼 레퍼런스로 전달된다.


#### 1.2.6 변수 범위
변수의 범위란 프로그램의 어느 위치에서 변수를 접근할 수 있는지를 의미한다.  
자바스크립트의 변수는 함수 범위(function scope)로 정의된다.  
함수 범위란 변수가 선언되고 정의된 함수 내에서는 자유롭게 변수의 값에 접근할 수 있음을 의미한다.  

함수 외부 즉, 메인 프로그램에서 변수를 선언하면 전역 범위를 갖는다.  
전역 범위란 함수를 포함한 프로그램의 어느 곳에서나 변수에 접근할 수 있음을 의미한다.
```js
function showScope() {
    return scope;
}
var scope = 'global';
console.log(scope);         // (출력값 global)
console.log(showScope());   // (출력값 global)
```
scope는 전역 변수으르모 showScope() 함수는 scope에 접근할 수 있다.  
전역 변수는 함수 정의 전이든 후든 관계없이 프로그램의 어느 곳에서나 선언할 수 있다.

```js
function showScope() {
    var scope = 'local';
    return scope;
}

var scope = 'global';
console.log(scope);         // (출력값 global)
console.log(showScope());   // (출력값 local)
```
앞에서 자바스크립트는 함수 범위를 갖는다고 설명했다.  
이 말은 다른 현대 프로그래밍 언어와 달리 자바스크립트는 블록(block)범위를 지원하지 않음을 의미한다.  
블록 범위에서는 블록 내에서 정의한 변수는 블록 외부에서는 접근할 수 있다.

#### 1.2.7 재귀
자바스크립트는 재귀 함수 호출을 지원한다.
```js
function factorial( number ){
    if (number == 1){
        return number;
    } else {
        return number * factorial( number -1 );
    }
}

console.log(factorial(5));    // (출력값 120)
```
재귀를 이용하는 모든 함수는 반복 기법으로도 구현할 수 있다.

### 1.3 객체와 객체지향 프로그래밍

자바스크립트는 객체를 정의하고 사용할 수 있는 다양한 방법을 제공한다.
```js
//계좌 Checking 객체의 생성자 함수 예제
function Checking( amount ) {
    this.balance = amount;  //프로퍼티
    this.deposit = deposit; //함수
    this.withdraw = withdraw;   //함수
    this.toString = toString;   //함수
}

function deposit( amount ){
    this.balance += amount;
}

function withdraw( amount ){
    if ( amount <= this.balance ){
        this.balance -= amount;
    }
    if ( amount > this.balance ){
        console.log('Insufficient funds');
    }
}

function toString(){
    return 'Balance: ' + this.balance;
}

var account = new Checking(500);
account.deposit(1000);
console.log(account.toString());    // (출력값 Balance: 1500)
account.withdraw(750);
console.log(account.toString());    // (출력값 Balance: 750)
account.withdraw(800);              // (출력값 Insufficient funds)
console.log(account.toString());    // (출력값 Balance: 750)
```
