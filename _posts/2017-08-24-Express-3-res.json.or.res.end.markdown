---
layout: post
title:  "which one I use res.json or res.end(JSON.stringify(data))"
date:   2017-08-24 17:00:52 +0900
categories: express update
---

## 관련자료

res.json 이 오버헤드가 없어 조금 더 빠르나 res.json 으로 쓰는 것이 일반적이다.  
[performance-difference-between-res-json-and-res-end]


[performance-difference-between-res-json-and-res-end]: https://stackoverflow.com/questions/22816856/performance-difference-between-res-json-and-res-end 