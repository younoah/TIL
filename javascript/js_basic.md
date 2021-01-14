![](https://images.velog.io/images/younoah/post/216b18bb-66f9-478f-8206-941dd76bdbed/2021-01-12_21-42-08.png)

## 주석

```javascript
// 한줄 주석

/*
여러줄
주석
*/
```



## 변수와 상수

> 기본적으로 `const`를 사용하고 값이 바뀌어야하는 변수가 필요할때만 `let` 을 사용하자. 

### 변수(let)

```javascript
let str = "abc";
```



### 상수(const)

```javascript
const nbr = 123;
```



❗️**var** 는 존재는 하나 사용하지 말자.

ES6 전에는 변수를 선언할때 `var` 만 사용할 수 있었다. javascript에서 'var hoisting'이라는 규칙과 'block scope'가 없기 때문에  `var` 키워드로 변수를 선언하게되면 의도치 않게 에러를 만날수 있으므로 사용하지 않는다.


### 전역변수 지역변수

```javascript
let globalName = "uno"; // 전역변수
{
	let localName = "younoah"; // 지역변수
	console.log(localName);
  	console.log(globalName);
}
console.log(globalName);
// uno
console.log(localName);
// 에러
```

지역변수는 중괄호 안에서 정의된 변수를 의미한다. 중괄호 안에서만 사용할 수 있고 중괄호가 끝나면 메모리에서 해제되어 사용할 수 없다.

반면 전역변수는 프로그램 종료전까지 계속 사용이 가능하고 어디서든(어느지역 안에서도) 사용이 가능하다. 프로그램이 종료되어야 메모리에 해제되기 때문에 가능한 적게 사용하는 것이 좋다.



## 자료형

> 자바스크립트에서는 기본적으로 자료형을 선언하지 않는다.
>
> 값을 넣는대로 자료형이 정해진다.



### 정수형(Int)

```javascript
const intNbr = 7;
```



### 실수형(Float)

```javascript
const floatNbr = 3.14;
```



### 문자열(String)

```javascript
const str1 = "This is String";
const str2 = "This is String too";
console.log('younoah\'s book\nThis book is good'); // 백슬래시를 사용하여 따옴표와 줄바꿈을 표현할 수 있다.
```

> C/C++에서는 문자는 따옴표('), 문자열은 큰따옴표(")로 구분하여 사용하지만
>
> 자바스크립트에서는 문자열 자료형과 문자 자료형을 구분하지 않고 모두 같은 문자열이기 때문에
>
> 큰따옴표("), 따옴표(') 모두 문자열로 사용된다.



### Boolean

false : `0` , `null` , `undefined` , `NaN` , `''`(빈문자열)
true : 이외 모든 값

> true와 1은 표현만 다를뿐 같은것이다. 
>
> true는 바이너리코드상으로 1로 저장이된다.
>
> 같은 맥락으로 false는 0으로 저장이 되어있다.


### `Infinity` 

양의 무한대

```javascript
const infinity = 1/0;
console.log(infinity);
//출력: Infinity
```



### `negativeInfinity`

음의 무한대

```javascript
const negativeInfinity = 1/0;
console.log(negativeInfinity);
//출력: negativeInfinity
```



### `NaN`

not a number

```javascript
const nAn = 1/0;
console.log(nAn);
//출력: NaN
```


### `null`

텅텅 비어있는 상태, null도 하나의 값이다.



### `undefined`

선언은 되어있지만 값 자체가 없는 상태



### `symbol`

고유한 식별자 역할을 하기위해 사용된다.

같은 값을 할당해줘도 고유한 식별자이기 때문에 비교연산을 해도 다르다고 나온다.

```javascript
const symbol1 = Symbol("id");
const symbol2 = Symbol("id");
console.log(symbol1 == symbol2);
// 출력 : false
```



동일한 symbol도 만들수 있다.

```javascript
const symbol1 = Symbol.for("id");
const symbol2 = Symbol.for("id");
console.log(symbol1 == symbol2);
// 출력 : true
```



symbol을 그냥 출력하면 에러가 발생한다.

출력할때는 `.description` 으로 문자열로 만들어준뒤 출력해야한다.

```javascript
console.log(`value: ${symbol1.description}`)
```



## 배열(Araay)

```javascript
const myArray = ["hi", true, 11, 3.14, nbr, {name:"younoah",gender:"Male"}, [1,2,3]];
console.log(daysOfWeek[2]) // 인덱싱의 시작은 0부터이다.
// 11
```

- 배열에는 다양한 자료형을 담을수 있다. 변수&상수, 배열, 객체도 담을 수 있다.



## 객체(Object)


```javascript
const nbr = 123;
const userInfo = {
    name: "younoah",
    age: 27,
    gender: "Female",
    myArray: ["hi", true, 11, 3.14, nbr], //배열과 변수,상수 할당 가능
	favorite: [ // 배열과, 객체의 복잡한 구조도 선언이 가능하다.
        {
            name: "watching movie",
            degree: "i love so much"
        },
        {
            name: "fighting with foods",
            degree: "sometimes"
        }
    ]
};

/*key로 value 접근*/
console.log(userInfo.name);
// "younoah"

/*key로 value 수정*/
userInfo.gender = "Male";
console.log(userInfo.gender);
// "Male"

/*새로운 key와 value 할당*/
userInfo.isHandsome = true;
console.log(userInfo.isHandsome);
// true

/*key와 value 삭제*/
delete userInfo.age;
console.log(userInfo.age);
// undefined

/* const이기 때문에 상수자체를 변경할 수 없음 */
userInfo = true;
// TypeError: Assignment to constant variable.
```

`const` 상수로 객체를 선언해도 객체 안에 담겨진 **키, 값들은 수정과 추가/삭제가 가능하다.**

단, `userInfo = true` 와 같이 상수 자체를 변경하는것이 불가능하다.

## 함수(function)

**반환값이 없는 함수**

```javascript
function sayHello(name, numberOfAge) { // name과 numberOfAge은 parameter(매개변수)라고 한다.
    console.log("Hello!", name, "you are", numberOfAge, "years old.");
}

sayHello("younoah", 17); // "younoah", 5는 argument(전달인자)라고 한다.
//Hello! younoah you are 17 years old.
```



**반환값이 있는 함수**

```javascript
const res;
function calcAdd(a, b) {
    return a + b;
}

res = calcAdd(1, 2);
console.log(res);
// 3
```



**객체에 함수를 담아서 사용하기**

> 객체의 함수를 메서드라고한다.

```javascript
let res;
const calculator = {
    plus: function(a, b){
        return a + b;
    },
    minus: function(a, b){
        return a - b;
    }
}

res = calculator.plus(1, 2);
console.log(res);

res = calculator.minus(5, 4);
console.log(res);
```