# jekyll-theme-velog

velog 스타일의 읽기 흐름을 좋아하는 개발자를 위해 만든 Jekyll starter theme입니다. GitHub Pages 배포, 시리즈 탭, 태그 필터, GitHub 프로필 동기화, 기여 그래프, Giscus/Disqus 댓글, Algolia 검색까지 바로 붙일 수 있게 구성했습니다.

라이브 데모: [https://woonyong-kr.github.io/jekyll-theme-velog/](https://woonyong-kr.github.io/jekyll-theme-velog/)

## 미리보기

### 홈

![홈 미리보기](assets/images/docs/home-preview.png)

### 시리즈

![시리즈 미리보기](assets/images/docs/series-preview.png)

### 글

![글 미리보기](assets/images/docs/post-preview.png)

## 이 저장소가 적합한 경우

- GitHub Pages에 바로 올릴 수 있는 개인 개발 블로그 starter가 필요할 때
- velog처럼 글 읽기 쉬운 레이아웃과 시리즈 탭을 같이 쓰고 싶을 때
- GitHub 프로필과 잔디 그래프를 블로그 홈에 노출하고 싶을 때
- Giscus, Disqus, Algolia, Google Analytics를 필요할 때만 선택적으로 켜고 싶을 때

## 포함된 기능

- 글 목록, 태그 필터, 로컬 검색
- 시리즈 탭과 시리즈별 필터
- 썸네일, 이전 글 / 다음 글 네비게이션
- 라이트 / 다크 모드
- GitHub 프로필 동기화와 1년 기여 그래프
- Giscus 댓글, Disqus 댓글
- Algolia DocSearch 기반 검색
- GitHub Actions, Jenkins 배포 예시
- Jekyll Feed, SEO Tag, Sitemap

## 시작 방법

이 저장소는 `remote_theme` 패키지가 아니라, 그대로 복제해서 사용하는 starter repository입니다.

- 가장 쉬운 방법: GitHub의 `Use this template`
- upstream 변경을 계속 따라가고 싶을 때: `fork`

fork로 시작하면 upstream 변경을 직접 merge하거나, 별도 sync workflow를 붙여 운영 저장소에 반영할 수 있습니다.

## 처음 세팅할 때 가장 먼저 할 일

1. 저장소를 복제합니다.
2. 저장소 이름을 정합니다.
3. `_config.yml`의 `url`, `baseurl`, `title`, `description`을 바꿉니다.
4. `_data/profile.yml`, `_data/theme.yml`, `_data/series.yml`을 바꿉니다.
5. `main` 브랜치에 push 합니다.
6. GitHub Pages source를 `gh-pages` 브랜치 `/ (root)` 로 지정합니다.

`baseurl` 규칙은 반드시 맞아야 합니다.

```text
저장소 이름이 my-blog          -> baseurl: "/my-blog"
저장소 이름이 username.github.io -> baseurl: ""
```

커스텀 도메인을 붙일 계획이라도, GitHub Pages 저장소 이름 규칙과 `baseurl` 설정은 먼저 정확히 맞춰두는 편이 안전합니다.

## 로컬 실행

이 저장소는 Ruby `3.2.9` 기준으로 검증했습니다. `.ruby-version` 도 함께 포함되어 있어 `rbenv`, `asdf`, `mise` 같은 버전 매니저를 쓰면 바로 맞출 수 있습니다.

```bash
BUNDLE_FORCE_RUBY_PLATFORM=true bundle install
BUNDLE_FORCE_RUBY_PLATFORM=true bundle exec jekyll doctor
BUNDLE_FORCE_RUBY_PLATFORM=true bundle exec jekyll serve
```

```text
http://127.0.0.1:4000/
```

GitHub 프로필과 잔디 그래프까지 같이 미리 보고 싶다면 아래 스크립트를 한 번 더 실행하면 됩니다.

```bash
ruby scripts/fetch_github_contributions.rb
```

인증은 아래 셋 중 하나면 충분합니다.

- `GITHUB_GRAPHQL_TOKEN`
- `GITHUB_TOKEN`
- `gh auth login`

토큰이 없으면 프로필 fallback 데이터가 표시되고, 빌드 자체는 계속됩니다.

## 처음 수정하는 파일

처음에는 아래 네 파일만 봐도 전체 구조를 거의 파악할 수 있습니다.

```text
_config.yml           사이트 URL, 제목, 댓글/검색/분석 설정
_data/profile.yml     프로필 fallback 데이터
_data/theme.yml       헤더, 탭, 홈 화면, 통계 표시 여부
_data/series.yml      시리즈 제목과 설명
```

### `_config.yml`

```yml
title: 내 블로그
description: 블로그 설명
url: "https://username.github.io"
baseurl: "/repo-name"
```

### `_data/theme.yml`

```yml
header:
  show_github_link: true
  show_rss_link: true
  show_theme_toggle: true

home:
  initial_post_count: 12
  search_placeholder: 검색어를 입력하세요

hero:
  github_contributions:
    enabled: true
    username: your-github-id

profile:
  github_sync:
    enabled: true
```

### `_data/profile.yml`

GitHub 프로필 동기화를 아직 붙이지 않았거나 실패했을 때 보여줄 fallback 값입니다.

```yml
display_name: 이름
bio: 한 줄 소개
intro: 추가 정보
avatar: /assets/images/avatar-placeholder.svg
github: https://github.com/your-handle
```

### `_data/series.yml`

```yml
my-series:
  title: 시리즈 표시 이름
  description: 시리즈 설명
```

포스트 front matter에서는 키만 넣으면 됩니다.

```yml
series: my-series
```

## 포스트 작성 예시

```md
---
title: 글 제목
description: 카드에 보일 설명
date: 2026-01-01 09:00:00 +0900
updated_at: 2026-01-01 21:00:00 +0900
thumbnail: /assets/images/posts/cover.png
series: my-series
tags:
  - Jekyll
  - GitHub Pages
---
```

## 배포

### GitHub Actions

`.github/workflows/deploy.yml` 이 포함되어 있어서 `main` 브랜치에 push 하면 아래 순서로 자동 배포됩니다.

```text
main push
-> bundle install
-> GitHub 프로필 / 잔디 캐시 생성
-> jekyll build
-> gh-pages 배포
```

잔디 그래프 자동 갱신을 위해 매일 새벽 3시 17분에도 스케줄 실행합니다.

GitHub Pages 설정은 아래처럼 맞추면 됩니다.

1. `Settings -> Pages`
2. `Source: Deploy from a branch`
3. `Branch: gh-pages`
4. `Folder: / (root)`

### 커스텀 도메인과 HTTPS

커스텀 도메인을 쓴다면 아래 순서가 가장 안정적입니다.

1. `Settings -> Pages` 에서 `Custom domain` 입력
2. DNS에서 CNAME 또는 A 레코드 연결
3. GitHub Pages가 TLS 인증서를 발급할 때까지 대기
4. `Enforce HTTPS` 가 활성화되면 켜기

인증서가 늦게 붙을 때는 custom domain을 한 번 제거 후 다시 저장하면 재프로비저닝이 시작되는 경우가 있습니다.

### Jenkins

Jenkins 환경에서도 같은 흐름으로 배포할 수 있도록 `Jenkinsfile` 을 포함했습니다.

필요한 Credentials 예시는 아래와 같습니다.

```text
credentialsId: github-pages
  username: GitHub 사용자명
  password: GitHub Personal Access Token
```

## 선택 기능

값을 채운 경우에만 활성화되도록 기본값은 비워두었습니다.

### GitHub 프로필 동기화와 잔디 그래프

`_data/theme.yml` 에서 아래 값을 켭니다.

```yml
hero:
  github_contributions:
    enabled: true
    username: your-github-id

profile:
  github_sync:
    enabled: true
```

배포 환경에서 자동으로 동기화하려면 저장소 `Settings -> Secrets and variables -> Actions` 에 `GH_PAT` 를 추가하면 됩니다. 기본 권한은 `read:user` 정도면 충분합니다.

### Giscus 댓글

`_config.yml` 예시:

```yml
comments:
  provider: "giscus"
  giscus:
    repo: "owner/repository"
    repo_id: "REPOSITORY_NODE_ID"
    category: "Announcements"
    category_id: "CATEGORY_NODE_ID"
    mapping: "pathname"
```

처음 설정할 때 필요한 조건:

1. 저장소가 public 이어야 함
2. GitHub Discussions 가 켜져 있어야 함
3. [giscus app](https://github.com/apps/giscus) 이 저장소에 설치되어 있어야 함
4. `repo_id`, `category_id` 는 [giscus.app](https://giscus.app/ko) 에서 생성한 값을 그대로 넣어야 함

이 테마는 라이트 / 다크 모드에 맞춰 Giscus도 velog 느낌의 커스텀 CSS 테마를 적용합니다.

### Disqus 댓글

```yml
comments:
  provider: "disqus"
  disqus:
    shortname: "your-shortname"
```

### Algolia 검색

```yml
search:
  provider: "algolia"
  algolia:
    app_id: "YOUR_APP_ID"
    api_key: "YOUR_SEARCH_API_KEY"
    index_name: "YOUR_INDEX_NAME"
    insights: false
```

값이 비어 있으면 자동으로 로컬 검색 UI만 유지됩니다.

### Google Analytics

```yml
analytics:
  google:
    measurement_id: "G-XXXXXXXXXX"
```

## fork 후 체크리스트

1. `_config.yml` 의 `url`, `baseurl`, `title`, `description` 을 바꿨는지
2. `_data/profile.yml` 과 `_data/theme.yml` 이 본인 정보로 바뀌었는지
3. 샘플 포스트와 소개 페이지를 유지할지 교체할지 결정했는지
4. Pages source가 `gh-pages` root 로 지정되어 있는지
5. 커스텀 도메인을 쓴다면 DNS 와 HTTPS 까지 확인했는지
6. 댓글, 검색, 분석처럼 필요한 외부 연동만 켰는지

## 트러블슈팅

### 스타일이 깨질 때

`baseurl` 이 저장소 이름과 다르면 CSS, JS, 이미지 경로가 거의 전부 깨집니다. 가장 먼저 `_config.yml` 의 `baseurl` 을 확인하세요.

### Pages는 성공했는데 화면이 비어 있을 때

`gh-pages` 브랜치에 실제 빌드 산출물이 올라갔는지, GitHub Pages source가 `gh-pages / (root)` 로 맞춰졌는지 순서대로 확인하면 대부분 해결됩니다.

### HTTPS가 바로 안 붙을 때

DNS가 정상이어도 GitHub Pages TLS 인증서 발급에 시간이 걸릴 수 있습니다. `Settings -> Pages` 에서 인증서 provisioning 상태를 먼저 확인하세요.

### 프로필 동기화가 안 될 때

`_data/theme.yml` 의 `hero.github_contributions.username` 과 실제 GitHub 계정이 일치하는지, Actions secret `GH_PAT` 또는 `gh auth login` 이 준비되어 있는지 확인하세요.

### 로컬에서 bundle install 이 실패할 때

이 저장소는 Ruby `3.2.9` 기준으로 검증했습니다. 다른 Ruby 버전에서는 네이티브 gem 설치 문제가 생길 수 있으니 `.ruby-version` 에 맞춰 실행하는 편이 안전합니다.

## 검증 상태

- 원격 GitHub Actions 배포 성공
- 로컬 `bundle exec jekyll doctor` 통과
- 로컬 `bundle exec jekyll build` 성공
- include / layout 기준으로 미참조 dead code는 확인되지 않음

## 라이선스

MIT

포함된 이미지 출처는 [NOTICE.md](NOTICE.md) 에 정리해두었습니다.
