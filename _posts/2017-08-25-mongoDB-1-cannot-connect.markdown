---
layout: post
title:  "Cannot connect to the MongoDB at localhost:27017."
date:   2017-08-25 13:00:52 +0900
categories: mongodb update
---

## 증상

robo3T 로 localhost(mongodb)에 connect 할 때   
`Cannot connect to the MongoDB at localhost:27017.` 의 alert창이 뜸.

## 해결

terminal 로 들어가서 `sudo mongod` 를 하여 몽고디비를 연결시킨다   
매번 이렇게 해야하는지에 대해서는 아직 알아내지 못하였다.