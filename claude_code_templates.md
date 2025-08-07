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
- ✨ **Black 자동 포매팅** - Pyt