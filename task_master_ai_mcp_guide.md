# Task Master AI MCP 사용 가이드

## 개요

Task Master AI는 AI 어시스턴트와 함께 작업하는 개발자를 위해 특별히 설계된 AI 기반 작업 관리 시스템입니다. Model Context Protocol(MCP)를 통해 Cursor, Lovable, Windsurf, Roo 등과 같은 코딩 환경과 완벽하게 통합됩니다.

## 주요 특징

### 핵심 기능들
- **PRD 파싱**: Product Requirements Document를 자동으로 파싱하고 구조화된 실행 가능한 작업을 생성
- **AI 워크플로우 깊은 통합**: AI 어시스턴트와의 자연스러운 협업을 위한 최적화
- **다중 모델 지원**: Claude, Perplexity, OpenAI 및 OpenRouter를 통해 다양한 AI 제공업체 지원
- **유연한 구현**: 표준 명령줄 도구 또는 통합 개발 도구 내의 MCP 서버로 사용 가능
- **작업 추적 및 관리**: 체계적인 작업 분해, 복잡성 분석, 진행 상황 추적

### AI 모델 설정
- **메인 모델**: 주요 작업 처리용
- **리서치 모델**: 연구 및 분석용 (옵션, 권장사항)
- **폴백 모델**: 메인이나 리서치 모델 실패 시 백업용

## 설치 및 설정

### MCP를 통한 설치 (권장)

**NPM 설치:**
```bash
# 전역 설치
npm install -g task-master-ai

# 또는 프로젝트 로컬 설치
npm install task-master-ai
```

**프로젝트 초기화:**
```bash
# 전역 설치인 경우
task-master init

# 로컬 설치인 경우
npx task-master init
```

### MCP 서버 구성

#### Cursor 설정
Cursor 설정 (Ctrl+Shift+J) → MCP 탭 → task-master-ai 활성화

**MCP 서버 구성 파일 (~/.cursor/mcp.json):**
```json
{
  "mcpServers": {
    "task-master-ai": {
      "command": "npx",
      "args": ["-y", "--package=task-master-ai", "task-master-ai"],
      "env": {
        "ANTHROPIC_API_KEY": "YOUR_ANTHROPIC_API_KEY_HERE",
        "PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
        "OPENAI_API_KEY": "YOUR_OPENAI_KEY_HERE",
        "GOOGLE_API_KEY": "YOUR_GOOGLE_KEY_HERE",
        "MISTRAL_API_KEY": "YOUR_MISTRAL_KEY_HERE",
        "GROQ_API_KEY": "YOUR_GROQ_KEY_HERE",
        "OPENROUTER_API_KEY": "YOUR_OPENROUTER_KEY_HERE",
        "XAI_API_KEY": "YOUR_XAI_KEY_HERE",
        "AZURE_OPENAI_API_KEY": "YOUR_AZURE_KEY_HERE",
        "OLLAMA_API_KEY": "YOUR_OLLAMA_API_KEY_HERE"
      }
    }
  }
}
```

#### Windsurf 설정
Windsurf에서 작은 망치 아이콘 → Configure 클릭하여 MCP 서버 설정

#### Claude Desktop 설정
```json
{
  "servers": {
    "task-master-ai": {
      "command": "npx",
      "args": ["-y", "--package=task-master-ai", "task-master-ai"],
      "env": {
        "ANTHROPIC_API_KEY": "YOUR_ANTHROPIC_API_KEY_HERE",
        "PERPLEXITY_API_KEY": "YOUR_PERPLEXITY_API_KEY_HERE",
        "OPENAI_API_KEY": "YOUR_OPENAI_KEY_HERE"
      },
      "type": "stdio"
    }
  }
}
```

### API 키 요구사항
**필수:** 최소 하나의 API 키 필요 (Claude Code 사용 시 제외)
**권장:** 모든 API 키 추가로 모델 제공업체 간 자유로운 전환 가능

- Anthropic API Key (Claude 3.7 사용 시)
- Perplexity API Key (연구 기능용, 강력히 권장)
- OpenAI API Key
- 기타 제공업체 키 (선택사항)

## 프로젝트 구조

### 새 프로젝트 구조
```
.taskmaster/
├── docs/
│   └── prd.txt          # Product Requirements Document
├── templates/
│   └── example_prd.txt  # PRD 템플릿 예시
└── config/              # 설정 파일들
```

### 기존 프로젝트 (레거시)
```
scripts/
└── prd.txt             # PRD 파일 위치
```

## 사용 워크플로우

### 1. PRD 작성
**새 프로젝트:** `.taskmaster/docs/prd.txt`에 PRD 생성
**기존 프로젝트:** `scripts/prd.txt` 사용 또는 `task-master migrate`로 마이그레이션

**PRD 작성 팁:**
- 10-15분 투자하여 최대한 상세하게 작성
- 앱의 기능, 요구사항, 제약사항 명확히 기술
- 더 상세한 PRD일수록 더 정확한 작업 생성

### 2. Task Master 초기화
```
Can you please initialize taskmaster-ai for this project?
```

AI가 다음을 수행합니다:
- 필요한 프로젝트 구조 생성
- 초기 설정 파일 구성
- 나머지 과정 가이드

### 3. PRD 파싱 및 작업 생성
```
I've initialized a new project with Claude Task Master. I have a PRD at .taskmaster/docs/prd.txt. Can you parse it and set up initial tasks?
```

결과:
- PRD가 일련의 작업 파일들(`/tasks` 하위)로 변환
- `/tasks/tasks.json` 파일에 구조화된 작업, 하위 작업, 메타데이터 목록 생성

### 4. 복잡성 분석
```
Can you analyze the complexity of our tasks to help me understand which ones need to be broken down further?
```

Perplexity를 사용하여 웹 연구 수행 후 1-10점 복잡성 점수 결정

### 5. 작업 분해
```
Please break down the identified tasks into subtasks.
```

복잡한 작업을 관리 가능한 단위로 분해

### 6. 작업 실행
각 작업을 새로운 채팅에서 시작 (컨텍스트 오버로드 방지):
```
Please implement task [number/name]
```

## CLI 명령어

### 기본 명령어
```bash
# PRD 파싱 및 작업 생성
task-master parse-prd prd.txt

# 작업 목록 표시
task-master list

# 다음 작업 표시
task-master next

# 작업 파일 생성
task-master generate

# 작업 복잡성 분석
task-master analyze-complexity

# 작업 분해
task-master breakdown-tasks
```

### 작업 이동 (병합 충돌 해결)
```bash
# 단일 작업 이동
task-master move --from=10 --to=16

# 다중 작업 이동
task-master move --from=10,11,12 --to=16,17,18
```

## Cursor 통합

### 자동 통합 (MCP 설정 시)
자연어로 Task Master와 상호작용:
```
What tasks are available to work on next?
Can you analyze the complexity of our tasks?
I'd like to implement task 4. What does it involve?
```

### 수동 통합 (MCP 미사용 시)
- `.cursor/rules/dev_workflow.mdc` 파일이 자동으로 로드됨
- PRD 문서를 `.taskmaster/docs/` 디렉터리에 배치
- Cursor AI 채팅에서 작업 관리 명령 직접 사용

## 실용적 사용 팁

### 효과적 사용법
- **상세한 PRD로 시작**: PRD가 더 상세할수록 생성되는 작업의 품질 향상
- **새로운 채팅으로 각 작업 시작**: 컨텍스트 오버로드 방지
- **작업별 체계적 접근**: 단계별 구현으로 품질 보장
- **버그를 작업으로 처리**: "고쳐줘" 대신 구체적인 버그 설명과 함께 새 작업 생성

### 생산성 극대화
- **연속 모드**: 일련의 작업을 자동으로 처리 (신중히 사용)
- **작업 분해**: 복잡한 작업은 항상 더 작은 단위로 분해
- **Git 관리**: `/tasks` 폴더를 Git에 추가하여 AI 실수에 대비

## 고급 기능

### 연구 기반 작업 생성
```
Research fresh information: Research the latest best practices for implementing JWT authentication with Node.js
```

### 컨텍스트 기반 연구
```
Research with context: Research React Query v5 migration strategies for our current API implementation in src/api.js
```

### 팀 협업
- 작업 ID 충돌 시 `move` 명령으로 해결
- JSON 파일 수동 병합 대신 체계적인 작업 재배치

## 문제 해결

### 일반적 문제들
- **MCP 설정에서 0개 도구 표시**: `args`에서 `--package=task-master-ai` 플래그 제거 시도
- **API 키 오류**: 환경 변수나 MCP 설정에서 올바른 키 확인
- **작업 생성 실패**: PRD 파일 경로와 내용 확인

### 최적화 팁
- **모델 선택**: Claude 3.7 Sonnet을 메인 모델로 권장
- **API 한도 관리**: 복잡한 프로젝트에서는 API 사용량 모니터링
- **컨텍스트 관리**: 긴 대화 시 새 채팅 세션으로 전환

## 버전 정보

- **최신 버전**: 0.23.0 (지속적으로 업데이트)
- **주요 개선사항**: Task Master 2.0에서 프로젝트 구조 개선, MCP 통합 강화

## 라이선스

MIT License

---

Task Master AI는 AI 기반 개발 워크플로우의 구조화와 체계화에 매우 유용한 도구로, 특히 "vibe coding" 접근 방식(자연어로 요구사항을 설명하고 AI가 구현 세부사항을 처리)을 선호하는 개발자들에게 최적화되어 있습니다.