# 🌟 feature-dev의 여정: 코드 실행 흐름 이야기

> **Claude Code 플러그인 시스템의 가장 정교한 워크플로우, feature-dev가 어떻게 새로운 기능을 탄생시키는지 그 여정을 따라가봅니다.**

---

## 프롤로그: 여행의 시작

어느 날, 개발자가 터미널에 명령을 입력합니다:

```bash
/feature-dev Add user authentication with OAuth
```

이 한 줄의 명령어가 입력되는 순간, feature-dev 플러그인의 위대한 여정이 시작됩니다. 이것은 단순한 명령어 실행이 아닙니다. 7개의 정교하게 설계된 단계를 거치며, 세 명의 전문 에이전트가 협력하여 하나의 기능을 완성해가는 장대한 이야기입니다.

---

## 1장: 발견의 시작 (Phase 1: Discovery)

**위치:** `/home/user/claude-code/plugins/feature-dev/commands/feature-dev.md`

여정의 첫 단계는 '이해'입니다. feature-dev 명령어는 사용자로부터 받은 `$ARGUMENTS` 변수에 담긴 내용을 조심스럽게 살펴봅니다. "사용자 인증을 OAuth로 추가하라"는 요청. 하지만 이것으로 충분할까요?

feature-dev는 성급하게 움직이지 않습니다. 대신, TodoWrite 도구를 사용하여 앞으로 거쳐갈 7개의 단계를 리스트로 작성합니다:

```
✓ Phase 1: Discovery - 무엇을 만들지 이해하기
○ Phase 2: Codebase Exploration - 기존 코드 탐색
○ Phase 3: Clarifying Questions - 명확화 질문
○ Phase 4: Architecture Design - 아키텍처 설계
○ Phase 5: Implementation - 구현
○ Phase 6: Quality Review - 품질 검토
○ Phase 7: Summary - 완료 요약
```

만약 요청이 불분명하다면, feature-dev는 사용자에게 질문을 던집니다:

- "어떤 문제를 해결하려고 하시나요?"
- "이 기능이 정확히 무엇을 해야 하나요?"
- "제약사항이나 요구사항이 있나요?"

사용자가 답변하고 확인을 주면, 첫 번째 체크포인트를 통과합니다. 여정의 첫 발걸음이 시작됩니다.

---

## 2장: 코드 탐험가들의 출동 (Phase 2: Codebase Exploration)

**위치:** `/home/user/claude-code/plugins/feature-dev/agents/code-explorer.md`

이제 본격적인 탐험이 시작됩니다. feature-dev는 혼자 움직이지 않습니다. **2~3명의 코드 탐험가(code-explorer) 에이전트**를 동시에 소환합니다. 이들은 노란색(yellow) 배지를 단 전문 탐험가들입니다.

### 탐험가들의 임무 분담

```
┌─────────────────────────────────────────────────────────────┐
│ 🔍 탐험가 #1: "비슷한 기능을 찾아 구현을 추적하라!"        │
│ 🔍 탐험가 #2: "아키텍처와 추상화 계층을 지도로 그려라!"    │
│ 🔍 탐험가 #3: "UI 패턴과 확장 포인트를 분석하라!"          │
└─────────────────────────────────────────────────────────────┘
```

각 탐험가는 **4단계 분석 프로세스**를 따릅니다:

### 🗺️ 1단계: Feature Discovery (기능 발견)
탐험가들은 코드베이스의 넓은 대지를 가로지르며 진입점을 찾습니다:
- API 엔드포인트는 어디에?
- UI 컴포넌트는 어디에?
- CLI 명령어는?

Glob과 Grep 도구를 휘두르며, 파일들을 뒤적입니다. 마치 고고학자가 유적을 발굴하듯이.

### 🧭 2단계: Code Flow Tracing (코드 흐름 추적)
진입점을 발견했다면, 이제 그 흐름을 따라갑니다:

```
Entry Point (API Handler)
    ↓
Controller Layer
    ↓ [데이터 변환]
Business Logic Layer
    ↓ [상태 변경]
Data Access Layer
    ↓ [부작용 발생]
Database / External API
```

모든 호출 체인을 따라가며, 데이터가 어떻게 변환되는지 기록합니다. Read 도구를 사용하여 파일을 하나하나 열어보며, 각 단계에서 일어나는 일을 문서화합니다.

### 🏗️ 3단계: Architecture Analysis (아키텍처 분석)
이제 큰 그림을 봅니다:
- 어떤 추상화 계층이 있는가? (프레젠테이션 → 비즈니스 로직 → 데이터)
- 어떤 디자인 패턴이 사용되는가?
- 컴포넌트 간의 인터페이스는?
- 인증, 로깅, 캐싱 같은 횡단 관심사는 어떻게 처리되는가?

### 📝 4단계: Implementation Details (구현 세부사항)
마지막으로 세세한 부분을 기록합니다:
- 핵심 알고리즘과 자료구조
- 에러 처리와 엣지 케이스
- 성능 고려사항
- 기술 부채나 개선 영역

### 탐험가들의 귀환

탐험을 마친 세 명의 탐험가가 돌아옵니다. 각자 손에는 **5~10개의 핵심 파일 목록**과 상세한 분석 리포트를 들고 있습니다:

```javascript
{
  "entryPoints": [
    "src/auth/routes/oauth.ts:23",
    "src/auth/middleware/authenticate.ts:45"
  ],
  "executionFlow": [
    "1. 사용자가 /auth/oauth 엔드포인트 호출",
    "2. OAuthController.handleCallback() 실행 (oauth.ts:23)",
    "3. TokenService.validateToken() 호출 (token.ts:67)",
    "4. User 모델에 토큰 저장 (user.model.ts:89)",
    "5. 세션 생성 후 리다이렉트"
  ],
  "keyFiles": [
    "src/auth/routes/oauth.ts",
    "src/auth/services/token.ts",
    "src/models/user.model.ts",
    "src/middleware/session.ts",
    "config/oauth.config.ts"
  ],
  "observations": "기존 인증 시스템은 JWT 기반. OAuth 통합 시 토큰 교환 로직 필요."
}
```

### 지식의 통합

feature-dev는 탐험가들이 가져온 모든 파일을 **직접 읽습니다**. 에이전트가 말로만 설명하는 것이 아니라, 실제 코드를 눈으로 확인합니다. 이것이 중요합니다. 피상적인 이해가 아닌, 깊은 이해를 얻기 위함입니다.

그리고 사용자에게 보고서를 제시합니다:
- "이런 비슷한 기능들을 찾았습니다..."
- "아키텍처는 이렇게 구성되어 있습니다..."
- "중요한 파일들은 이것들입니다..."

사용자가 확인하면, 두 번째 체크포인트를 통과합니다.

---

## 3장: 질문의 시간 (Phase 3: Clarifying Questions)

**중요도: ⭐⭐⭐⭐⭐ (가장 중요한 단계 중 하나)**

탐험을 마치고 돌아온 feature-dev는 이제 앉아서 생각합니다. 모든 것을 알았을까? 아니, 아직 모호한 것들이 남아있습니다.

### 빈틈 찾기

feature-dev는 체크리스트를 만들며 하나씩 점검합니다:

```
□ 엣지 케이스: OAuth 제공자가 응답하지 않으면?
□ 에러 처리: 토큰이 만료되면 어떻게?
□ 통합 지점: 기존 세션 시스템과 어떻게 통합?
□ 범위: 어떤 OAuth 제공자를 지원? (Google? GitHub? 둘 다?)
□ 디자인 선호도: UI는 팝업? 리다이렉트?
□ 하위 호환성: 기존 JWT 사용자는?
□ 성능: 토큰 검증을 매번? 캐시는?
```

### 질문의 목록

feature-dev는 사용자에게 정리된 질문 목록을 제시합니다:

```
📋 명확화가 필요한 사항들:

1. **OAuth 제공자**
   - 어떤 제공자를 지원해야 하나요? (Google, GitHub, Facebook 등)

2. **기존 사용자 처리**
   - 이미 JWT로 인증된 사용자는 어떻게 처리하나요?
   - 마이그레이션이 필요한가요?

3. **에러 처리**
   - OAuth 인증 실패 시 사용자를 어디로 리다이렉트하나요?
   - 토큰 갱신은 자동으로 처리하나요?

4. **보안**
   - CSRF 토큰을 사용하나요?
   - State 파라미터 검증은?

5. **UI/UX**
   - 로그인 흐름은 팝업 방식? 전체 페이지 리다이렉트?
```

### 중요한 대기

**여기서 feature-dev는 멈춥니다.** 사용자의 답변을 기다립니다. 절대 혼자서 추측하지 않습니다.

만약 사용자가 "알아서 해주세요"라고 하면, feature-dev는 자신의 추천을 제시하고 명시적인 확인을 받습니다.

사용자가 모든 질문에 답변하면, 세 번째 체크포인트를 통과합니다. 이제 모호함 없이 명확한 요구사항을 갖게 되었습니다.

---

## 4장: 건축가들의 회의 (Phase 4: Architecture Design)

**위치:** `/home/user/claude-code/plugins/feature-dev/agents/code-architect.md`

이제 설계의 시간입니다. feature-dev는 다시 전문가들을 소환합니다. 이번에는 **2~3명의 건축가(code-architect) 에이전트**들입니다. 그들은 초록색(green) 배지를 달고 있습니다.

### 건축가들의 다른 관점

```
┌──────────────────────────────────────────────────────────────┐
│ 🏛️ 건축가 #1: "최소 변경 접근법"                             │
│    → 기존 코드를 최대한 재사용, 가장 작은 변경               │
│                                                              │
│ 🏛️ 건축가 #2: "클린 아키텍처 접근법"                         │
│    → 유지보수성, 우아한 추상화                               │
│                                                              │
│ 🏛️ 건축가 #3: "실용적 균형 접근법"                           │
│    → 속도 + 품질의 균형                                      │
└──────────────────────────────────────────────────────────────┘
```

### 건축가들의 3단계 프로세스

#### 🔍 1단계: 패턴 분석
각 건축가는 먼저 코드베이스의 패턴을 분석합니다:
- 기술 스택은?
- 모듈 경계는?
- 유사한 기능은 어떻게 구현되었는가?
- CLAUDE.md에 프로젝트 가이드라인이 있는가?

#### 🎨 2단계: 아키텍처 설계
이제 각자의 철학에 따라 설계합니다:

**건축가 #1 (최소 변경)의 설계:**
```
"기존 AuthController를 확장하여 oauthCallback 메서드만 추가합니다.
TokenService에 validateOAuthToken 메서드 하나만 추가하면 됩니다.
총 2개 파일 수정으로 완료 가능합니다."
```

**건축가 #2 (클린 아키텍처)의 설계:**
```
"새로운 OAuth 도메인을 생성합니다:
- OAuthProvider 인터페이스
- GoogleOAuthProvider, GitHubOAuthProvider 구현체
- OAuthService (비즈니스 로직)
- OAuthRepository (데이터 접근)
깔끔하게 분리되어 테스트와 확장이 용이합니다."
```

**건축가 #3 (실용적 균형)의 설계:**
```
"OAuthService를 새로 만들되, 기존 TokenService와 통합합니다.
Provider 패턴은 사용하지만 지나친 추상화는 피합니다.
개발 속도와 유지보수성의 균형을 맞춥니다."
```

#### 📐 3단계: 구현 청사진

각 건축가는 완전한 청사진을 제공합니다:

```yaml
Implementation Blueprint:

  Files to Create:
    - src/auth/services/oauth.service.ts
      Role: "OAuth 인증 로직 처리"
      Dependencies: ["axios", "TokenService", "UserRepository"]
      Interface: |
        - authenticateWithProvider(provider, code)
        - refreshOAuthToken(token)

    - src/auth/providers/google.provider.ts
      Role: "Google OAuth 제공자 구현"

  Files to Modify:
    - src/auth/routes/auth.routes.ts:15
      Change: "POST /auth/oauth/:provider 라우트 추가"

    - config/oauth.config.ts
      Change: "provider별 client ID, secret 설정 추가"

  Data Flow:
    1. 사용자가 /auth/oauth/google 클릭
    2. Google 인증 페이지로 리다이렉트
    3. Callback: /auth/oauth/google/callback?code=xxx
    4. OAuthService.authenticateWithProvider('google', code)
    5. Google API로 토큰 교환
    6. 사용자 정보 조회 → DB 저장/업데이트
    7. 세션 생성 → 앱으로 리다이렉트

  Build Sequence:
    Phase 1: ✓ 설정 파일 구성
    Phase 2: ✓ Provider 인터페이스 및 구현
    Phase 3: ✓ OAuthService 구현
    Phase 4: ✓ 라우트 및 컨트롤러 추가
    Phase 5: ✓ 기존 인증 시스템과 통합
    Phase 6: ✓ 에러 처리 및 테스트
```

### 건축가들의 귀환과 결정

세 건축가가 각자의 설계안을 가지고 돌아옵니다. feature-dev는 이것들을 검토하고, 현재 작업에 가장 적합한 것이 무엇인지 판단합니다:

- 작은 버그 수정인가, 큰 기능인가?
- 긴급한가?
- 복잡도는?
- 팀의 컨텍스트는?

그리고 사용자에게 비교표를 제시합니다:

```
┌────────────────────────────────────────────────────────────────┐
│ 아키텍처 접근법 비교                                            │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│ 접근법 #1: 최소 변경                                            │
│ • 장점: 빠른 개발, 기존 코드와 일관성                           │
│ • 단점: 확장성 제한, 미래 provider 추가 시 코드 중복           │
│ • 파일 변경: 2개 파일 수정                                      │
│                                                                │
│ 접근법 #2: 클린 아키텍처                                        │
│ • 장점: 높은 테스트 가능성, 쉬운 확장                           │
│ • 단점: 초기 개발 시간 증가, 복잡도 증가                        │
│ • 파일 변경: 8개 파일 생성, 3개 파일 수정                       │
│                                                                │
│ 접근법 #3: 실용적 균형 ⭐ [추천]                                │
│ • 장점: 적절한 추상화, 빠른 개발, 미래 확장 가능                │
│ • 단점: 중간 복잡도                                             │
│ • 파일 변경: 4개 파일 생성, 2개 파일 수정                       │
│                                                                │
│ 📌 추천 이유:                                                   │
│ 이 프로젝트는 이미 서비스 계층 패턴을 사용하고 있으며,          │
│ OAuth는 향후 확장 가능성이 있어 적절한 추상화가 필요합니다.     │
│ 접근법 #3은 두 마리 토끼를 모두 잡습니다.                       │
└────────────────────────────────────────────────────────────────┘

어떤 접근법을 선택하시겠습니까?
```

### 사용자의 선택

사용자가 접근법을 선택하면, 네 번째 체크포인트를 통과합니다. 이제 명확한 구현 계획이 있습니다.

---

## 5장: 실행의 시간 (Phase 5: Implementation)

**⚠️ 중요: 명시적 승인 필요**

feature-dev는 코드를 작성하기 전에 한 번 더 멈춥니다:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️  구현 승인 요청

선택된 아키텍처: 실용적 균형 접근법
예상 변경사항:
  • 4개 파일 생성
  • 2개 파일 수정

구현을 시작해도 될까요?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

사용자가 "예"라고 하면, 다섯 번째 체크포인트를 통과합니다. 이제 진짜 코드 작성이 시작됩니다.

### 파일 읽기의 시간

먼저 feature-dev는 Phase 2-4에서 식별된 모든 관련 파일을 읽습니다. Read 도구를 사용하여:

```javascript
// Phase 2에서 탐험가들이 찾은 파일들
Read("src/auth/services/token.ts")
Read("src/models/user.model.ts")
Read("src/middleware/session.ts")

// Phase 4에서 건축가가 참고하라고 한 파일들
Read("src/auth/routes/auth.routes.ts")
Read("config/database.config.ts")
```

### 코드 작성

이제 Write와 Edit 도구를 사용하여 코드를 작성합니다. 건축가의 청사진을 정확히 따릅니다:

**1️⃣ 새 파일 생성:**
```typescript
// src/auth/services/oauth.service.ts 생성
Write("src/auth/services/oauth.service.ts", `
import axios from 'axios';
import { TokenService } from './token';
import { UserRepository } from '../repositories/user';

export class OAuthService {
  constructor(
    private tokenService: TokenService,
    private userRepo: UserRepository
  ) {}

  async authenticateWithProvider(
    provider: string,
    code: string
  ): Promise<User> {
    // Google API로 토큰 교환
    const tokenData = await this.exchangeCodeForToken(provider, code);

    // 사용자 정보 조회
    const userInfo = await this.fetchUserInfo(provider, tokenData.access_token);

    // DB에 저장 또는 업데이트
    const user = await this.userRepo.findOrCreateByOAuth(userInfo);

    // 세션 토큰 생성
    user.token = await this.tokenService.createToken(user.id);

    return user;
  }

  private async exchangeCodeForToken(provider: string, code: string) {
    // ... 구현 ...
  }

  private async fetchUserInfo(provider: string, accessToken: string) {
    // ... 구현 ...
  }
}
`)
```

**2️⃣ 기존 파일 수정:**
```typescript
// src/auth/routes/auth.routes.ts 수정
Edit("src/auth/routes/auth.routes.ts", {
  old_string: `
  router.post('/login', authController.login);
  router.post('/logout', authController.logout);`,

  new_string: `
  router.post('/login', authController.login);
  router.post('/logout', authController.logout);
  router.get('/oauth/:provider', authController.oauthRedirect);
  router.get('/oauth/:provider/callback', authController.oauthCallback);`
})
```

### 진행 상황 추적

feature-dev는 작업하면서 계속 TodoWrite를 업데이트합니다:

```
✓ Phase 1: Discovery
✓ Phase 2: Codebase Exploration
✓ Phase 3: Clarifying Questions
✓ Phase 4: Architecture Design
⏳ Phase 5: Implementation
   ✓ 설정 파일 구성
   ✓ OAuthService 구현
   ⏳ 라우트 추가
   ○ 컨트롤러 구현
   ○ 에러 처리
○ Phase 6: Quality Review
○ Phase 7: Summary
```

### 코드 작성 원칙

feature-dev는 다음을 철저히 지킵니다:
- **Phase 4의 아키텍처** 정확히 따르기
- **Phase 3의 명확화된 요구사항** 모두 반영
- **Phase 2에서 발견한 패턴** 일관되게 사용
- 깔끔하고 **잘 문서화된 코드** 작성
- 프로젝트 **컨벤션** 준수

모든 구현이 완료되면, Phase 5가 끝납니다.

---

## 6장: 검토자들의 엄격한 심사 (Phase 6: Quality Review)

**위치:** `/home/user/claude-code/plugins/feature-dev/agents/code-reviewer.md`

코드가 작성되었습니다. 하지만 정말 좋은 코드일까요? 이제 **3명의 검토자(code-reviewer) 에이전트**가 등장합니다. 그들은 빨간색(red) 배지를 달고 있습니다.

### 검토자들의 전문 분야

```
┌──────────────────────────────────────────────────────────────┐
│ 🔴 검토자 #1: "단순성/DRY/우아함"                              │
│    → 코드 품질과 유지보수성 집중                              │
│                                                              │
│ 🔴 검토자 #2: "버그/기능적 정확성"                            │
│    → 로직 에러와 기능 문제 집중                               │
│                                                              │
│ 🔴 검토자 #3: "컨벤션/추상화"                                 │
│    → 프로젝트 표준과 패턴 준수 집중                           │
└──────────────────────────────────────────────────────────────┘
```

### 검토 프로세스

#### 1️⃣ 변경사항 확인
각 검토자는 먼저 `git diff`를 확인합니다:

```bash
git diff --staged  # 스테이징된 변경사항
git diff           # 스테이징되지 않은 변경사항
```

#### 2️⃣ 가이드라인 검토
프로젝트의 CLAUDE.md 파일을 읽어 명시적 규칙을 확인합니다:

```markdown
# CLAUDE.md
- 모든 async 함수는 try-catch로 감싸야 함
- 에러는 반드시 로깅해야 함
- 테스트 커버리지는 80% 이상 유지
- import는 절대 경로 사용
```

#### 3️⃣ 이슈 발견과 신뢰도 점수

검토자들은 발견한 모든 문제에 **신뢰도 점수**를 매깁니다:

```
0점: 확신 없음 - 오탐이거나 기존 문제
25점: 약간 확신 - 실제 문제일 수도, 오탐일 수도
50점: 보통 확신 - 실제 문제이지만 사소할 수 있음
75점: 높은 확신 - 확인된 실제 문제, 실무에서 발생할 것
100점: 절대 확신 - 확인된 심각한 문제, 자주 발생할 것
```

**중요한 필터:** **신뢰도 ≥ 80점인 문제만 보고합니다.**

이것은 노이즈를 줄이기 위함입니다. 사소한 니트픽이 아닌, 진짜 문제만 보고합니다.

### 검토자들의 발견

**검토자 #1 (단순성/DRY)의 보고:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 코드 품질 이슈 (신뢰도: 85점)

📍 위치: src/auth/services/oauth.service.ts:45

문제: 코드 중복
설명: exchangeCodeForToken 메서드 내의 토큰 교환 로직이
Google과 GitHub provider에서 거의 동일하게 반복됩니다.

가이드라인 위반: CLAUDE.md - "DRY 원칙 준수"

제안 수정:
공통 로직을 baseExchangeToken() 메서드로 추출하고,
provider별 차이점만 설정으로 관리하세요.

영향도: 중간 (유지보수성 저하)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**검토자 #2 (버그/기능)의 보고:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 심각한 버그 발견 (신뢰도: 95점)

📍 위치: src/auth/controllers/auth.controller.ts:78

문제: 에러 처리 누락
설명: oauthCallback 메서드에서 OAuthService.authenticateWithProvider()
호출이 try-catch로 감싸져 있지 않습니다. OAuth provider가 에러를
반환하면 애플리케이션이 크래시합니다.

가이드라인 위반: CLAUDE.md - "모든 async 함수는 try-catch 필수"

제안 수정:
```typescript
async oauthCallback(req, res) {
  try {
    const user = await this.oauthService.authenticateWithProvider(
      req.params.provider,
      req.query.code
    );
    // ... 성공 처리
  } catch (error) {
    logger.error('OAuth authentication failed', error);
    res.redirect('/login?error=oauth_failed');
  }
}
```

영향도: 높음 (프로덕션 크래시 가능)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**검토자 #3 (컨벤션)의 보고:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 컨벤션 위반 (신뢰도: 82점)

📍 위치: src/auth/providers/google.provider.ts:3

문제: import 경로 패턴 불일치
설명: 이 프로젝트는 절대 경로 import를 사용하는데
(예: 'src/services/...'), 이 파일은 상대 경로를 사용합니다
(예: '../../services/...').

가이드라인 위반: CLAUDE.md - "import는 절대 경로 사용"

제안 수정:
import { OAuthConfig } from '../../config/oauth'
→
import { OAuthConfig } from 'src/config/oauth'

영향도: 낮음 (일관성 문제)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 통합 보고

feature-dev는 세 검토자의 보고를 통합하여 심각도별로 그룹화합니다:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 코드 검토 결과

🔥 치명적 (Critical):
  1. [95점] 에러 처리 누락 - auth.controller.ts:78
     → 프로덕션 크래시 가능

⚠️  중요 (Important):
  2. [85점] 코드 중복 - oauth.service.ts:45
     → 유지보수성 저하

  3. [82점] import 경로 불일치 - google.provider.ts:3
     → 프로젝트 컨벤션 위반

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

이 문제들을 어떻게 하시겠습니까?
  A) 지금 수정하기
  B) 나중에 수정하기
  C) 이대로 진행하기
```

### 사용자의 결정

사용자가 "A) 지금 수정하기"를 선택하면, feature-dev는 문제를 수정합니다. 그리고 다시 검토자들을 불러 재검토를 진행할 수 있습니다.

모든 문제가 해결되거나 사용자가 승인하면, 여섯 번째 체크포인트를 통과합니다.

---

## 7장: 여정의 끝, 새로운 시작 (Phase 7: Summary)

마지막 단계입니다. feature-dev는 TodoWrite를 열어 모든 항목을 완료 상태로 표시합니다:

```
✓ Phase 1: Discovery
✓ Phase 2: Codebase Exploration
✓ Phase 3: Clarifying Questions
✓ Phase 4: Architecture Design
✓ Phase 5: Implementation
✓ Phase 6: Quality Review
✓ Phase 7: Summary
```

### 최종 보고서

그리고 사용자에게 최종 보고서를 제시합니다:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✨ 기능 개발 완료: OAuth 사용자 인증

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📋 구현 내용:
  • Google OAuth 인증 통합
  • 기존 JWT 시스템과의 원활한 통합
  • 토큰 갱신 자동 처리
  • CSRF 보호 구현

🏗️ 선택된 아키텍처:
  실용적 균형 접근법
  - Provider 패턴 사용으로 향후 확장 가능
  - 기존 서비스 계층과 일관된 구조
  - 적절한 추상화로 테스트 가능성 확보

📁 변경된 파일:
  생성됨:
    • src/auth/services/oauth.service.ts
    • src/auth/providers/google.provider.ts
    • src/auth/controllers/oauth.controller.ts
    • config/oauth.config.ts

  수정됨:
    • src/auth/routes/auth.routes.ts (+4 lines)
    • src/models/user.model.ts (+12 lines)

🔑 주요 결정사항:
  • OAuth 제공자: Google (GitHub는 다음 단계)
  • 기존 사용자: 자동 마이그레이션 없음
  • 에러 처리: /login?error=oauth_failed로 리다이렉트
  • UI: 전체 페이지 리다이렉트 방식

📊 품질 지표:
  • 신뢰도 ≥80 버그: 모두 수정됨 ✓
  • 프로젝트 컨벤션: 준수 ✓
  • 코드 중복: 최소화 ✓

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 제안하는 다음 단계:
  1. 통합 테스트 작성
     - OAuth 플로우 전체 테스트
     - 에러 케이스 테스트

  2. 문서화
     - API 문서에 새 엔드포인트 추가
     - 사용자 가이드 업데이트

  3. 추가 Provider 지원
     - GitHub OAuth 추가
     - Facebook OAuth 추가

  4. 모니터링
     - OAuth 인증 성공/실패율 추적
     - 토큰 갱신 빈도 모니터링

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ 기능 개발이 완료되었습니다!
```

---

## 에필로그: 여정을 돌아보며

### 여정의 지도

우리는 7개의 단계를 거쳐 하나의 기능을 완성했습니다:

```
출발점: /feature-dev 명령어
    ↓
1. Discovery ──────────→ 이해 확보
    ↓
2. Exploration ────────→ 코드 탐험 (3명의 탐험가)
    ↓                     └─> 5~10개 핵심 파일 식별
3. Questions ──────────→ 모호함 제거 ⚠️ 중요!
    ↓                     └─> 사용자 확인 필수
4. Architecture ───────→ 설계 (3명의 건축가)
    ↓                     └─> 3가지 접근법, 1개 선택
5. Implementation ─────→ 구현 ⚠️ 승인 필요
    ↓                     └─> 청사진 정확히 따름
6. Review ─────────────→ 품질 검증 (3명의 검토자)
    ↓                     └─> 신뢰도 ≥80 문제만
7. Summary ────────────→ 완료 보고
    ↓
도착점: 완성된 기능
```

### 핵심 원칙들

이 여정을 통해 우리가 본 feature-dev의 핵심 원칙들:

#### 1. 🤝 협업적 (Collaborative)
- **6개의 사용자 체크포인트**
- 혼자 결정하지 않음
- 명시적 승인 필요

#### 2. 🔄 병렬적 (Parallel)
- **2-3명의 code-explorer** 동시 실행
- **2-3명의 code-architect** 동시 실행
- **3명의 code-reviewer** 동시 실행
- 효율성 극대화

#### 3. 📊 신뢰도 기반 (Confidence-Based)
- 신뢰도 점수 0-100
- ≥80점만 보고
- 노이즈 최소화, 실제 문제 집중

#### 4. 📚 깊은 이해 (Deep Understanding)
- 에이전트가 파일을 찾으면
- 직접 읽어서 이해
- 피상적 분석 거부

#### 5. 🎯 점진적 상세화 (Progressive Refinement)
- Phase 2: 큰 그림
- Phase 3: 빈틈 메우기
- Phase 4: 상세 설계
- Phase 5: 구체적 구현

#### 6. ✅ 체계적 추적 (Systematic Tracking)
- TodoWrite 도구 사용
- 모든 단계 문서화
- 진행 상황 투명화

### 기술적 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│                   feature-dev 명령어                     │
│                  (오케스트레이터)                         │
└─────────────────────────────────────────────────────────┘
         │
         ├──────────────┬──────────────┬──────────────┐
         ↓              ↓              ↓              ↓
┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌─────────┐
│code-explorer │ │code-architect│ │code-reviewer │ │ Tools   │
│   (노란색)    │ │   (초록색)    │ │   (빨간색)    │ │         │
│              │ │              │ │              │ │ • Glob  │
│ • 탐험       │ │ • 설계       │ │ • 검증       │ │ • Grep  │
│ • 분석       │ │ • 청사진     │ │ • 점수 부여  │ │ • Read  │
│ • 파일 발견  │ │ • 비교       │ │ • 필터링     │ │ • Write │
└──────────────┘ └──────────────┘ └──────────────┘ │ • Edit  │
                                                    └─────────┘
```

### 숫자로 보는 여정

```
7개 단계
6번의 사용자 체크포인트
8-9명의 전문 에이전트 (최대)
3가지 관점 (탐험, 설계, 검증)
2-3번의 병렬 실행
≥80 신뢰도 필터
5-10개 핵심 파일 (탐험가당)
100% 사용자 승인 기반
```

---

## 결론: 왜 feature-dev인가?

feature-dev 플러그인은 단순한 코드 생성기가 아닙니다. 그것은 **소프트웨어 개발의 모범 사례를 코드화한 워크플로우**입니다.

### 인간 개발자처럼 생각하기

1. **먼저 이해하고** (Discovery, Exploration)
2. **질문하고** (Clarifying Questions)
3. **여러 옵션을 고려하고** (Architecture)
4. **신중하게 구현하고** (Implementation)
5. **철저히 검토합니다** (Review)

### AI의 강점 활용하기

1. **병렬 처리** - 여러 관점을 동시에 탐색
2. **일관성** - 패턴을 놓치지 않음
3. **철저함** - 모든 파일, 모든 의존성 추적
4. **객관성** - 신뢰도 기반 필터링

### 인간의 판단 존중하기

1. **6개의 체크포인트**
2. **명시적 승인 요구**
3. **옵션 제공, 강요하지 않음**
4. **투명한 추론 과정**

---

## 부록: 파일 위치 참조

```
/home/user/claude-code/plugins/feature-dev/
├── .claude-plugin/
│   └── plugin.json ────────────────→ 플러그인 메타데이터
├── commands/
│   └── feature-dev.md ─────────────→ 메인 오케스트레이터
│                                     (7단계 워크플로우)
└── agents/
    ├── code-explorer.md ───────────→ 노란색 탐험가
    │                                 (4단계 분석 프로세스)
    ├── code-architect.md ──────────→ 초록색 건축가
    │                                 (3단계 설계 프로세스)
    └── code-reviewer.md ───────────→ 빨간색 검토자
                                      (신뢰도 기반 검증)
```

---

## 에필로그의 에필로그: 메타 여정

이 이야기 자체가 feature-dev의 원칙을 따랐습니다:

1. **Discovery**: Claude Code 프로젝트 이해
2. **Exploration**: feature-dev 플러그인 탐색 (Explore agent 사용)
3. **Clarifying**: 어떤 내용을 담을지 결정
4. **Architecture**: 스토리텔링 구조 설계
5. **Implementation**: 마크다운 문서 작성
6. **Review**: (이제 당신이 리뷰 중입니다! 😊)
7. **Summary**: 이 문서

---

**끝.**

---

> 💭 **생각해볼 점:**
> feature-dev는 단순히 코드를 생성하는 것이 아니라,
> **어떻게 생각하고, 어떻게 결정하고, 어떻게 협업하는지**를
> 보여줍니다. 이것이 진정한 AI 협업의 미래일지도 모릅니다.

---

**작성 날짜:** 2025-11-10
**분석 대상:** Claude Code feature-dev 플러그인 v1.x
**작성자:** Claude (Sonnet 4.5) with 💙
