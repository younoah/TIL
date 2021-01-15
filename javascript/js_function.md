## 함수

**자바스크립트에서 함수는 일급객체이다.**

- 변수에 담을 수 있다.
- 파라미터로 전달 할 수 있다.
- 반환값으로 사용할 수 있다.



## 1. 함수

**기명 함수**

```javascript
// named function
function 함수명() {...}

add(1 + 2);
function add(a, b) {
    return a + b;
}
```

- 기명함수는 선언 이전에서도 함수를 사용할 수 있다. 즉, 호이스팅(hoisting)이가능하다.
- 자바스크립트는 컴파일을 할 때 선언한 것들을 자동으로 제일 위로 올리기 때문이다.



**익명 함수** (**함수 표현식** 혹은 **함수표현** 이라고도 한다.)

```javascript
// anonymous function
function () {...};
             
const print = function () {
	console.log('print');
};
print(); // 함수를 변수에 할당하면 해당 변수를 함수를 사용할 때 처럼 사용할 수 있다.
const printAgain = print; // printAgain은 위에 선언된 anonymous function을 가리킨다.
printAgain();
```

- 익명함수는 함수가 변수에 할당이 된 이후부터 사용이 가능하다.



> 하나의 함수는 하나의 동작만하다록 설계하자.
>
> 네이밍은 동사로 시작하게한다.
>
> e.g. createCardAndPoint -> createCard, createPoint



## 2. 파라미터 (Parameters)

> premitive parameters: passed by value
>
> object parameter : passed by reference



**객체의 메모리 참조**

![](https://images.velog.io/images/younoah/post/1d7fd250-a01f-4462-8587-c91ccd850033/js_object.png)



```javascript
function changeName(obj) {
	obj.name = 'coder';
}
const uno = { name: 'younoah'};
changeName(uno);
console.log(uno);
```

- 함수의 인자로 **premitive 타입**을 전달하면 함수에 값 자체가 전달이 된다.

- 함수의 인자로 **객체**를 전달하면 객체의 레퍼런스가 전달된다.



## 3. 기본매개변수 (Default parameters)

파라미터에 값이 안들어올 경우를 대비해 디폴트 값을 줄 수 있다.

```javascript
function showMessage(message, from = 'unknown') {
	console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```



## 4. 나머지 매개변수 (Rest Parameters)

나머지 매개변수는 이름을 정해주지 않은 파라미터들을 **배열형태**로 받는다.

매개변수중에 가장 마지막에 작성한다.

```javascript
function printAll(a, b, ...args) {
	// 아래 3가지 형태의 loop는 같은 역할을 한다.
// 	for (let i = 0; i < args.length; i++) {
// 		console.log(args[i]);
// 	}
	for (const arg of args) {
		console.log(arg);
	}

	args.forEach((arg) => console.log(arg));
}
printAll('dream', 'coding', 'uno');
```



## 5. 지역변수 (Local scope)

함수 안에서 선언된 변수는 함수안에서만 사용할 수 있는 지역변수이다.

```javascript
let globalMesaage = 'global'; // 전역변수
function printMessage() {
	let message = 'hello'; // 지역변수
	console.log(message);
	console.log(globalMesaage);
}
printMessage();
```



## 6. 반환값 (Return a Value)

함수는 반환값을 줄 수 있다.

return 이 없는 함수에는 return undefined가 선언되어 있는거와 같다.

```javascript
function sum(a, b){
	return a + b;
}
const result = sum(1, 2); // 3
console.log(`result: ${result}`);
console.log(`sum: ${sum(1, 2)}`);
```



## 7. *Early return, early exit*

**bad**

아래 코드는 조건이 맞을때 긴 로직이 동작하느 코드이다.

이렇게 작성하면 가독성이 좋지 않다.

```javascript
function upgradeUser(user) {
	if (user.point > 10) {
		// long upgrade logic...
	}
}
```



**good**

이번에는 조건이 맞지 않다면 함수를 빨리 리턴해서 빨리 종료하는 방식이다.

이렇게 작성하면 가독성이 훨씬 올라간다.

```javascript
function upgradeUser(user) {
	if (user.point <= 10) {
		return;
	}
	// long upgrade logic...
}
```



## 8. 콜백함수 (Callback function)

인자로 다른 함수를 받아와서 다른 함수를 호출해서 사용하는 함수를 **콜백함수**라고 한다.

인자에 **"함수의 정의:**만 넘겨주면 된다.

> 함수 사용 : `함수명();`
>
> 함수 정의 : `함수명`



```javascript
function randomQuiz(answer, printYes, printNo) {
	if (answer === 'like you') printYes();
	else printNo();
}

const printYes = function () {// anonymous function
	console.log('yes!');
};

const printNo = function print() { // named function
	console.log('no!');
}
randomQuiz('wrong', printYes, printNo);
randomQuiz('like you', printYes, printNo);
```



## 9. 화살표 함수 (Arrow function)

함수의 표현을 한줄로 간결하게 작성할 때 사용한다.

> function 키워드 지우고
>
> 중괄호를 지운다음에 한 줄로 작성한다.



```javascript
const simplePrint = function () {
	console.log('simplePrint!');
};
```

이 함수의 표현을

```javascript
const simplePrint = () => console.log('simplePrint!');
```

이렇게 한줄로 간결하게 나타낼수 있다.



**인자와 리턴값이 있을때**

```javascript
const add = function (a, b) {
    return a + b;
};
```

```javascript
const add = (a, b) => a + b;
```



## 10. IIFE: Immediately Invoked Function Expression

함수를 선엄하과 동시에 바로 실행해 보고 싶을때 사용하는 표현이다.

잘 사용하지는 않지만 바로바로 함수르 실행시켜 보고싶을 때 유용하다.

```javascript
(function hello() {
	console.log('IIFE');
})();
```

