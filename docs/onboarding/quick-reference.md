# ⚡ Claude Code 빠른 참조 가이드

이 문서는 자주 사용하는 명령어와 패턴을 빠르게 찾을 수 있는 치트시트입니다.

## 🚀 기본 명령어

### 시작 및 종료

```bash
# Claude Code 시작
claude

# 종료
exit
# 또는 Ctrl+C / Cmd+C
```

### 내장 명령어

```bash
/help              # 도움말 보기
/clear             # 대화 기록 지우기
Ctrl+R             # 대화 기록 보기 (Transcript 모드)
```

---

## 💬 일반적인 요청 패턴

### 코드 이해하기

```
✓ "이 프로젝트의 구조를 설명해줘"
✓ "인증 시스템이 어떻게 작동하는지 알려줘"
✓ "UserService 클래스의 역할을 설명해줘"
✓ "이 함수가 무엇을 하는지 알려줘"
```

### 파일 읽기

```
✓ "README 파일을 읽어줘"
✓ "src/auth/auth.service.ts의 내용을 보여줘"
✓ "package.json의 dependencies를 확인해줘"
```

### 코드 작성

```
✓ "UserService에 deleteUser 메서드를 추가해줘"
✓ "Login 페이지를 위한 React 컴포넌트를 만들어줘"
✓ "비밀번호 검증 유틸 함수를 작성해줘"
```

### 코드 수정

```
✓ "auth.service.ts의 login 메서드에 에러 처리를 추가해줘"
✓ "이 함수를 async/await로 변경해줘"
✓ "중복 코드를 제거해줘"
```

### 버그 찾기

```
✓ "로그인 버그를 찾아서 수정해줘"
✓ "메모리 누수가 있는지 확인해줘"
✓ "타입 에러를 찾아줘"
```

### 테스트

```
✓ "AuthService에 대한 단위 테스트를 작성해줘"
✓ "테스트를 실행해줘"
✓ "실패한 테스트를 고쳐줘"
```

### 리팩토링

```
✓ "이 함수를 더 읽기 쉽게 리팩토링해줘"
✓ "중복된 로직을 공통 함수로 추출해줘"
✓ "TypeScript로 변환해줘"
```

### 문서화

```
✓ "이 함수에 JSDoc 주석을 추가해줘"
✓ "API 엔드포인트 문서를 작성해줘"
✓ "README에 설치 가이드를 추가해줘"
```

---

## 🔧 슬래시 명령어

### 프로젝트 명령어

```bash
/feature-dev "기능 설명"    # 새 기능 개발 (7단계 워크플로우)
/commit-push-pr             # 커밋 + 푸시 + PR 생성
/dedupe                     # 중복 GitHub 이슈 찾기
/oncall-triage              # 긴급 이슈 트리아지
```

### 사용 예시

#### /feature-dev

```bash
# 간단한 기능
> /feature-dev "다크 모드 추가"

# 구체적인 기능
> /feature-dev "사용자가 Google 계정으로 로그인할 수 있도록 OAuth 인증 추가"

# 복잡한 기능
> /feature-dev "실시간 알림 시스템 구축 (WebSocket 사용)"
```

**7단계 프로세스:**
1. Discovery → 2. Exploration → 3. Questions → 4. Design → 5. Implementation → 6. Review → 7. Summary

#### /commit-push-pr

```bash
# 현재 변경사항을 자동으로 커밋, 푸시, PR 생성
> /commit-push-pr

# Claude가 자동으로:
# 1. git status 확인
# 2. git diff 분석
# 3. 커밋 메시지 작성
# 4. 파일 스테이징
# 5. 커밋 생성
# 6. 원격 저장소에 푸시
# 7. GitHub PR 생성
```

---

## 📝 효과적인 요청 작성법

### ✅ 좋은 예시

```
명확하고 구체적:
> "UserController의 updateProfile 메서드에 이메일 중복 검사를 추가해줘.
  이메일이 이미 존재하면 400 에러를 반환해야 해."

컨텍스트 제공:
> "NestJS 프로젝트야. AuthService의 login 메서드에서 비밀번호 검증 시
  bcrypt를 사용하고 있어. 여기에 rate limiting을 추가해줘."

단계별 요청:
> "먼저 User 모델에 profilePicture 필드를 추가해줘.
  그 다음에 업로드 API를 만들어줄게."
```

### ❌ 나쁜 예시

```
너무 모호함:
> "뭔가 고쳐줘"
> "프로젝트를 개선해줘"

너무 광범위함:
> "전체 인증 시스템을 다시 만들어줘"

컨텍스트 부족:
> "에러 고쳐줘" (어떤 에러?)
```

---

## 🎯 일반적인 작업 흐름

### 새 기능 추가

```
1. /feature-dev "기능 설명"
2. Phase별로 진행 (자동)
3. 구현 완료
4. /commit-push-pr
```

### 버그 수정

```
1. "로그인 시 세션이 저장 안 되는 버그를 찾아줘"
2. Claude가 원인 분석
3. "수정해줘" (승인)
4. 테스트 실행
5. /commit-push-pr
```

### 코드 리뷰

```
1. "최근 변경사항을 리뷰해줘"
   또는
   "src/auth/ 디렉토리의 코드를 리뷰해줘"

2. Claude가 이슈 발견
3. "발견된 이슈를 수정해줘"
4. /commit-push-pr
```

### 레거시 코드 이해

```
1. "이 프로젝트의 인증 시스템을 설명해줘"
2. Claude가 3개 에이전트로 병렬 탐색
3. 상세 보고서 제공
4. "문서로 정리해줘" (선택사항)
```

### 리팩토링

```
1. "UserController의 중복 코드를 찾아줘"
2. Claude가 중복 패턴 발견
3. "공통 함수로 추출해줘"
4. 테스트 실행
5. /commit-push-pr
```

---

## 🛡️ 보안 관련

### 보안 경고 이해하기

```
⚠️  보안 경고가 나타나면:

1. 메시지를 주의 깊게 읽기
2. 제안된 안전한 대안 확인
3. 코드 수정 승인

일반적인 보안 패턴:
- GitHub Actions injection
- Command injection (os.system, child_process.exec)
- Code injection (eval, new Function)
- XSS (dangerouslySetInnerHTML)
- Unsafe deserialization (pickle.loads)
```

### 세션별 경고

```
보안 경고는 세션당 한 번만 표시됩니다.
→ 의도된 동작입니다 (경고 피로 방지)
→ 새 세션에서는 다시 표시됩니다
```

---

## 📊 에이전트 이해하기

### Code Explorer

```
용도: 코드베이스 탐색 및 분석
실행: 자동 (필요 시 3개 병렬)
속도: 빠름 (Haiku 모델)

언제 사용:
- "인증 시스템 찾아줘"
- "API 엔드포인트 구조 설명해줘"
- "어떤 파일들이 관련되어 있는지 알려줘"
```

### Code Architect

```
용도: 아키텍처 설계
실행: /feature-dev의 Phase 4
모델: Sonnet (깊은 사고)

3가지 접근법 제시:
1. Minimal Changes (빠른 구현)
2. Clean Architecture (확장성)
3. Pragmatic Balance (권장)
```

### Code Reviewer

```
용도: 코드 품질 검사
실행: /feature-dev의 Phase 6
모델: Sonnet (정확성)

3가지 관점:
1. Simplicity & DRY
2. Bugs & Correctness
3. Conventions & Abstractions

신뢰도 ≥80%만 보고
```

---

## 🔍 파일 및 코드 검색

### 파일 찾기

```
✓ "auth 관련 파일을 찾아줘"
✓ "**.tsx 파일을 모두 나열해줘"
✓ "설정 파일들을 찾아줘"
```

Claude가 자동으로 Glob 도구 사용.

### 코드 검색

```
✓ "createUser 함수가 어디에 정의되어 있는지 찾아줘"
✓ "TODO 주석을 모두 찾아줘"
✓ "console.log가 있는 파일을 찾아줘"
```

Claude가 자동으로 Grep 도구 사용.

---

## 🎨 Git 작업

### 자동 커밋

```bash
> /commit-push-pr

# Claude가 자동으로:
# 1. 변경사항 분석
# 2. 커밋 메시지 작성 (프로젝트 스타일 학습)
# 3. 스테이징
# 4. 커밋
# 5. 푸시
# 6. PR 생성
```

### 커밋 메시지 스타일

```
Claude는 프로젝트의 커밋 히스토리를 학습합니다:

git log -5 --oneline 결과:
  a3f5b92 Add user profile page
  7d2e8c4 Fix authentication bug
  b1c9f5a Update dependencies

→ Claude도 같은 스타일로 작성:
  "Add dark mode toggle"
  "Fix session storage bug"
```

### PR 생성

```
자동 생성되는 내용:
- 제목 (커밋 메시지 기반)
- 요약
- 주요 변경사항
- 변경된 파일 목록
- 테스트 체크리스트

모두 변경사항을 분석하여 자동 생성!
```

---

## ⚙️ 유용한 팁

### 1. 점진적으로 작업하기

```
❌ "인증 시스템 전체를 다시 만들어줘"

✓ 1단계: "User 모델을 먼저 설계해줘"
✓ 2단계: "이제 AuthService를 구현해줘"
✓ 3단계: "API 엔드포인트를 추가해줘"
✓ 4단계: "테스트를 작성해줘"
```

### 2. 파일 경로 명시하기

```
모호함:
> "이 파일을 수정해줘"

명확함:
> "src/services/auth.service.ts를 수정해줘"
```

### 3. 예시 제공하기

```
효과적:
> "login 메서드에 rate limiting을 추가해줘.
  1분에 5번 이상 시도하면 429 에러를 반환해야 해.
  express-rate-limit 라이브러리를 사용하면 좋을 것 같아."
```

### 4. 작업 범위 지정하기

```
광범위:
> "전체 프로젝트를 TypeScript로 변환해줘"

적절:
> "src/services/ 디렉토리를 TypeScript로 변환해줘"
```

### 5. 정기적으로 커밋하기

```
큰 작업 중간중간:
> "여기까지 작업을 커밋해줘"

이유:
- 변경사항 추적 용이
- 롤백 가능
- 리뷰하기 쉬움
```

---

## 🐛 일반적인 문제 해결

### "파일을 찾을 수 없습니다"

```
원인:
- 잘못된 파일 경로
- .gitignore에 포함된 파일
- 프로젝트 루트가 아닌 곳에서 실행

해결:
1. 경로 확인: ls src/
2. Git 상태: git status
3. 프로젝트 루트로 이동: cd /path/to/project
```

### "권한이 거부되었습니다"

```
원인:
- SSH 키 또는 토큰 문제
- 브랜치 보호 규칙

해결:
1. Git 설정 확인: git config --list
2. SSH 키 확인: ssh -T git@github.com
3. 권한 확인: GitHub 저장소 설정
```

### "에이전트가 너무 오래 걸립니다"

```
원인:
- 검색 범위가 너무 넓음
- Thoroughness가 너무 높음

해결:
> "src/auth/ 디렉토리만 빠르게 탐색해줘 (quick 모드)"
```

### "보안 경고가 계속 나옵니다"

```
정상:
보안 경고는 세션당 한 번만 표시됩니다.
새 세션(claude 재시작)에서는 다시 표시됩니다.

이것은 버그가 아닙니다!
```

---

## 📋 체크리스트

### 작업 시작 전

```
☐ 올바른 디렉토리에 있는가?
☐ Git 상태가 깨끗한가? (git status)
☐ 작업 브랜치를 만들었는가?
☐ 요청이 명확하고 구체적인가?
```

### 작업 중

```
☐ 변경사항을 정기적으로 확인하는가?
☐ 보안 경고를 무시하지 않는가?
☐ 중간중간 테스트를 실행하는가?
☐ 큰 작업은 단계별로 나누는가?
```

### 작업 완료 후

```
☐ 모든 테스트가 통과하는가?
☐ 코드 리뷰를 받았는가?
☐ 커밋 메시지가 명확한가?
☐ PR 설명이 충분한가?
```

---

## 🚀 다음 단계

### 초보자

```
✓ 기본 README 읽기: docs/onboarding/README.md
✓ 간단한 질문으로 연습
✓ 파일 읽기/수정 요청
```

### 중급자

```
✓ /feature-dev 사용해보기
✓ /commit-push-pr로 PR 생성
✓ 시나리오 문서 읽기: docs/scenarios/
```

### 고급자

```
✓ 플러그인 탐색: plugins/
✓ 커스텀 명령어 만들기
✓ Hook 설정하기
```

---

## 🔗 유용한 링크

```
📚 공식 문서: https://docs.claude.com/en/docs/claude-code
🐛 이슈 제보: https://github.com/anthropics/claude-code/issues
💬 팀 채널: Slack #claude-code
📖 온보딩 가이드: docs/onboarding/README.md
📕 시나리오 문서: docs/scenarios/
```

---

## 💡 기억하세요

```
1. 명확하고 구체적으로 요청하세요
2. 큰 작업은 단계별로 나누세요
3. 보안 경고를 주의 깊게 확인하세요
4. 정기적으로 커밋하세요
5. 궁금한 점은 언제든 물어보세요!
```

---

**이 문서를 즐겨찾기하세요!** 자주 참조하게 될 것입니다. 📌

**문서 버전**: 1.0
**최종 업데이트**: 2025-11-10
