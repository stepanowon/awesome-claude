# Shrimp Task Manager 사용 가이드

## 개요

Shrimp Task Manager는 AI 에이전트를 위해 구축된 작업 도구로, chain-of-thought(연쇄 사고), reflection(반성), 스타일 일관성을 강조합니다. 자연어를 종속성 추적과 반복적 개선이 포함된 구조화된 개발 작업으로 변환하여 추론 AI 시스템에서 에이전트와 같은 개발자 행동을 가능하게 합니다.

## 주요 특징

### 핵심 기능들
- **작업 계획 및 분석**: 복잡한 작업 요구사항의 깊은 이해 및 분석
- **지능형 작업 분해**: 큰 작업을 관리 가능한 작은 작업으로 자동 분해
- **의존성 관리**: 작업 간 의존성을 정확히 처리하여 올바른 실행 순서 보장
- **실행 상태 추적**: 작업 실행 진행 상황 및 상태 실시간 모니터링
- **작업 완성도 검증**: 작업 결과가 예상 요구사항을 만족하는지 확인
- **작업 복잡성 평가**: 작업 복잡성을 자동으로 평가하고 최적 처리 제안 제공

### 고급 기능들
- **자동 작업 요약 업데이트**: 작업 완료 시 자동으로 요약 생성하여 메모리 성능 최적화
- **작업 메모리 기능**: 작업 히스토리를 자동으로 백업하여 장기 메모리 및 참조 기능 제공
- **연구 모드**: 체계적인 기술 연구 기능으로 기술, 모범 사례, 솔루션 비교 탐색을 위한 가이드 워크플로우
- **프로젝트 규칙 초기화**: 프로젝트 표준 및 규칙을 정의하여 대규모 프로젝트에서 일관성 유지
- **Web GUI**: 작업 관리를 위한 선택적 웹 기반 그래픽 사용자 인터페이스

## 설치 및 설정

### 자동 설치 (Smithery를 통한 권장 방법)
```bash
npx -y @smithery/cli install @cjo4m06/mcp-shrimp-task-manager --client claude
```

### 수동 설치
```bash
# 의존성 설치
npm install

# 빌드 및 서비스 시작
npm run build
```

## 구성 설정

### Cursor IDE 전역 구성
`~/.cursor/mcp.json` 파일을 열고 다음 구성을 추가합니다:

**절대 경로 모드 (프로젝트 격리):**
```json
{
  "mcpServers": {
    "shrimp-task-manager": {
      "command": "npx",
      "args": ["-y", "mcp-shrimp-task-manager"],
      "env": {
        "DATA_DIR": "/Users/username/ShrimpData",
        "TEMPLATES_USE": "en",
        "ENABLE_GUI": "false"
      }
    }
  }
}
```

### 프로젝트별 구성
프로젝트 루트에 `.cursor/mcp.json` 파일을 생성:

**상대 경로 모드 (프로젝트 포함):**
```json
{
  "mcpServers": {
    "shrimp-task-manager": {
      "command": "npx",
      "args": ["-y", "mcp-shrimp-task-manager"],
      "env": {
        "DATA_DIR": ".shrimp",
        "TEMPLATES_USE": "en",
        "ENABLE_GUI": "false"
      }
    }
  }
}
```

## 사용 워크플로우

### 1. 연구 모드 활용
새로운 기술이나 프레임워크를 탐색할 때:
- `"research [your topic]"`
- `"enter research mode for [technology/problem]"`
- `"Research and compare [options A vs B]"`

### 2. 프로젝트 규칙 초기화
새 프로젝트에서 작업할 때:
- `"init project rules"`
- `"init rules"`

### 3. 작업 계획
기능을 개발하거나 업데이트할 때:
- `"plan task [your description]"`

### 4. 작업 실행
계획된 작업을 구현할 때:
- `"execute task [task name or ID]"`
- 작업명이나 ID를 지정하지 않으면 자동으로 최우선순위 작업 실행

### 5. 연속 모드
모든 작업을 순차적으로 처리하려면:
- `"continuous mode"`

## 고급 기능 활용

### 연구 모드
연구 모드는 체계적인 기술 조사 및 지식 수집을 위해 설계된 특화 기능입니다. 구조화된 워크플로우를 제공하여 기술 탐색, 솔루션 비교, 모범 사례 조사, 프로그래밍 작업을 위한 포괄적인 정보 수집을 지원합니다.

**연구 모드 활용 시기:**
- 새로운 기술이나 프레임워크 조사
- 서로 다른 기술적 접근 방식이나 아키텍처 평가
- 복잡한 기술적 과제에 대한 심층 조사
- 아키텍처 계획 및 디자인 패턴 연구

### 작업 메모리 기능
시스템은 작업 실행 히스토리를 메모리 디렉터리에 자동으로 백업하며, 백업 파일은 시간순으로 명명됩니다(`tasks_backup_YYYY-MM-DDThh-mm-ss.json` 형식). 작업 계획 에이전트는 메모리 기능 사용 방법에 대한 가이드를 자동으로 받습니다.

**장점:**
- **중복 작업 방지**: 과거 작업을 참조하여 유사한 문제를 처음부터 해결할 필요가 없음
- **성공 경험 학습**: 검증된 효과적인 솔루션을 활용하여 개발 효율성 향상
- **지식 축적**: 시스템 사용량이 증가함에 따라 지속적으로 확장되는 지식베이스 형성

## 환경 변수 설정

### 주요 환경 변수
- `DATA_DIR`: 작업 데이터 저장 디렉터리
- `TEMPLATES_USE`: 프롬프트용 템플릿 세트 지정 (기본값: "en", "zh" 지원)
- `ENABLE_GUI`: 웹 기반 GUI 활성화/비활성화
- `WEB_PORT`: 웹 GUI용 포트 지정 (지정하지 않으면 자동 선택)

### 프롬프트 커스터마이징
```json
{
  "env": {
    "MCP_PROMPT_PLAN_TASK": "Custom planning guidance...",
    "MCP_PROMPT_EXECUTE_TASK_APPEND": "Additional execution instructions...",
    "TEMPLATES_USE": "en"
  }
}
```

## Cursor Custom Modes 설정

### TaskPlanner 모드
```
You are a professional task planning expert. You must interact with users, analyze their needs, and collect project-related information. Finally, you must use "plan_task" to create tasks. When the task is created, you must summarize it and inform the user to use the "TaskExecutor" mode to execute the task.

You must focus on task planning. Do not use "execute_task" to execute tasks.
```

### TaskExecutor 모드
```
You are a professional task execution expert. When a user specifies a task to execute, use "execute_task" to execute the task.

If no task is specified, use "list_tasks" to find unexecuted tasks and execute them.

You can only perform one task at a time, and when a task is completed, you are prohibited from performing the next task unless the user explicitly tells you to.

If the user requests "continuous mode", all tasks will be executed in sequence.
```

## 주요 도구 개요

| 카테고리 | 도구명 | 설명 |
|---------|--------|------|
| 작업 계획 | `plan_task` | 작업 계획 시작 |
| 작업 분석 | `analyze_task` | 작업 요구사항 심층 분석 |
| | `process_thought` | 복잡한 문제에 대한 단계별 추론 |
| 솔루션 평가 | `reflect_task` | 솔루션 개념 반영 및 개선 |
| 연구 및 조사 | `research_mode` | 체계적인 기술 연구 모드 진입 |
| 프로젝트 관리 | `init_project_rules` | 프로젝트 표준 및 규칙 초기화 |
| 작업 관리 | `split_tasks` | 작업을 하위 작업으로 분해 |
| | `list_tasks` | 모든 작업 및 상태 표시 |
| | `query_task` | 작업 검색 및 나열 |
| | `get_task_detail` | 완전한 작업 세부사항 표시 |
| | `delete_task` | 미완료 작업 삭제 |
| 작업 실행 | `execute_task` | 특정 작업 실행 |
| | `verify_task` | 작업 완료 검증 |

## 데이터 디렉터리 설정

### ListRoots 프로토콜 지원 클라이언트 (예: Cursor IDE)

**절대 경로 모드 (프로젝트 격리):**
- 구성: `"DATA_DIR": "/Users/username/ShrimpData"`
- 동작: `{DATA_DIR}/{project-name}/` 자동 생성
- 예시: "my-app" 프로젝트 → `/Users/username/ShrimpData/my-app/`
- 장점: 완벽한 격리로 모든 프로젝트에 하나의 전역 구성 사용

**상대 경로 모드 (프로젝트 포함):**
- 구성: `"DATA_DIR": ".shrimp"` 또는 `"DATA_DIR": "shrimp-data"`
- 동작: 프로젝트 내에 `{project-root}/{DATA_DIR}/` 생성
- 예시: DATA_DIR "shrimp-data" → `./shrimp-data/`
- 장점: 데이터가 프로젝트와 함께 유지, 버전 관리에서 쉬운 포함/제외

### ListRoots 미지원 클라이언트
- 절대 경로 사용을 강력히 권장 (경로 해석 문제 방지)
- 상대 경로 사용 시 환경에 따른 불일치 발생 가능

## 권장 모델

최상의 경험을 위해 다음 모델을 권장합니다:
- **Claude 3.7**: 강력한 이해 및 생성 능력 제공
- **Gemini 2.5**: Google의 최신 모델로 탁월한 성능

## 기술 스택

- **Node.js**: 고성능 JavaScript 런타임 환경
- **TypeScript**: 타입 안전 개발 환경 제공
- **MCP SDK**: 대규모 언어 모델과의 원활한 상호작용을 위한 인터페이스
- **UUID**: 고유하고 신뢰할 수 있는 작업 식별자 생성

## 라이선스

이 프로젝트는 MIT 라이선스 하에 라이선스가 부여됩니다.

---

Shrimp Task Manager는 AI 에이전트와의 체계적이고 효율적인 협업을 위한 포괄적인 작업 관리 시스템으로, 특히 복잡한 개발 프로젝트에서 일관성 있고 체계적인 워크플로우를 제공합니다.