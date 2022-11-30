<h1> JoonSimJoon_ git blog</h1>
윈도우환경에서 deploy 진행했습니다. <br>

## git init
Git repository("username".github.io) 생성 <br> 
생성 이후 upload 하고자 하는 폴더에 

~~~
git init
git add . 
git remote add "레포지토리 주소"
git commit -m "커밋 메세지"
git push origin master 
~~~
를 통해 git에 upload 하였다. 

## Jekyll Install
[공식 reference](https://jekyllrb.com/docs/installation/) 참조 

지킬 설치 이전에 ruby를 설치해야한다. 
[공식 reference](https://rubyinstaller.org/downloads/) 를 참조하자.  
Ruby + Devkit ~~ 를 설치해야한다.  
ruby 설치가 완료 되었다면 Start Command Prompt with Ruby를 실행한다.
~~~
gem install jekyll bundler
~~~
로 jekyll을 설치하자!

## Create Blog
~~~
jekyll new joonsimjoon
cd joonsimjoon
bundle exec jekyll serve
~~~
로 joonsimjoon이란 이름의 블로그가 생성되고, 해당 레포로 이동한뒤 로컬서버에서 블로그를 실행하자.

## Apply theme

이렇게 기본 생성된 지킬 블로그는 밋밋하다.  
테마를 추가해주자. 나는 [so simple theme](https://github.com/mmistakes/so-simple-theme)을 사용했다. sst에 있는 example 폴더를 복사(fork)해서 joonsimjoon 폴더 안에 넣어줬다. 

## Customization
fork 한 파일에 있는 정보를 내 블로그에 맞게 바꿔줘야한다. 
~~~
title: "JoonSimJoon_blog"
repository: "JoonSimJoon/JoonSimJoon.github.io"
description: "Woke up with yawning, it's dawnin. I'm still alive. Turned on my radio. To start up a new day"
baseurl: "" # the subpath of your site, e.g. "/blog"
url: # the base hostname & protocol for your site e.g. "https://mmistakes.github.io"
logo: "/images/joonsimjoon_me.jpg" # path of site logo, e.g. "/assets/images/logo.png"
~~~
config.yml 을 위와 같이 변경하였다. title, 연결 레포, 설명, 로고 등등 여러가지를 사용자화 하였다.
### p.s.  
 so-simple-theme의 경우 배포시 config.yml에서 remote-theme을 설정하고 배포해줘야한다. 

## Comment
원래 깃 블로그를 운영할때는 disqus 를 통해 댓글을 관리하였는데, 
패키지가 무겁고 설정하지 않은 광고 때문에 불편했다. 이 참에 깃 블로그를 정리하며 ["utterances"](https://github.com/apps/utterances)로 변경하였다. 
먼저 위 사이트에서 사용하고자 하는 레포에 install 해주자. (나는 내 깃블로그에만 install 하였다)  
이후 repo, Issue Mapping type, Theme 를 설정해주자. 
~~~
<script src="https://utteranc.es/client.js"
        repo="[ENTER REPO HERE]"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
~~~ 
그럼 위와 같이 코드가 작성되는데, 위 코드를 포스트를 담당하는 html에 붙여넣어주자. 나의 경우 layouts/post.html에 넣었다. 마지막으로 config.yml에 
~~~
comments:
  provider: "utterances"
  utterances:
    theme: "boxy-light"
    issue_term: "pathname"
~~~
를 추가하여 관련 정보를 설정해주자. 

## Google Analytics
블로그에 꼭 있는 기능인 조회수 기능, 혹은 페이지 방문자의 정보를 기록하기 위해서는 [Google Analytics](https://analytics.google.com/ ) 를 사용하면 된다. 후에 Advertisement 를 넣어 혹시 모를 수익창출을 기도하기에도 좋다.  
링크에 들어가 회원가입 하자. 이후 Analytics 기능을 적용 시킬 계정의 이름, 웹사이트 이름, 웹사이트 주소, 카테고리, 사용 시간대를 설정해주자.
이후 여러가지 약관에 확인 하면 추적 DB가 생긴다.  
이제 우리가 만든 깃 블로그에 연결을 해줘야하는데 config.yml에 아래 부분을 추가해주자. 
~~~
google_analytics: 
  provider: google
  google:
    tracking_id: ""
~~~
tracking_id 부분에는 Analytics에서 여러분의 트래킹 id를 확인하고 넣어주면 된다.  
앞으로 두가지 부분만 해주면 된다. _includes/analytics.html를 생성하고 아래 코드를 넣어주자. 
~~~
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=(여러분의 트래킹아이디)"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', '여러분의 트래킹아이디');
</script>
~~~
마지막으로 _layouts/default.html에 한줄만 추가해주면 끝이다. 
~~~
{% include analytics.html %}
~~~

git push 이후 Google Analytics 로 가보면 잘 연결 된걸 확인할 수 있다. 끄읕.