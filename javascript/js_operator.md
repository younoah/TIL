## 연산자



## 1. 문자열 붙이기 (string concatenation)

```javascript
console.log('my' + 'cat');
console.log('1' + 2); // 문자와 숫자를 더하면 결과는 문자로 계산해준다.
console.log(`string literals: 1 + 2 = ${1 + 2}`);
```



## 2. 숫자 연산자 (numeric operator)

```javascript
console.log(1 + 1); // add
console.log(1 - 1); // substract
console.log(1 / 1); // divide
console.log(1 * 1); // multiply
console.log(5 % 2); // remainder
console.log(2 ** 3); // exponentiation
```



## 3. 증감 연산자 (Increment and decrement operator)

```javascript
let count = 2;
const preIncrement = ++count;
console.log(`preIncrement: ${preIncrement}, count: ${count}`);

const postIncrement = count++;
console.log(`postIncrement: ${postIncrement}, count: ${count}`);

const preDecrement = --count;
console.log(`preDecrement: ${preDecrement}, count: ${count}`);

const postDecrement = count--;
console.log(`postDecrement: ${postDecrement}, count: ${count}`);
```



## 4. 할당 연산자 (Assignment operator)

```javascript
let x = 3;
let y = 6;
x += y; // x = x + y;
x -= y; // x = x - y;
x *= y; // x = x * y;
x /= y; // x = x / y;
```



## 5. 비교 연산자 (Comparison operator)

```javascript
console.log(10 < 6) // less than
console.log(10 <= 6) // less than or equal
console.log(10 > 6) // more than
console.log(10 >= 6) // more than or equal
```



## 6. 논리 연산자 (Logical operators)

**or : `||`**

or연산자는 처음으로 true가 나오면 곧 바로 멈춘다. 왜냐하면 1개만 true 이기만 하면 되기 때문이다.

따라서 or연산자를 사용할 떄는 가장 앞에 가변운 녀석부터 넣는고 무거운 녀석일수록 뒤에 놓는게 효율적이다.

```javascript
const value1 = true;
const value2 = 4 < 2;
function check() {
	for (let i = 0; i < 10; i++) {
		// wasting time
		console.log('😱');
	}
	return true;
}
console.log(`or: ${value1} || ${value2} || ${check()}`); // true
```

만약  `console.log(or: ${check()} || ${value1} || ${value2});` 이라고 작성하면 `value1` 을 앞에 두면 `true`라 금방 종료할 수 있는데  굳이 무거운 함수를 앞에 두면 비효율적이다.



**and : `&&`**

and연산자도 무거운 녀석일수록 뒤로 보는게 좋다.

```javascript
const value1 = true;
const value2 = 4 < 2;
function check() {
	for (let i = 0; i < 10; i++) {
		// wasting time
		console.log('😱');
	}
	return true;
}
console.log(`and: ${value1} && ${value2} && ${check()}`); // false
```



>  and연산은 간편하게 null체크를 할 때 사용한다.
>
> 아래 두 문법은 동일하게 작동한다.

```javascript
if (nullableObject != null) {
	nullableObject.something;
}

nullableObject && nullableObject.something
```

`nullableObject && nullableObject.something` 의 뜻은

`nullableObject`이 `false` 이면 뒤에가 실행이 안되고

`nullableObject`이  `true` 이면 뒤에가 실행이 된다.



**not : `!`**

```javascript
const value = true;
console.log(!value); // false
```





## 7. 동등 연산자 (Equality)

```javascript
const stringFive = '5';
const numberFive = 5;

// == loose equality, with type conversion
console.log(stringFive == numberFive); // true
console.log(stringFive != numberFive); // false

// === strict equality, no type conversion
console.log(stringFive === numberFive); // false
console.log(stringFive !== numberFive); // true

// object equality by referance
const user1 = { name: 'younoah'};
const user2 = { name: 'younoah'};
const user3 = user1;
console.log(user1 == user2); //false
console.log(user1 === user2); //false
console.log(user1 == user3); //true
console.log(user1 === user2); //false
// user1과 user2는 서로 다른 오브젝트를 참조하기 때문에 타입에 상관없이 서로 다르다.
// user1과 user3는 서로 같은 오브젝트를 참조하기 때문에 타입에 상관없이 서로 같다.

// equality - puzzler
console.log(0 == false); // true
console.log(0 === false); // false
console.log('' == false); // true
console.log('' === false); // true
console.log(null == undefined); // true
console.log(null == undefined); // false
```

