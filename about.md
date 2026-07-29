---
layout: page
title: About
lang: en
alt_url: /ko/about/
lede: Cloud Infrastructure & Backend Engineer. OSS enthusiast building MCP servers, AI agents, developer tools and cloud-native services.
description: Jungwon Sohn — Cloud Infrastructure & Backend Engineer. Building TypeMCP, TypeChain and OpenVideo under Theorvane.
---

Cloud infrastructure and backend engineer, and an OSS enthusiast — most of what I build now is open source: MCP servers, AI agents, developer tools and cloud-native services.

That direction came out of two years and three months owning the backend of a government-funded vocational training LMS. Course progress there was the basis for tuition reimbursement, so the habit I took from it is simple: check that the numbers are right before checking that the feature works.

I handled deployment and operations alongside development, and moved into infrastructure from there. Watching learners lose their progress on every deploy is why I treat zero-downtime deployment as a data-integrity requirement rather than a feature.

## Open source

I build under [**Theorvane**](https://theorvane.tech) — open-source developer tools for explicit contracts and inspectable systems. Small public surfaces, typed contracts, transparent capability boundaries.

- [**TypeMCP**](https://github.com/Theorvane/type-mcp) — decorator-first TypeScript declarations and runtime tooling for Model Context Protocol servers. Definition validation, MCP SDK compilation, stdio and Streamable HTTP transports, and a tools-only LangChain adapter. Published on npm as [`@theorvane/type-mcp`](https://www.npmjs.com/package/@theorvane/type-mcp).
- [**TypeChain**](https://github.com/Theorvane/type-chain) — a decorator-first, type-safe authoring layer for LangChain JS tools and agents. `@Tool()` / `@Agent()` / `@Policy()` decorators, LangChain Core adapters, and an in-process TypeMCP bridge. On npm as [`@theorvane/type-chain`](https://www.npmjs.com/package/@theorvane/type-chain), published through GitHub Actions Trusted Publishing.
- [**OpenVideo**](https://github.com/Theorvane/openvideo) — a local-first desktop video editor with an AI agent that operates the timeline: reading a project, cutting clips, generating voice and video, exporting through local FFmpeg. Media stays on the machine and model providers are opt-in — a local Ollama engine needs no account.
- [**type-mcp-api-agent-skill**](https://github.com/Theorvane/type-mcp-api-agent-skill) — an orchestration skill and deterministic CLI workspace that turns API specifications into TypeMCP repositories.
- [**examples**](https://github.com/Theorvane/examples) — runnable TypeChain and TypeMCP examples with explicit runtime boundaries.

Outside the org: [Youth Policy MCP](https://github.com/sjungwon03/data-go-youth-policy-mcp), which exposes Korea's public youth-policy API as MCP tools, and [a chatbot](https://github.com/sjungwon03/data-go-youth-policy-chatbot) built on top of it.

## Certifications

- [AWS Certified Solutions Architect – Associate](https://www.credly.com/badges/6bc4a7c1-e9b5-4a2d-b484-10fc2ced198e/public_url)
- [HashiCorp Certified: Terraform Associate](https://www.credly.com/badges/c3392494-6836-4ab7-9376-698b420c522a/public_url)
- Engineer Information Processing · SQL Developer (SQLD)

## Contact

- Email — [sjungwon03@gmail.com](mailto:sjungwon03@gmail.com)
- GitHub — [github.com/sjungwon03](https://github.com/sjungwon03)

Full detail is on the [résumé]({{ '/resume/' | relative_url }}) page.
