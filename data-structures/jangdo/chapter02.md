## Chapter02 배열
컴퓨터 프로그래밍에서 가장 자주 사용하는 자료구조는 배열이다.  
모든 프로그래밍 언어가 배열을 지원한다.  
배열은 내장 기능이므로 매우 효율적이며 데이터를 쉽게 저장할 수 있다.

### 2.1 자바스크립트 배열 정의
배열은 정수 인덱스(오프셋)를 이용해 **각 요소에 접근할 수 있게 순차적으로 요소를 저장한 집합체** 다.

자바스크립트는 일반적인 프로그래밍 언어와는 다른 종류의 배열을 제공한다.  

자바스크립트의 배열은 특화된 자바스크립트 객체며 정수 인덱스(객체의 프로퍼티 이름 역할)로 객체 내 테이터 오프셋을 표현한다.  
정수를 인덱스로 사용하면 자바스크립트 객체 요구사항에 맞게 내부적으로 정수를 `문자열`로 변환한다.

Array는 자바스크립트에서 공식적으로 제공하는 객체이므로 미리 정의된 프로퍼티와 함수를 이용할 수 있다.

### 2.2 배열 사용하기
자바스크립트의 배열은 매우 유용하다.  
배열을 만들고, 배열의 요소에 잡근하고, 배열에 저장된 요소를 검색하거나 정렬하는 등의 동작을 다양한 방법으로 수행할 수 있다.

#### 2.2.1 배열 만들기
**`[]`를 이용해 배열 변수를 선언하는 것이 배열을 만드는 가장 간단한 방법**
```js
var numbers = [];

console.log(numbers.length);    // (출력값 0)
```
위와 같은 방법으로 배열을 만들면 길이가 0인 배열이 만들어진다.  
내장된 length 프로퍼티를 이용해 배열의 길이를 확인할 수 있다.

**기호 안에 요소 집합을 이용해 배열 변수를 선언하는 방법**
```js
var numbers = [1, 2, 3, 4, 5];

console.log(numbers.length);    // (출력값 5)
```

**Array 생성자를 호출해서 배열을 만다는 방법**
```js
var numbers = new Array();

console.log(numbers.length);    // (출력값 0)
```

**Array 생성자의 인자에 요소 집합을 제공하는 방법**
```js
var numbers = new Array(1, 2, 3, 4, 5);

console.log(numbers.length);    // (출력값 5)
```

**Array 생성자에 배열 길이를 지정하는 방법(1개의 인자만 사용)**
```js
var numbers = new Array(10);

console.log(numbers.length);    // (출력값 10)
```

다른 언어와는 달리 자바스크립트에서는 한 배열이 다양한 종류의 요소를 포함할 수 있다.
```js
var objects = [1, "Joe", true, null];
```

**Array.isArray() 메서드**
Array.isArray() 메서드를 이용해 특정 객체가 배열인지 여부를 확인할 수 있다.
```js
var numbers = 3;
var arr = [7, 4, 1776];
console.log(Array.isArray(numbers));
console.log(Array.isArray(arr));
```

#### 2.2.2 배열 요소 접근하고 값 고치기
**할당 문에 `[]`를 이용해 배열 요소에 값을 할당할 수 있다.**
```js
var nums = [];
for(var i = 0; i < 10; ++i){
    nums[i] = i+1;
}

console.log(nums);  // (출력값 [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
```
**`[]`기호를 이용해 배열 요소에 접근할 수 있다.**
```js
var numbers = [1, 2, 3, 4, 5];
var sum = numbers[0] + numbers[1] + numbers[2] + numbers[3] + numbers[4];

console.log(sum);   // (출력값 15)
```

**for문을 이용하면 좀 더 쉽게 모든 배열 요소에 순차적으로 접근할 수 있다.**
```js
var numbers = [1, 2, 3, 5, 8];
var sum = 0;
for(var i = 0; i < numbers.length; ++i){
    sum += numbers[i];
}

console.log(sum);   // (출력값 19)``
```

#### 2.2.3 문자열로 배열 만들기
문자열에 split() 함수를 호출하면 배열이 생성된다.  
split() 함수는 문자열을 특정 구분자로 분리한 다음 분리된 문자열을 포함하는 배열을 만든다.
```js
var sentence = "this quick brown fox jumped over the lazy dog";
var words = sentence.split(" ");

console.log(words);    // (출력값 ["this", "quick", "brown", "fox", "jumped", "over", "the", "lazy", "dog"])

for(var i = 0; i < words.length; ++i){
    console.log("word " + i + ": " + words[i]);
}
/*
word 0: this
word 1: quick
word 2: brown
word 3: fox
word 4: jumped
word 5: over
word 6: the
word 7: lazy
word 8: dog
*/
```
#### 2.2.4 배열 전체에 적용되는 기능
배열 전체에 적용되는 기능도 있다.  
배열을 다른 배열로 할당할 수 있다.
```js
var nums = [];
for(var i = 0; i < 10; ++i){
    nums[i] = i+1;
}

var samenums = nums;

console.log(nums);      // (출력값 [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
console.log(samenums);  // (출력값 [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
```

배열을 다른 배열로 할당 할 때 실제로는 할당된 배열의 레퍼런스를 할당하는 것이다.  
따라서 원래 배열을 바꾸면 할당된 배열도 바뀐다.
```js
var nums = [];
for(var i = 0; i < 10; ++i){
    nums[i] = i+1;
}

var samenums = nums;
nums[0] = 400;
console.log(samenums[0]);   // (출력값 400)
```
이와 같은 동작을 **얕은 복사(shallow copy)** 라고 한다.  
새로 할당된 배열은 단순히 원래 배열의 요소를 카리킬 뿐이다.  
얕은 복사보다는 깊은 복사(deep copy) 즉, 원래 배열 요소를 새로운 배열 요소로 복사하는 기능이 필요할 때가 있다.
```js
function copy( arr1, arr2 ){
    for(var i = 0; i < arr1.length; ++i){
        arr2[i] = arr1[i];
    }
}

var nums = [];
var samenums = [];
for(var i = 0; i < 10; ++i){
    nums[i] = i+1;
}

copy(nums, samenums);
nums[0] = 400;
console.log(samenums[0]);   // (출력값 1)
```

### 2.3 접근자 함수
자바스크립트는 배열 요소에 접근할 수 있는 다양한 함수를 제공한다.  
이들을 접근자 함수(accessor function)라 부르며 특정값을 포함하는 결과 배열을 반환한다.

#### 2.3.1 값 검색하기
가장 자주 사용하는 접근자 함수 중 하나는 indexOf() 함수다.  
indexOf() 함수는 인자로 제공된 값이 배열에 존재하는지 알려준다.  
함수의 인자로 제공한 값이 배열에 있으면 **인덱스 위치를 반환** 하고 값이 배열에 없으면 **-1** 을 반환한다.
```js
var names = ['David', 'Mike', 'Cynthia'];
var name = 'Mike';
var firstPos = names.indexOf(name);

console.log(firstPos);  // (출략값 1)
```
indexOf() 함수로 찾으려는 값이 배열에 여러 개가 있으면 첫 번째로 발견한 인자의 인덱스를 반환한다.  
lastIndexOf() 함수는 indexOf() 함수와 비슷한 함수로 배열에서 일치하는 값 중 마지막 인자의 위치를 , 값을 찾지 못하면 `-1`을 반환한다.
```js
var names = ['David', 'Mike', 'Cynthia', 'Mike'];
var name = 'Mike';
var firstPos = names.indexOf(name);
var lastPos = names.lastIndexOf(name);

console.log(firstPos);  // (출력값 1)
console.log(lastPos);   // (출력값 3)
```

#### 2.3.2 배열을 문자열로 표현하기
join() 함수, toString() 함수는 배열을 문자열 형식으로 반환하는 함수다.  
두 함수 모두 배열의 요소를 콤마(,)로 구분하는 문자열을 반환한다.
```js
var names = ['David', 'Mike', 'Cynthia', 'Mike'];
var joinStr = names.join();
var toStr = names.toString();

console.log(joinStr);  // (출력값 David,Mike,Cynthia,Mike)
console.log(toStr);  // (출력값 David,Mike,Cynthia,Mike)
```

#### 2.3.3 기존 배열을 이용해 새 배열 만들기

concat() 함수, splice() 함수는 기존 배열을 이용해 새 배열을 만드는 함수다.  

**concat() 함수**  
두 개 이상의 배열을 합쳐 새 배열을 만든다.

기존의 배열에 concat() 함수를 호출하면 인자로 또 다른 기존 배열을 제공한다.  
그러면 인자로 제공된 배열이 원래 **concat() 함수를 호출한 배열 뒤로 추가** 된다.
```js
var cisDept = ["Mike", "Clayton", "Terrill", "Danny", "Jennifer"];
var dmpDept = ["Raymond", "Cynthia", "Bryan"];
var itDiv = cisDept.concat(dmpDept);

console.log(itDiv);     // (출력값 ["Mike", "Clayton", "Terrill", "Danny", "Jennifer", "Raymond", "Cynthia", "Bryan"])

itDiv = dmpDept.concat(cisDept);

console.log(itDiv);     // (출력값 ["Raymond", "Cynthia", "Bryan", "Mike", "Clayton", "Terrill", "Danny", "Jennifer"])
```

**splice() 함수**  
기존 배열의 서브셋으로 새 배열을 만든다.  

splice() 함수는 사용할 첫 요소의 위치, 기존 배열에서 사용할 요소의 수를 인자로 받는다.
```js
var itDiv = ["Mike", "Clayton", "Terrill", "Danny", "Jennifer"];
var dmpDept = itDiv.splice(3, 2);
var cisDept = itDiv;

console.log(dmpDept);   // (출력값 ["Danny", "Jennifer"])
console.log(cisDept);   // (출력값 ["Mike", "Clayton", "Terrill"])
```
배열에 요소를 추가하거나 배열의 요소를 제거하는 등 배열을 고치는 용도로 splice() 함수를 활용할 수 있다.

### 2.4 변형자 함수
자바스크립트는 개별적으로 요소를 건드리지 않고 배열 전체 내용을 고치는 여러 변형자 함수(mutator function)를 제공한다.  
이들 함수를 잘 활용하면 어려운 문제도 쉽게 해결할 수 있다.

#### 2.4.1 배열에 요소 추가하기
push() 함수, unshift() 함수는 각각 배열에 요소를 추가하고, 배열의 요소를 제거하는 함수다.
```js
var nums = [1, 2, 3, 4, 5];
console.log(nums);  // (출력값 [1, 2, 3, 4, 5])
nums.push(6);
console.log(nums);  // (출력값 [1, 2, 3, 4, 5, 6])
```
length 프로퍼티를 이용해 배열을 확장하는 것보다 push() 함수를 이용하는 것이 더 직관적이다.  

배열의 처음에 요소를 추가하는 것보다 배열의 끝에 요소를 추가하는 것이 쉽다.  
배열의 처음에 요소를 추가할 때 변형자 함수가 없다면 배열에 있던 기존의 모든 요소를 한 칸씩 뒤로 이동 시킨 다음 새 데이터를 추가해야 한다.  
```js
var nums = [2, 3, 4, 5];
var newnum = 1;
var N = nums.length;
for(var i = N; i >= 0; --i){
    nums[i]  = nums[i-1];
}
nums[0] = newnum;
console.log(nums);  // (출력값 [1, 2, 3, 4, 5])
```

unshift() 함수는 이런 고민을 간단하게 해결해준다.
```js
var nums = [2, 3, 4, 5];
var newnum = 1
nums.unshift(newnum);
console.log(nums);  // (출력값 [1, 2, 3, 4, 5])

nums = [3, 4, 5];
nums.unshift(newnum, 2);
console.log(nums);  // (출력값 [1, 2, 3, 4, 5])
```
unshift() 호출 코드는 한 번에 여려 요소를 배열 앞으로 추가할 수 있음을 알 수 있다.

#### 2.4.2 배열의 요소 삭제하기
pop() 변형자 함수를 이용하면 간단하게 배열의 **마지막 요소를 제거** 할 수 있다.
```js
var nums = [1, 2, 3, 4, 5, 9];
nums.pop();

console.log(nums);  // (출력값 [1, 2, 3, 4, 5])
```
배열의 앞 요소를 제거할 때 변형자 함수가 없다면 배열의 앞 요소를 제거한 다음 나머지 요소를 앞으로 이동시켜야 한다.  
결국 배열 앞에 요소를 추가할 때와 마찬가지로 비효율적인 동작을 수행하게 한다.
```js
var nums = [9, 1, 2, 3, 4, 5];
for(var i = 0; i < nums.length; ++i){
    nums[i] = nums[i+1];
}

console.log(nums);  // (출력값 [1, 2, 3, 4, 5, undefined])
```
제거된 요소의 자리를 채우느라 나머지 모든 요소를 이동시키고 나면 맨 끝에는 불필요한 값이 저장된다.  

shift() 함수를 이용하면 간단히 배열의 맨 처음 요소를 제거할 수 있다.
```js
var nums = [9, 1, 2, 3, 4, 5];
nums.shift();

console.log(nums);  // (출력값 [1, 2, 3, 4, 5])
```
배열의 끝에 불필요한 요소가 없어졌음을 알 수 있다.  
pop() 함수, shift() 함수는 제거된 요소를 반환하므로 필요하다면 반환된 요소를 변수에 저장할 수 있다.
```js
var nums = [6, 1, 2, 3, 4, 5];
var first = nums.shift();
nums.push(first);

console.log(nums);  // (출력값 [1, 2, 3, 4, 5, 6])
```

#### 2.4.3 배열 중간에 요소를 추가하거나 배열의 중간에 있는 요소 삭제하기

배열의 중간에 요소를 추가하거나 삭제할 때도 배열의 처음에 요소를 추가하거나 삭제할 때처럼 다른 요소를 이동시켜야 하는 문제가 생긴다.  
`splice() 변형자 함수`를 이용하면 한번에 두 가지 동작을 수행할 수 있다.  

**splice() 함수**
- 시작 인덱스(어느 지점부터 요소를 추가할 것인지)
- 삭제할 요소의 개수(요소를 추가할 때는 0)
- 배열의 추가할 요소들

```js
var nums = [1, 2, 3, 7, 8, 9];
var newElements = [4, 5, 6];
nums.splice(3, 0, 4, 5, 6);
console.log(nums);  // (출력값 [1, 2, 3, 4, 5, 6, 7, 8, 9])
```

#### 2.4.4 배열 요소 정렬하기
**reverse() 함수**
reverse() 함수는 배열의 요소를 역순으로 바꾼다.
```js
var nums = [1, 2, 3, 4, 5];
nums.reverse();

console.log(nums);  // (출력값 [5, 4, 3, 2, 1])
```

**sort() 함수**
배열 요소를 순서대로 정렬할 때 사용한다.  
특히 문자열을 정렬할 때 유용하다.
```js
var names = ['David', 'Mike', 'Cynthia', 'Clayton', 'Bryan'];
names.sort();

console.log(names); // (출력값 ["Bryan", "Clayton", "Cynthia", "David", "Mike"])
```
숫자는 생각대로 정렬되지 않는다.
```js
var nums = [3, 1, 2, 100, 4, 200];
nums.sort();

console.log(nums);  // (출력값 [1, 100, 2, 200, 3, 4])
//// ASCII 문자 순서로 정렬되어 숫자의 크기대로 나오지 않음
```
sort() 함수는 배열 요소를 모두 문자열로 간주하고 알파벳순으로 요소르 정렬한다.  
sort() 함수에 순서를 결정해주는 함수(ordering function)를 인자로 전달하면 sort() 함수는 인자로 전달된 함수를 이용해 숫자를 올바르게 정렬할 수 있다.  
sort() 함수는 인자로 전달된 함수를 이용해 배열 요소 값이 올바른 순서로 정렬되었는지 검사한다.
```js
function compare( num1, num2 ){
    console.log(num1, num2)
    return num1 - num2;
}
var nums = [3, 1, 2, 100, 4, 200];
nums.sort(compare);

console.log(nums);  // (출력값 [1, 2, 3, 4, 100, 200])
```

### 2.5 반복자 함수

반복자 함수는 **배열의 각 요소에 함수를 적용한 다음 그 결과 값 또는 집합 또는 새로운 배열을 반환** 한다.

#### 2.5.1 배열을 만들지 않는 반복자 함수
**forEach() 함수**
forEach() 함수는 배열의 모든 요소에 인자로 받은 함수를 호출한다.
```js
function square( num ){
    console.log(num, num * num);
}

var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
nums.forEach(square);

/*
1 1
2 4
3 9
4 16
5 25
6 36
7 49
8 64
9 81
10 100
*/
```
**every() 함수**

every() 함수는 불린 함수를 배열에 적용해 **배열의 모든 요소가 참** 이면 `true`를 반환한다.
```js
function isEven( num ){
    return num % 2 == 0;
}

var nums = [2, 4, 6, 8, 10];
var even = nums.every(isEven);
if ( even ){
    console.log('true');
} else {
    console.log('false');
}

// --------------------------

var nums = [2, 3, 4, 6, 8];
var even = nums.every(isEven);
if ( even ){
    console.log('true');
} else {
    console.log('false');
}
// (출력값 false)
```

**some() 함수**

some() 함수는 배열 요소 중에 **한 요소라도 인자로 받은 불린 요소의 기준을 만족** 하면 `true`를 반환한다.

```js
function isEven( num ){
    return num % 2 == 0;
}

var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var someEven = nums.some(isEven);
if ( someEven ){
    console.log('true');
} else {
    console.log('false');
}
// (출력값 true)

// --------------------------

var nums = [1, 3, 5, 7, 9];
var someEven = nums.some(isEven);
if ( someEven ){
    console.log('true');
} else {
    console.log('false');
}
// (출력값 false)
```

**reduce() 함수**
reduce() 함수는 누적자 함수를 인자로 받은 다음 배열의 모든 요소를 누적자 함수에 적용한다.
```js
function add(runningTotal, currentValue){
    return runningTotal + currentValue;
}

var nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var sum = nums.reduce(add);

console.log(sum);   // (출력값 55)
```
reduce() 함수를 이용해 문자열을 연결할 수도 있다.
```js
function concat(accumulatedString, item){
    return accumulatedString + item;
}

var words = ['the ', 'quick ', 'brown ', 'fox '];
var sentence = words.reduce(concat);

console.log(sentence);  // (출력값 the quick brown fox)
```

reduceRight() 함수를 이용해 배열 요소의 순서를 뒤집을 수 있다.

#### 2.5.2 새 배열을 반환하는 반복자 함수
map() 함수, filter() 함수는 모두 새 배열을 반환하는 반복자 함수다.  
map() 함수는 forEach() 함수처럼 배열의 각 요소에 함수를 적용하는 함수다.  

**map() 함수**

map() 함수는 배열 요소에 함수를 적용한 결과를 포함하는 **새 배열을 반환** 한다는 점이 다르다.
```js
function curve( grade ){
    return grade += 5;
}
var grades = [1, 2, 3, 4, 5];
var newgrades = grades.map(curve);
console.log(grades);        // (출력값 (5) [1, 2, 3, 4, 5])
console.log(newgrades);     // (출력값 (5) [6, 7, 8, 9, 10])

//문자열에 map() 함수 사용
function first( word ){
    return word[0];
}

var words = ['for', 'your', 'information'];
var acronym = words.map(first);
console.log(acronym);           // (출력값 ["f", "y", "i"])
console.log(acronym.join(""));  // (출력값 fyi)
```
**filter() 함수**
filter() 함수는 every() 함수와 비슷하다.  
다만 every() 함수처럼 배열의 모든 요소가 불린 함수를 만족할 때 true를 반환하는 것이 아니라, filter() 함수는 **불린 함수를 만족하는 요소를 포함하는 새로운 배열을 반환** 한다.
```js
function isEven ( num ) {
    return num % 2 == 0;
}

function isOdd ( num ) {
    return num % 2 != 0;
}

var num = [];
for ( var i = 0; i < 20; ++i ){
    nums[i] = i+1;
}

var evens = nums.filter(isEven);
console.log(evens);     // (출력값 [2, 4, 6, 8, 10, 12, 14, 16, 18, 20])

var odds = nums.filter(isOdd);
console.log(odds);      // (출력값 [1, 3, 5, 7, 9, 11, 13, 15, 17, 19])
```
filter() 함수를 다음처럼 활용할 수 있다.
```js
function passing( num ){
    return num >= 60;
}

var grades = [];
for ( var i = 0; i < 10; ++i ){
    grades[i] = Math.floor(Math.random() * 101);
}

var passGrades = grades.filter(passing);

console.log(grades);    // (출력값 [11, 72, 87, 91, 61, 51, 25, 83, 32, 42])
console.log(passGrades);// (출력값 [72, 87, 91, 61, 83])
```

### 2.6 이차원 배열과 다차원 배열
자바스크립트는 기본적으로 일차원 배열만 지원한다.  
하지만 배열의 배열을 이용해 다차원 배열을 만들수 있다.

#### 2.6.1 이차원 배열 만들기
이차원 배열은 행과 열을 가진 스프레드시트 같은 구조다.  
이차원 배열을 만들려면 배열을 만든 다음 각 요소를 배열로 만들어야 한다.  
최소한의 배열의 행 개수를 알아야 이차원 배열을 만들 수 있다.
```js
var twod = [];
var rows = 5;
for (var i = 0; i < rows; ++i){
    twod[i] = [];
}
console.log(twod);  // (출력값 [Array(0), Array(0), Array(0), Array(0), Array(0)])
```
