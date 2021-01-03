# C/C++ 헤더파일 만들기

## 0. 헤더파일이란?

 프로그램의 규모가 커지면서 각종 구조체와 함수가 많아지게 되고 여러 파일들로 쪼개야할 필요성이 생긴다. 이때 공통으로 사용하는 부분은 헤더 파일에 넣고, 각종 함수들은 기능별로 파일을 분리하게된다. 

즉, 헤더파일은 공통으로 사용하는 부분인 함수, 구조체, 전역변수, 매크로, 심지어 또 다른 헤더파일들을 한군데로 모아 관리하고 편하게 사용하기 위해 사용한다.

> 헤더파일은 매크로로 정의한다.



## 1. 헤더파일 구조

C/C++ 에서 헤더파일의 가장 기본적인 구조는 아래와 같다.

```
#ifndef HEADER_H
# define HEADER_H

[include할 다른 헤더 파일 명시]

[매크로 정의]

[사용자 struct, type 정의]

[전역 변수 선언]

[함수 선언]
```



## 2. 구조 설명

### 2.1. 처음과 끝

헤더파일의 시작과 끝은 아래와 같이 작성한다.

```
#ifndef HEADER_H
# define HEADER_H

... 
// 전처리 문법 사용시 들여쓰기로 구분한다.

#endif
```

- `#ifndef HEADER_H` : 만약  HEADER_H 정의 되어 있지 않으면
- `# define HEADER_H` : HEADER_H 매크로를 정의한다.
- `#endif` : HEADER_H 매크로 정의의 끝



참고로 전처리기 문법에서 `#ifndef [헤더 구분자]`  와 `#endif` 사이에 또 다른 전처리 문법이 온다면 아래와 같이  `#` 을 치고 들여쓰기를 해주자. 하나의 언어처럼 가독성을 위해 들여쓰기를 한다.

```
#ifndef HEADER_H // if부터 end까지 나오는 전처리 문법은 모두 들여쓰기로 작성
# define HEADER_H

# ifndef PI // if부터 end까지 나오는 전처리 문법은 모두 들여쓰기로 작성
#  define PI 3.141592
# endif

#endif
```



이때 `#ifndef [헤더 구분자]` 의 형태로 정의를 하는데 `[헤더 구분자]` 의 명명규칙은 아래와 같다.

> 1. 헤더 파일명에서 소문자를 대문자로 바꾼다.
> 2. 마침표 `.` 를 언더바 `_` 로 바꾼다.
> 3. 파일 이름 앞뒤로 두개의 언더바 `__` 를 붙인다. (이 부분은 선택적인듯 싶다.)



### 2.2. 다른 헤더파일 include

```
#ifndef HEADER_H
# define HEADER_H

// include할 다른 헤더 파일 명시
# include <stdio.h> // stdio.h라는 표준 라이브러리를 포함하는 전처리
# include "header2.h" // header2.h라는 또 다른 사용자 정의 헤더를 포함하는 전처리

#endif
```

표준 라이브러리는 꺽쇠 `<>` 를 사용하고 사용자 정의 라이브러리는 큰따옴표 `""` 를 사용한다.



### 2.3. 매크로 정의

필요에 따라 매크로함수, 매크로 상수를 정의할 수 있다.

```
// 매크로 정의
# define PI	3.141592 // 상수
# define SQRT(X) X*X // 함수
```



### 2.4. struct, type 정의

사용자 정의 struct 혹은 type을 정의 할 수 있다.

```
// struct 정의
typedef		struct _Person {
	char	name[10];
    int		age;
    char	address[128];
} 			Person;

// type 정의
typedef long int file_size_t
```



### 2.5. 전역 변수 선언

헤더파일에 전역변수를 선언함으로써 해당 헤더를 포함한 파일에서 전역변수를 사용할 수도 있다. 전역변수를 선언 할 때는 앞에 `extern` 키워드를 작성해야한다.

```
// 전역 변수 선언
extern long long arr_len;
```



### 2.6. 함수 선언

프로젝트안에 작성된 함수를 헤더파일에 선언한다. 해당 헤더파일을 사용하는 파일에서는 헤더파일에 선언된 함수를 사용할 수 있다.

```
int		ft_isalpha(int c);
int		ft_isdigit(int c);
```



## 3. 마무리

### 3.1. 헤더파일 예제 최종 완성

```
// header.h

#ifndef HEADER_H
# define HEADER_H

# include <stdio.h>
# include "header2.h"

# define PI	3.141592
# define SQRT(X) X*X

typedef		struct _Person {
	char	name[10];
    int		age;
    char	address[128];
} 			Person;  

typedef long int file_size_t

extern long long arr_len;

int		ft_isalpha(int c);
int		ft_isdigit(int c);

#endif
```



### 3.2. 헤더 파일 사용하기

예시로 main.c라는 파일을 생성하고 `#include "header.h"` 라는 전처리를 작성한다.

```c
#include "header.h"

int		main(void)
{
	if (ft_isalpha('a'))
		printf("a는 알파벳입니다.\n");
	else
		printf("알파벳이 아닙니다.\n");
	if (ft_isdigit(123))
		printf("123은 숫자입니다.\n");
	else
		printf("숫자가 아닙니다.\n");
    printf("PI는 %f\n", PI);
	printf("2의 제곱은 %d\n", SQRT(2));
	return (0);
}
```



