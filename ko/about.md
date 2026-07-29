---
layout: page
title: 소개
lang: ko
permalink: /ko/about/
alt_url: /about/
avatar: true
lede: 클라우드 인프라 · 백엔드 엔지니어. MCP 서버, AI 에이전트, 개발자 도구, 클라우드 네이티브 서비스를 오픈소스로 만듭니다.
description: 손정원 — 클라우드 인프라 · 백엔드 엔지니어. Theorvane에서 TypeMCP · TypeChain · OpenVideo를 만듭니다.
---

클라우드 인프라와 백엔드를 다룹니다. 지금 만드는 것의 대부분은 오픈소스입니다 — MCP 서버, AI 에이전트, 개발자 도구, 클라우드 네이티브 서비스.

## 오픈소스

[**Theorvane**](https://theorvane.tech)이라는 이름으로 개발자 도구를 만듭니다. 겉으로 드러나는 API는 작게, 지켜야 할 약속은 타입으로, 무엇을 할 수 있는지는 코드에서 바로 보이게. 이 세 가지를 기준으로 두고 있습니다.

| 프로젝트 | 설명 |
| --- | --- |
| [**TypeMCP**](https://github.com/Theorvane/type-mcp)<br>[`@theorvane/type-mcp`](https://www.npmjs.com/package/@theorvane/type-mcp) | MCP 서버를 데코레이터로 선언하는 TypeScript 라이브러리입니다. 선언을 검증해 MCP SDK 코드로 만들고 stdio와 Streamable HTTP를 지원합니다. LangChain에서 도구로 가져다 쓰는 어댑터도 함께 넣었습니다. |
| [**TypeChain**](https://github.com/Theorvane/type-chain)<br>[`@theorvane/type-chain`](https://www.npmjs.com/package/@theorvane/type-chain) | 같은 방식을 LangChain JS 쪽에 적용했습니다. `@Tool()`, `@Agent()`, `@Policy()`로 선언하면 LangChain Core가 쓰는 형태로 바뀌고, TypeMCP로 만든 도구를 같은 프로세스 안에서 바로 끌어올 수 있습니다. npm 배포는 GitHub Actions가 처리합니다. |
| [**OpenVideo**](https://github.com/Theorvane/openvideo) | AI가 타임라인을 직접 만지는 데스크톱 영상 편집기입니다. 프로젝트를 읽고, 클립을 자르고, 음성과 영상을 만들고, FFmpeg으로 내보내는 것까지 에이전트가 합니다. 영상은 기기 밖으로 나가지 않고 모델은 원하는 것만 연결하면 됩니다. Ollama를 로컬로 띄우면 계정 없이 씁니다. |
| [**type-mcp-api-agent-skill**](https://github.com/Theorvane/type-mcp-api-agent-skill) | API 문서를 넣으면 TypeMCP 저장소를 만들어 주는 도구입니다. |
| [**examples**](https://github.com/Theorvane/examples) | TypeChain과 TypeMCP를 실제로 돌려 보는 예제 모음입니다. |

## 프로젝트

| 프로젝트 | 설명 |
| --- | --- |
| [**청년정책 MCP**](https://github.com/sjungwon03/data-go-youth-policy-mcp) | 온통청년 공공 API를 MCP 도구로 감쌌습니다. 별도 연동 없이 정책을 검색하고 걸러낼 수 있습니다. |
| [**청년정책 챗봇**](https://github.com/sjungwon03/data-go-youth-policy-chatbot) | 위 MCP 서버를 물려서 만든 정책 상담 챗봇입니다. |
| [**YouthPick**](https://github.com/YouthPick) | 청년정책 추천 플랫폼입니다. Spring Boot 3.5 · Java 21 · React 19으로 만들었고, 5인 팀의 팀장으로 인증 · 관리자 · 채팅 · 파일 · 프로필 도메인을 맡았습니다. |
| [**KOSA 최종 프로젝트**](https://github.com/sjungwon03/kosa-final-project) | Proxmox 온프레미스와 AWS를 묶은 하이브리드 인프라입니다. 물리 서버 4대 위에 VM 25대와 Kubernetes HA 클러스터를 Terraform · Ansible로 올렸고, 5인 팀의 인프라 총괄을 맡았습니다. |

## 자격증

- [AWS Certified Solutions Architect – Associate](https://www.credly.com/badges/6bc4a7c1-e9b5-4a2d-b484-10fc2ced198e/public_url)
- [HashiCorp Certified: Terraform Associate](https://www.credly.com/badges/c3392494-6836-4ab7-9376-698b420c522a/public_url)
- 정보처리기사 · SQL 개발자(SQLD)

## 연락

- 이메일 — [sjungwon03@gmail.com](mailto:sjungwon03@gmail.com)
- GitHub — [github.com/sjungwon03](https://github.com/sjungwon03)

자세한 내용은 [이력]({{ '/ko/resume/' | relative_url }}) 페이지에 있습니다.
