## 조건문

### `if`, `else if`, `else`

```javascript
const name =  'younoah';
if (name === 'younoah') {
	console.log('welcome, younoah!');
} else if (name === 'coder') {
	console.log('you are amazing coder');
} else  {
	console.log('unknown');
}
```



### 삼항연산자

```javascript
const flag = (name === 'younoah') ? 'yse' : 'no';
```



### 스위치 (Switch)

```javascript
const browser = 'IE';
switch (browser) {
	case 'IE':
		console.log('go away!');
		break;
	case 'Chrome':
	case 'Firefox':
		console.log('love you!');
		break;
	default:
		console.log('same all!');
		break;
}
```

- 여러 조건을 확인할때 사용한다.

- 열거형 같은 변수를 확인할 때 사용한다.
- 타입을 확인할 때 사용한다.



## 반복문



### do-while

```javascript
do {
	console.log(`do while: ${i}`);
	i--;
} while (i > 0);
```



### for문

```javascript
let i;
for (i = 3; i > 0; i--) {
	console.log(`for: ${i}`);
}

// or

for (let i = 0; i < 10; i++) {
    // i는 지역변수이다.
	for (let j = 0; j < 10; j++) {
		console.log(`i: ${i}, j: ${j}`);
	}
}
```



### break 와 continue

```javascript
// 짝수출력하기
for (let i = 0; i <= 10; i++) {
	if (i % 2 !== 0) continue;
    console.log(`${i}`);
}
```

```javascript
// 8까지 출력하기
for (let i = 0; i <= 10; i++) {
	if (i > 8) break;
	console.log(`${i}`);
}
```

