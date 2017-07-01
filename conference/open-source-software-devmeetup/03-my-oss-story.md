# 나의 오픈소스 이야기 by [김준기](https://github.com/achimnol) from [Lablup](http://www.lablup.com/#/) CTO

## First experience: Textcube

기술적 기반이 부족한 이들을 위한 php 기반 설치형 블로그

- 2004.03 TatterTools
- 2005    TNC(태터앤컴퍼니) 설립
- 2006.05 다음 티스토리 서비스 오픈 (TatterTools 기반)
- 2007.08 Textcude로 브랜드 변경
- 2008.09 Google TNC / textcube.com수인수

## Textcube 프로젝트 경험

대학 학부생 시절 대규모 사용자가 존재하는 코드 작성 경험 기회 ++

오픈소스 개발 방법론 체화
  1. Subversion + Trac
  2. Mercurial + Trac
  3. Git + Github

엔지니어링의 성공 (국내 웹 생태계의 긍정적인향영향)
- 웹표준(Html 5)의 적극적 / 선도적 도입
- 웹호스팅 업체들의 UTF-8 / PHP 5 지원 유도

실패의 경험: 자체 웹프레임워크화 (insight from Django) - 처참한 성능으로 롤백 ([branch 1.8-blackhistory](https://github.com/Needlworks/Textcube/tree/1.8-blackhistory1))
- Request 마다 소스를 chain compile하는 과정에서 급격한 성능 저하 - 당시 phython의 한계

## 한글 iPuTTY 프로젝트 경험

별도로 관리하던 저장소를 당시 타인이 운영하던 iPuTTY 저장소에 병합하는 방식으로 진행

C언어로 만들어진 대규모 Win32 코드를 읽어본 첫 경험

Cross-platform 지원을 위한 빌드환경 구축과 코드 추상화(입력 레이어와 실행 레이어의 분리)에 대해 알게됨

## Network Balancing Act

KAIST 박사과정 3년 간 full-time 개발: 24k rows C++ codes

자체적 가속기 API 탑재한 고성능 패킷 처리 프레임워크

복잡한 빌드 구성으로 인한 외부 기여 장벽 ++

## Sorna ([Github](https://github.com/lablup/sorna))

Lablup 회사 산하에서 개발중인 프로덕트, 다양한 오픈소스를 조합해서 만듬

비전: 코드(특히 머신러닝) 실행을 쉽고 빠르게!

- Zero-config
- Scalable
- Multi-tenent

잘 나와있는 오픈소스 많으니까 뚝딱뚝딱 조합하변 잘 되겠지??
- 전혀 아님. 니가 다 고쳐서 PR 보내고있다.
- 유지보수가 오래, 잘 되어있는 프로젝트에 비해 신생 or 안정화가 덜 된 프로젝트는 내가 수정해서 써야함.

## aiodocker

Docker 컨테이너를 비동기적으로 pooling

Python asyncio의 위험성

aiodocker 개발 story
- 비동기 내에서 동기 코드가 들어가면 반드시 병목이 되므로 모두 async로 이루어져야함
- docker-py에서 async를 지원하지 않음.
- aiodocker가 있으나 개발자가 머지만 하고 릴리즈를 안함. 메인테이너와 이야기해서 넘겨받음.

2016 PyCon APAC aiohttp 스프린트 참여
- 현대적인 Python 프로젝트의 CI / 테스팅 기법 습득

aiodocer 프로젝트 인수 후 협업
- 코드 리팩토링, CI 협업 경험
- docker swarm API를 타 개발자가 작성해서 PR 보내주기도 함

## aiotools [[Github](https://github.com/achimnol/aiotools)]

Sorna 내부 리팩토링 과정에서 asyncio 관련 중복 코드 라이브러리화

만든지 2달밖에 안됐는데 Star 12..?
- 저겆ㄹ한 곳에 홍보
- 지인에게 홍보
- 세미나 와서 홍보

PyCon 2017에서 발표 예정 [프로그램 안내](https://www.pycon.kr/2017/program/184)

## 경험으로부터의 조언

들이대기 (알아주고, 관심가져 줄 것)
영어는 기본 소양
피드백에 대한 긍정적인 수용 (더 좋은 프로그램을 만들자는 공통의 목적을 잊지 말 것)
참여를 원하는 프로젝트의 기존 개발자들이 뭘 중요시하는가? ++
오픈소스 개발 방법론 체득
- Git
- PR / issue reporting 요령
- Forum 문화
- Test case 및 CI 작성 요령 ++
