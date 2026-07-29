---
layout: page
title: 소개
lang: ko
permalink: /ko/about/
alt_url: /about/
lede: 클라우드 인프라 · 백엔드 엔지니어. MCP 서버, AI 에이전트, 개발자 도구, 클라우드 네이티브 서비스를 오픈소스로 만듭니다.
description: 손정원 — 클라우드 인프라 · 백엔드 엔지니어. Theorvane에서 TypeMCP · TypeChain · OpenVideo를 만듭니다.
---

클라우드 인프라와 백엔드를 다룹니다. 지금 만드는 것의 대부분은 오픈소스입니다 — MCP 서버, AI 에이전트, 개발자 도구, 클라우드 네이티브 서비스.

이 방향은 정부지원 직업훈련 LMS의 백엔드를 2년 3개월간 주 담당하면서 잡혔습니다. 수강 진도율이 훈련비 환급의 근거인 도메인이라, 기능이 동작하는지보다 값이 맞는지를 먼저 보는 습관이 여기서 생겼습니다.

개발과 함께 배포·운영을 맡았고 거기서 인프라로 넘어왔습니다. 배포할 때마다 수강생의 진도가 사라지는 것을 겪었기 때문에, 무중단 배포를 기능이 아니라 데이터 정합성 요건으로 다룹니다.

## 오픈소스

[**Theorvane**](https://theorvane.tech)에서 만듭니다 — 명시적 계약과 들여다볼 수 있는 시스템을 위한 오픈소스 개발자 도구. 공개 표면을 작게 두고, 타입으로 계약을 고정하고, 권한 경계를 드러내는 것을 원칙으로 합니다.

- [**TypeMCP**](https://github.com/Theorvane/type-mcp) — Model Context Protocol 서버를 위한 데코레이터 우선 TypeScript 선언과 런타임 도구. 정의 검증, MCP SDK 컴파일, stdio · Streamable HTTP 전송, 도구 전용 LangChain 어댑터를 제공합니다. npm [`@theorvane/type-mcp`](https://www.npmjs.com/package/@theorvane/type-mcp)로 공개돼 있습니다.
- [**TypeChain**](https://github.com/Theorvane/type-chain) — LangChain JS 도구와 에이전트를 위한 데코레이터 우선 타입 안전 작성 계층. `@Tool()` / `@Agent()` / `@Policy()` 데코레이터, LangChain Core 어댑터, 인프로세스 TypeMCP 브리지를 담고 있습니다. GitHub Actions Trusted Publishing으로 npm [`@theorvane/type-chain`](https://www.npmjs.com/package/@theorvane/type-chain)에 배포합니다.
- [**OpenVideo**](https://github.com/Theorvane/openvideo) — 타임라인을 직접 조작하는 AI 에이전트를 붙인 로컬 우선 데스크톱 영상 편집기. 프로젝트를 읽고 클립을 자르고 음성·영상을 생성하며 로컬 FFmpeg으로 내보냅니다. 미디어는 기기에 남고 모델 제공자는 선택 사항이라, 로컬 Ollama만 쓰면 계정이 필요 없습니다.
- [**type-mcp-api-agent-skill**](https://github.com/Theorvane/type-mcp-api-agent-skill) — API 명세를 TypeMCP 저장소로 바꾸는 오케스트레이션 스킬과 결정론적 CLI 워크스페이스.
- [**examples**](https://github.com/Theorvane/examples) — 런타임 경계를 명시한 TypeChain · TypeMCP 실행 예제.

조직 밖으로는 청년정책 공공 API를 MCP 도구로 노출하는 [청년정책 MCP](https://github.com/sjungwon03/data-go-youth-policy-mcp)와, 그 위에 올린 [챗봇](https://github.com/sjungwon03/data-go-youth-policy-chatbot)이 있습니다.

## 자격증

- [AWS Certified Solutions Architect – Associate](https://www.credly.com/badges/6bc4a7c1-e9b5-4a2d-b484-10fc2ced198e/public_url)
- [HashiCorp Certified: Terraform Associate](https://www.credly.com/badges/c3392494-6836-4ab7-9376-698b420c522a/public_url)
- 정보처리기사 · SQL 개발자(SQLD)

## 연락

- 이메일 — [sjungwon03@gmail.com](mailto:sjungwon03@gmail.com)
- GitHub — [github.com/sjungwon03](https://github.com/sjungwon03)

자세한 내용은 [이력]({{ '/ko/resume/' | relative_url }}) 페이지에 있습니다.
