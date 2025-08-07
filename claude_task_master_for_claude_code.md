# Claude Task Master - Claude Code 활용 가이드

## 개요

Claude Task Master는 AI 기반 개발을 위한 작업 관리 시스템으로, Claude Code와 완벽하게 통합되어 구조화된 개발 워크플로우를 제공합니다. Claude Code CLI를 통해 API 키 없이도 사용할 수 있으며, PRD(Product Requirements Document)를 실행 가능한 작업으로 자동 분해하여 체계적인 개발을 가능하게 합니다.

## Claude Code와의 통합 장점

### **API 키 불필요**
- Claude Code CLI를 통해 로컬 Claude 인스턴스 활용
- 별도의 API 비용 없이 Task Master 기능 사용
- `claude-code/opus` 및 `claude-code/sonnet` 모델 지원

### **원활한 워크플로우**
- Claude Code의 네이티브 도구와 완벽 통합
- 터미널에서 직접 작업 관리
- 컨텍스트 손실 없는 작업 추적

## 설치 및 설정

### **전제 조건**
```bash
# Claude Code CLI가 설치되어 있어야 함
# 설치 확인
claude --version
```

### **Task Master 설치**
```bash
# 전역 설치 (권장)
npm install -g task-master-ai

# 또는 프로젝트별 설치
npm install task-master-ai
```

### **MCP 서버로 설정**
Claude Code에서 MCP 서버로 Task Master를 추가:

```bash
# MCP 서버 추가
claude mcp add-json "task-master-ai" '{
  "command": "npx",
  "args": ["-y", "--package=task-master-ai", "task-master-ai"],
  "env": {
    "CLAUDE_CODE_ENABLED": "true"
  }
}'
```

### **모델 설정**
`.taskmaster/config.json`에서 Claude Code 모델 구성:

```json
{
  "models": {
    "main": {
      "provider": "claude-code",
      "modelId": "sonnet",
      "maxTokens": 64000,
      "temperature": 0.2
    },
    "research": {
      "provider": "claude-code", 
      "modelId": "opus",
      "maxTokens": 32000,
      "temperature": 0.1
    },
    "fallback": {
      "provider": "claude-code",
      "modelId": "sonnet",
      "maxTokens": 64000,
      "temperature": 0.2
    }
  }
}
```

## 프로젝트 초기화

### **새 프로젝트 시작**
```bash
# 프로젝트 초기화
task-master init

# 또는 특정 규칙으로 초기화
task-master init --rules cursor,windsurf,vscode
```

### **프로젝트 구조**
```
.taskmaster/
├── docs/
│   ├── prd.txt              # Product Requirements Document
│   └── specifications/      # 추가 사양 문서
├── templates/
│   └── example_prd.txt      # PRD 템플릿
├── config.json              # Task Master 설정
└── rules/
    └── dev_workflow.mdc     # 개발 워크플로우 규칙
```

## Claude Code에서 사용하기

### **1. PRD 작성 및 파싱**

**PRD 작성:**
`.taskmaster/docs/prd.txt`에 상세한 요구사항 작성

**Claude Code에서 파싱:**
```
Initialize taskmaster-ai in my project and parse the PRD at .taskmaster/docs/prd.txt
```

**또는 직접 명령:**
```bash
task-master parse-prd .taskmaster/docs/prd.txt
```

### **2. 작업 조회 및 관리**

**다음 작업 확인:**
```
What's the next task I should work on?
```

**특정 작업 조회:**
```
Can you show me details for task 3?
```

**여러 작업 동시 조회:**
```
Can you show me tasks 1, 3, and 5?
```

### **3. 작업 실행**

**단일 작업 실행:**
```
Can you help me implement task 4?
```

**연구 기반 작업:**
```
Before implementing task 5 (authentication), research the latest JWT security recommendations.
```

**컨텍스트 기반 연구:**
```
Research React Query v5 migration strategies for our current API implementation in src/api.js
```

### **4. 작업 분해 및 확장**

**복잡한 작업 분해:**
```
Task 5 seems complex. Can you break it down into subtasks?
```

**보안 중심 분해:**
```
Please break down task 5 with a focus on security considerations.
```

**모든 작업 분해:**
```
Please break down all pending tasks into subtasks.
```

## CLI 명령어 참조

### **핵심 명령어**
```bash
# 프로젝트 초기화
task-master init

# PRD 파싱 및 작업 생성
task-master parse-prd <prd-file>

# 작업 목록 보기
task-master list

# 다음 작업 확인
task-master next

# 특정 작업 상세 보기
task-master show <task-id>

# 작업 파일 생성
task-master generate
```

### **고급 명령어**
```bash
# 프로젝트 복잡성 분석
task-master analyze-complexity

# 연구 수행
task-master research "JWT authentication best practices"

# 작업 상태 변경
task-master set-status --id=task-001 --status=in-progress

# 작업 이동 (병합 충돌 해결)
task-master move --from=10 --to=16
```

## Claude Code 최적 활용 패턴

### **1. 서브에이전트 활용**
Claude Code의 Task 도구를 활용하여 복잡한 문제를 여러 관점에서 분석:

```
Use the Task tool to create a sub-agent that will analyze our authentication implementation from a security perspective while I continue with the main development.
```

### **2. 병렬 개발**
여러 Claude Code 인스턴스를 활용한 병렬 작업:

- 하나는 프론트엔드 구현
- 다른 하나는 백엔드 API 개발
- 세 번째는 테스트 작성

### **3. 단계별 구현**
```
Please implement task 3 step by step:
1. First, create the basic structure
2. Then implement core functionality  
3. Add error handling
4. Write tests
5. Update documentation
```

### **4. 커스텀 슬래시 명령어**
`.claude/commands/` 디렉터리에 재사용 가능한 명령어 생성:

**예: `implement-task.md`**
```markdown
Please implement the task: $ARGUMENTS

Follow these steps:
1. Review the task requirements from .taskmaster/
2. Check dependencies and prerequisites
3. Implement the solution with proper error handling
4. Write comprehensive tests
5. Update relevant documentation
6. Commit changes with descriptive message

Ensure code follows our project standards defined in .taskmaster/rules/
```

## 고급 설정 및 최적화

### **Claude Code 특화 설정**
`.taskmaster/config.json`에서 Claude Code 전용 설정:

```json
{
  "claudeCode": {
    "maxTurns": 50,
    "permissionMode": "ask",
    "allowedTools": ["bash", "editor", "browser"],
    "customSystemPrompt": "You are working with Task Master. Always check task context before implementing."
  },
  "commandSpecific": {
    "parse-prd": {
      "temperature": 0.1,
      "maxTokens": 32000
    },
    "implement": {
      "temperature": 0.2,
      "maxTokens": 64000
    }
  }
}
```

### **워크플로우 자동화**
```bash
# Git pre-commit 훅에 Task Master 검증 추가
echo '#!/bin/bash
task-master validate-current-task
' > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

### **팀 협업 설정**
```bash
# 공유 가능한 커스텀 명령어 추가
mkdir -p .claude/commands
cat > .claude/commands/review-task.md << 'EOF'
Please review the implementation of task $ARGUMENTS:

1. Check if requirements are met
2. Verify code quality and standards
3. Ensure proper testing coverage
4. Validate documentation updates
5. Suggest improvements if needed

Reference the original task definition in .taskmaster/
EOF
```

## 문제 해결

### **일반적인 문제들**

**Claude Code CLI 인식 오류:**
```bash
# Claude Code 경로 확인
which claude
export PATH="$PATH:/path/to/claude"
```

**Task Master 도구 인식 실패:**
```bash
# MCP 서버 재시작
claude mcp restart task-master-ai
```

**컨텍스트 오버플로우:**
- 새로운 Claude Code 세션 시작
- `/clear` 명령으로 컨텍스트 정리
- 작업을 더 작은 단위로 분해

### **성능 최적화**

**메모리 효율적 사용:**
```bash
# 대형 프로젝트에서 특정 작업만 로드
task-master show --minimal <task-id>
```

**빠른 작업 전환:**
```bash
# 작업 컨텍스트 빠른 전환
task-master context switch <task-id>
```

## 실제 사용 예시

### **웹 스크래퍼 프로젝트 예시**
```bash
# 1. 프로젝트 초기화
task-master init --name="firecrawl-scraper"

# 2. PRD 작성 후 파싱
# Claude Code에서:
"I need to build a web scraper using Firecrawl SDK with authentication, proxy rotation, and data pipeline. Please parse my PRD and create implementation tasks."

# 3. 단계별 구현
"Let's start with task 1: Authentication module. Please implement with proper error handling and retry logic."

# 4. 종속성 확인 후 다음 작업
"Check dependencies for task 2 and implement the proxy rotation system."
```

### **마이크로서비스 개발 예시**
```bash
# 병렬 개발을 위한 여러 Claude Code 인스턴스
# 인스턴스 1: API 개발
"Implement the user authentication API from task 3"

# 인스턴스 2: 프론트엔드
"Create the login form component from task 5" 

# 인스턴스 3: 테스트
"Write comprehensive tests for the authentication flow"
```

## 모범 사례

### **효과적인 PRD 작성**
- 기술적 요구사항과 비즈니스 로직을 명확히 분리
- 각 기능의 우선순위와 종속성 명시
- 예상 제약사항과 엣지 케이스 포함
- 성능 요구사항과 보안 고려사항 기술

### **작업 관리 전략**
- 복잡한 작업은 항상 하위 작업으로 분해
- 각 작업에 명확한 완료 조건 설정
- 정기적으로 `task-master generate`로 컨텍스트 새로고침
- Git 커밋과 작업 완료를 연동

### **Claude Code 활용 팁**
- `--dangerously-skip-permissions` 플래그로 개발 속도 향상 (개발 환경에서만)
- 복잡한 작업은 Plan Mode (Shift+Tab) 활용
- 정기적으로 `/clear` 명령으로 컨텍스트 정리
- 서브에이전트를 활용한 병렬 분석 및 구현

## 라이선스 및 제한사항

### **라이선스**
- MIT License with Commons Clause
- 개인, 상업, 학술 목적 사용 가능
- Task Master 기반 제품 개발 및 판매 가능

### **제한사항**
- Task Master 자체 판매 불가
- 호스티드 서비스로 제공 불가
- Task Master 기반 경쟁 제품 생성 불가

---

Claude Task Master와 Claude Code의 조합은 AI 기반 개발에서 가장 효율적인 워크플로우 중 하나를 제공합니다. 구조화된 작업 관리와 강력한 AI 에이전트의 결합으로 복잡한 프로젝트도 체계적이고 예측 가능한 방식으로 완성할 수 있습니다.