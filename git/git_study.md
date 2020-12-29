## git 세팅

### .gitconfig

> 깃을 설치하게 되면 깃에 관련된 모든 환경 설정이 `.gitconfig` 라는 파일안에 저장이 된다.
>
> 아래와 같은 명령어로 터미널에서 간단하게 확인할수 있다.

```
git config --list // 간단하게 터미널에서 설정을 확인하기.
git config --global core.editor "vi" //vscode와 연동 세팅
git config --global core.editor "code" //vscode와 연동 세팅
git config --global core.editor "code --wait" //vscode와 연동 세팅, +에디터(vscdode)가 종료되어야 터미널이 다시 활성화된다. --wait 옵션을 꼭 설정해야 잡다한 에러를 피할 수 있다.
git config --global -e // 에디터창(vi or vscode)통해 .gitconfig 파일을 실행한다.
```

- 깃에 관련되 모든 설정을 확인할 수 있다.
- `--global` 옵션은 전역환경설정을 의미한다.



#### 사용자 이름, 이메일 설정

```
git config --global user.name "younoah" // 이름 설정
git config --global user.email "kr_uno_10@naver.com" // 이메일 설정
git config user.name // 설정된 이름 출력
git config user.email // 설정된 이메일 출력
```



#### push / pull 설정

```python
# in .gitconfig
[user]
	name = 유저 이름
    email = 유저 이메일

# 추가
[push]
	default = current

# 추가
[pull]
	rebase = true
```

- push를 할때 default를 current으로 설정하므로서
- 로컬에 있는 브랜치 이름이 항상 리무트와 동일하다고 설정
- push를 할때 일일이 'git push --set-upstream origin master' 옵션을 작성하지 않아도 된다.

- pull 명령어는 merge와 rebase 옵션을 선택해서 동작할 수 있다. 우선 `rebase` 로 설정하자.

	

### 운영체제별 설정

![core.autocrlf](./images/core.autocrlf.png)

```
git config --global core.authcrlf input // mac
git config --global core.authcrlf true // window
```

- 운영체제 마다 에디터에서 새로운 줄바꿈을 할 때 들어가는 문자열이 달라진다.
- 윈도우에서는 작성한 텍스트 뒤에  `\r` (carriage-return), `\n` (line-feed) 가 동시에 들어가는 반면에
- 맥에서는 작성한 텍스트뒤에   `\n` (line-feed) 1개만 들어가게된다.
- 이런 차이점 때문에 깃 레파지토리를 다양한 운영체제에서 쓰는 경우 내가 수정하지 않았음에도 불구하 줄바꿈 문자열이 달라져서 깃히스토리나 깃블레을 보는데 문제가 있을수 있다.
- `autocrlf` 옵션이 이것을 수정할 수 있는 속성이다.
- 윈도우에서 `true` 로 설정하게 되면 깃에 저장할때에는 `\r` (carriage-return) 을 삭제하게 되고 다시 깃에서 뒨도우로 가져올 때는 자동으로 `\r` (carriage-return)을 붙여준다.
- 맥에서는 `input` 으로 설정하게 되면 깃에서 받아 올 때는 별다른 수정이 일어나지 않지만 깃에 저장할 때는 `\r` (carriage-return)을 삭제 해준다.
- 맥에서 `\r` (carriage-return)이 텍스트 뒤에 붙지 않음에도 불구하고 설정하는 이유는 맥에서 이메일을 받아 온 텍스트를 복사해서 붙여넣을 때 실수로 `\r` (carriage-return)이 들어갈 수 있기 때문이다.



### git 명령어 구조

```
git 명령어 -축약옵션 --비축약옵션
```

- 깃 명령어는 위와 같은 구조로 구성된다.



### git 시작하기

- 기본적으로 깃을 관리하기 위한 디렉토리를 생성한다.

```
mkdir projects // 프로젝트들을 관리하기위한 디렉토리
cd projects
mkdir git // 깃이라는 디렉토리를 생성하여 이 디렉토리에서 깃을 관리한다.
cd git
```

- 깃 초기화.

```
git init // 현재 디렉토리에 git을 초기화(세팅)한다.
ls -al // 해당 명령어를 치면 .git폴더가 생성되어 git일 잘 설정되어 있는것을 확인할 수 있다.
rm -rf .git // 숨겨진 깃폴더를 삭제함으로써 해당 디렉토리에 깃을 삭제한다.(더이상 깃프로젝트가 아니다.)
```

- **.git**폴더 안에는 현재 디렉토리에 설정된 git에 내부 구현 사항이나 관련된 모든 정보가 담겨있다.
- git을 초기화 하면 기본적으로 `master` 브랜치가 생성이 된다.
- `master` 브랜치는 해당 깃에 가장 기본적인 최고관리자 격인 브랜치인다.



### git alias

> git에서 자주사용하는 명령어를 좀더 빠르게 쓰기 위해서는 alias를 통해 단축해서 사용할 수 있다.

```
git config --global alias.st status
```

- `git status` 명령어를 `git st` 로 단축해서 사용할 수 있다.



### git 명령어의 속성 검색

1. 터미널 (명령어)

	```
	git config --h
	```

	- 터미널을 통해서 간단하게 해당 명령어에 대해 어떤 옵션이 있는지 확인할 있다.

2. 깃 공식 사이트 (https://git-scm.com/docs)

	- 깃 공식 사이트 레퍼런스에서 어떤 명령어와 옵션이 있는지 자세히 확인할 수 있다.



## git 시작하기

### git workflow

![깃작업환경](./images/git_workflow.jpg)

## 현재 상태 확인하기 status

```
git status
git status -s //상태 간략하게 보기
```



## 파일비교하기 diff

> `git status` 로는 어떤 파일이 수정이 되었고, staging area에 있는지 확인할 수 있지만 정확하게 어떤 내용이 수정되었는지는 확인할 수 없다.
>
> 정확하게 어떤 파일의 내용이 수정이 되었는지 확인하기 위함.



### Woriking Directory에서의 변경사항들 확인하기

> 워킹디렉토리 기준에서 현재 워키디렉토리에 있는 파일들의 변경사항들을 확인한다.

```
git diff
```

### `git diff` 명령어 결과

```
diff --git a/c.txt b/c.txt    // a는 이전 버전, b는 현재 버전(수정된 현재 상태)
index d3a231a..97043e8 100644 // index는 git 내부적으로 파일을 참조할때 사용한다. 알필요는 없을듯
--- a/c.txt      // 이전 버전(a)의 c.txt파일은 마이너스(-)로 표기
+++ b/c.txt		 // 현재 버전(b)의 c.txt파일은 플러스(+)로 표기
@@ -1,3 +1,4 @@  // 아래 변경사항을 어떻게 이해하면 좋을지 안내해주는 역할, 
				 // 이전버전(-)은 1~3줄까지이다. 현재버전(+)는 1~4줄까지이다.
 hello world!
 uno
 add
+add             // 이전버전(-)에서 현재버전(+)에는 add가 추가가 되었다.
```



### Staging Area에서의 변경사항들 확인하기

> 스테이징 에어리어 기준에서 현재 스테이징 에어리어에 있는 파일들의 변경사항들을 확인한다.
>
> `staged` 와 `cashed` 는 staging area를 가리키는 동의어이다.

```
git diff --staged
git diff --cashed
```

### `git diff --staged` 명령어 결과

```
diff --git a/style.css b/style.css  // a는 이전 버전, b는 현재 버전(수정된 현재 상태)
new file mode 100644
index 0000000..c8658a5
--- /dev/null           // 이전에는 아무런 파일도 없었다.
+++ b/style.css         // 현재(b)는 style.css 파일이 추가되었다.
@@ -0,0 +1 @@           // 이전버전(-)은 0줄까지이다. 현재버전(+)는 1줄까지이다.
+styling
```



## VScode로 파일비교하기

> 위에 처럼 터미널에서 `git diff`를 확인할 수 있지만
>
> 내가 원하는 편집기를 통해 UI적으로 좀더 편하게 변경사항 확인(파일비교)가 가능하다.



#### .gitconfig파일에서  아래와 같이 코드를 추가한다. `git config --global -e`

```
## in .gitconfig

# diff의 tool은 vscode를 사용한다.
[diff]
	tool = vscode

# vscode의 명령어는 code하고 실행시 터미널에서 기다리는고 있는다.
# 그리고 diff를 실행하고, LOCAL과 REMOTE를 비교한다.
[difftool "vscode"]
	cmd = code --wait --diff $LOCAL $REMOTE
```



#### 이후 설정한 에디터로 파일비교가 가능하다.

- Woriking Directory에서의 변경사항들 에디터로 확인하기

	```
	git difftool
	```

- Staging Area에서의 변경사항들 확인하기

	```
	git difftool --staged
	```



## 버전 등록하기 commit

> Statging area에 있는 변경사항들을 Git repository에 옮겨준다.



```
git commit
```

- 아무런 옵션을 주지 않으면 내가 설정한 에디터가 열리면서 메시지를 작성하게 한다.
- 커밋 메세지를 디테일하게 작성할 때는 이 방식으로 에디터를 열어서 메세지를 작성하는게 좋을것 같다.



```
git commit -m "메세지"
```

- -m 옵션을 주어 메세지를 빠르고 간편하게 작성하여 좀더 편하게 커밋을 할 수 있다.



### 수정된 파일 add 없이 commit하기

> 만약 워킹 디렉토리에  있는 모든 변경 사항이 마음에 들어서 굳이 staging area를 거치지 않고 한번에 commit을 할수 있다.
>
> 단 기존에 트래킹 되고 있던 파일의 변경사항만 가능하므로 새로 추가한 파일은 불가하다.



```
git commit -a
git commit -am "메세지"
```

- `-a`  옵션은 staging area와 working diretoy에 있는 모든 파일을 지칭할 때 사용한다. 
- 즉 staging area와 working diretoy에 있는 모든 파일들을 메세지와 함께 커밋한다.





## git으로 파일삭제 & 파일명 변경

![git_file_change_delete](/Users/uno/Desktop/git_file_change_delete.png)

일반적으로 `rm` `mv` 명령어로 파일을 삭제하거나 파일명을 변경하면 위와 같이 파일에 대한 변경사항이 staged area에 추가되지 않아 `git add` 를 또 해야한다.



하지만 `git rm 파일명`  `git mv 현재파일명 새로운파일명` 이라는 명령어를 사용한다면 git에서 알아서 staged area에 등록해준다.(.tracked)





## 버전들 목록보기 log

```
git log // 가장 최신커밋이 위에 오게끔 정렬되어 출력된다.
git log -3 // 최근 커밋 3개만 출력
git log --reverse // 역순 출력
git log --oneline // 간결하게 정리된 버전들을 확인할 수 있다.

git log --patch // log와 함께 각 버전에서 변경사항을을 확인 할수 있다. 
// 주로 커밋의 자세한 내용을 확인할때 사용한다. 
git log -p      // git log --patch와 동일

git log --author="유저이름" // 해당 유저가 작성한 커밋만 확인하기
git log --before="2020-10-29" // 해당 기간 이전의 커밋만 확인하기
git log --grep="문장" // 해당 문장이 커밋메세지에 포함된 커밋만 확인하기
git log -S "문장" // 해당 문장이 커밋된 파일안에 포함되어있는 커밋만 확인하기
git log 파일명 // 해당 파일에 관련된 커밋만 확인하기

git log HEAD // 현재 헤드까지 커밋들 확인하기
git log HEAD~1 // 현재 헤드의 1개이전(부모) 헤드까지의 커밋들 확인하기
git log HEAD~2 // 현재 헤드의 2개이전(부모의 부모) 헤드까지의 커밋들 확인하기

// Tip. 해쉬코드는 꼭 전체를 복사하지 않아도 되고 어느정도까지만 복사해 알아서 찾아준다.
git show 해쉬코드 // 해당 해쉬코드에 대한 커밋을 자세하게 확인하기
git show 해쉬코드:파일명 // 해당 해쉬코드에서 해당 파일의 내용을 확인할 수 있다.

git diff 해쉬코드1 해쉬코드2 // 두 해쉬코드의 커밋에 대한 차이를 확인 할 수 있다.
git diff 해쉬코드1 해쉬코드2 파일명 // 두 해쉬코드의 커밋에서 해당파일의 변경사항 차이를 확인 할 수 있다.
```



## Head 와 Master 브랜치

![git_head_master](/Users/uno/Desktop/git_head_master.png)



- 처음에 `a`  를 커밋하고 이후에 `b` 를 커밋하게 되면 `b` 는 `a` 커밋을 참조하게된다.
- 즉, 뒤에 커밋은 이전 커밋을 참고하게 된다. (뒤에 커밋이 이전커밋을 가리키고 있는 포인터가 생성된다.)
- commit을 해 나아가는 기본 줄기가 `master` 브랜치 이다.
- `master` 브랜치는 언제나 가장 최신 커밋을 가리키고 있다.
- 가장 마지막으로 `d` 를 커밋했다면 `head` 는 `d` 를 향하게 된다. ( `head` 는 가장 최신 커밋을 기본적으로 가리킨다.)
- `head` 는 내가 바라보는 이 시점에 버전을 가리키게된다. 
- 헤드에서 물결모양을 쓴다음에 1을 붙인다면 현재 헤드에서 이전버전(부모)을 가리키게된다.
- 마찬가지로 `head~2` 라고 하면 현재 헤드에서 이전 이전 버전(부모의 부모)을 가리키게된다.
- `git checkout 해쉬코드` 를 입력하면 해쉬코드가 가리키는 이전 커밋 상태로 돌아가게 되면서 헤드가 해당 커밋을 가리키게된다.
- 이전 커밋에서 가자 최신 커밋으로 돌아오려면 `git checkout master` 를 입력해서 가장 기본줄기의 최신으로 돌아온다. 
- 또한 다른 브랜치로 이동할 때도 `git checkout 브랜치명` 을 사용하여 브랜치를 옮겨 갈 수 있다.



## git log 포맷팅 (로그 이쁘게 만들기)

```
git log --pretty=oneline
```

- `pretty` 옵션을 주어 좀 더 보기 좋게 바꿀수 있다.



```
git log --pretty=format:"%h %an" // 해쉬코드와 작성자명 만을 포맷팅하여 출력
```

- `pretty=format:"%h %an"` 옵션을 사용하면 원하는 방식대로 포맷팅하여 로그를 확인할 수 있다.
- `%h` : 해쉬코드
- `%an` : author name
- `%ar` : 커밋 날짜
- `%s` : 타이틀

깃 레퍼런스(https://git-scm.com/docs/git-log) 에서 더 많은 포맷 옵션을 확인할 수 있다.



```
git log --oneline --graph --all
```

- 커밋들을 그래프적으로 확인할 수 있다. 
- 그래프로 확인하면 브랜치의 정보와 여러 브랜츠가 어떤 것을 커밋했는지에 대한 정볼르 확인할 수 있다.
- `--all` 명령어를 작성해야 master 브랜치와 여러 브랜치들의 정보를 그래프로 볼수 있다. 해당 옵션을 주지 않으면 현재 선택된 브랜치의 커밋들만 확인 할 수 있다.



## git tag

> 깃 히스토리에 commit들이 점점 더 많아지거나 git log가 굉장히 길어진다면 어떤 특정한 부분으로 돌아 가려고 할때 어려울 수 있다.
>
> 어떤 특정한 커밋을 북마크하고 싶을때 사용하는 것이 git tag이다.
>
> 보통 버전을 tag로 많이 사용한다.
>
> 즉, 태그는 기다란 버전(커밋) 히스토리에 특정한 부분을 태그해둠으로써  언제 릴리즈 버전이 되었는지 태그별로 관리가 쉽고 전환이 빠르게 될 수 있도록 도와주는 유용한 북마크 같은 역할을 한다.



### sementic versioning (시멘틱 버전)

![sementic_versioning](/Users/uno/Desktop/sementic_versioning.png)

시멘틱 버전은 대중적으로 많이 사용하는 버전 표기 방식이다. 숫자 3가지를 사용하여 메이저버전, 마이너업데이트, 픽스 버전을 구분해서 정한다.

- 메이저번호 : 커다란 기능이 추가된거나 전체적인 업데이트가 발생했을 때 하나씩 올려가는 버전
- 마이너번호 : 조금의 기능들이 업데이트 되거나 개선이 되었을 때 마이너 버전을 업데이트 한다.

- 픽스번호 : 기존에 존재하는 기능에서 오류수정을 했을 때 하니씩 올리는 버전



### git tag 추가하기

- 현재 헤드에 tag 추가하기

	```
	git tag 문자열
	```



- 특정 커밋에 tag 추가하기

	```
	git tag 문자열 해쉬코드
	```



- 특정 커밋에 tag를 추가하면서 동시에 tag에 대한 메세지(정보) 추가하기

	```
	git tag 문자열 해쉬코드 -am "태그에 대한 메시지 정보"
	```

	> `-a` : annotate, 이 태그에 주석(정보)를 추가하겠다.
	>
	> `-m` : message, 어떤 정보냐면 메세지를 남기겠다.
	>
	> 태그에 대한 메시지정보는 `git show 태그명`으로 확인할 수 있다.



### 태그로 커밋 확인하기

```
git show 태그명
```



### 해당 태그로 이동하기

```
git checkout 태그명
```



### 태그 확인하기

- 태그 목록 확인하기

```
git tag
```



- 태그 목록중에서 옵션을 주어 특정 태그를 검색해서 확인하기

```
git tag -l "문장"
```

> `-l` : 리스트로 출력, 태그의 리스트
>
> 해당 문장이 포함되어있는 태그들만 리스트로 출력한다.



### 태그를 remote 서버에 업로드하기 (synchronize)

> remote 서버와 synchronize하는 것은 나중에 더 자세하 알아보자.

```
git push origin 태그명
```

- 하나의 특정 태그만 `origin` 이 가리키는 remote 서버에 태그를 업로드를 한다.



```
git push origin --tags
```

- 존재하는 모든 태그들을 `origin` 이 가리키는 remote 서버에 태그들을 업로드를 한다.



```
git push origin --delete 태그명
```

- `origin` 이 가리키는 remote 서버에서 특정 태그를 삭제한다.

