# Caching your GitHub password in Git
Git 사용시 SSH 인증이 아닌 ID / Password 로 인증 할 경우, credential.helper를 활용해보자.

## Mac
노트북에서의 push를 위해 Mac 부분의 코드를 참고했다. [[링크](https://help.github.com/articles/caching-your-github-password-in-git/#platform-mac)]

1. 확인용 커맨드

    Usage 관련 메시지가 출력되었다면 이미 설치된 것.
    
    (Usage: git credential-osxkeychain <get|store|erase>)

    ```
    $ git credential-osxkeychain
    ```

2. 전역 설정

    git 전역에서 osxkeychain을 credential.helper로 사용하도록 설정해준다.

    ```
    $ git config --global credential.helper osxkeychain
    ```

3. Push

    clone이 아닌 git init 후 최초의 push인 경우,

    remote set-url로 저장소의 url을 지정해준 후 push한다.

    차례로 username과 password를 입력하고 인증에 성공하면 push가 이루어진다.

    ```
    $ git remote set-url "repository_name" "repository_url"
    $ git push "repository_name" "branch_name"
    Username for 'https://github.com':
    Password for 'https://"Username"@github.com':
    ```

## Windows
데스크탑 개발환경에서도 간편하게 push가 가능하도록 설정한다. [[링크](https://help.github.com/articles/caching-your-github-password-in-git/)]

1. 전역 설정

    Windows의 경우 wincred를 사용한다.

    ```
    $ git config --global credential.helper wincred
    ```

2. Push

    하던대로 하면 된다.

    ```
    $ git push "repository_name" "branch_name"
    Username for 'https://github.com':
    Password for 'https://"Username"@github.com':
    ```