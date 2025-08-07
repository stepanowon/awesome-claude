# Claude Code Templates 사용법 및 도움말

**Claude Code Templates**는 다양한 프로그래밍 언어와 프레임워크에 최적화된 Claude Code 설정을 자동으로 생성해주는 CLI 도구입니다.

## 🚀 빠른 시작

### 설치 및 실행
```bash
cd your-project-directory
npx claude-code-templates@latest
```

### 자동 설치 과정
설치 프로그램이 자동으로:
- 🔍 프로젝트 타입 감지 (JavaScript, Python 등)
- 🎯 프레임워크 선택 (React, Django, Flask 등)
- 📋 명령어 선택 (테스팅, 린팅, 디버깅)
- 🔧 자동화 훅 선택 (포매팅, 타입 체킹 등)
- ✅ 설치 전 확인

## 📁 프로젝트 구조

```
claude-code-templates/
├── cli-tool/          # NPM 패키지
├── common/            # 범용 템플릿
├── javascript-typescript/  # JS/TS 템플릿
├── python/            # Python 템플릿
├── go/               # Go 템플릿 (준비 중)
└── rust/             # Rust 템플릿 (준비 중)
```

## 📊 지원되는 언어 및 프레임워크

| 언어 | 프레임워크 | 상태 | 명령어 | 훅 | MCP |
|------|-----------|------|--------|-----|-----|
| JavaScript/TypeScript | React, Vue, Angular, Node.js | ✅ 완료 | 7+ | 9+ | 4+ |
| Python | Django, Flask, FastAPI | ✅ 완료 | 5+ | 8+ | 4+ |
| Common | 범용 | ✅ 완료 | 2+ | 1+ | 4+ |
| Go | Gin, Echo, Fiber | 🚧 준비 중 | - | - | - |
| Rust | Axum, Warp, Actix | 🚧 준비 중 | - | - | - |

## 🔧 자동화 훅 (Automation Hooks)

자동화 훅은 Claude Code의 워크플로우에서 특정 순간에 자동으로 실행되는 스크립트입니다.

### 훅 실행 시점
- **PreToolUse**: 도구 사용 전 (Write, Edit, Bash 등)
- **PostToolUse**: 도구 사용 후
- **Stop**: 코딩 세션 종료 시
- **Notification**: 시스템 알림 발생 시

### JavaScript/TypeScript 훅
- 🗂️ **Bash 명령어 로깅** - 모든 bash 명령어를 `~/.claude/bash-command-log.txt`에 추적
- 🚫 **Console.log 감지** - `console.log` 포함된 파일 저장 방지
- 🛡️ **NPM 보안 감사** - `package.json` 변경 시 `npm audit` 실행
- ✨ **Prettier 자동 포매팅** - JS/TS 파일 수정 후 자동 정렬
- 📝 **TypeScript 타입 체킹** - TS 파일 수정 후 `npx tsc --noEmit` 실행
- ⚠️ **와일드카드 임포트 경고** - `import *` 구문에 대한 경고
- 🧪 **자동 테스트 실행** - 코드 변경 시 관련 테스트 파일 실행
- 📢 **알림 로깅** - 모든 Claude Code 알림을 `~/.claude/notifications.log`에 기록
- 🔍 **ESLint 검사** - 코딩 세션 종료 시 수정된 파일에 ESLint 실행
- 📊 **번들 크기 분석** - 코딩 세션 종료 시 번들 크기 영향 분석

### Python 훅
- 🗂️ **Bash 명령어 로깅** - 모든 bash 명령어 추적
- 🚫 **Print 구문 감지** - `print()` 포함된 파일 방지
- 🛡️ **pip 보안 검사** - requirements.txt 변경 시 의존성 감사
- ✨ **Black 자동 포매팅** - Python 코드 자동 정렬
- 📝 **MyPy 타입 체킹** - 타입 힌트 검증
- 🧪 **자동 테스트 실행** - 수정된 파일에 pytest 자동 실행

### Go 훅 (준비 중)
- 🗂️ **Bash 명령어 로깅** - 모든 bash 명령어 추적
- 🚫 **Debug 구문 감지** - `fmt.Print` 구문 포함된 파일 방지
- 🛡️ **go mod 보안 검사** - go.mod 변경 시 의존성 감사
- ✨ **gofmt 자동 포매팅** - Go 코드 자동 정렬
- 🧪 **자동 테스트 실행** - 수정된 파일에 go test 실행

### Rust 훅 (준비 중)
- 🗂️ **Bash 명령어 로깅** - 모든 bash 명령어 추적
- 🚫 **Debug 구문 감지** - `println!` 구문 포함된 파일 방지
- 🛡️ **cargo 보안 검사** - Cargo.toml 변경 시 의존성 감사
- ✨ **rustfmt 자동 포매팅** - Rust 코드 자동 정렬
- 🧪 **자동 테스트 실행** - 수정된 파일에 cargo test 실행

### 훅 선택 예시
```
🔧 Select automation hooks to include (use space to select):
❯ ◉ PreToolUse: Block console.log statements in JS/TS files
  ◉ PostToolUse: Auto-format JS/TS files with Prettier
  ◉ PostToolUse: Run TypeScript type checking
  ◯ PostToolUse: Warn about wildcard imports
  ◯ PostToolUse: Run tests automatically for modified files
  ◯ Stop: Run ESLint on changed files
  ◯ Stop: Analyze bundle size impact
  ◯ Notification: Log Claude Code notifications

Controls:
- Space - 특정 훅 토글 on/off
- Enter - 선택 확인
- ← Back - 이전 단계로 돌아가기
```

## 🔌 MCP (Model Context Protocol) 서버

MCP 서버는 Claude Code를 데이터베이스, API, 파일 시스템 등의 전문 기능으로 확장합니다.

### 범용 MCP 서버
- 🛠️ **TypeScript SDK** - MCP 서버/클라이언트 개발용 공식 Anthropic SDK
- 🐙 **GitHub MCP** - GitHub API 통합 (저장소, 이슈, PR 관리)
- 🤖 **Puppeteer MCP** - Google Puppeteer를 사용한 브라우저 자동화
- 💬 **Slack MCP** - 실시간 Slack 대화 및 워크플로우 접근
- 📁 **File System MCP** - 모든 언어와 호환되는 로컬 파일 관리
- 🧠 **Memory Bank MCP** - AI 에이전트용 중앙화된 메모리 시스템
- 🤔 **Sequential Thinking MCP** - LLM이 복잡한 작업을 논리적 단계로 분해 지원
- 🔍 **Brave Search MCP** - 개인정보 보호 중심 웹 검색 도구
- 🗺️ **Google Maps MCP** - 지리적 위치 및 경로 안내용 Google Maps 통합
- 🕸️ **Deep Graph MCP** - DeepGraph를 통해 소스 코드를 의미 그래프로 변환

### JavaScript/TypeScript MCP 서버
- 🤖 **Puppeteer MCP** - 웹 스크래핑, 자동화 테스팅, 스크린샷 생성
- 📓 **Jupyter MCP** - 대화형 Jupyter 노트북과의 통합
- 🗄️ **PostgreSQL MCP** - PostgreSQL 데이터베이스에 대한 자연어 쿼리

### Python MCP 서버
- 🐍 **Python SDK** - FastMCP를 사용한 빠른 개발용 공식 Python SDK
- 🐳 **Docker MCP** - Docker 컨테이너를 통한 격리된 코드 실행
- 📊 **Opik MCP** - 추적 및 메트릭을 통한 LLM 앱 관찰 가능성

### Go MCP 서버 (준비 중)
- 🟢 **Go SDK** - Go 개발용 Google과 함께 유지 관리되는 공식 SDK
- 🔍 **MCP Language Server** - Go용 의미적 도구: 정의, 참조, 진단
- 🌐 **Gin MCP** - Gin API를 MCP 도구로 자동 노출
- 🗃️ **Go MySQL MCP** - Go로 구축된 사용하기 쉬운 MySQL 서버
- 🏹 **Go Archer** - Go 패키지용 시각적 의존성 분석

### Rust MCP 서버 (준비 중)
- ⚡ **Rust MCP SDK** - Rust용 고성능 비동기 SDK
- 🖥️ **HT MCP** - 헤드리스 터미널 상호작용을 위한 순수 Rust 구현
- 📚 **Rust Docs MCP** - 업데이트된 Rust 문서로 구식 코드 제안 방지
- ⛓️ **Substrate MCP** - Substrate 기반 블록체인과의 상호작용
- 🔄 **MCP Proxy** - stdio와 SSE 프로토콜 간의 빠른 프록시

### MCP 서버 선택 예시
```
🔧 Select MCP servers to include (use space to select):
❯ ◉ TypeScript SDK - Official Anthropic SDK for building MCP servers and clients in JS/TS
  ◉ File System MCP - Local file management; compatible with any language
  ◉ Memory Bank MCP - Centralized memory system for AI agents
  ◯ GitHub MCP - Integration with GitHub API for managing repos, issues, and PRs
  ◯ Puppeteer MCP - Browser automation using Google Puppeteer
  ◯ Slack MCP - Access to real-time Slack conversations and workflows
  ◯ Sequential Thinking MCP - Helps LLMs decompose complex tasks into logical steps
  ◯ Brave Search MCP - Privacy-focused web search tool
  ◯ Google Maps MCP - Integrates Google Maps for geolocation and directions
  ◯ Deep Graph MCP (Code Graph) - Transforms source code into semantic graphs via DeepGraph

Controls:
- Space - 특정 MCP 서버 토글 on/off
- Enter - 선택 확인
- ← Back - 이전 단계로 돌아가기
```

### MCP 설정 파일 예시
선택된 MCP 서버는 `.mcp.json` 파일에 구성됩니다:

```json
{
  "mcpServers": {
    "typescript-sdk": {
      "name": "TypeScript SDK",
      "description": "Official Anthropic SDK for building MCP servers and clients in JS/TS",
      "command": "node",
      "args": ["path/to/ts-sdk-server.js"],
      "env": {}
    },
    "github": {
      "name": "GitHub MCP",
      "description": "Integration with GitHub API for managing repos, issues, and PRs",
      "command": "node",
      "args": ["path/to/server-github"],
      "env": {
        "GITHUB_TOKEN": "..."
      }
    }
  }
}
```

## 🚀 사용 예시

### 대화형 설치
```bash
# 프로젝트 디렉토리에서 실행
cd my-react-app
npx claude-code-templates

# 설치 프로그램이 React를 감지하고 최적 설정 제안
# 설정 중 ← Back을 사용해 이전 선택 수정 가능
```

### 명령줄 옵션을 사용한 빠른 설치

#### JavaScript/TypeScript 프로젝트
```bash
# React + TypeScript 프로젝트 (모든 React 전용 명령어 포함)
npx claude-code-templates --language javascript-typescript --framework react --yes

# Node.js API (데이터베이스 및 미들웨어 명령어 포함)
npx claude-code-templates --language javascript-typescript --framework node --yes

# Vue.js 프로젝트 (컴포저블 및 컴포넌트 명령어 포함)
npx claude-code-templates --language javascript-typescript --framework vue --yes

# Angular 프로젝트 (서비스 및 컴포넌트 명령어 포함)
npx claude-code-templates --language javascript-typescript --framework angular --yes
```

#### Python 프로젝트
```bash
# Django 프로젝트
npx claude-code-templates --language python --framework django --yes

# Flask 프로젝트
npx claude-code-templates --language python --framework flask --yes

# FastAPI 프로젝트
npx claude-code-templates --language python --framework fastapi --yes
```

#### 기타 옵션
```bash
# 설치 미리보기 (실제 설치하지 않음)
npx claude-code-templates --dry-run

# 프롬프트 스킵하고 기본값 사용
npx claude-code-templates --yes

# 다른 디렉토리에 설치
npx claude-code-templates --directory /path/to/project

# 프레임워크 없이 특정 언어만
npx claude-code-templates --language javascript-typescript --framework none --yes
```

## 💡 주요 장점

### 시간 절약
**수동 설정:**
```bash
# CLAUDE.md를 수동으로 생성
# 언어와 프레임워크의 모범 사례 연구
# React/Vue/Angular/Node.js/Django/Flask/FastAPI용 사용자 정의 명령어 설정
# 각 프레임워크에 대한 린팅 및 포매팅 구성
# 다양한 프레임워크용 테스팅 워크플로우 추가
# 코드 품질을 위한 자동화 훅 설정
# ... 수시간의 구성 연구
```

**자동화된 설정:**
```bash
# JavaScript/TypeScript + React
npx claude-code-templates --language javascript-typescript --framework react --yes

# Python + Django
npx claude-code-templates --language python --framework django --yes

# ✅ 프레임워크별 명령어와 자동화로 30초 만에 완료!
```

### 자동화된 품질 보증
- **🔄 자동 품질 보증** - 코드 포매팅, 린팅, 타입 체킹 자동 실행
- **⚡ 빠른 개발** - 포매팅이나 테스팅 명령어를 수동으로 실행할 필요 없음
- **🛡️ 보안** - 자동 의존성 감사 및 취약점 감지
- **📊 성능 모니터링** - 번들 크기 분석 및 최적화 경고
- **🧪 테스트 커버리지** - 자동 테스트 실행으로 코드 품질 보장

### 프레임워크 특화 기능
각 프레임워크에 최적화된 명령어 제공:
- **React**: 컴포넌트, 훅, 스타일링
- **Vue**: 컴포저블, 컴포넌트, 라우팅
- **Angular**: 서비스, 컴포넌트, 모듈
- **Node.js**: API, 미들웨어, 데이터베이스
- **Django**: 모델, 뷰, 템플릿
- **Flask/FastAPI**: 엔드포인트, 미들웨어

### 확장된 기능
- **🔌 확장된 기능** - Claude의 기본 기능을 넘어선 전문 도구 및 서비스 접근
- **🏗️ 사용자 정의 통합** - Claude를 기존 도구 및 워크플로우에 연결
- **📊 데이터 접근** - 데이터베이스, API, 외부 서비스 직접 쿼리
- **🤖 자동화** - 여러 시스템이 필요한 복잡한 워크플로우 자동화
- **🛡️ 제어된 환경** - 각 MCP 서버는 자체 제어된 컨텍스트에서 실행

## 🛡️ 안전한 설치

### 보호 기능
- **자동 백업** - 기존 `CLAUDE.md` 및 `.claude/` 파일 백업
- **확인 필요** - 변경사항 적용 전 항상 확인 (`--yes` 플래그 사용하지 않는 한)
- **드라이런 모드** - `--dry-run`으로 설치될 내용 미리보기
- **언제든지 취소** - Ctrl+C를 누르거나 'No'로 답해 설치 취소
- **뒤로 가기 탐색** - 대화형 설정 중 이전 선택사항 수정 가능

## 🔧 요구사항

- **Node.js 14+** (설치 프로그램용)
- **[Claude Code](https://docs.anthropic.com/en/docs/claude-code) 설치 필요**

### Claude Code 설치
```bash
npm install -g @anthropic-ai/claude-code
```

### 프로젝트에서 사용
```bash
cd your-project
npx claude-code-templates
claude  # Claude Code 실행
```

## 📋 수동 설치 (선택사항)

자동화된 설치를 선호하지 않는 경우, 템플릿을 직접 복사할 수 있습니다:

```bash
# 저장소 복제
git clone https://github.com/davila7/claude-code-templates.git

# JavaScript/TypeScript + React 템플릿 복사
cp -r claude-code-templates/javascript-typescript/CLAUDE.md your-project/
cp -r claude-code-templates/javascript-typescript/.claude/ your-project/
cp -r claude-code-templates/javascript-typescript/examples/react-app/.claude/commands/* your-project/.claude/commands/

# 또는 Node.js API 템플릿 복사
cp -r claude-code-templates/javascript-typescript/CLAUDE.md your-project/
cp -r claude-code-templates/javascript-typescript/.claude/ your-project/
cp -r claude-code-templates/javascript-typescript/examples/node-api/.claude/commands/* your-project/.claude/commands/
```

## 🧪 테스트

### 포괄적인 테스트 스위트
```bash
# 전체 테스트 스위트 실행
npm test

# 특정 시나리오 테스트
npm start -- --language python --framework django --dry-run
npm start -- --language javascript-typescript --framework react --dry-run

# 대화형 모드 테스트
npm start
```

## 🤝 기여하기

모든 기여를 환영합니다! Claude Code를 모든 사용자를 위해 더 좋게 만들어주세요.

### 기여 방법
1. 이 저장소 포크
2. 기능 브랜치 생성 (`git checkout -b feature/amazing-template`)
3. 개선사항 또는 새로운 언어 지원 추가
4. 실제 프로젝트로 템플릿 테스트
5. 풀 리퀘스트 제출

### 기여 영역
- **새로운 언어 지원** - Rust, Go, Java, C#, PHP 등
- **프레임워크 템플릿** - Svelte, Next.js, Nuxt.js, NestJS, Laravel, Spring Boot 등
- **개선된 명령어** - 더 나은 테스팅, 배포, 디버깅 워크플로우
- **문서화** - 더 명확한 가이드 및 예시
- **버그 수정** - 기존 템플릿 개선

### 기여 가이드라인
- 기존 폴더 구조 따르기
- 포괄적인 `CLAUDE.md` 및 `README.md` 파일 포함
- `.claude/commands/`에 실용적인 사용자 정의 명령어 추가
- 실제 예시 제공
- 제출 전 실제 프로젝트로 테스트

## 📚 추가 자료

- **이슈** - [버그 신고 또는 기능 요청](https://github.com/davila7/claude-code-templates/issues)
- **토론** - [커뮤니티 토론 참여](https://github.com/davila7/claude-code-templates/discussions)
- **문서** - [Claude Code 공식 문서](https://docs.anthropic.com/en/docs/claude-code)

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 라이선스가 부여됩니다 - 자세한 내용은 [LICENSE](https://github.com/davila7/claude-code-templates/blob/main/LICENSE) 파일을 참조하세요.

## 🙏 감사의 말

- **Anthropic** - Claude Code 생성
- **커뮤니티** - 이 템플릿 개선에 도움을 주는 모든 기여자
- **오픈 소스 프로젝트** - create-react-app, vue-cli 및 유사한 도구의 영감

---

⭐ 유용했다면 GitHub에 별을 주세요!

🚀 Claude Code로 개발을 강화할 준비가 되셨나요? 지금 `npx claude-code-templates`를 실행하세요!
