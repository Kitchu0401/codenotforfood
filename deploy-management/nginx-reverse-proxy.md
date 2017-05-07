# Nginx

## Official documents

You should look at the following URL's in order to grasp a solid understanding of Nginx configuration files in order to fully unleash the power of Nginx.

- [http://wiki.nginx.org/Pitfalls](http://wiki.nginx.org/Pitfalls)
- [http://wiki.nginx.org/QuickStart](http://wiki.nginx.org/QuickStart)
- [http://wiki.nginx.org/Configuration](http://wiki.nginx.org/Configuration)

## Bookmarked documents

### Reverse proxy

- [Opentutorial.org](https://opentutorials.org/module/384/4526)
- [stackoverflow.com](http://stackoverflow.com/questions/16549026/how-to-run-more-than-one-app-on-one-instance-of-ec2)
- [nginx를 이용한 Reverse Proxy 서버 구축 by 제이크](http://interconnection.tistory.com/27)
- [stackoverflow.com - Nginx reverse proxy + URL rewrite](https://serverfault.com/questions/379675/nginx-reverse-proxy-url-rewrite)

# Reverse proxy 구축

[[Official document](https://www.nginx.com/resources/admin-guide/reverse-proxy/)]

Proxy 서버는 클라이언트가 자신을 통해서 다른 네트워크 서비스에 연결하게 중계해주는 소프트웨어. ([출처](https://www.joinc.co.kr/w/man/12/proxy))

그 중에서도 Reverse-proxy는 동일한 서버 내의 다른 서비스 처리를 하는 곳으로 보내주는 것을 말함. ([출처](http://interconnection.tistory.com/27))

현재 단일 AWS EC2 인스턴스에서 다수의 서비스를 띄우기 위해 **Nginx**를 위해 Reverse-proxy를 간단하게 구성하였음.

## Nginx 설치

``` sh
$ sudo apt-get update
$ sudo apt-get -y nginx
```

## Nginx 설정

Nginx는 기본적으로 ```/etc/nginx/site-enabled/default``` 파일을 읽어 구동된다.

```/etc/nginx/site-available/[configuration-file-name].conf``` 파일을 생성하고

이를 ```/etc/nginx/site-enabled/``` 폴더에 동일한 파일명으로 생성하여 설정파일 단위로 관리하는걸 권장하는 듯 하지만

최초 구동이라 ```default``` 파일에 그대로 작성했다.

```/etc/nginx/site-available/default``` 파일에 작성하면 서비스 구동 시점에 자동으로 ```site-enabled``` 폴더로 복사되는 듯.

아래는 실제 설정파일. 기본 제공되는 내용 중 주석이 쳐진 부분은 일단 제거했다.
``` sh
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;

	# Add index.php to the list if you are using PHP
	index index.html index.htm index.nginx-debian.html;

	server_name _;

	# ORIGINAL SETTING: commented
	# location / {
	#	# First attempt to serve request as file, then
	#	# as directory, then fall back to displaying a 404.
	#	try_files $uri $uri/ =404;
	# }

    # /url-for-proxy로 들어온 요청을 port-number 포트로 포워딩하도록 설정.
    # port-number에는 node express 서비스가 돌고있다.
    # node express served path를 url-for-proxy로 설정한다면 하단의 rewrite directive가 필요없을 것.
    location /url-for-proxy {
        # Rewrite url
        rewrite /url-for-proxy(.*) $1 break;
        # Setting proxy
        proxy_redirect                  off;
        proxy_pass                      http://localhost:port-number;
        proxy_pass_header               Server;
        # 아래는 타 블로그에서 보고 추가했으나 변수 에러가 발생해 사용하지 않았다.
        # proxy_set_header Host           $http_host;
        # proxy_set_header X-Real-IP      $remote_addr;
        # proxy_set_header X-Schema       $schema;
    }
}
```

설정을 수정한 경우 다음의 커맨드를 입력하여 변경된 설정을 적용한다.

restart 커맨드도 존재하지만 권장되지 않는다.

``` sh
sudo service nginx reload
```