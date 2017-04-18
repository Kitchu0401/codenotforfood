# Issues

## Template 성격의 프로젝트를 내려받아 실제 저장소로 변경하는 경우
1. 우선 적용할 템플릿 프로젝트를 저장소에서 clone 한다.
``` sh
git clone https://github.com/user-name/template-repo-name.git
```

2. 폴더로 이동하여 `git remote` 명령어로 바라보는 repository 주소를 변경한다.

- 사실 이 부분에선 `remove` 후 `add` 하는 것보다 `set-url` 이 **당연하지만** 정석일 것 같다.-_-;
``` sh
cd template-repo-name
git remote remove origin
git remote add origin https://github.com/user-name/real-repository-name.git
```

3. 저장소를 생성하여 충돌이 일어나는 경우 (ex: README.md를 생성해둔 경우)
``` sh
git pull origin master
# conflict를 해결하시고
git push origin master
```

** 또는 1.로 돌아가서, 실제로 수행했던 방법 **
clone 후 디렉토리 이름 변경해주기 귀찮아서 이렇게 했다.
1. 프로젝트 디렉토리를 생성하고, `git init` 으로 저장소를 초기화한다.
``` sh
mkdir real-repository-name
cd real-repository-name
git init
```

2. 당연하게도 `git remote` 로 템플릿 프로젝트를 받은 후, `git pull`
``` sh
git remote add origin https://github.com/user-name/template-repo-name.git
git pull origin master
```

3. 위의 2. 부터 수행하여 저장소 실제걸로 바꾸고, conflict 해결한 후 사용한다.