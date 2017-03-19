# Installation on windows
윈도우 10 환경에서의 설치 및 서비스 구동법


## 설치

[[설치페이지](https://www.mongodb.com/download-center)]

커뮤니티 버전, windows server로 되어있어 불안했지만 64-bit and later로 설치.

환경변수는 설정이 되어있었나 모르겠는데, 안되어있다면 "C:\Program Files\MongoDB\Server\3.4\bin\" 를 추가해주면 될 것

\+ 글 쓰고나서 확인해보니 안되어있길래 추가해줌.-_-



## 서비스 등록
windows에서 제공하는 sc.exe를 활용한 방법도 있다고 하지만 [[참고](http://joont.tistory.com/44)]

mongodb에서 커맨드라인 명령어로 service install을 지원해준다. (mongod -h 참고)

    mongod -f "C:\Program Files\MongoDB\Server\3.4\bin\mongo.conf" --install



## 설정
custom configuration file을 참조하게 해보려고 시간을 조금 쓰다가

뭔가 마음대로 되지 않아 dbPath만 바꾸고 일단 그냥 서비스로 올려둠;

추후 추가 설정 옵션이 생기면 수정 할 것.

[[링크는_아직_없다](https://github.com/Kitchu0401/codenotforfood/blob/master/mongodb/mongo.conf)]



## 참고
[[[MongoDB] 강좌 1편: 소개, 설치 및 데이터 모델링](https://velopert.com/436)] by Velopert