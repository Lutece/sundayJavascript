## 리스트
### 3.1 리스트 ADT
- 리스트는 순서가 있는 일련의 데이터 집합이다.  
- 리스트에 저장된 각 데이터 항목을 요소(element)라 부른다.  
- 자바스크립트에서는 모든 데이터형이 리스트의 요소가 될 수 있다.  
- 리스트에 저장할 수 있는 요소 수에는 제한이 없다.  

[리스트 ADT 표]

| listSize(프로퍼티) | 리스트의 요소 수
| :----------------- | :-----------
| pos (프로퍼티)     | 현재 위치
| length (프로퍼티)  | 리스트의 요소 수 반환
| clear (함수)       | 리스트의 모든 요소 삭제
| toString (함수)    | 리스트를 문자열로 표현해 반환
| getElement (함수)  | 현재 위치를 반환
| insert (함수)      | 기존 요소 위로 새 요소를 추가
| append (함수)      | 새 요소를 리스트 끝에 추가
| remove (함수)      | 리스트의 요소 삭제
| front (함수)       | 현재 위치를 리스트 첫 번째 요소로 설정
| end (함수)         | 현재 위치를 리스트 마지막 요소로 설정
| prev (함수)        | 현재 위치를 한 요소 뒤로 이동
| next (함수)        | 현재 위치를 한 요소 앞으로 이동
| currPos (함수)     | 리스트의 현재 위치 반환
| moveTo (함수)      | 현재 위치를 지정된 위치로 이동

### 3.2 List 클래스 구현
위에서 정의한 리스트 ADT를 이용해 List 클래스를 구현할 수 있다.  
ADT에는 없었지만 우선 생성자 함수부터 정의한다.
```js
function List(){
    this.listSize = 0;
    this.pos = 0;
    this.dataStore = [];    // 리스트 요소를 저장할 빈 배열 초기화
    this.clear = clear;
    this.find = find;
    this.toString = toString;
    this.insert = insert;
    this.append = append;
    this.remove = remove;
    this.front = front;
    this.end = end;
    this.prev = prev;
    this.next = next;
    this.lenght = lenght;
    this.currPos = currPos;
    this.moveTo = moveTo;
    this.getElement = getElement;
    this.contains = contains;
}
```

#### 3.2.1 Append :  리스트에 요소 추가
append() 함수는 리스트의 다음 가용 위치(= listSize 변수의 값)에 새 요소를 추가하는 함수다.
```js
function append(element){
    this.dataStore[this.listSize++] = element;
}
```
요소를 추가한 다음 listSize를 1만큼 증가시킨다.

#### 3.2.2 Remove : 리스트의 요소 삭제
remvoe() 함수는 List 클래스의 함수 중 가장 구현하기 어려운 함수에 속한다.  
우선 리스트에서 삭제하려는 요소를 찾은 다음, 요소를 삭제하고 나머지 배열 요소를 왼쪽으로 이동시켜 요소가 삭제된 자리를 메워야 한다.
```js
function find(element){
    for ( var i = 0; i < this.dataStore.length; ++i ){
        if (this.dataStore[i] == element){
            return i;
        }
    }
    return -1;
}
```

#### 3.2.3 Find : 리스트의 요소 검색
find() 함수는 루프로 dataStore를 반복하면서 원하는 요소를 검색한다.  
요소를 발견하면 요소의 위치를 반환한다.  
요소를 발견하지 못하면 배열에서 요소를 찾지 못했을 때 반환하는 표준 값인 -1을 반환한다.  

remove() 함수는 find() 함수의 반환값으로 에러를 검사할 수 있다.
```js
function remove(element){
    var foundAt = this.find(element);
    if (foundAt > -1){
        this.dataStore.splice(foundAt, 1);
        --this.listSize;
        return true;
    }
    return false;
}
```
remove() 함수는 find() 함수의 반환값을 splice() 함수에 넘겨주어 원하는 요소를 삭제한 다음 dataStore 배열을 연결한다.  
remove() 함수는 요소를 삭제했으면 `true`를 반환하고, 요소를 삭제하지 못했으면 `false`를 반환한다.

#### 3.2.4 Length : 리스트의 요소 개수
length() 함수는 리스트의 요소 수를 반환한다.
```js
function length(){
    return this.listSize;
}
```

#### 3.2.5 toString : 리스트의 요소 확인
이번에는 리스트의 요소를 확인하는 함수를 만든다.  
다음은 간단한 toString() 함수를 구현한 코드다.
```js
function toString(){
    return this.dataStore;
}
```
엄밀히 말해 toString() 함수는 문자열이 아닌 배열 객체를 반환한다.  
하지만 배열을 반환하므로 현재 요소 상태를 확인할 수 있다.  
```js
var names = new List();

names.append('Cynthia');
names.append('Raymond');
names.append('Barbara');
console.log(names.toString());  // (출력값 ["Cynthia", "Raymond", "Barbara"])
names.remove('Barbara');
console.log(names.toString());  // (출력값 ["Cynthia", "Raymond"])
```

#### 3.2.6 Insert : 리스트에 요소 삽입
요소를 삽입하려면 어디에 요소를 삽입할 지 지시해야 한다.  
insert() 함수에서는 리스트의 기존 요소 뒤에 새로운 요소를 삽입하게 한다.
```js
function insert(element, after){
    var insertPos = this.find(after);
    if ( insertPos > -1 ){
        this.dataStore.splice(insertPos + 1, 0, element);
        ++this.listSize;
        return true;
    }
    return false;
}
```
insert() 함수는 헬퍼 함수 find(after)를 이용해 새 요소의 삽입 위치를 결정한다.  
요소를 삽입할 위치를 찾았으면 splice() 함수를 이용해 새 요소를 리스트에 추가한다.  
그리고 listSize를 1만큼 증가시키고 요소를 성공적으로 삽입했으므로 `true`를 반환한다.

#### 3.2.7 리스트의 모든 요소 삭제
새로운 요소를 리스트에 입력할 수 있게 리스트의 모든 요소를 삭제하는 함수이다.
```js
function clear(){
    delete this.dataStore;
    this.dataStore.length = 0;
    this.listSize = this.pos = 0;
}
```
clear() 함수는 delete 명령어로 dataStore 배열을 삭제한 다음 빈 배열을 다시 만든다.

#### 3.2.8 Contains : 리스트에 특정값이 있는지 판단
contains() 함수는 어떤 값이 리스트에 포함되어 있는지를 확인할 때 사용한다.
```js
function contains(element){
    for ( var i = 0; i < this.dataStore.length; ++i){
        if ( this.dataStore[i] == element ){
            return true;
        }
    }
    return false;
}
```

#### 3.2.9 리스트 탐색
다음 함수는 리스트 탐색 관련 기능과 관련이 있으며 마지막의 getElement() 함수는 리스트의 현재 요소를 출력한다.
```js
function front(){
    this.pos = 0;
}

function end(){
    this.pos = this.listSize-1;
}

function prev(){
    if ( this.pos > 0 ){
        --this.pos;
    }
}

function next(){
    if ( this.pos < this.listSize-1 ){
        ++this.pos;
    }
}

function currPos(){
    return this.pos;
}

function moveTo(posiiton){
    this.pos = position;
}

function getElement(){
    return this.dataStore[this.pos];
}

var names = new List();

names.append('Cynthia');
names.append('Raymond');
names.append('Barbara');
names.front();
console.log(names.getElement());    // (출력값 Cynthia)
names.next();
console.log(names.getElement());    // (출력값 Raymond)
```

### 3.3 리스트와 반복
반복자를 이용하면 List 클래스의 내부 저장소를 직접 참조하지 않고 리스트를 탐색할 수 있다.  
List 클래스의 front() 함수, end() 함수, prev() 함수, next() 함수, currPos() 함수를 이용해 반복자를 구현할 수 있다.  
반복자는 배열의 인덱스에 비해 다음과 같은 장점이 있다.
