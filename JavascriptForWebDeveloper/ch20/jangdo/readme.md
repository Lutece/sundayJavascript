# JSON
더글라스 크락포드가 처음 만든 자바스크립트 객체 표기법(JavaScript Object Notation)
- JSON은 자바스크립트의 엄격한 부분집합니다.
- 자바스크립트의 여러 가지 패턴을 사용해 구조화된 데이터를 표현한다.
- JSON은 eval()에 직접 넘길 수 있으며 DOM을 따로 생성할 필요가 없다.
- JSON은 프로그래밍 언어가 아니라 <strong>데이터 형식</strong>이다.
- 많은 프로그래밍 언어에서 JSON파싱과 직렬화를 지원한다.

## 20.1 문법
JSON문법은 세가지 타입을 사용한다.
- 단순한 값 - JSON에서 문자열, 숫자, 불리언, null은 모두 자바스크립트와 같은 문법으로 표현한다. (undefined는 지원안함)
- 객체 - 객체는 순서 있는 키-값 쌍으로 표현한다. 각 값은 원시 타입일 수도 있고 객체나 배열 같은 복잡한 타입일 수도 있다.
- 배열 - 배열은 숫자형 색인으로 접근할 수 있는, 순서 있는 목록으로 표현한다.
각 값은 단순한 값이나 객체, 다른 배열 등을 모두 쓸 수 있다.

### 20.1.1 단순한 값
자바스크립트 문자열과 JSON 문자열의 차이는 JSON 문자열은 반드시 큰따옴표로 감싸야만 유효하다는 점이다.
불리언 값과 null은 그 자체로 유효한 JSON이다.

### 20.1.2 객체
JSON 객체는 객체 리터럴 표기법과 매우 비슷하다.
```js
//자바스크립트 객체 리터럴
var person = {
    name : "Nicholas",
    age : 29
};

var object = {
    "name" : "Nicholas",
    "age" : 29
};
```
JSON에서는 프로퍼티 이름도 따옴표로 묶어야 한다.
```js
//JSON 객체
{
    "name" : "Nicholas",
    "age" : 29
}
```
###### 자바스크립트 예제와 다른 몇 가지
1. 변수 선언이 없다.(JSON에는 변수가 존재하지 않는다.)
2. 문장을 마치는 세미콜론이 없다.(자바스크립트 문장이 아니므로 필요 없다.)
3. 값은 JSON에서 허용하는 모든 타입을 쓸 수 있으며 객체 안에 객체를 쓸 수 있다.
```js
{
    "name" : "Nicholas",
    "age" : 29,
    "school" : {
        "name" : "School College",
        "lacation" : "North Andover, MA"
    }
}
```

### 20.1.3 배열
JSON 배열은 자바스크립트의 배열 리터럴 표기법으로 표현한다.
```js
// JavaScript 배열
var values = [25, "hi", true];

// JSON 배열
[25, "hi", true]
```
변수와 세미콜론이 없다.

객체와 배열은 일반적으로 JSON 데이터 구조에서 최상위 레벨에 있으며 이들을 조합하여 다양한 데이터 구조를 만들 수 있다.

### 20.2 파싱과 직렬화
- 친근한 문법
- JSON 데이터를 파싱하면 바로 사용할 수 있는 자바스크립트 객체가 된다.

## 20.2.1 JSON 객체
JSON 객체에는 stringify()와 parse() 두 가지 메서드가 있다.
이들 메서드는 각각 자바스크립트 객체를 JSON 문자열로 직렬화하며, JSON을 파싱하여 네이티브 자바스크립트 값으로 바꾼다.
```js
//stringify()
var book = {
    title : "Professtional JavaScript",
    authors : [
        "Nicholas C. Zakas"
    ],
    edition : 3,
    year : 2011
};

var jsonText = JSON.stringify(book);

{"title":"Professtional JavaScript","authors":["Nicholas C. Zakas"],"edition":3,"year":2011}
```
JSON.stringify()가 직렬화한 JSON 문자열에는 공백이나 들여쓰기가 전혀 없다.
- 자바스크립트 객체를 직렬화 할 때는 모든 함수와 프로토타입 멤버가 생략된다.(의도한 결과이다.)
- 값이 undefined인 프로퍼티도 모두 생략한다.(JSON 데이터 타입으로 표현 가능한 인스턴스 프로퍼티만 남는다.)

JSON 문자열을 JSON.parse()에 넘기면 적절한 자바스크립트 값이 생성된다.
```js
//parse()
var bookCopy = JSON.parse(jsonText);

Object {title: "Professtional JavaScript", authors: Array(1), edition: 3, year: 2011}
```
JSON.parse()에 전달한 텍스트가 유효한 JSON이 아닐 경우 에러가 발생한다.

### 20.2.2 직렬화 옵션 (JSON.stringify())
JSON.stringify() 메서드는 직렬화할 객체 외에 두 가지 매개변수를 더 받을 수 있다.
1. 첫 번째 매개변수는 필터이다 (배열이나 함수를 쓸 수 있다.)
2. 두 번째 JSON 문자열의 들여쓰기를 조절합니다.

### 결과 필터링
##### 첫 번째 매개변수
```js
var book = {
    title : "Professtional JavaScript",
    authors : [
        "Nicholas C. Zakas"
    ],
    edition : 3,
    year : 2011
};

var jsonText = JSON.stringify(book, ["title", "edition"]);

{"title":"Professtional JavaScript","edition":3}
```
직렬화할 객체의 프로퍼티와 일치하는 프로퍼티만 JSON 문자열에 포함된다.

##### 두 번째 매개변수
- 두 번째 매개변수가 함수일 경우엔 조금 다르게 동작한다.
- 콜백 함수는 자동으로 프로퍼티의 이름과 값을 매개변수로 받는다.
- 키 이름에 따라 프로퍼티를 다르게 처리할 수 있다.
- undefined가 반환되면 해당 프로퍼티는 생략된다.
```js
var book = {
    title : "Professtional JavaScript",
    authors : [
        "Nicholas C. Zakas"
    ],
    edition : 3,
    year : 2011
};

var jsonText = JSON.stringify(book, function(key, value){
    switch(key){
        case "authors" :
            return value.join(",")
        case "year" :
            return 5000;
        case "edition" :
            return undefined;
        default :
            return value;
    }
});

{"title":"Professtional JavaScript","authors":"Nicholas C. Zakas","year":5000}
```
이 함수는 키에 따라 다른 값을 반환한다.
필터 함수를 만들 때는, 넘어온 값을 그대로 반환다는 기본 동작(default 절)을 넣는 것이 중요하다.

### 문자열 들여쓰기
- JSON.stringify()의 세 번째 매개변수는 들여쓰기와 공백을 컨트롤 한다.
- 매개변수에 <code>숫자</code>를 넘기면 각 레벨마다 그만큼을 들여쓴다.
```js
var book = {
    title : "Professtional JavaScript",
    authors : [
        "Nicholas C. Zakas"
    ],
    edition : 3,
    year : 2011
};

var jsonText = JSON.stringify(book, null, 4);

{
    "title": "Professtional JavaScript",
    "authors": [
        "Nicholas C. Zakas"
    ],
    "edition": 3,
    "year": 2011
}
```
들여쓰기 최댓값은 <strong>10</strong>이며, 이보다 큰 값은 자동으로 10으로 바뀐다.

### 20.2.3 파싱 옵션 (JSON.parse())
JSON.parse() 메서드 역시 각 키-값 쌍에서 호출될 콜백 함수를 추가적인 매개변수로 받는다.
```js
var book = {
    title : "Professtional JavaScript",
    authors : [
        "Nicholas C. Zakas"
    ],
    edition : 3,
    year : 2011,
    releaseDate : new Date(2017, 04, 1)
};

var jsonText = JSON.stringify(book);

var bookCopy = JSON.parse(jsonText, function(key, value){
    if ( key == "releaseDate") {
        return new Date(value);
    } else {
        return value;
    }
});

Object {title: "Professtional JavaScript", authors: Array(1), edition: 3, year: 2011, releaseDate: Mon May 01 2017 00:00:00 GMT+0900 (대한민국 표준시)}
```

## 요약
- JSON은 복잡한 데이터 구조를 쉽게 표현하도록 디자인된 경량화된 데이터 형식이다.
- 형식은 자바스크립트 문법희 부분집합을 이용하여 객체, 배열, 문자열, 숫자, 불리언, null을 표현한다.
