# AWS EC2 인스턴스에서 Elasticsearch 구동하기

제목 그대로, AWS EC2에서 Elasticsearch 구동하고 원격 접근이 가능하도록 설정해본다.

## 설치

설치는 무난하게 [공식 문서의 설치과정](https://www.elastic.co/guide/en/elasticsearch/guide/master/running-elasticsearch.html)을 참조한다.

7.0.0 버전 기준으로:

``` sh
# tar 파일 다운로드
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.0.0-alpha1.tar.gz

# 압축 해제
tar -xvf elasticsearch-7.0.0-alpha1.tar.gz

# 폴더 이동 후 실행
cd elasticsearch-7.0.0-alpha1/bin
./elasticsearch
```

## 설정 변경 - Host

Elasticsearch가 설치된 폴더로 이동 후 `config/elasticsearch.yml` 파일을 열고 아래의 항목을 주석해제 후 IP를 입력한다.

``` yml
#
# Set the bind address to a specific IP (IPv4 or IPv6):
#
network.host: <IP_ADDRESS>
```

여기서 주의해야할 부분 - Public IP를 입력하면 접근이 안된다.

AWS의 특성 때문인지 확실하게 모르겠지만, Private IP를 입력해야한다.


관련된 내용은 [여기](https://discuss.elastic.co/t/elasticsearch-5-0-1-fails-to-start-on-aws-with-discovery-ec2-bindexception-cannot-assign-requested-address/66524)를 참고하자.

## 설정 변경 - Virtual Memory

`localhost`로 잡고 시운행 했을 때는 아무런 문제 없이 구동되더니 `network.host` 변경 후 메모리 관련 오류가 발생한다.

[공식 문서](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)를 참고해 변경해주자.

``` sh
# 커맨드 라인으로:
sysctl -w vm.max_map_count=262144

# /etc/sysctl.conf 파일에서:
vm.max_map_count=262144
```