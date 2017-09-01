---
layout: post
title:  "소스가 수정될 때 grunt를 이용하여 express App 자동 reload 하기"
date:   2017-08-31 12:00:52 +0900
categories: etc update
---

### 포스트 목적

현재 express 를 사용하여 개발을 진행하고 있다. 매번 'npm start' 를 사용하여 'node ./bin/www'라는   
스크립트를 실행시키는데 앱을 매번 브라우저를 reload 하고 npm start 를 타이핑하는데 문제를 느낌.   
개발자라면 do not repeat yourself 를 실쳔해야 한다는데 이번 포스트에서 한번 해보기로함.

원래는 gulp를 살짝 건드려 보았는데 grunt, gulp, webpack를 대충은 알아두면 좋을 것같아 grunt를 사용.  

차이점은 다음 포스트를 참고 [webpack,gulp,grunt]

*먼저 관련자료는 다음 블로그를 참고하자.*
[grunt설치]  

나는 독해능력이 부족한 것인가...뭔가 필요한 기능을 찾는데 오버해드가 많은 것 같아서  
필자처럼 
### 어떤 소스가 수정되었을 때 express App 만 reload 시키고 싶다  
면 다음과 같이 하도록 하자. 

원하는 곳에가서 디렉토리를 하나 만들고 필자의 경우는 grunt 를 생성.
터미널로 디렉토리에 들어가 
`npm install grunt`,
`npm install grunt-cli`
를 해준다.

첫번째 스크립트는 grunt를 설치하는 것이고 두번째는 cli환경에서 grunt 같은 명령어를 실행 할 수 있도록 한다.

grunt/gruntfile.js를 만들고 스크립트를 채운다.
```
module.exports = function(grunt) {
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    uglify: {
      build: {
        src: '../bin/www',
        dest: '../bin/app.min.js'
      }
    },
    express: {
    	all: {
    		options: {
    			port: 3000,
    			hostname: 'localhost',
    			bases:['../public'],
    			livereload:true
    		}
    	}
    },
    watch: {
    	options:{livereload:true},
      scripts: {
        files: ['../*/*.*'],
        tasks: ['uglify'],
        options: {
          spawn: false,
        }
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-uglify')
  grunt.loadNpmTasks('grunt-contrib-watch')
  grunt.loadNpmTasks('grunt-express')
  grunt.registerTask('default', ['express','watch'])
}
```

완벽하게 이해하지는 못했지만 gruntfile.js 는 grunt가 실행될때 참고하는 파일이라고 보면 된다 `package.json`을 읽는데 grunt가 실행될때 필요한 의존성 모듈을 찾는 것이므로 express app의 package.json 과는 관련이 없다. 

스크립트가 변경된 것을 알기 위해 watch를 사용하고 express앱을 리로드하기 위해 express 를 사용한다.

`npm install grunt-express --save`,`npm install grunt-contrib-watch --save`

를 해주면 package.json 에 등록 될테니 npm install 을 해서 node_modules 에 추가.(이거 안하면 function을 찾을 수 없다고 나옴.)

그리고 나면 터미널로 grunt디렉토리에서 grunt 를 하게 되면 default task를 실행하게 된다. 

끝~

[webpack,gulp,grunt]

[grunt설치]: https://gruntjs.com/getting-started


[performance-difference-between-res-json-and-res-end]: https://stackoverflow.com/questions/22816856/performance-difference-between-res-json-and-res-end 