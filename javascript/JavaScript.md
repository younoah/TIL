## 코딩컨벤션 - 명명규칙

### 변수와 상수

카멜케이스를 사용한다.

```javascript
let nbr = 123;
const str = "hello";
```



### 함수

카멜케이스를 사용한다

```javascript
function myFunction() {...}
```



### 객체

카멜케이스를 사용한다.

```javascript
const thisIsMyObject = {...};
```

❗️단, 객체를 export할 때는 파스칼케이스를 사용한다.

```javascript
const MyObject = {...};
export default MyObject;
```



### 클래스

파스칼케이스를 사용한다.

```javascript
class MyStudent {...};
```



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

ES6 전에는 변수를 선언할때 `var` 만 사용할 수 있었다. javascript에서 'var hosting'이라는 규칙과 'block scope'가 없기 때문에  `var` 키워드로 변수를 선언하게되면 의도치 않게 에러를 만날수 있으므로 사용하지 않는다.



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
```

> C/C++에서는 문자는 따옴표('), 문자열은 큰따옴표(")로 구분하여 사용하지만
>
> 자바스크립트에서는 문자열 자료형과 문자 자료형을 구분하지 않고 모두 같은 문자열이기 때문에
>
>  큰따옴표("), 따옴표(') 모두 문자열로 사용된다.



### Boolean

참 키워드 : `true`, `1`

거짓 키워드 : `false`, `0`

> true와 1은 표현만 다를뿐 같은것이다. 
>
> true는 바이너리코드상으로 1로 저장이된다.
>
> 같은 맥락으로 false는 0으로 저장이 되어있다.



## 배열(Araay)

```javascript
const myArray = ["hi", true, 11, 3.14, nbr, {name:"younoah",gender:"Male"}, [1,2,3]];
console.log(daysOfWeek[2]) // 인덱싱의 시작은 0부터이다.
// 11
```

- 배열에는 다양한 자료형을 담을수 있다. 변수&상수, 배열, 객체도 담을 수 있다.



## 객체(Object)

> 사전자료형이다.

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

단, `userInfo = true` 와 같이 상수자체를 변경하는것이 불가능하다.

