---
layout: post
title:  "구글 검색에서 githubPage 노출하기"
date:   2017-08-30 10:00:52 +0900
categories: jekyll update
---

### 계기

github Page 를 만들고 구글에서 검색해보았지만 나오지 않았다.  
온갖 검색어(url,title,content,description 등등)으로   search해 보았는데 나오지 않음.  
그래서 왜그런가 찾게됨.  

*안타깝게도 기본 설정의 GitHub 페이지는 일반적인 포탈사이트 블로그나 티스토리 등과는 달리 검색엔진에서 백날 검색해도 글이 나오지 않는다. 다시 말해, 아무리 좋은 글을 써놨다고 하더라도 누구 하나 볼 사람이 없다는 뜻이다. 고도로 연결된 정보화 사회의 정점을 달리는 우리들이 이런 고독감을 맛보면 되겠나? 당장 주요 검색엔진들에게 나 자신을 어필해보자. 
[kycfeel.github.io]*

*그렇다면 나도...구글검색에 노출하기로 했다.*{: style="text-decoration: line-through"}

### 개발 환경
github Page with Jekyll.

### 수많은 시행 착오

 #첫번째 시도  

 sitemap.xml 을 만들어서 넣으면 구글검색에 노출된다기에 `jekyll-sitemap` plugins 을 설치해 보았다. 
 _config.yml 을 열어 아래와 같이 해서 빌드해보았지만 빌드가 깨지더라.
```
# Build settings
markdown: kramdown
theme: minima
exclude:
  - Gemfile
  - Gemfile.lock
plugins:
  - jekyll-sitemap
```

 #두번째 시도  

  찾아보니 exclude 된 Gemfile에서 build에 필요한 정보를 가져오는 것을 확인  
  (의존성이라 부르기도 하지아마)  
  `Gemfile`을 열어 아래와 같이 해준다.
```
# If you have any plugins, put them here!
group :jekyll_plugins do
   gem "jekyll-feed", "~> 0.6"
   gem "jekyll-sitemap"
end
```

이제야 `_site`directory 에 sitemap.xml 이 생기고. 
`localhost:4000/sitemap.xml` 로 접속이 되었다.  

### but,근본적인 문제
##### *dublincity.github.io/sitemap.xml 접속이안되..*
{: style="color: red"}
 #세번째 시도  

 git push 해보니 sitemap.xml 이 안올라감. 이유는 다음과 같다.  
 내 경우에는 .gitignore 파일을 가지고 있는데 `sitemap.xml`이 들어있는 `_site` directory를  
 remote에 올리지 않게 되어 있다.
 .gitignore 에서 _site 를 빼서 repository에 올렸지만 `githubId.github.io/sitemap.xml` 에 접속이 안되는 것은 마찬가지.

 #네번째 시도  

 해결방법 : githubPage는 내부적으로 build하기 때문에 _site directory도 필요없고 내 로컬에서 쓰는 gemfile 이나 plugins 자체를 먹일 수 가 없는 것을 확인.  

 *결과적으로 _post디렉토리 빼곤 다 내 로컬에서 돌리기 위해 필요한 것이였다.*

 root에 sitemap.xml 을 만들고 [이 포스트]와 같은 내용 채움.  
 결과는 성공.

 -------------- 이제 거의 다 왔다 힘내자 ------------

### 나머지 과정

 1. 구글에 뜨기 위해서는 search console 에 등록해야 된다고 함.  
 search console 로 들어가서 사이트 추가시켜야 함.  

 2. sitemap.xml 만든 것 처럼 html파일 만들어서 root에 추가시키고 url로 접속해 보고 *로봇이 아닙니다 체크* 후   
 확인 누르자 
 그리고 sitemap.xml을 등록시키면 아래 이미지와 같이 나타나는데 접수중이 끝나려면   
 만 2일정도 기다려야 한다고 한다.  

 *동작이 안되면 이 포스트는 세상에 나올수 없을 것 같다..ㅎㅎ*{: style="text-decoration: line-through"}  

 진짜 끝... 

### 거의 빼기다 시피 한 참고자료
[kycfeel.github.io]  

[이 포스트]

##### *포스트 올려 주셔서 감사합니다.*

[kycfeel.github.io]: https://kycfeel.github.io/2017/03/03/검색엔진에서-GitHub-페이지-검색-가능하게-하기/

[이 포스트]: http://dveamer.github.io/homepage/Sitemap.html

