# Commit Convention
: 명확한 Commit 히스토리를 생성하기 위한 규정

사용 이유: 

- Change Log 자동 생성 
- Semantic version 자동 변경
- 빌드 및 배포 프로세스 수행
- 프로젝트 기여에 대한 난이도를 낮추기 위함
- 팀, 타인 등 다른 사람들에게 변화의 본질을 제대로 전달하기 위함

## 구조
``` bash
<타입>[적용 범위(선택 사항)]: <설명>
[본문(선택 사항)]
[꼬리말(선택 사항)]
```

<타입>[적용 범위(선택 사항)]: <설명> `subject`

- 소문자로 작성
- <타입> 및 <설명> 필수
- 온점`.` 사용하지 않음
- <설명>은 100자 이내로
- 명령형, 현재 시제

[본문(선택 사항)] `body`

- 명령형, 현재 시제
- 변경 이유와 이전과 달라진 점 등

[꼬리말(선택 사항)] `footer`

- 주요 변경 내용, 이슈
    - 이슈 번호는 별도 라인으로 작성 
    - 자동 클로즈 `Closes #123`
- 무엇을 고쳤는지, 왜 고쳤는지, 마이그레이션은 어떻게 해야 하는지





## 요소

|  타입  |  설명  |  특징  |
| :----: | :----: | :----:|
| fix: | 버그 수정 | PATCH |
| feat: | 새로운 기능 추가 | MINOR |
| BREAKING CHANGE: <br>또는 타입/스코프 뒤에 `!` | 버전 수정 등 큰 변화가 있음을 의미 | MAJOR
| | |
| refactor: | 기능을 추가하지 않는 코드 리팩토링 |
| docs: | documentation 작성 및 업데이트 | |
| perf: | 성능 개선 | 
| ci: | CI config 파일 및 스크립트 변경 | |
| style: | 코드에 영향을 주지 않는 스타일 변경 | white space, formatting, missing semi colon ...  |
| test: | 테스트 추가 및 기존 테스트 수정 | |
| revert: | 작업 되돌리기 | 
| build: | 시스템 또는 외부 종속성에 영향을 미치는 변경 사항 | npm, gulp, yarn 레벨 |
| chore: | 기타 변경 사항 | 패키지 매니저, assets, 빌드 스크립트 수정 등 |
| | |
| 그 외 | |
| init: | 프로젝트 초기 생성 | |
| comment: | 주석 추가 및 수정 | |
| rename: | 파일/폴더 수정 | |
| design: | CSS 등 사용자 UI 디자인 변경 | |



## 예제

#### Commit message
``` bash
docs: correct spelling of CHANGELOG
```

#### 적용 범위 + Commit message
``` bash
feat(lang): add polish language
```

#### 설명 + BREAKING CHANGE 꼬리말 
```bash
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

#### BREAKING CHANGE `!` 
``` bash
feat!: send an email to the customer when a product is shipped
```

#### BREAKING CHANGE `!` + 적용 범위
``` bash
feat(api)!: send an email to the customer when a product is shipped
```

#### BREAKING CHANGE `!` + BREAKING CHANGE 꼬리말
``` bash
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

#### 다중 단락 본문 + 다수의 꼬리말을 가진 커밋 메세지
``` bash
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```


---
!!! quote
    - [Gitmoji](https://gitmoji.dev/)
    - [Conventionalcommits](https://www.conventionalcommits.org/en/v1.0.0/)
    - [유의적버전2.0.0](https://semver.org/lang/ko/)
    - [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)
    - [AngularJS commit convention](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)
    - [POST-1](https://kdjun97.github.io/git-github/commit-convention/)
    - [POST-2](https://programmer-ririhan.tistory.com/335)
