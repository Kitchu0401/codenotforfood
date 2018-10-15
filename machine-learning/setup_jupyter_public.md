# Jupyter Notebook 공용 접속 설정

머신러닝 스터디 중 텐써플로우 GPU 설치가 안되는 스터디원분을 위해 Jupyter Notebook 원격접속이 가능하도록 설정해봤다.

## 참고 링크

기록의 상세한 내용은 다음의 링크에서 참고했다.

- [Remote access to a public jupyter notebook server](https://luppeng.wordpress.com/2017/04/18/remote-access-to-jupyter-notebook/) - 전반적인 설정
- [Windows 방화벽에서 TCP 80번 포트 열기](https://wiki.mcneel.com/ko/zoo/window7firewall) - 윈도우즈 포트 개방 참조

## Jupyter Notebook 설정 파일 생성 및 IP 주소 지정

Jupyter Notebook 설치 후, 다음의 커맨드로 설정 파일 생성

```
$ jupyter notebook --generate-config
```

아래의 항목을 주석제거하고 `localhost` 부분을 본인의 ip로 변경한다.

```
## The IP address the notebook server will listen on.
#c.NotebookApp.ip = 'localhost'
```

## 윈도우 방화벽 포트 개방 설정

Windows 10에서:

```
설정 - 네트워크 및 인터넷 - Windows 방화벽 - 고급 설정 - 인바운드 규칙 - 새 규칙 생성

포트 - TCP - Jupyter Notebook default 포트인 8888 개방 설정
```

이후 Jupyter Notebook을 실행했을 때 커맨드라인에서 확인 가능한 `token` 값을

Jupyter Notebook 실행시 뜨는 창에 입력해주면 원격접속이 가능해진다.

## ID / Password 설정

후일 추가 예정