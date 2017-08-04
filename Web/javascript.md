### basic of basic

- alert();

- confirm();

- prompt();

- console.log()

- = vs == vs ===

- "string".substring(0, 6);

- "Hamburgers".substring(3, );

- 변수선언 : var

### function

- 함수 선언
```js
function funcA () {

    //...

}
```
- 함수 표현식
```js
var funcA = function() {

    //...

}
```

#### undefined
- 만약 함수 내부에서 리턴값을 지정하지 않았다면, 자동으로 undefined가 반환된다.

```js
var divideByThree = function (number) {

    var val = number / 3;

    console.log(val);

};

divideByThree(6);
```

```js
function divideByFour (number) {

    var val = number / 4;

    console.log(val);

};

divideByFour(10);
```

```js
function divideByFour (number) {

    var val = number / 4;

    return number / 4;

};
```

### for loop
#### forEach loop

- forEach()
```js
donuts.forEach(function(donut) {
        donut += " hole";
        donut = donut.toUpperCase();
        console.log(donut);
        });
``
- forEach의 매개변수 안에 함수가 들어가면, 각 배열의 값을 한번씩 해당 함수의 파라미터로 보내주는듯?

### tuple
```js
var tuple = ["Name", 100, true, "aaaaa"];

console.log(tuple[0]);
```

### array
- .push()

- push할때[]안에 값이 아닌 변수가 들어있으면, 해당 값이 출력됨
```js
var a = 10;

var ary = [a];

console.log(ary[0]) //10이 출력됨
```

- .pop()    //뒤에서부터 하나씩 뺌

- .shift()  //앞에서부터 하나씩 뺌

- .splice(없앨놈 인덱스, 얼마나 없앨지, 붙일값, 붙일값,..)  //접착
```js
var donuts = ["cookies", "cinnamon sugar", "creme de leche"];

donuts.splice(-2, 0, "chocolate frosted", "glazed");

// 결과 : ["cookies", "chocolate frosted", "glazed", "cinnamon sugar", "creme de leche"]
``

- .slice()

- .reverse()    //배열 거꾸로.. 문자열일 경우에도 거꾸로. 숫자나 bool타입일경우 에러

- .sort()

- .join('');
```js
['a', 'b', 'c', 'd'].join()     //'a,b,c,d'
```
```js
['a', 'b', 'c', 'd'].join('')     //'abcd'
```

### Hoisting
- 함수or 변수 호출이 정의보다 먼저 이루어진다고 하더라도, 자바스크립트 해석기는 정의 부분을 먼저 띄워서 해석한다. (그렇다고 소스코드를 건들지는 않음)

#### example
```js
// 다음과 같은 코드라 하더라도
hello()

function hello() {

    console.log("hello!");

}

```

```js
// 이렇게 해석해서 실행됨
hello()

function hello() {

    console.log("hello!");

}

```

#### example
```js
function hello() {
// 다음과 같은 코드라고 하더라도
    console.log(greeting);

    var greeting = "hello!";

}

```
```js
// 이렇게 해석되서 실행됨
function hello() {

    var greeting;

    console.log(greeting);

    greeting = "hello!";

}
// console.log에서 출력할 내용이 없으므로 출력 결과는 undefined가 됨.
// 결론 : 함수의 정의와 필드의 정의를 위에다 해서 자잘한 버그를 막자!

```
```js
sayHi("Julia");

function sayHi(name) {
      console.log(greeting + " " + name);
        var greeting;
}
// 위의 출력 결과는: undefined julia
```

#### 기타 
- JavaScript는 함수 선언과 변수 선언을 현재 범위의 맨 위로 올린다.

- 변수 할당은 게양되지 않는다.

- 함수의 정의방법 중 함수 표현식은 계양되지 않는다.(변수의 할당이기 때문에?)

- 스크립트의 맨 위에 함수와 변수를 선언하면 구문과 동작이 서로 일치한다.

### object

```js
var obj = {
    name: 'aaa',
    
    age: 100,
    
    getAge: function() {

    }

};  

//오브젝트 기본형식. 필드명or 메소드명을 "name"등으로 쓰지 말고, 숫자로 시작하지도 말것
//메소드 or 필드에 접근하는법 : obj.name, obj["name"] 두가지로 가능
```

