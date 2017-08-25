---
layout: post
title:  "zsh: command not found: express"
date:   2017-08-24 17:00:52 +0900
categories: express update
---

## 증상

{% highlight ruby %}
zsh: command not found: express
{% endhighlight %}

## 해결

install할 때  `-g` 옵션만 줄 게 아니라,  
`sudo` 로 인스톨해야 express-cli를 사용하게 됨.

{% highlight ruby %}
sudo npm install -g express-generator
#=> Password: 
/usr/local/bin/express -> /usr/local/lib/node_modules/express-generator/bin/express-cli.js
{% endhighlight %}

