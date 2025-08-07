# awesome-claude
- 유용한 claude, claude code 에서 사용가능한 강력한 유용한 도구들
---
## Claude Code 관련
### Claude 기본 사용법
[상세 설명 문서](claude_code_guide.md)  

### claude code templates
[상세 설명 문서](claude_code_templates.md)  
https://github.com/davila7/claude-code-templates  
개요 : 다양한 프로그래밍 언어와 프레임워크에 최적화된 Claude Code 설정을 자동으로 생성해주는 CLI 도구  

### supeclaude framework
[상세 설명 문서](superclaude_guide.md)  
https://github.com/SuperClaude-Org/SuperClaude_Framework  
개요 : Claude Code를 확장하여 개발 작업을 더 효율적으로 만들어주는 도구  

---
## Claude에서 사용하면 유용한 MCP 
### github MCP Server
https://github.com/SuperClaude-Org/SuperClaude_Framework  
기능 : GitHub API와 직접 연동하여 이슈, PR, 커밋 관리  
사용 예시:  
  * "authentication 관련 이슈들을 찾아줘"
  * "새로운 PR 생성하고 CI/CD 트리거"
  * "커밋 히스토리 분석해줘"
    
### Filesystem MCP Server
https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem  
기능 : 안전한 파일 시스템 조작 및 프로젝트 관리  
사용 예시:  
  * 프로젝트 파일 읽기/쓰기/편집
  * 로그 파일 분석
  * 빠른 코드 수정
### PostgreSQL MCP Server
https://github.com/modelcontextprotocol/servers/tree/main/src/postgres  
https://github.com/HenkDz/postgresql-mcp-server  
기능: 데이터베이스 스키마 검사 및 쿼리 실행  
사용 예시:  
  * 데이터베이스 스키마 탐색
  * 성능 분석 및 느린 쿼리 찾기
  * 인덱스 최적화 제안

### Apidog MCP Server
https://apidog.com/blog/top-10-mcp-servers-for-claude-code/  
기능: API 문서화, 테스팅, 클라이언트 코드 생성  
사용 예시:  
  * API 스펙 쿼리 및 엔드포인트 테스트
  * 클라이언트 코드 자동 생성
    
### Sequential Thinking MCP Server
https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking  
기능: 복잡한 작업을 논리적 단계로 분해  
사용 예시:  
  * 아키텍처 설계 단계별 분석
  * 리팩토링 계획 수립
  * 프로젝트 계획 수립
    
### Memory MCP Server
https://github.com/modelcontextprotocol/servers/tree/main/src/memory  
기능: 지식 그래프 기반 영구 메모리 시스템  
사용 예시:  
  * 프로젝트 히스토리 및 컨텍스트 저장
  * 개발 패턴 및 결정사항 기록
    
### Docker MCP Server
https://github.com/docker/mcp-servers  
기능: Docker 컨테이너 및 Compose 관리  
사용 예시:  
  * 컨테이너 상태 모니터링
  * Docker Compose 서비스 관리
  * 로그 분석

### Puppeteer MCP Server
https://github.com/modelcontextprotocol/servers/tree/main/src/puppeteer  
기능: 웹 자동화 및 스크래핑  
사용 예시:  
  * 웹 페이지 자동 테스트
  * 스크린샷 및 PDF 생성
  * 폼 자동화

### Slack MCP Server
https://github.com/modelcontextprotocol/servers/tree/main/src/slack  
기능: Slack 워크스페이스 통합  
사용 예시:  
  * "새로운 PR이 열리면 Slack 메시지 전송"
  * 팀 커뮤니케이션 자동화

### Zapier MCP Server
https://github.com/Paragon-AI/zapier-mcp-server  
기능: 130+ SaaS 앱과의 통합 자동화  
사용 예시:  
  * 크로스 앱 워크플로 자동화
  * Gmail, Salesforce, Notion 등 연동

### MYSQL MCP
https://github.com/executeautomation/mcp-database-server  
  
### Linear MCP
프로젝트 관리& 협업 도구. 이슈 및 프로젝트 상태 실시간 컨텍스트  
https://linear.app/mcp   






