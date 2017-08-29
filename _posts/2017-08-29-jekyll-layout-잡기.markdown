---
layout: post
title:  "Jekyll layout 살펴보기"
date:   2017-08-29 16:19:52 +0900
categories: jekyll update
---

## 문제점

jekyll로 github page 를 열면서 디렉토리를 구별하고 싶은 생각이 떠올랐다.  
  
### 1.구현과정

일단 default로 jekyll을 설치했을 때 about페이지가 있음을 알 수 있다.
우리는 about 페이지와 같이 다른 express 페이지를 만들고 원하는 카테고리의 post list만 보이게 만들고 싶다. 

첫 github page에서 보이듯이 `layout: home` 의 모양으로 말이다.
따라서 let's see home's layout.

but when we see the directory, we can't find any directory seem to be relative to LAYOUT. 
because jekyll is using gemfile to avoid asome of repeative work. coursely, layout.

when jekyll build the all of our documentation, jekyll also build layout using gemfile.

anyway, let's see the home layout first.

### 2.How to find home layout

open terminal and type. 
`bundle show minima`

and type following statement successively
`cd $(bundle show minima)`

can you see the `_layout` directory?
enter the directory and see the home.html  

then copy home.html to express/index.md 
and modify 


```
for post in site.posts
```
to
```
for post in site.categories.express
```

that's all done.

if some post's categories is similar below
```
---
layout: post
title:  "Jekyll layout 살펴보기"
date:   2017-08-29 16:19:52 +0900
categories: express update
---
```

they look in expess page.

#### TIP
date in front matter cannot proceed current time
if you do jekyll wont' build your post.  
Jekyll documentation에 따르면  
`global variables, site variables, page variables`. 
가 있다는 것을 볼 수 있다.  

#### [jekyll-variables]



[jekyll-variables]: https://jekyllrb.com/docs/variables/
