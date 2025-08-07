# SuperClaude Framework 사용방법 가이드

SuperClaude Framework는 Claude Code를 확장하여 개발 작업을 더 효율적으로 만들어주는 도구입니다. 다음은 설치부터 활용까지의 종합 가이드입니다.

## 🚀 설치 방법

### 1단계: Python 패키지 설치

**권장 방법 (PyPI):**
```bash
uv add SuperClaude
```

**대안 (소스에서 설치):**
```bash
git clone https://github.com/NomenAK/SuperClaude.git
cd SuperClaude
uv sync
```

**uv 패키지 매니저 설치:**
```bash
curl -Ls https://astral.sh/uv/install.sh | sh
```

### 2단계: SuperClaude 설치 및 설정

**빠른 설정 (권장):**
```bash
python3 -m SuperClaude install
```

**설치 옵션들:**
- `--interactive`: 구성요소를 선택적으로 설치
- `--minimal`: 핵심 프레임워크만 설치
- `--profile developer`: 모든 기능 포함 설치
- `--help`: 모든 옵션 보기

## 🛠️ 주요 기능

### 1. 16가지 전문 명령어

**개발 관련:**
- `/sc:implement` - 기능 구현
- `/sc:build` - 컴파일/패키징
- `/sc:design` - 설계 작업

**분석 관련:**
- `/sc:analyze` - 코드/시스템 분석
- `/sc:troubleshoot` - 문제 해결
- `/sc:explain` - 코드 설명

**품질 관리:**
- `/sc:improve` - 코드 개선
- `/sc:test` - 테스트 작성
- `/sc:cleanup` - 코드 정리

**기타:**
- `/sc:document` - 문서 작성
- `/sc:git` - Git 관련 작업
- `/sc:estimate` - 작업 추정
- `/sc:task` - 작업 관리
- `/sc:index` - 인덱싱
- `/sc:load` - 로딩
- `/sc:spawn` - 새 인스턴스 생성

### 2. AI 전문가 페르소나

시스템이 자동으로 적절한 전문가를 선택합니다:
- 🏗️ **architect** - 시스템 설계 및 아키텍처
- 🎨 **frontend** - UI/UX 및 접근성
- ⚙️ **backend** - API 및 인프라
- 🔍 **analyzer** - 디버깅 및 문제 분석
- 🛡️ **security** - 보안 관련 작업
- ✍️ **scribe** - 문서화 및 작성
- 그 외 5개 추가 전문가

### 3. MCP 서버 통합

- **Context7** - 공식 라이브러리 문서 및 패턴 제공
- **Sequential** - 복잡한 다단계 사고 지원
- **Magic** - 현대적인 UI 컴포넌트 생성
- **Playwright** - 브라우저 자동화 및 테스트

## 📁 파일 구조

설치 후 다음 위치에 파일들이 생성됩니다:
- `~/.claude/settings.json` - 메인 설정 파일
- `~/.claude/*.md` - 프레임워크 동작 파일들

## 🔧 설정 및 커스터마이징

대부분의 사용자는 기본 설정으로 충분하지만, 필요시 다음 파일들을 수정할 수 있습니다:
- `~/.claude/settings.json` - 메인 설정
- `~/.claude/*.md` - 프레임워크 동작 문서

## 📚 추가 학습 자료

프로젝트 문서에서 더 자세한 가이드를 확인할 수 있습니다:
- **User Guide** - 완전한 개요 및 시작 가이드
- **Commands Guide** - 16개 슬래시 명령어 상세 설명
- **Flags Guide** - 명령어 플래그 및 옵션
- **Personas Guide** - 페르소나 시스템 이해
- **Installation Guide** - 자세한 설치 지침

## ⚠️ 주의사항

- 이는 초기 릴리스로 버그가 있을 수 있습니다
- v2에서 업그레이드하는 경우 기존 파일들을 먼저 정리해야 합니다
- `/build` 명령어가 `/sc:build` (컴파일/패키징)와 `/sc:implement` (기능 구현)으로 분리되었습니다

## 📋 마이그레이션 가이드 (v2 → v3)

v2에서 v3으로 업그레이드하는 경우:

1. **v2 언인스톨 (가능한 경우)**
2. **수동 정리 - 다음 파일/폴더들을 삭제:**
   - `SuperClaude/`
   - `~/.claude/shared/`
   - `~/.claude/commands/`
   - `~/.claude/CLAUDE.md`
3. **v3 설치 진행**

## 🛡️ 시스템 요구사항

- Python 3.7 이상
- Claude Code 설치 필요
- 운영체제: Linux, macOS, Windows 지원

## 📖 결론

이 도구는 개발 워크플로우를 더 효율적으로 만들어주는 것을 목표로 하며, Claude Code와 함께 사용하여 더 전문적이고 컨텍스트에 맞는 개발 지원을 받을 수 있습니다.

---
*작성일: 2025년 8월*  
*출처: https://github.com/SuperClaude-Org/SuperClaude_Framework*