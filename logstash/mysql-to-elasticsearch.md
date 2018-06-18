# Logstash Mysql plugin 사용해보기

Mysql - Elasticsearch 연동을 위해 Logstash config 파일을 빌드해야할 일이 있었다.

본 글에서는 Logstash Mysql plugin 사용시 발생했던 문제들과 조치내역을 기록해본다.

## Base config

작성한 기본 설정 파일은 다음과 같다.

``` yml
input {
  jdbc {
    jdbc_driver_library => "{FULL_PATH_OF_CONNECTOR_JAR_FILE}"
    jdbc_driver_class => "com.mysql.cj.jdbc.Driver"
    jdbc_connection_string => "jdbc:mysql://{IP_ADDRESS}:{PORT}/{DEFAULT_SCHEMA}"
    jdbc_user => "{ACCOUNT_NAME}"
    jdbc_password => "{ACCOUNT_PASSWORD}"
    schedule => "*/6 * * * *"
    use_column_value => true
    tracking_column => "{COLUMN_NAME}"
    statement => "SELECT * FROM {SCHEMA}.{TABLE_NAME} WHERE {COLUMN} > IFNULL(:sql_last_value, 0)"
  }
}

output {
  elasticsearch {
    hosts => ["{IP_ADDRESS}:{PORT}"]
    index => "{INDEX_NAME}"
    document_type => "{TYPE_NAME}"
  }
}
```

Mysql plugin 사용을 위해선 Mysql connector jar가 있어야 하니 참고하자.

Mysql plugin 각 파라미터에 대해 알아보면:

- `jdbc_driver_library`: 상술한 connector jar의 경로, 가급적 full path를 넣어준다.
- `jdbc_driver_class`: connector jar 내에서 찾는 classpath를 적는 것 같음.
- `jdbc_connection_string`: 요청을 보낼 Mysql uri.
- `jdbc_user`: Mysql 계정명
- `jdbc_password`: Mysql 패스워드
- `schedule`: 요청을 주기적으로 보내기 위해 설정한다. 내부적으로 [Rufus Scheduler](https://github.com/jmettraux/rufus-scheduler)을 사용하며, Crontab 형식으로 입력해준다.
- `use_column_value`: Logstash가 새롭게 추가된 데이터임을 확인하기 위해 임의의 변수(`:sql_last_value`)를 사용하는데, `true`일 경우 Mysql 테이블의 칼럼 값을 사용한다. `false`일 경우 쿼리 수행시각이 사용됨
- `tracking_column`: 상술한 `use_column_value` 설정이 true일 경우, 이 값에서 가리키는 칼럼의 값을 사용한다. `numeric` 또는 `timestamp` 형식만 지원함
- `statement`: Mysql에 보낼 쿼리문. 상기 예제 config처럼 `:sql_last_value`를 사용 가능하다.

`use_column_value` 및 `tracking_column` 관련해서 [공식문서](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-jdbc.html#_predefined_parameters)에 기재된 간략한 예제도 참고하자.

``` yml
input {
  jdbc {
    statement => "SELECT id, mycolumn1, mycolumn2 FROM my_table WHERE id > :sql_last_value"
    use_column_value => true
    tracking_column => "id"
    # ... other configuration bits
  }
}
```

## Troubleshooting

### Mysql 계정 비밀번호 만료 관련

Config 작성 후 다른 Device로의 원격접속 시도시 다음과 같은 오류가 발생했다.

```
"Java::JavaSql::SQLException: Your password has expired. To log in you must change it using a client that supports expired passwords."
```

[Stackoverflow 질문](https://stackoverflow.com/questions/33387879/mysql-password-expired-cant-connect)의 답변에서 확인 할 수 있듯, `5.7.10`버전부터 매 1년 마다 주기적으로 비밀번호가 만료되도록 바뀌었다고 한다.

해당 답변에서는:

1. `root` 계정으로 접근해 `SET GLOBAL default_password_lifetime = 0;` 커맨드로 비밀번호 만료 주기를 제거하거나,

2. 설정파일 내 동일한 이름의 파라미터를 추가해줌

으로써 영구적으로 비밀번호 만료를 막는 방법이 있었으나, 그냥 아래의 코드로 `root` 계정의 비밀번호 기한을 수정하는걸로 타협을 봤다.

``` sql
ALTER USER `root`@`localhost` IDENTIFIED BY 'new_password', `root`@`localhost` PASSWORD EXPIRE NEVER;
```

근데 이게 실효가 있었는지 모르겠다.

이 정도 레벨의 문제는 config 요구처에서 해결하도록 하자고 해서..

### Server timezone issue

두 번째로 timezone 관련된 이슈였다.

문제 해결 후 포스팅을 위해 뒤져보니 다들 `KST` timezone이 인식되지 않는다고 포스팅들 해놓으셨던데, 내 경우는 아예 Mysql에 tiemzone 데이터가 없었다.

``` sql
-- SYSTEM 값이 튀어나온다.
SELECT @@global.time_zone, @@session.time_zone;
```

일단 위의 쿼리문을 돌려 적용중인 timezone을 확인했을 때 `SYSTEM`이란 값이 튀어나왔고, 에러메시지에는 디코딩에 실패한듯한 문자열이 출력됐었다.

Linux, FreeBSD, Sun Solaris 등 OS 내에서 timezone 데이터를 지원하는 경우는 [공식문서](https://dev.mysql.com/doc/refman/5.5/en/mysql-tzinfo-to-sql.html)를 참고해 `mysql_tzinfo_to_sql`을 사용하면 되고

내 경우는 OS Windows라 역시 [공식문서](https://dev.mysql.com/downloads/timezones.html)에서 timezone 데이터를 넣어주는 sql문을 다운받아 실행했다.

이후 Mysql의 설정파일(`C:\ProgramData\MySQL\{VERSION}\my.ini`)에 다음과 같이 timezone 관련 코드를 추가하고 Mysql을 재기동하면 된다.

``` ini
default-time-zone=Asia/Seoul
```

### 덧

[JAVA MYSQL 연동시 발생하는 에러 모음](https://yenaworldblog.wordpress.com/2018/01/24/java-mysql-%EC%97%B0%EB%8F%99%EC%8B%9C-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-%EC%97%90%EB%9F%AC-%EB%AA%A8%EC%9D%8C/)에서도 timezone 오류와 함께 ssl 관련된 오류 등을 정리해두셨다. 참고해보자.
