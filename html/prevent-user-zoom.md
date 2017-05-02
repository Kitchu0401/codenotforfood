# Prevent-user-zoom

*모바일 환경에서* 사용자 임의로 화면 확대를 할 수 없도록 막으려면:

``` html
<!doctype html>
<html lang="ko">
  <head>
    <meta charset="utf-8">
    <!-- 아래의 코드 중 'initial-scale=1, maximum-scale=1, user-scalable=no'를 추가한다. -->
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <link rel="shortcut icon" href="/favicon.ico">
    <title>your-application-name</title>
  </head>
  <body>

    <div id="content"></div>
    
  </body>
</html>
```

참고 [[stackoverflow.com](http://stackoverflow.com/questions/4389932/how-do-you-disable-viewport-zooming-on-mobile-safari)]