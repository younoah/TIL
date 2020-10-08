## 참고 사이트

> https://martianlee.github.io/posts/django-gae-deploy/#google-cloud-platform-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%84%B8%ED%8C%85
>
> https://iamthejiheee.tistory.com/76
>
> https://www.youtube.com/watch?v=z6WOMYI-WiU&list=PL1jdJcP6uQttVWZTd1X2x22kv32Rhkiyc
>
> https://ohohs.tistory.com/entry/Google-Cloud-Docker%EB%A1%9C-%EA%B0%84%EB%8B%A8%ED%95%98%EA%B2%8C-%EC%9B%B9%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0feat-Django-1?category=695701
>
> https://velog.io/@secho/nodejs-06-GCP%EB%A1%9C-%EC%84%9C%EB%B2%84%EB%B0%B0%ED%8F%AC



## gcp

Google Cloud Platform은 구글에서 제공하는 클라우드 플랫폼서비스이다.

사용자는 크게 두가지를 이용할 수 있는데, App engine과 Compute Engine이다.

##### App engine

App engine은 코드만 추가하면 자동으로 도메인연결로 진행이된다. 방법은 매우 간단하지만, 코드를 수정할 때 마다 다시 수정사항을 구글 클라우드에 반영해야하므로, 시간이 오래걸린다는 점이 있다.



##### compute engine

Compute Engine은 VM을 제공받아, 해당 VM에서 서버를 구동시키면, 외부IP로 배포가 됩니다. 외부 IP와 도메인네임을 연결하면 도메인네임으로 접속가능하다.

VM에서 해당 프로젝트서버를 구동시켜야하기 때문에 개발환경에 대해 세팅해줘야 한다.

> 예를 들어 현재 진행하고 있는 프로젝트는 nodejs, express, mysql을 사용하고 있는데, 이를 구동시키기 위한 패키지들을 설치하고, VM에서 코딩하거나, 로컬(내컴퓨터)에서 작성한 코드를 git에서 pull한 다음에 코드에서 사용했던 데이터베이스에 대한 계정설정, DB, 테이블 구성까지 완료해야합니다. 즉, 로컬과 동일한 환경을 세팅해주어야하는 과정이 필요합니다.



##### compute engine으로 서버 배포하기

서버 구동까지의 일련의 순서는 다음과 같다.

1. GCP 계정생성
2. 프로젝트 생성
3. VM 머신 스펙설정
4. VPC네트워크에서 방화벽규칙설정 (VM에서 구동할 포트번호를 방화벽규칙에 설정해주어야 외부에서 접근 가능)
5. VM생성, SSH연결
6. DB구성 및 개발환경 설치 SSH 개발환경설치 (현재 위치)
7. 작성된 코드 clone

