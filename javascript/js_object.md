## 1. 객체 (Object)란?



**선언방법**

```javascript
const obj1 = {}; // 'object literal' syntax
const obj2 = new Object(); // 'object contructor' syntax
```



>  자바스크립트에서는 클래스가 없어도 객체를 생성할 수 있다.
>
> 객체는 데이터 자료형 중 하나이다.
>
> 객체는 관련된 데이터들과 메서드들의 집합체이다.
>
> 모든 객체는 자바스크립트의 기본 내장된 Object 객체의 인스턴스이다.
>
> `object = {key : value};` 객체는 키와 밸류들의 집합체이다.



### 객체의 사용

예를 들어 mike에 대한 모든 정보를 함수로 처리 할려고 한다.

```javascript
// mike에 대한 변수들
const name = 'mike';
const age = '20';

// mike에 대한 변수들을 처리할 함수
functon print(name, age) {
	console.log(name);
	console.log(age);
}

print(name, age);
```

현재는 mike에 대한 변수들이 2개 밖에 없지만 mike의 주소,  성별, 학력 등 정보가 추가 된다면

함수도 그만큼 인즈를 계속 추가해줘야 하는 엄청난 번거룸이 생긴다. 또한 가독성도 안좋아지고 유지보수하기 힘들어진다.



이럴때 객체를 사용하면 유용하다.

```javascript
const mike = { name: 'mike', age: 4 };
function print(person) {
  console.log(person.name);
  console.log(person.age);
}
print(mike);
```

이런식으로 작성하면 mike에 대한 정보들이 한눈에 보기쉽고 관리하기 용이해진다.



### 객체의 특징

자바스크립트의 객체는 특이하게 생성된 이후에 프로퍼티를 추가하거나 삭제할 수 있다.

하지만 코드가 길어 젔을때 유지보수와 가독성이 좋지 않기 때문에 가급적 사용을 피하자.

```javascript
mike.address = 'seoul'; // 추가
console.log(mike.adress);

delete mike.adrresss; // 삭제
console.log(mike.adress); // undefined
```







## 2. Conputed property



객체의 값에 접근하는 방법은 크게 2가지이다.

1. 일반적인 방법

```javascript
mike.age;
```



2. Computed properties

```javascript
mike['age'];
```

인덱싱하듯이 접근할수 있다.

이때 **키는 문자열**로 사용해야 한다.



Computed properties는 특수한 경우에 사용한다.

**동적으로 키의 밸류를 가지고 와야할때 유용하게 쓰인다.**



예를들어 아래와 같이 함수의 인자로 객체와 키를 동적으로 받아서 처리해햐 한다고 하자.

```javascript
function printValue(obj, key) {
  console.log(obj.key); // 이런식으로는 사용불가
}
printValue(mike, 'name');
```

함수 내에서 매개변수로 `obj.key` 이런식으로 사용이 안돤다.



따라서 이때 매개변수들을 `obj[key]` 방식으로 사용해야 한다.

```javascript
function printValue(obj, key) {
  console.log(obj[key]); // good!
}
printValue(mike, 'name');
```



## 3. Property value shorthand



```javascript
const person1 = { name: 'bob', age: 15 };
const person2 = { name: 'steve', age: 16 };
const person3 = { name: 'dave', age: 17 };
...
```

이렇게 같은 구조의 객체를 반복적으로 생성 할 일이 있다고 하자.



이때 함수를 사용하면 좀 더 편하게 같은 구조의 객체를 반복적으로 생성할 수  있을 거다.

```javascript
function makePerson(name, age) {
  return {
    name: name,
    age: age,
  };
}

const person4 = makePerson('alice', 19);
```



이때 위 함수를 아래와 같이 **간결**하게 작성할 수 있다.

```javascript
function makePerson(name, age) {
  return {
    name,
    age,
  };
}

const person5 = makePerson('andy', 22);
```

인자를 키로 !  값을 밸류로 ! 알아서 인식해서 함수가 작동된다.

**이 함수가 클래스 역할을 하게된다.**

이 클래스와 같은 역할을 하는 함수로 템플릿 구조를 짜서 객체를 찍어낼수 있다.



이 클래스 역할을 하는 함수를 좀 더 간결하고 클래스의 느낌을 내서 작성한것이 

아래 나오는 **생성자 함수 (Constructor Function)** 이다.



## 4. 생성자 함수 (Constructor Function)



위에서 사용한 함수를 **생성자 함수 (Constructor Function)** 스럽게 작성하면 아래와 같다.

```javascript
function Person(name, age) {
  // this = {}; 형태가 생략되어있다.
  this.name = name;
  this.age = age;
  // return this; 형태가 생략되어있다.
}
```

this 는 객체를 지칭한다. this라는 객체를 생성(`this = {};`) 이 생략되어 자동으로 작동된다.

또한 this라는 객체를 반환하는 `return this;` 도 생략되어 자바스크립트가 알아서 작동해준다. 신기하다!



## 5. 객체 연산자 `in` (feat. `of`)



`in` 이라는 키워드를 사용하면 좀 더 객체를 다루기 편해진다.



### `in` 의 사용

1. 해당 객체 엔에 키가 있는지 없는지 확인할 때 사용한다.

```javascript
console.log('name' in mike); // 반환값은 bool
console.log('randome' in mike); // 정의하지 않은 값이라면 undefined 출력
```



2. for문에서 for문을 돌면서 객체의 key를 받아온다.

```javascript
for (key in mike) {
  console.log(key);
}
```



### `of` 키워드는?

배열, 리스트, 객체와 같은 순차적인 값이 나열된 자료형에서 for문을 돌면서 값을 받아올 수 있다.

**배열**

```javascript
const array = [1, 2, 3, 4, 5];
for (value of array) {
  console.log(value);
}
```



**객체**

```javascript
const mike = { name: 'mike', age: 4 };
for (i in mike) {
  console.log(i);
}
```



## 7. 객체 복제(복사), Cloning, (Object.assing)



객체를 다른 변수에 복사해야 할 일이 생겼다고 해보자.



```javascript
const user = { name: 'sam', age: '21' };
const user2 = user; // user2는 user의 같은 레퍼런스가 할당이 된다.

user2.name = 'coder'; // user2의 이름을 변경하면 user의 이름도변경이된다.
console.log(user);
```

이렇게 객체를 다른 변수에 할당하면 동일한 객체를 가리키는 변수를 하나 더 만드는 셈이 되어서



![js_cloning](/Users/uno/Desktop/web/js/dreamcode/images/js_cloning.png)



`user2`로 프로퍼티를 변경하면 `user`의 프로퍼티도 변경이된다.

이렇게 하면 객체의 속성이 어떻게 변경될지 예측이 어렵고 유지보수가 힘들어진다.



### 진짜 복사하는 방법은?



올드한 방식부터 알아보자.

**Old way**

```javascript
const user1 = {}; // 빈 객체 생성
for (key in user) {
  user1[key] = user[key];
}
```

빈 객체를 생성하고 반복문을 돌면서 빈객체에 키와 밸류를 넣어주는 방식이다.



***Object.assing***

자바스크립트 안에는 Object라는 기본적을 내장된 함수가 있다.

또한 모든 객체들은 Object를 상속한다.

Object에는 다양한 메소드가 있는데 `assign` 이라는 메소드를 활용하면 복사가 편하다.

```javascript
// 기존 객체를 새로운 객체에 할당하기
const user1 = {};
Object.assign(user1, user);

// 또는

const user1 = Object.assign({}, user);
```



**또 다른 활용방법**

`Object.assing` 을 이용하면 여러 객체를 합치면서 다른 객체에 복사할 수 있다.

```javascript
const fruit1 = { color: 'blue', size: 'big' };
const fruit2 = { color: 'red' };
const mixed = Object.assign({}, fruit1, fruit2); // 뒤의 인자일수록 앞을 덮어 씌운다.
console.log(mixed);
// {color: "red", size: "big"}
```

이 때 fruit1, fruit2 순서로 인자를 작성했는데 뒤에 있는 인자가 앞을 덮어 씌우면서 복사가된다.



## 참고

**참고1 - MDN, Object**

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object

**참고2 - MDN, Object Basic**

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics

