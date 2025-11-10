# ❓ 자주 묻는 질문 (FAQ)

## 목차

- [기본 사용](#기본-사용)
- [기능 및 제한사항](#기능-및-제한사항)
- [워크플로우](#워크플로우)
- [보안](#보안)
- [성능](#성능)
- [문제 해결](#문제-해결)
- [고급 주제](#고급-주제)

---

## 기본 사용

### Q: Claude Code가 정확히 무엇인가요?

**A:** Claude Code는 Anthropic의 공식 AI 코딩 어시스턴트 CLI입니다. 자연어로 요청하면 코드 작성, 리뷰, 리팩토링, 문서화 등을 자동으로 수행합니다.

```bash
# 터미널에서 실행
claude

# 자연어로 요청
> "이 프로젝트의 인증 시스템을 설명해줘"
```

---

### Q: Claude Code와 ChatGPT/GitHub Copilot의 차이는?

**A:**

| 특징 | Claude Code | GitHub Copilot | ChatGPT |
|------|-------------|----------------|---------|
| **실행 환경** | CLI (터미널) | IDE 플러그인 | 웹 브라우저 |
| **파일 접근** | 직접 읽기/쓰기 ✓ | 제한적 | 없음 |
| **Git 통합** | 자동화 ✓ | 수동 | 없음 |
| **에이전트** | 여러 전문 에이전트 | 없음 | 없음 |
| **워크플로우** | 7단계 자동화 | 없음 | 없음 |
| **플러그인** | 확장 가능 ✓ | 제한적 | 없음 |

**핵심 차이점:**
- Claude Code는 **실제 파일을 직접 수정**합니다
- **Git 작업을 자동화**합니다 (커밋, 푸시, PR)
- **전문 에이전트들이 협업**합니다

---

### Q: 무료인가요?

**A:** Claude Code는 Anthropic API를 사용하므로 API 요금이 발생합니다. 회사 계정을 사용하는 경우 팀 리더에게 문의하세요.

---

### Q: 어떤 프로그래밍 언어를 지원하나요?

**A:** Claude Code는 거의 모든 프로그래밍 언어를 지원합니다:

```
✓ JavaScript/TypeScript
✓ Python
✓ Java
✓ C/C++/C#
✓ Go
✓ Rust
✓ Ruby
✓ PHP
✓ Swift/Kotlin
... 등등
```

언어별 특화 기능은 없지만, 각 언어의 일반적인 패턴과 모범 사례를 이해합니다.

---

## 기능 및 제한사항

### Q: Claude Code가 할 수 있는 것과 할 수 없는 것은?

**A:**

#### ✅ 할 수 있는 것

```
✓ 코드 읽기/쓰기/수정
✓ 파일 생성/삭제
✓ Git 명령어 실행
✓ 터미널 명령어 실행 (npm, python 등)
✓ 웹에서 정보 검색
✓ 복잡한 리팩토링
✓ 테스트 작성 및 실행
✓ PR 생성
✓ 코드 리뷰
```

#### ❌ 할 수 없는 것

```
✗ GUI 애플리케이션 직접 실행
✗ 실시간 디버깅 (브레이크포인트 등)
✗ 바이너리 파일 편집
✗ 네트워크 서버 직접 실행
✗ 사용자 인터페이스 조작
```

---

### Q: 한 번에 얼마나 큰 프로젝트를 처리할 수 있나요?

**A:** Claude Code는 토큰 제한이 있지만, 스마트하게 작동합니다:

```
한계:
- 컨텍스트 윈도우: 200,000 토큰 (약 150,000 단어)
- 한 번에 읽을 수 있는 파일: 제한 없음 (병렬 처리)
- 프로젝트 크기: 제한 없음

전략:
- 전체 프로젝트를 한 번에 읽지 않음
- 필요한 파일만 선택적으로 읽음
- 에이전트가 병렬로 탐색
- 요약 및 압축 기법 사용
```

**실제 예시:**
- 작은 프로젝트 (10-100 파일): 문제없음
- 중간 프로젝트 (100-1000 파일): 문제없음, 탐색 시간 증가
- 대형 프로젝트 (1000+ 파일): 가능하지만, 구체적인 범위 지정 권장

---

### Q: Claude가 실수하면 어떻게 하나요?

**A:** Claude도 완벽하지 않습니다. 다음과 같이 대응하세요:

```
1. Git으로 되돌리기:
   git checkout src/auth/auth.service.ts

2. 구체적으로 수정 요청:
   "auth.service.ts의 login 메서드에서 에러 처리가 잘못됐어.
    try-catch를 사용해서 다시 작성해줘."

3. 단계별로 검토:
   "먼저 계획을 설명해줘. 내가 승인하면 실행해."
```

**예방책:**
- 중요한 작업 전에 커밋하기
- 변경사항을 즉시 검토하기
- 큰 작업은 단계별로 나누기

---

### Q: 보안이 걱정됩니다. 안전한가요?

**A:** Claude Code는 여러 보안 메커니즘을 갖추고 있습니다:

```
✓ PreToolUse Hook: 위험한 패턴 감지
  - Command injection
  - Code injection
  - XSS
  - GitHub Actions injection

✓ allowed-tools: 명령어별 도구 제한

✓ 로컬 실행: 코드가 서버로 전송되지 않음
  (단, API 요청은 Anthropic으로 전송)

⚠️  주의사항:
- .env 파일, 시크릿 등은 .gitignore 처리
- 보안 경고를 무시하지 말 것
- 프로덕션 데이터베이스에서 직접 실행하지 말 것
```

---

## 워크플로우

### Q: /feature-dev는 언제 사용해야 하나요?

**A:**

**사용해야 할 때:**
```
✓ 완전히 새로운 기능 추가
✓ 여러 파일에 걸친 변경
✓ 아키텍처 설계가 필요한 경우
✓ 코드 리뷰가 중요한 경우
```

**사용하지 않아도 될 때:**
```
✗ 간단한 버그 수정
✗ 단일 파일 수정
✗ 문서 작성
✗ 빠른 실험
```

**예시:**
```bash
# 적합: 복잡한 기능
> /feature-dev "사용자 프로필 시스템 구축 (업로드, 수정, 삭제)"

# 부적합: 간단한 수정
> "오타 고쳐줘" (그냥 직접 요청)
```

---

### Q: /feature-dev의 7단계가 너무 길어요. 건너뛸 수 있나요?

**A:** 각 단계는 품질을 보장하기 위해 설계되었지만, 간단한 작업에는 부담스러울 수 있습니다.

```
대안:

1. 일반 요청 사용 (7단계 없음):
   > "다크 모드 토글 버튼을 Header에 추가해줘"

2. 단계 건너뛰기 요청:
   > "/feature-dev를 사용하되, 질문 단계는 건너뛰고 바로 구현해줘"

3. 빠른 모드:
   > "빠르게 구현해줘 (리뷰 건너뛰기)"
```

**권장:**
- 중요한 기능: 전체 7단계 사용
- 실험적 기능: 일반 요청 사용
- 긴급 수정: 일반 요청 사용

---

### Q: /commit-push-pr이 실패하면 어떻게 하나요?

**A:** 일반적인 실패 원인과 해결책:

#### 1. Pre-commit Hook 실패

```
원인: 린트 에러, 타입 에러, 포맷팅 문제

해결:
1. Claude가 자동으로 수정 시도
2. 수정 실패 시:
   > "Pre-commit hook 에러를 수정해줘"
```

#### 2. Push 실패

```
원인: 네트워크 문제, 권한 문제

해결:
1. Claude가 자동으로 재시도 (exponential backoff)
2. 4번 재시도 후 실패 시:
   - SSH 키 확인
   - Git 설정 확인
   - 수동 푸시: git push origin [branch]
```

#### 3. PR 생성 실패

```
원인: gh CLI 미설치, 권한 문제

해결:
1. gh CLI 설치:
   brew install gh  # macOS

2. 인증:
   gh auth login

3. 재시도:
   > "/commit-push-pr 다시 시도해줘"
```

---

## 보안

### Q: 보안 경고가 계속 나타나는데 무시해도 되나요?

**A:** **절대 안 됩니다!**

```
보안 경고가 나타나는 이유:

⚠️  GitHub Actions Injection
   → PR 제목/본문을 직접 스크립트에 사용
   → 공격자가 악의적인 명령어 삽입 가능

⚠️  Command Injection
   → 사용자 입력을 os.system, exec에 전달
   → 시스템 명령어 실행 위험

⚠️  Code Injection
   → eval, new Function 사용
   → 임의 코드 실행 위험
```

**올바른 대응:**
1. 경고 메시지를 읽고 이해하기
2. Claude가 제안하는 안전한 대안 확인
3. 안전한 방법으로 재구현

**세션별 경고:**
- 같은 세션에서는 한 번만 경고
- 새 세션에서는 다시 경고
- 이것은 정상 동작 (경고 피로 방지)

---

### Q: .env 파일을 Claude에게 보여줘도 되나요?

**A:** **주의해야 합니다!**

```
✓ 안전한 경우:
   - 로컬 개발 환경
   - 테스트용 시크릿
   - .env.example (시크릿 없는 템플릿)

⚠️  위험한 경우:
   - 프로덕션 시크릿
   - API 키
   - 데이터베이스 비밀번호
   - 암호화 키
```

**모범 사례:**
```bash
# 1. .env.example 사용
> ".env.example 파일을 보여줘"

# 2. 시크릿은 마스킹
> "DATABASE_URL=postgresql://user:***@localhost:5432/db 형식으로
   .env 파일을 만들어줘"

# 3. 절대 커밋하지 않기
> ".gitignore에 .env가 있는지 확인해줘"
```

---

## 성능

### Q: Claude가 너무 느려요. 왜 그런가요?

**A:** 느려지는 이유와 해결책:

#### 원인 1: 넓은 검색 범위

```
문제:
> "프로젝트 전체에서 TODO를 찾아줘"
→ 수천 개 파일 검색

해결:
> "src/ 디렉토리에서만 TODO를 찾아줘"
```

#### 원인 2: 복잡한 분석

```
문제:
> "/feature-dev 'entire backend rewrite'"
→ 수백 개 파일 분석

해결:
- 작은 단위로 나누기
- 구체적인 범위 지정
```

#### 원인 3: 모델 선택

```
느림: Sonnet (깊은 사고, 정확도 높음)
빠름: Haiku (빠른 실행, 간단한 작업)

요청 시 모델 지정:
> "빠르게 (Haiku 모드로) 파일 목록을 보여줘"
```

#### 원인 4: 네트워크

```
API 호출 지연, 인터넷 연결 문제

확인:
- 인터넷 연결 상태
- Anthropic API 상태
```

---

### Q: 병렬 에이전트가 항상 빠른가요?

**A:** 대부분은 빠르지만, 항상 그런 것은 아닙니다.

**빠른 경우:**
```
✓ 독립적인 탐색 작업
✓ 여러 디렉토리/모듈 분석
✓ 다양한 관점의 리뷰

예시:
3개 에이전트가 동시에 탐색:
- Agent 1: 인증 로직
- Agent 2: 데이터베이스
- Agent 3: API 엔드포인트

순차: 30초
병렬: 10초 (3배 빠름!)
```

**느린 경우:**
```
✗ 순차적 의존성 (A → B → C)
✗ 공유 리소스 경쟁
✗ 너무 많은 에이전트 (오버헤드)

예시:
5개 에이전트로 같은 파일 분석
→ 중복 작업, 오히려 느림
```

---

## 문제 해결

### Q: "파일을 찾을 수 없습니다" 에러가 계속 나요.

**A:** 체크리스트:

```bash
# 1. 현재 디렉토리 확인
pwd

# 2. 파일이 실제로 존재하는지 확인
ls -la src/auth/auth.service.ts

# 3. Git에서 추적 중인지 확인
git ls-files | grep auth.service.ts

# 4. .gitignore 확인
cat .gitignore

# 5. 절대 경로로 시도
> "/home/user/project/src/auth/auth.service.ts 파일을 읽어줘"
```

---

### Q: Claude가 잘못된 파일을 수정했어요!

**A:** 즉시 되돌리고 다시 시도:

```bash
# 1. 변경사항 되돌리기
git checkout src/auth/wrong-file.ts

# 2. 더 구체적으로 요청
> "src/auth/auth.service.ts 파일의 25번째 줄에 있는
   login 메서드만 수정해줘. 다른 파일은 건드리지 마."

# 3. 한 번에 하나씩
> "먼저 auth.service.ts만 수정해줘.
   내가 확인하고 다음 파일을 요청할게."
```

---

### Q: Git 충돌이 발생했어요.

**A:** Claude는 Git 충돌을 직접 해결하지 못합니다. 수동으로 해결하세요:

```bash
# 1. 충돌 파일 확인
git status

# 2. 파일 열어서 수동 해결
# <<<<<<< HEAD
# =======
# >>>>>>> branch
# 마커를 찾아서 수동 편집

# 3. 해결 후 Claude에게 요청
> "충돌을 해결했어. 이제 커밋해줘"
```

---

### Q: 실행 중인 작업을 취소하고 싶어요.

**A:**

```bash
# Claude 응답 중단
Ctrl+C  # (macOS: Cmd+C)

# 주의:
# - 파일 수정 중이었다면 부분적으로 수정되었을 수 있음
# - git status로 확인
# - 필요하면 git checkout으로 되돌리기
```

---

## 고급 주제

### Q: 커스텀 슬래시 명령어를 만들 수 있나요?

**A:** 네! `.claude/commands/` 디렉토리에 마크다운 파일을 만들면 됩니다.

```bash
# 1. 디렉토리 생성
mkdir -p .claude/commands

# 2. 명령어 파일 생성
cat > .claude/commands/my-command.md << 'EOF'
---
name: my-command
description: My custom command
---

# My Command

This is a custom command that does XYZ.

When executed, perform the following steps:
1. Read package.json
2. Check dependencies
3. Report outdated packages
EOF

# 3. 사용
claude
> /my-command
```

---

### Q: Hook을 추가하려면 어떻게 하나요?

**A:** 플러그인에 Hook을 추가할 수 있습니다.

**예시: PreToolUse Hook**

```bash
# 1. 플러그인 디렉토리 생성
mkdir -p .claude/plugins/my-plugin/hooks
mkdir -p .claude/plugins/my-plugin/hooks-handlers

# 2. hooks.json 생성
cat > .claude/plugins/my-plugin/hooks/hooks.json << 'EOF'
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PLUGIN_ROOT}/hooks-handlers/my-hook.sh"
          }
        ]
      }
    ]
  }
}
EOF

# 3. Hook 스크립트 생성
cat > .claude/plugins/my-plugin/hooks-handlers/my-hook.sh << 'EOF'
#!/bin/bash
# 입력 데이터는 stdin으로 전달됨
# JSON 형식

# 검사 수행...
# 문제 없으면: exit 0
# 차단하려면: exit 2
EOF

chmod +x .claude/plugins/my-plugin/hooks-handlers/my-hook.sh
```

---

### Q: 에이전트를 커스터마이징할 수 있나요?

**A:** 네! 커스텀 에이전트를 만들 수 있습니다.

```markdown
<!-- .claude/plugins/my-plugin/agents/my-agent.md -->

---
name: my-agent
description: My custom agent
model: haiku
color: blue
tools: Glob, Grep, Read
---

# My Custom Agent

## Mission

Analyze code quality and suggest improvements.

## Process

1. Search for code smells
2. Identify anti-patterns
3. Suggest refactoring
4. Report findings

## Output Format

Provide a structured report with:
- Issues found
- Severity (HIGH/MEDIUM/LOW)
- Suggested fixes
```

**사용:**
```
> 내 커스텀 에이전트를 실행해줘
```

---

### Q: 여러 프로젝트에서 동일한 설정을 사용하려면?

**A:** 사용자 레벨 플러그인을 만드세요.

```bash
# 1. 사용자 플러그인 디렉토리
mkdir -p ~/.claude/plugins/my-global-plugin

# 2. 설정 추가
cp -r .claude/plugins/my-plugin/* ~/.claude/plugins/my-global-plugin/

# 3. 모든 프로젝트에서 사용 가능
```

---

### Q: Claude Code를 CI/CD에서 사용할 수 있나요?

**A:** 가능하지만 권장하지 않습니다.

```bash
# Headless 모드 (비대화형)
echo "내 요청" | claude --non-interactive

# 주의사항:
⚠️  API 비용 발생
⚠️  비결정적 출력 (매번 다를 수 있음)
⚠️  실행 시간 예측 불가
⚠️  에러 처리 복잡

# 대안:
✓ 로컬 개발에서만 사용
✓ PR 생성은 자동화 (GitHub Actions 등)
✓ 코드 생성은 개발자가 검토
```

---

### Q: API 사용량을 줄이려면?

**A:** 몇 가지 전략:

```
1. 구체적인 요청으로 재시도 감소
   ✓ "src/auth/auth.service.ts의 login 메서드를 수정해줘"
   ✗ "뭔가 고쳐줘"

2. 불필요한 탐색 줄이기
   ✓ "src/auth/ 디렉토리만 검색해줘"
   ✗ "전체 프로젝트 검색해줘"

3. Haiku 모델 사용 (간단한 작업)
   > "빠르게 (Haiku로) 파일 목록 보여줘"

4. 캐싱 활용
   - 같은 세션에서는 컨텍스트 유지
   - 새 세션 시작하지 않기

5. 배치 작업
   ✓ "이 3개 파일을 모두 수정해줘"
   ✗ 파일마다 따로 요청
```

---

### Q: 프라이버시가 걱정됩니다. 코드가 어디로 전송되나요?

**A:**

```
전송되는 것:
✓ 사용자 요청 (프롬프트)
✓ 관련 파일 내용
✓ 도구 실행 결과
→ Anthropic API 서버로 전송

전송되지 않는 것:
✓ 프로젝트 전체
✓ .gitignore된 파일
✓ 바이너리 파일
✓ 읽지 않은 파일

Anthropic의 데이터 정책:
- 학습에 사용 안 함 (기본 설정)
- 30일 후 삭제
- 암호화 전송

민감한 프로젝트:
→ 회사 정책 확인
→ Self-hosted 옵션 고려 (Enterprise)
```

---

## 추가 질문이 있으신가요?

### 📚 리소스

```
공식 문서: https://docs.claude.com/en/docs/claude-code
GitHub: https://github.com/anthropics/claude-code
팀 채널: Slack #claude-code
```

### 💬 팀 내부 지원

```
담당자: [팀 리더 이름]
이메일: [이메일]
Slack: @[핸들]
```

### 🐛 버그 제보

```
GitHub Issues: https://github.com/anthropics/claude-code/issues

포함할 내용:
1. Claude Code 버전
2. 운영체제
3. 재현 단계
4. 예상 동작 vs 실제 동작
5. 에러 메시지 (있다면)
```

---

**이 FAQ가 도움이 되셨나요?**

추가 질문이나 개선 제안은 언제든 환영합니다! 🙌

**문서 버전**: 1.0
**최종 업데이트**: 2025-11-10
