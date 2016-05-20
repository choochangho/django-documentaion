# 첫번째 장고 앱 만들기, 파트1

예제로 배우기를 시작하자.

본 튜토리얼을 통해 기본적인 투표 어플리케이션 만들기를 보여줄 것이다.

본 튜토리얼은 아래의 두가지를 포함한다.

- 투표를 보고 투표할 수 있는 공개 사이트
- 투표를 추가, 변경 그리고 삭제할 수 있는 관리 사이트

장고를 이미 [설치](https://docs.djangoproject.com/en/1.9/intro/install/)했다고 가정하자. 아래의 명령어로 설치된 장고의 버전을 알아 낼 수 있다.

```shell
$ python -c "import django; print(django.get_version())"
1.9.6
```

장고가 설치되어 있다면 설치된 버전을 볼 수 있다. 그렇지 않다면,"No module named django" 에러를 보게 될 것이다.

본 튜토리얼은 장고 1.9 와 Python 3.4 또는 이후 버전으로 작성되었다. 장고 버전이 일치 하지 않는다면   본 페이지 하단 오른쪽에서
버전을 바꾸거나 최신버전으로 장고를 업데이트 한다. 여전히 Python 2.7 을 사용중이라면, 코멘트에 기술된 대로 샘플 코드를 약간
바꿀 필요가 있을 것이다.

구버전을 제거하고 새로운 버전을 설치하기 위해서 [장고설치방법](https://docs.djangoproject.com/en/1.9/topics/install/)을 참고 한다.

> **도움을 얻는곳:**
> 
> 튜토리얼을 진행하면 어려움이 생기면 [django-users](https://docs.djangoproject.com/en/1.9/internals/mailing-lists/#django-users-mailing-list) 에 메시지를 포스트하거나 [#django on irc.freenode.net](irc://irc.freenode.net/django) 도움을 줄지도 모르는 다른 장고 사용자와 대화를 한다. 


## 프로젝트 생성

장고 사용이 처음이라면 초기 셋업에 신경을 써야 할것이다. 즉, 장고 [프로젝트](https://docs.djangoproject.com/en/1.9/glossary/#term-project)(데이터베이스 설정, 장고 옵션 그리고 어플리케이션 설정을 포함하는 장고 인스턴스 설정 모음)를 설정하는 자동 생성되는 약간의 코드가 필요 할 수도 있다.

커맨드 라인에서 코드를 저장하고자고자 하는 디렉토리에서 다음의 명령을 실행 한다.

```shell
$ django-admin startproject myste
```

현재 디렉토리에 mysite 라는 디렉토리가 생성된다. 그렇지 않다면  Problems running django-admin(https://docs.djangoproject.com/en/1.9/faq/troubleshooting/#troubleshooting-django-admin) 를 참고하자.

> **Note**
>
> 파이썬의 내장 또는 장고 컴포넌트의 이름으로 프로젝트를 만들지 말라.
> 특히, django(장고 자체와 충돌) 또는 test(파이썬의 내장 패키지와 충돌)와 같은 이름 사용을 피하라는 의미 이다. 

.

> **어디에 코드를 저장할 것인가?** 
> 
> 과거 PHP 에 대한 경험이 있다면 아마도 웹서버의 Document root(/var/www와 같은) 에 코드를 저장했을 것이다. 장고에서는 그렇게 하지 않는다. 웹을 통해 코드가 공개될 수 있기 때문에 파이썬 코드를 웹서버의 document root  에 저장하는 것은 좋은 생각이 아니다. 보안상 좋지 않다.
> 
> 코드는 /home/mycode 와 같은 document root 외부에 저장 한다.