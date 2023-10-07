# Git
: 분산 버전 관리 시스템(Distributed Version Control System, DVCS) 중 하나로, 소스 코드의 변경 내용을 효과적으로 관리하고 추적할 수 있는 도구
<br>여러 개발자가 협업하는 상황에서 소스 코드를 효과적으로 관리할 수 있다


## 흐름

![git-1](./images/git-1.png)

#### 동작 개념
- Working directory : 이력 관리 대상(tracked) 파일들이 위치하는 영역
    - 지정된 디렉터리에서 .git 폴더를 제외한 공간
    - 작업된 파일이나 코드가 저장되는 공간
- Staging area : commit할 대상 파일들이 위치하는 영역
    - .git 폴더 하위에 파일 형태로 존재 -> `index`
    - `git add` 명령을 입력하면, staging 할 파일들의 정보가 index 파일에 기록된다
- Repository : 이력이 기록된(committed) 파일들이 위치하는 영역
    - .git 폴더에 이력 관리를 위한 모든 정보가 저장되어 관리됨

#### Git이 관리하는 3가지 파일 상태

- Modified : 관리 대상 파일이 수정되고, commit이 되지 않은 상태
- Staged : 수정된 파일이 Staging area에 있는 상태
- Committed : 파일 변경사항 기록이 완료된 상태

-> 새로운 파일이 WD에 추가되면, 기존 tracking 대상에 없던 것이므로 Untracked 상태
<br>-> git add를 통해 Staging area로 이동시키면, Staged 상태
<br>-> Staged 파일에 git commit을 사용하면, Committed 상태 (Tracked, Unmodified)

!!! note 
    Staging Area가 필요한 이유?

    - 일부 파일만 commit : 수정된 파일들 중 일부만 선별적으로 commit해야 하는 상황에서, 원하는 파일만 선별하기 위함
    - 충돌 수정 : 둘 이상의 commit 이력을 merge하는 상황 또는 두 파일 간 자동 병합을 할 수 없는 충돌이 발생한 상황에서, 파일별 충돌을 해결하기 위해 중간에 commit을 해두는 것이 안정적
    - commit 수정 : 과거에 기록한 commit 이력을 수정하고자 할 때, 파일을 Staged 상태로 내리고 추가적으로 변경할 사항만 반영하여 commit을 하면 효율적이다


---
## Start

#### Repository
: git을 통하여 파일, 라이브러리, 패키지 등을 관리하는 공간

- `git init` : 빈 git 저장소 생성, 프로그램의 개발 이력이 기록되는 .git 폴더가 생성된다
- .gitignore : 이력 관리 대상에서 제외할 경로나 파일 지정
``` bash
mkdir repository_name && cd repository_name
git init
```

#### 사용자 설정
- global : 사용자의 PC 안 모든 저장소의 config 설정 동일하게 유지
``` bash
git config --global user.name "{name}"
git config --global user.email "{ID}@{email address}"
```

#### git reset 이해하기

이미 commit을 완료한 파일을 제거하는 방법 ?

1. 파일을 삭제 후 commit 진행 -> 파일을 추가했던 이력 존재
2. 파일을 추가하기 전 상태로 복귀하고, 이후의 commit 삭제 -> 파일 추가 이력까지 삭제

![git reset](./images/git-reset.png)

``` bash
git reset [option] [이동할 Hash]
```

| OPTION | Working dir | Staging Area | Repository | 
| :----: | :-------: | :-------: | :------: |
| --hard (내용 제거)| 변경 | 변경 | 변경 |
| --mixed | 유지 | 변경 | 변경 |
| --soft | 유지 | 유지 | 변경 | 

** git reset으로 commit이 삭제된 걸까?

- commit이 삭제되는 것은 아님
- HEAD는 브랜치를 참조하며, 브랜치는 항상 최신 commit을 참조한다
- 현재는 reset을 통해 브랜치가 참조하는 commit이 변경되어 이후의 commit 이력이 검색되지 않는 것
- 최신 commit의 hash 값을 통해 복귀할 수 있다

#### git commit --amend 이해하기

![Git amend](./images/git-amend.png)

---
!!! quote
    - Visual studio를 위한 Git -> [wikidocs](https://wikidocs.net/book/7060)
    - openai