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

## MongoDB 설치 [[Document](https://docs.mongodb.com/getting-started/shell/tutorial/install-mongodb-on-ubuntu/)]
``` sh
# Import the public key used by the package management system.
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv [public-key]

# 아래 명령어를 실행하기 전 운영체제의 버전을 확실하게 모른다면 아래의 명령어로 운영체제의 버전을 체크한다.
grep . /etc/*-release

# Create a list file for MongoDB.
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

# Reload local package database.
sudo apt-get update

# Install the MongoDB packages.
sudo apt-get install -y mongodb-org

# 기본 설정으로 /data/db 폴더가 생성되어있어야 한다.
sudo mkdir /data
sudo mkdir /data/db

# Launch
sudo mongod
```

## 주의

- `apt-get`이 익숙하다면, 운영체제 선택시 **Ubuntu**를 선택 할 것.