# AWS EC2 Instance

## 최초 인스턴스 시작 및 SSH 접속 설정

AWS Service 패널에서 EC2를 선택한 후 Instance를 생성하여 시작한다.

1. 서버의 종류를 선택하고

2. **Security group**을 새로 생성하여 지정하거나, 기존의 것을 지정

    - 새롭게 생성하려면 좌측 Network & Security > Security group

3. **Key pairs**을 새로 생성하여 지정하거나, 기존의 것을 지정

    - 새롭게 생성하려면 좌측 Network & Security > Key pairs

    - 새롭게 생성하는 경우 자동으로 다운로드 되는 **.pem 파일**을 로컬에 잘 저장해둔다.

4. 올라간 인스턴스의 **Public-DNS**를 잘 기록해둔다.

5. 로컬에서 다음의 명령어를 통해 원격SSH로 인스턴스 콘솔에 접속한다.
    
    `ssh -i [private-key-file-name] [instance-user-name]@[instance-public-dns]`

    Ex: `ssh -i "aws-lazecrew-2.pem" ec2-user@ec2-52-79-118-202.ap-northeast-2.compute.amazonaws.com`

## Node.js 및 npm 설치 [[Document](https://nodejs.org/ko/download/package-manager/#debian-ubuntu-linux)]
``` sh
# 이 명령줄을 생략하면 하위 버전(v4.0~)의 Node.js가 설치되니 주의. Npm이 함께 설치되지 않는다.
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## Git 설치
``` sh
sudo apt-get install git
```

## 주의

- `apt-get`이 익숙하다면, 운영체제 선택시 **Ubuntu**를 선택 할 것.