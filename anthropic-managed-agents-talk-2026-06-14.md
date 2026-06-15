# Anthropic Managed Agents 토크 요약

> 출처: "How to get to production faster with Claude Managed Agents" — Claude 채널 (2026.05.21)
> 발표: Michael & Harrison (Anthropic MTS)

---

## 핵심 전제

- **모델보다 인프라가 중요하다**
- **54%**가 관측성 제로인 상태로 에이전트를 출시한다
- 개발자 3명 중 1명이 메모리/컨텍스트 관리 실패
- 절반 이상이 인프라를 프로덕션 #1 블로커로 꼽음

---

## 4가지 핵심 개념

| 개념 | 설명 |
|---|---|
| **Agent** | 모델, 시스템 프롬프트, 도구, MCP 서버, 스킬의 설정 묶음 |
| **Environment** | 세션이 실행될 샌드박스 환경 (클라우드 or 자체 호스팅) |
| **Session** | 환경 내에서 실행되는 에이전트 인스턴스 |
| **Event** | 앱과 에이전트 간 메시지 (user turns, tool results, status) |

## 4개 이벤트 도메인

- **User Events** — 텍스트, 이미지, 문서, 인터럽트, 도구 결과, 확인(HITL), 결과 정의
- **Agent Events** — Claude의 응답, 도구 실행, 타 에이전트와 조율
- **Session Events** — 수명주기 (idle→running, 에러 복구, 결과 처리)
- **Span Events** — 장기 작업의 시작/종료 마커

---

## 본론: 핵심 기능

### 🤖 멀티 에이전트 오케스트레이션
Claude가 다른 Claude 스레드를 생성해 작업 위임

### ✅ Outcomes
평가 루브릭 정의 → 스스로 채점 → 만족할 때까지 반복

### 💭 Dreaming (연구 프리뷰)
수천 개 세션을 한번에 분석 → 메모리 자동 생성·편집

### 🔥 Self-Hosted Sandboxes (신규)
자체 VPC 내에서 샌드박스 운영, 네트워크/감사 완전 통제

### 🔥 MCP Tunnels (연구 프리뷰)
비공개 MCP 서버를 인터넷 노출 없이 안전하게 연결

---

## 샌드박스 파트너

| 파트너 | 포지션 |
|---|---|
| **Vercel** | Fluid Compute — 전체 VM, 빌드/샌드박스/함수 동일 기반 |
| **Modal** | 대규모 확장 — 수십만 개 샌드박스를 몇 분 내, GPU 지원 |
| **Daytona** | OS/스펙 다양화 — 일시정지/재개/포크 지원 |
| **Cloudflare** | microVM + Isolates — 경량, 서브밀리세컨드 기동 |
