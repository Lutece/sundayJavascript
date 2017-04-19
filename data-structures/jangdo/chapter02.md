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
console.log(typeof names);
```
