# Flybook Cli - Static web site generator

[Haroopress](https://github.com/rhiokim/haroopress), [Haroopad](https://github.com/rhiokim/haroopad) 개발자분, OSS 밋업에서도 뵈었던!

마크다운 문서를 정적 웹문서로 변환하여 publishing

    Jekyll과 다른 점은 무엇?

## 실제 웹페이지 업로드 시연

1. 디펜던시 설치

``` sh
npm install flybook -D
npm install gh-pages -D
```

2. 정적 문서로 변환 후 깃헙 페이지 내 배포

``` sh
flybook docs --outdir=out
gh-pages -d out
```

        circle ci는 무엇인가?

## 현업에서의 문서화 예제

1. 문서 작성자 push
2. Github webhook > CI (Jenkins, [Circleci](https://circleci.com/))
3. Flybook build
4. Gh-pages deploy
