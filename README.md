# sjungwon03.github.io

개인 사이트. GitHub Pages(Jekyll)로 빌드·배포됩니다.

## 구조

```
_config.yml        사이트 설정
_layouts/          default · page · post
_includes/         head · header · footer
_posts/            글 (YYYY-MM-DD-제목.md)
assets/css/        스타일
index.html         글 목록
resume.md          이력
about.md           소개
feed.xml           Atom 피드
```

## 글 쓰기

`_posts/`에 `YYYY-MM-DD-슬러그.md` 형식으로 파일을 만듭니다.

```markdown
---
title: 글 제목
description: 목록과 검색에 노출되는 한 줄 요약
tags: [백엔드, 인프라]
---

본문.
```

`main`에 push하면 GitHub Pages가 자동으로 빌드합니다.

## 로컬 확인

```bash
bundle install
bundle exec jekyll serve
```

## 이력 페이지

`resume.md`는 별도 관리하는 이력서 원본에서 옮겨온 내용입니다.
공개 사이트라 자격증 등록번호와 병역 상세는 제외했습니다.
