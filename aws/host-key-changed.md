# Host key가 변경되어 SSH 접속에 실패 할 때

AWS 내 새로운 Instance를 생성하여 기존의 key pair를 적용하고,

Elastic IPs를 적용하여 public-dns가 변경되었을 때 (Elastic IP 적용시 주의 메시지가 출력됨)

``` sh
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
[private-key-fingerprints-value].
Please contact your system administrator.
Add correct host key in /Users/Kitchu/.ssh/known_hosts to get rid of this message.
Offending RSA key in /Users/Kitchu/.ssh/known_hosts:6
RSA host key for [public-dns-value] has changed and you have requested strict checking.
Host key verification failed.
```

이렇게 혹시 공격받은거 아니냐고 징징댐;

## 해결 [[참고](http://visu4l.tistory.com/343)]

아래의 커맨드를 실행해 새롭게 private-key를 등록한다.

``` sh
ssh-keygen -R [public-dns-value]
```

해결이 되지 않는다면 링크를 한 번 더 참고하여 저장된 파일을 지워보도록 하자.