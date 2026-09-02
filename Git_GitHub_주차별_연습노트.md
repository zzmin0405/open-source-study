# Git·GitHub 15주 통합 연습 노트

## 시작 전 준비

- Git 설치
- GitHub 계정
- SourceTree 설치(선택)
- VS Code 또는 메모장

연습은 별도 폴더에서 진행하고, 비밀번호·API 키·개인 인증서 등 비밀 정보는 GitHub에 올리지 않습니다.
## 문서 구성

이 노트는 강의계획서의 1~15주 과정에 기존 요약 내용과 『Pro Git 2nd Edition』의 공개 내용을 합친 통합본입니다. 각 주차는 핵심 개념, 명령어, 실습 또는 확인 문제 순서로 구성했습니다.

## 1주차 — 버전 관리와 Git의 사고방식

버전 관리 시스템은 파일이 언제, 누구에 의해, 어떻게 바뀌었는지 기록하여 과거 상태를 복구하고 여러 사람의 작업을 합칠 수 있게 합니다. 로컬 방식은 한 컴퓨터에서만 기록하고, 중앙집중형은 하나의 서버를 공동 사용하며, Git 같은 분산형은 각 사용자가 저장소의 전체 이력을 복제합니다.

Git은 파일별 변경분만 연속해서 저장한다고 생각하기보다, 커밋 시점의 프로젝트 전체 모습을 스냅샷으로 기록합니다. 바뀌지 않은 파일은 기존 데이터에 대한 연결을 재사용합니다. 대부분의 작업이 로컬에서 가능하고, 객체는 해시값으로 식별되며, 한번 커밋된 데이터는 일반적인 사용 과정에서 쉽게 사라지지 않습니다.

확인 문제:

1. 중앙집중형과 분산형 버전 관리의 차이는?
2. Git에서 스냅샷이란 무엇인가?
3. 인터넷 연결 없이도 가능한 Git 작업 세 가지를 적어 보세요.

## 2주차 — 오픈소스와 라이선스

Pro Git 자체도 Creative Commons BY-NC-SA 3.0으로 공개된 오픈소스 책입니다. 소프트웨어의 소스가 보인다고 해서 아무 조건 없이 사용할 수 있는 것은 아니며, LICENSE에 적힌 허용 사항과 의무를 따라야 합니다.

- 퍼미시브 계열(MIT, BSD, Apache 2.0): 비교적 넓게 재사용할 수 있지만 저작권 고지 등 조건을 지켜야 함
- 약한 카피레프트(LGPL, MPL 등): 정해진 범위에서 수정 소스 공개 의무가 발생할 수 있음
- 강한 카피레프트(GPL 계열): 결합·수정한 저작물을 배포할 때 동일 계열 조건과 소스 공개 의무가 발생할 수 있음

실습: 관심 있는 GitHub 저장소 3개의 LICENSE와 README를 확인해 라이선스 이름, 허용 사항, 의무, 금지 사항을 표로 만듭니다.

## 3주차 — 라이선스 호환성과 오픈소스 기여

여러 코드의 라이선스를 한 결과물에서 함께 사용할 때는 각각의 조건을 동시에 만족할 수 있는지 확인해야 합니다. 특히 배포 여부, 링크 방식, 수정 여부, 고지문 유지, 특허 조항에 따라 판단이 달라질 수 있습니다.

오픈소스 기여 전에는 CONTRIBUTING, CODE_OF_CONDUCT, LICENSE를 먼저 읽고 Issue나 Pull Request 양식을 지킵니다. 커밋은 한 가지 논리적 변경을 담고, 목적이 드러나는 메시지를 작성합니다.

연습: 공개 프로젝트에서 CONTRIBUTING 파일을 찾아 기여 절차를 다섯 단계로 요약합니다.

## 4주차 — 설치, 설정, 도움말

Git 설정은 system, global, local 순으로 적용되며 더 구체적인 설정이 앞의 값을 덮어씁니다.

```bash
git --version
git config --global user.name "이름"
git config --global user.email "메일"
git config --global init.defaultBranch main
git config --list --show-origin
git help config
git help commit
```

이름과 이메일은 커밋 작성자 정보가 됩니다. 저장소별로 다른 값을 쓰고 싶으면 해당 폴더에서 --global 없이 설정합니다.

## 5주차 — 저장소와 파일 상태

저장소를 얻는 방법은 기존 폴더를 git init으로 초기화하거나 원격 저장소를 git clone으로 복제하는 것입니다. Git이 보는 파일 상태는 크게 untracked와 tracked로 나뉘며, tracked 파일은 unmodified, modified, staged 상태를 오갑니다.

```bash
git init
git status
git status -s
git add README.md
git diff
git diff --staged
git commit -m "README 작성"
```

`git add`는 새 파일 추적 시작뿐 아니라 수정된 파일의 현재 내용을 다음 커밋에 포함시키는 명령입니다. `git diff`는 아직 스테이지하지 않은 변경을, `git diff --staged`는 다음 커밋에 들어갈 변경을 보여줍니다.

실습: 한 파일을 수정한 뒤 일부 시점에 add하고 다시 수정하여 staged 변경과 unstaged 변경이 동시에 존재하게 만듭니다.

## 6주차 — 커밋 이력, 삭제·이동, 무시 파일

```bash
git log
git log --oneline --graph --decorate --all
git log -p -2
git show HEAD
git rm old.txt
git mv old.md new.md
```

`.gitignore`에는 빌드 결과, 임시 파일, 비밀 설정처럼 저장소에 넣지 않을 경로를 기록합니다. 이미 추적 중인 파일은 나중에 .gitignore에 적는 것만으로 추적이 중단되지 않습니다.

예시:

```gitignore
.env
*.log
build/
node_modules/
```

## 7주차 — 되돌리기와 안전한 복구

```bash
git commit --amend
git restore 파일명
git restore --staged 파일명
git revert 커밋ID
git reflog
```

`amend`는 직전 커밋을 새 커밋으로 교체합니다. restore는 작업 폴더나 스테이지의 변경을 되돌립니다. revert는 과거 변경을 반대로 적용한 새 커밋을 만들기 때문에 공유 이력을 보존할 수 있습니다. reflog는 HEAD와 브랜치가 이동한 기록을 보여주어 잃어버린 커밋을 찾는 데 도움이 됩니다.

주의: `git reset --hard`와 `git clean -fd`는 작업 파일을 제거할 수 있으므로 결과를 이해하지 못한 상태에서는 실행하지 않습니다.

## 8주차 — 중간시험 종합 연습

다음 과정을 자료 없이 수행합니다.

1. 새 저장소를 만들고 사용자 설정을 확인한다.
2. README와 .gitignore를 작성한다.
3. 세 개의 의미 있는 커밋을 만든다.
4. log와 diff로 이력을 확인한다.
5. 잘못 수정한 파일을 restore한다.
6. 한 커밋을 revert한다.

설명형 대비: working tree, staging area, repository, HEAD, commit, hash의 관계를 자기 말로 설명합니다.

## 9주차 — 원격 저장소와 GitHub

원격 저장소는 인터넷 어딘가의 저장소 복사본입니다. origin은 clone할 때 흔히 만들어지는 기본 별칭일 뿐 특별한 예약어는 아닙니다.

```bash
git remote -v
git remote add origin 저장소주소
git fetch origin
git push -u origin main
git remote show origin
```

fetch는 원격 데이터를 내려받고 원격 추적 브랜치를 갱신하지만 현재 작업 브랜치를 자동으로 합치지 않습니다.

## 10주차 — clone, fetch, pull, push

```bash
git clone 저장소주소
git fetch origin
git pull origin main
git push origin main
```

`pull`은 보통 fetch 후 merge 또는 rebase를 수행하는 편의 명령입니다. push가 거절되면 원격에 내가 갖고 있지 않은 커밋이 있는지 먼저 확인합니다. 무조건 강제 push로 덮어쓰지 않습니다.

실습: GitHub 웹에서 README를 한 번 수정하고, 로컬에서는 다른 파일을 수정한 다음 fetch와 pull의 결과 차이를 관찰합니다.

## 11주차 — GitHub 협업

공개 프로젝트 기여의 일반적인 흐름은 fork → clone → topic branch → commit → push → Pull Request입니다. 프로젝트 관리자는 PR의 변경 내용을 검토하고 토론하며 병합할 수 있습니다.

```bash
git switch -c docs/readme-fix
git add README.md
git commit -m "docs: 사용법 보완"
git push -u origin docs/readme-fix
```

좋은 Pull Request에는 변경 이유, 주요 변경점, 확인 방법, 관련 Issue가 들어갑니다. 리뷰에서 수정 요청을 받으면 같은 브랜치에 추가 커밋을 push하면 PR이 갱신됩니다.

## 12주차 — 브랜치와 HEAD의 원리

Git 브랜치는 특정 커밋을 가리키는 가벼운 이동 포인터입니다. 커밋하면 현재 브랜치가 새 커밋을 가리키도록 이동합니다. HEAD는 현재 체크아웃한 브랜치를 가리킵니다.

```bash
git branch
git switch -c feature/login
git log --oneline --graph --decorate --all
git switch main
git branch -d feature/login
```

원격 추적 브랜치인 origin/main은 마지막 fetch 시점에 관찰한 원격 main의 위치를 나타냅니다.

## 13주차 — 병합, 충돌, rebase

Fast-forward 병합은 main을 대상 브랜치의 끝으로 그대로 이동할 수 있을 때 발생합니다. 두 브랜치가 각각 진행됐다면 공통 조상을 이용한 3-way 병합으로 새 병합 커밋을 만들 수 있습니다.

```bash
git switch main
git merge feature/login
git status
git merge --abort
```

충돌 파일의 표식을 정리한 뒤 테스트하고 add와 commit을 실행합니다. rebase는 커밋을 다른 기준 위에서 다시 만들어 직선형 이력을 만들지만, 이미 다른 사람에게 공개한 커밋에는 함부로 사용하지 않습니다.

```bash
git switch feature/login
git rebase main
```

## 14주차 — 배포, 태그, GitHub Pages

태그는 릴리스처럼 중요한 커밋에 고정된 이름을 붙입니다. annotated tag에는 작성자, 날짜, 메시지가 포함됩니다.

```bash
git tag -a v1.0.0 -m "첫 배포"
git show v1.0.0
git push origin v1.0.0
```

GitHub Pages 실습: index.html을 main에 커밋하고 저장소 Settings → Pages에서 배포 원본을 선택합니다. README에는 프로젝트 목적, 실행 방법, 라이선스, 배포 주소를 기록합니다.

## 15주차 — 심화 도구와 최종 프로젝트

Pro Git의 심화 장에는 interactive staging, stash, 검색, 이력 재작성, 고급 병합, rerere, bisect, submodule, hook, Git 객체와 참조가 포함됩니다.

```bash
git add -p
git stash push -m "작업 임시 보관"
git stash list
git grep 검색어
git blame 파일명
git bisect start
git cat-file -t HEAD
git rev-parse HEAD
```

최종 프로젝트 요구 사항:

- LICENSE, README, .gitignore 포함
- 의미 있는 커밋 5개 이상
- 기능 브랜치 2개 이상
- Pull Request 1개 이상
- 병합 또는 충돌 해결 기록
- v1.0.0 태그
- GitHub Pages 배포

## Pro Git 장별 수업 대응표

| Pro Git 장 | 핵심 내용 | 수업 주차 |
|---|---|---|
| 1장 Getting Started | 버전 관리, Git 특징, 설치와 설정 | 1·4주 |
| 2장 Git Basics | 저장소, add, commit, log, undo, remote, tag | 5~10주 |
| 3장 Git Branching | 브랜치, 병합, 원격 브랜치, rebase | 12~13주 |
| 4장 Git on the Server | 프로토콜, SSH, 서버 저장소 | 9~10주 심화 |
| 5장 Distributed Git | 분산 협업과 프로젝트 기여 | 11주 |
| 6장 GitHub | 계정, 기여, 프로젝트 관리 | 9~11주 |
| 7장 Git Tools | stash, reset, 검색, bisect, submodule | 7·15주 |
| 8장 Customizing Git | 설정, attributes, hooks | 15주 심화 |
| 9장 Git and Other Systems | 다른 VCS와 연동·이전 | 선택 학습 |
| 10장 Git Internals | 객체, 참조, packfile, 복구 | 12·15주 심화 |

## 출처 및 이용 조건

- Pro Git 공식 한국어판: https://git-scm.com/book/ko/v2
- Pro Git 공식 영문판: https://git-scm.com/book/en/v2
- 원문 저장소: https://github.com/progit/progit2
- 이용허락: Creative Commons Attribution-NonCommercial-ShareAlike 3.0

이 상세 학습편은 공개 교재 내용을 그대로 복제한 것이 아니라 강의 주차에 맞게 요약·재구성한 학습 자료입니다.
