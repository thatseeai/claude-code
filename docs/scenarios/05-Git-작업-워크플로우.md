# 시나리오 5: 완벽한 배포 - Git 작업 워크플로우

## 프롤로그: 완성된 코드

수진은 하루 종일 작업한 새로운 기능을 완성했다. "다크 모드" 기능이었다. 10개의 파일을 수정하고, 3개의 새 파일을 만들었다. 이제 이 변경사항을 커밋하고, 푸시하고, Pull Request를 만들어야 했다.

예전 같았으면 수동으로 `git add`, `git commit`, `git push`, 그리고 GitHub 웹사이트에서 PR을 만들었을 것이다. 하지만 이번에는 Claude Code에게 맡겨보기로 했다.

```
> /commit-push-pr
```

Enter 키를 누르는 순간, Claude Code의 Git 워크플로우가 시작되었다.

## 제1막: 상황 파악 (Situation Assessment)

### 장면 1: /commit-push-pr 명령어의 활성화

**파일**: `plugins/commit-commands/commands/commit-push-pr.md`

명령어가 로드되면서, YAML 프론트매터를 확인했다:

```yaml
---
name: commit-push-pr
description: Commit, push, and open a PR
allowed-tools:
  - Bash(git checkout --branch:*)
  - Bash(git add:*)
  - Bash(git status:*)
  - Bash(git push:*)
  - Bash(git commit:*)
  - Bash(gh pr create:*)
---
```

**도구 제한 확인:**
```
허용된 도구:
✓ git checkout (브랜치 전환)
✓ git add (스테이징)
✓ git status (상태 확인)
✓ git commit (커밋)
✓ git push (푸시)
✓ gh pr create (PR 생성)

금지된 도구:
✗ Read, Write, Edit (파일 읽기/쓰기)
✗ git reset --hard (위험한 명령어)
✗ git push --force (강제 푸시)
```

이 제한은 명령어가 Git 작업에만 집중하도록 보장했다.

### 장면 2: 병렬 정보 수집

Claude는 현재 상황을 파악하기 위해 3개의 Git 명령어를 동시에 실행했다:

```
[단일 메시지로 3개 Bash 도구 호출]

Bash 1: git status
Bash 2: git diff
Bash 3: git log -5 --oneline
```

**결과 1: git status**
```bash
$ git status

On branch feature/dark-mode
Changes not staged for commit:
  modified:   src/components/ThemeProvider.tsx
  modified:   src/styles/theme.ts
  modified:   src/components/Header.tsx
  modified:   src/components/Sidebar.tsx
  modified:   src/utils/storage.ts
  modified:   package.json
  modified:   README.md
  modified:   src/hooks/useTheme.ts

Untracked files:
  src/components/ThemeSwitcher.tsx
  src/components/DarkModeToggle.tsx
  src/contexts/ThemeContext.tsx

no changes added to commit
```

**결과 2: git diff (일부)**
```diff
$ git diff

diff --git a/src/components/ThemeProvider.tsx b/src/components/ThemeProvider.tsx
index 3a5f2c1..8b9e4d2 100644
--- a/src/components/ThemeProvider.tsx
+++ b/src/components/ThemeProvider.tsx
@@ -1,10 +1,25 @@
 import React from 'react';
+import { ThemeContext } from '../contexts/ThemeContext';
+import { lightTheme, darkTheme } from '../styles/theme';

 export const ThemeProvider: React.FC = ({ children }) => {
+  const [isDark, setIsDark] = useState(false);
+
+  useEffect(() => {
+    const saved = localStorage.getItem('theme');
+    if (saved) setIsDark(saved === 'dark');
+  }, []);
+
   return (
-    <div>
+    <ThemeContext.Provider value={{ isDark, toggleTheme }}>
+      <ThemeWrapper isDark={isDark}>
+        {children}
+      </ThemeWrapper>
+    </ThemeContext.Provider>
-    </div>
   );
 };
...
```

**결과 3: git log**
```bash
$ git log -5 --oneline

a3f5b92 Add user profile page
7d2e8c4 Fix authentication bug
b1c9f5a Update dependencies
5e3a2d1 Refactor API endpoints
9f8d7c2 Add unit tests for auth
```

### 장면 3: 커밋 메시지 스타일 학습

Claude는 최근 커밋 메시지들을 분석했다:

```
[커밋 메시지 패턴 분석]

관찰된 패턴:
- "Add ..." : 새로운 기능 추가
- "Fix ..." : 버그 수정
- "Update ..." : 기존 기능 개선
- "Refactor ..." : 코드 리팩토링

스타일:
- 명령형 (Imperative mood)
- 첫 글자 대문자
- 마침표 없음
- 간결함 (50자 이하)

→ 이 스타일을 따르겠음
```

## 제2막: 커밋 메시지 작성 (Commit Message Crafting)

### 장면 4: 변경사항 분석

Claude는 git diff의 내용을 면밀히 분석했다:

```
[분석 결과]

수정된 파일 (8개):
1. src/components/ThemeProvider.tsx
   → 다크/라이트 테마 전환 기능 추가

2. src/styles/theme.ts
   → darkTheme 객체 정의 추가

3. src/components/Header.tsx
   → 테마 토글 버튼 추가

4. src/hooks/useTheme.ts
   → 테마 상태 관리 훅

5. src/utils/storage.ts
   → 테마 설정 localStorage 저장

6-8. package.json, README.md 등
   → 문서 및 의존성 업데이트

신규 파일 (3개):
1. src/components/ThemeSwitcher.tsx
2. src/components/DarkModeToggle.tsx
3. src/contexts/ThemeContext.tsx

종합:
→ 완전히 새로운 "다크 모드" 기능
→ "Add" 동사 사용 적절
→ 기존 기능 확장이 아닌 신규 기능
```

### 장면 5: 완벽한 커밋 메시지

Claude는 커밋 메시지를 작성했다:

```
제목: Add dark mode theme toggle

본문:
Implement comprehensive dark mode support with theme switching.

Features:
- ThemeContext for global theme state management
- ThemeSwitcher and DarkModeToggle components
- Persistent theme preference in localStorage
- Light and dark color schemes
- Smooth theme transitions

Updated components to support theme switching and
added theme toggle button in header.
```

**특징:**
- 제목은 50자 이하
- 명령형 동사 사용 ("Add")
- 본문은 "무엇을", "왜" 설명
- 기능 목록으로 구조화
- 프로젝트 스타일과 일치

## 제3막: 스테이징과 커밋 (Staging and Commit)

### 장면 6: 파일 스테이징

Claude는 변경된 파일들을 스테이징했다:

```bash
[Bash 도구 실행]

git add src/components/ThemeProvider.tsx && \
git add src/components/ThemeSwitcher.tsx && \
git add src/components/DarkModeToggle.tsx && \
git add src/components/Header.tsx && \
git add src/contexts/ThemeContext.tsx && \
git add src/styles/theme.ts && \
git add src/hooks/useTheme.ts && \
git add src/utils/storage.ts && \
git add package.json && \
git add README.md
```

**결과:**
```
10개 파일 스테이징 완료 ✓
```

### 장면 7: 커밋 생성

Claude는 커밋을 생성했다. 하지만 여기서 중요한 기술이 사용되었다: **HEREDOC**

```bash
[Bash 도구 실행]

git commit -m "$(cat <<'EOF'
Add dark mode theme toggle

Implement comprehensive dark mode support with theme switching.

Features:
- ThemeContext for global theme state management
- ThemeSwitcher and DarkModeToggle components
- Persistent theme preference in localStorage
- Light and dark color schemes
- Smooth theme transitions

Updated components to support theme switching and
added theme toggle button in header.
EOF
)"
```

**HEREDOC을 사용하는 이유:**
```
문제: 여러 줄 메시지를 셸에 안전하게 전달하기 어려움
   - 줄바꿈 처리
   - 따옴표 이스케이핑
   - 특수문자 처리

해결: HEREDOC 사용
   ✓ 여러 줄을 그대로 전달
   ✓ 이스케이핑 불필요
   ✓ 가독성 향상
   ✓ 안전성 보장
```

**결과:**
```bash
$ git commit -m "..."

[feature/dark-mode b4e7c2a] Add dark mode theme toggle
 10 files changed, 287 insertions(+), 42 deletions(-)
 create mode 100644 src/components/ThemeSwitcher.tsx
 create mode 100644 src/components/DarkModeToggle.tsx
 create mode 100644 src/contexts/ThemeContext.tsx
```

### 장면 8: Pre-commit Hook의 개입

커밋이 생성되는 순간, **Pre-commit Hook**이 작동했다!

```bash
[Pre-commit Hook 실행]

Running pre-commit hooks...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Linting...
   ✓ ESLint passed

2. Type checking...
   ✗ TypeScript found 2 errors:

   src/components/ThemeSwitcher.tsx:15:10
   Property 'theme' does not exist on type 'Props'

   src/hooks/useTheme.ts:8:5
   Type 'string' is not assignable to type 'Theme'

3. Formatting...
   Modified 3 files:
   - src/components/ThemeProvider.tsx
   - src/components/Header.tsx
   - src/styles/theme.ts

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Pre-commit hook failed!
Fix the errors and try again.
```

커밋이 실패했다! Pre-commit Hook이 타입 에러를 발견한 것이다.

### 장면 9: 타입 에러 수정

Claude는 당황하지 않았다. 에러를 확인하고 수정 방법을 안내했다:

```
Pre-commit hook에서 2개의 타입 에러가 발견되었습니다.

1. src/components/ThemeSwitcher.tsx:15:10
   문제: Props 타입에 'theme' 속성이 없음
   해결: Props 인터페이스에 theme 추가 필요

2. src/hooks/useTheme.ts:8:5
   문제: 'string' 타입을 'Theme' 타입에 할당 불가
   해결: 타입 캐스팅 또는 타입 가드 필요

이 에러들을 수정해주시겠어요? 제가 수정해드릴까요?
```

수진: "네, 수정해주세요."

Claude는 Edit 도구로 파일들을 수정했다. (이 명령어는 allowed-tools에 없지만, 사용자가 명시적으로 요청했으므로 예외로 처리)

수정 후, 다시 커밋을 시도했다.

### 장면 10: 두 번째 커밋 시도

```bash
[Bash 도구 실행]

git add src/components/ThemeSwitcher.tsx src/hooks/useTheme.ts && \
git commit --amend --no-edit
```

**Amend를 사용하는 이유:**
```
상황: Pre-commit hook이 파일을 수정함
옵션 1: 새로운 커밋 생성 → 커밋 히스토리 지저분
옵션 2: Amend로 기존 커밋 수정 ✓

Amend 사용 조건 확인:
✓ 커밋이 아직 push되지 않음
✓ 작성자가 나 (git log 확인)
✓ Hook에 의한 자동 수정임

→ Amend 사용 안전
```

**결과:**
```bash
[Pre-commit Hook 재실행]

Running pre-commit hooks...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Linting...
   ✓ ESLint passed

2. Type checking...
   ✓ TypeScript passed

3. Formatting...
   ✓ No changes needed

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
All checks passed! ✓

[feature/dark-mode b4e7c2a] Add dark mode theme toggle
 10 files changed, 289 insertions(+), 42 deletions(-)
 create mode 100644 src/components/ThemeSwitcher.tsx
 create mode 100644 src/components/DarkModeToggle.tsx
 create mode 100644 src/contexts/ThemeContext.tsx
```

커밋 성공!

## 제4막: 브랜치와 푸시 (Branch and Push)

### 장면 11: 브랜치 확인

```bash
[Bash 도구 실행]

git status
```

**결과:**
```bash
On branch feature/dark-mode
Your branch is ahead of 'origin/feature/dark-mode' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

좋다! 브랜치가 이미 존재하고, 원격 추적 중이다.

### 장면 12: 푸시 with 재시도 메커니즘

Claude는 네트워크 안정성을 고려하여 푸시를 시도했다:

```bash
[Bash 도구 실행]

git push -u origin feature/dark-mode
```

**첫 번째 시도:**
```bash
$ git push -u origin feature/dark-mode

Enumerating objects: 25, done.
Counting objects: 100% (25/25), done.
Delta compression using up to 8 threads
Compressing objects: 100% (15/15), done.
Writing objects: 100% (15/15), 3.24 KiB | 1.62 MiB/s, done.
Total 15 (delta 10), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (10/10), completed with 5 local objects.
To github.com:user/my-project.git
   a3f5b92..b4e7c2a  feature/dark-mode -> feature/dark-mode
Branch 'feature/dark-mode' set up to track remote branch 'feature/dark-mode' from 'origin'.
```

성공! 첫 시도에 푸시가 완료되었다.

**만약 실패했다면?**

Claude는 재시도 로직을 가지고 있었다:

```python
# 재시도 로직 (의사코드)

max_retries = 4
backoff_delays = [2, 4, 8, 16]  # 초

for attempt in range(max_retries):
    result = git_push()

    if result.success:
        break

    if attempt < max_retries - 1:
        delay = backoff_delays[attempt]
        print(f"Push 실패. {delay}초 후 재시도... ({attempt + 1}/{max_retries})")
        sleep(delay)
    else:
        print("최대 재시도 횟수 도달. 푸시 실패.")
```

**Exponential Backoff의 이유:**
```
네트워크 일시적 문제:
- 연결 타임아웃
- DNS 해석 실패
- GitHub API 제한

재시도 전략:
1차: 2초 대기 (일시적 문제 회복)
2차: 4초 대기 (조금 더 심각)
3차: 8초 대기 (네트워크 복구 대기)
4차: 16초 대기 (최후의 시도)

총 최대 대기: 30초
```

## 제5막: Pull Request 생성 (PR Creation)

### 장면 13: PR 컨텍스트 수집

PR을 만들기 전에, Claude는 전체 컨텍스트를 파악했다:

```bash
[Bash 도구 실행 - 병렬]

Bash 1: git log main..feature/dark-mode --oneline
Bash 2: git diff main...feature/dark-mode --stat
Bash 3: git log -1 --format='%B'
```

**결과 1: 브랜치의 모든 커밋**
```bash
$ git log main..feature/dark-mode --oneline

b4e7c2a Add dark mode theme toggle
```

한 개의 커밋만 있었다. 간단하다!

**결과 2: 변경 통계**
```bash
$ git diff main...feature/dark-mode --stat

 README.md                             |   5 +++
 package.json                          |   3 +-
 src/components/DarkModeToggle.tsx     |  45 +++++++++++++++
 src/components/Header.tsx             |  12 ++--
 src/components/ThemeProvider.tsx      |  38 ++++++++----
 src/components/ThemeSwitcher.tsx      |  67 ++++++++++++++++++++++
 src/contexts/ThemeContext.tsx         |  34 +++++++++++
 src/hooks/useTheme.ts                 |  28 +++++++++
 src/styles/theme.ts                   |  42 +++++++++++++-
 src/utils/storage.ts                  |  13 +++++
 10 files changed, 289 insertions(+), 42 deletions(-)
```

**결과 3: 최신 커밋 메시지**
```
Add dark mode theme toggle

Implement comprehensive dark mode support with theme switching.

Features:
- ThemeContext for global theme state management
- ThemeSwitcher and DarkModeToggle components
- Persistent theme preference in localStorage
- Light and dark color schemes
- Smooth theme transitions

Updated components to support theme switching and
added theme toggle button in header.
```

### 장면 14: PR 설명 작성

Claude는 모든 정보를 종합하여 PR 설명을 작성했다:

```markdown
## Summary

이 PR은 애플리케이션에 다크 모드 지원을 추가합니다.

### 주요 변경사항

- **ThemeContext 도입**: 전역 테마 상태 관리
- **테마 전환 컴포넌트**: ThemeSwitcher와 DarkModeToggle
- **영속성**: localStorage를 사용한 사용자 설정 저장
- **컬러 스킴**: 라이트/다크 모드용 완전한 색상 팔레트
- **부드러운 전환**: CSS 트랜지션으로 매끄러운 테마 변경

### 변경된 파일

- 신규 파일 3개: ThemeSwitcher, DarkModeToggle, ThemeContext
- 수정된 파일 7개: 기존 컴포넌트들에 테마 지원 추가

### 테스트 계획

- [ ] 라이트 모드에서 다크 모드로 전환 확인
- [ ] 다크 모드에서 라이트 모드로 전환 확인
- [ ] 페이지 새로고침 후 테마 설정 유지 확인
- [ ] 모든 컴포넌트가 두 테마에서 올바르게 렌더링되는지 확인
- [ ] 헤더의 토글 버튼 작동 확인

### 스크린샷

(테스트 후 스크린샷 추가 예정)
```

### 장면 15: GitHub CLI로 PR 생성

```bash
[Bash 도구 실행]

gh pr create \
  --title "Add dark mode theme toggle" \
  --body "$(cat <<'EOF'
## Summary

이 PR은 애플리케이션에 다크 모드 지원을 추가합니다.

### 주요 변경사항

- **ThemeContext 도입**: 전역 테마 상태 관리
- **테마 전환 컴포넌트**: ThemeSwitcher와 DarkModeToggle
- **영속성**: localStorage를 사용한 사용자 설정 저장
- **컬러 스킴**: 라이트/다크 모드용 완전한 색상 팔레트
- **부드러운 전환**: CSS 트랜지션으로 매끄러운 테마 변경

### 변경된 파일

- 신규 파일 3개: ThemeSwitcher, DarkModeToggle, ThemeContext
- 수정된 파일 7개: 기존 컴포넌트들에 테마 지원 추가

### 테스트 계획

- [ ] 라이트 모드에서 다크 모드로 전환 확인
- [ ] 다크 모드에서 라이트 모드로 전환 확인
- [ ] 페이지 새로고침 후 테마 설정 유지 확인
- [ ] 모든 컴포넌트가 두 테마에서 올바르게 렌더링되는지 확인
- [ ] 헤더의 토글 버튼 작동 확인

### 스크린샷

(테스트 후 스크린샷 추가 예정)
EOF
)" \
  --base main \
  --head feature/dark-mode
```

**HEREDOC 다시 사용:**

여러 줄의 복잡한 마크다운을 안전하게 전달하기 위해 HEREDOC 사용.

**결과:**
```bash
$ gh pr create ...

Creating pull request for feature/dark-mode into main in user/my-project

https://github.com/user/my-project/pull/142

✓ Pull Request created successfully!
```

## 제6막: 최종 검증 (Final Verification)

### 장면 16: Git 상태 재확인

모든 작업이 끝난 후, Claude는 상태를 확인했다:

```bash
[Bash 도구 실행]

git status
```

**결과:**
```bash
$ git status

On branch feature/dark-mode
Your branch is up to date with 'origin/feature/dark-mode'.

nothing to commit, working tree clean
```

완벽하다!

### 장면 17: 최종 보고

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Git 워크플로우 완료!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✓ 파일 스테이징: 10개 파일
✓ 커밋 생성: b4e7c2a "Add dark mode theme toggle"
✓ Pre-commit Hook: 통과 (타입 에러 수정 포함)
✓ 푸시 완료: origin/feature/dark-mode
✓ PR 생성: #142

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Pull Request URL:
https://github.com/user/my-project/pull/142

다음 단계:
1. PR 검토 요청 (팀원에게 알림)
2. CI/CD 파이프라인 확인
3. 리뷰어 피드백 대응
4. 승인 후 머지

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## 에필로그: 완벽한 자동화

### 장면 18: 수진의 만족

수진은 PR 링크를 클릭했다. GitHub 페이지가 열렸고, 완벽하게 작성된 PR이 보였다:

- ✓ 명확한 제목
- ✓ 상세한 설명
- ✓ 체크리스트
- ✓ 변경 통계
- ✓ 깨끗한 커밋 히스토리

```
수진의 생각:

"수동으로 했다면?"
→ git add 명령어 10번
→ git commit 작성 (5분)
→ git push
→ GitHub 웹사이트 열기
→ PR 양식 작성 (10분)
→ 총 15분 이상

"Claude Code로?"
→ /commit-push-pr 입력
→ 타입 에러 수정 승인
→ 총 2분 (대부분 자동)

"절약된 시간"
→ 13분
→ 정신적 부담 감소
→ 실수 가능성 제거
```

### 장면 19: Git 워크플로우의 핵심

이 전체 과정에서 중요한 것들:

```
1. 안전성 (Safety)
   ✓ Pre-commit Hook으로 코드 품질 보장
   ✓ allowed-tools로 위험한 명령어 제한
   ✓ Amend 사용 전 조건 확인

2. 지능성 (Intelligence)
   ✓ 커밋 메시지 스타일 학습
   ✓ 변경사항 분석 및 요약
   ✓ 적절한 PR 설명 생성

3. 견고성 (Robustness)
   ✓ 네트워크 실패 시 재시도
   ✓ Exponential backoff
   ✓ 에러 처리 및 복구

4. 효율성 (Efficiency)
   ✓ 병렬 명령어 실행
   ✓ 불필요한 단계 제거
   ✓ 사용자 시간 절약

5. 사용자 경험 (UX)
   ✓ 명확한 진행상황 표시
   ✓ 에러 발생 시 친절한 안내
   ✓ 최종 결과 요약
```

## 기술적 세부사항

### Git 명령어 실행 순서

```
Phase 1: 정보 수집 (병렬)
    ├─ git status
    ├─ git diff
    └─ git log -5 --oneline

Phase 2: 스테이징과 커밋
    ├─ git add [files...]
    ├─ git commit -m "..."
    ├─ [Pre-commit Hook 실행]
    ├─ [Hook 실패 시]
    │   ├─ 파일 수정
    │   └─ git commit --amend --no-edit
    └─ [Hook 성공]

Phase 3: 푸시
    └─ git push -u origin [branch]
        ├─ 재시도 1 (2초 대기)
        ├─ 재시도 2 (4초 대기)
        ├─ 재시도 3 (8초 대기)
        └─ 재시도 4 (16초 대기)

Phase 4: PR 생성 컨텍스트 수집 (병렬)
    ├─ git log main..[branch] --oneline
    ├─ git diff main...[branch] --stat
    └─ git log -1 --format='%B'

Phase 5: PR 생성
    └─ gh pr create --title "..." --body "..." --base main --head [branch]

Phase 6: 최종 검증
    └─ git status
```

### HEREDOC 사용 패턴

```bash
# ✓ 올바른 방법: HEREDOC 사용
git commit -m "$(cat <<'EOF'
여러 줄의
커밋 메시지
특수문자 "포함" 가능
EOF
)"

# ✗ 잘못된 방법: 직접 문자열
git commit -m "여러 줄의\n커밋 메시지\n문제 발생"
```

### Pre-commit Hook 처리

```
커밋 시도
    ↓
Pre-commit Hook 실행
    ├─ Linting (ESLint)
    ├─ Type checking (TypeScript)
    └─ Formatting (Prettier)
    ↓
Hook 결과
    ├─ 성공 → 커밋 완료
    │
    └─ 실패 → 커밋 취소
        ├─ 에러 메시지 표시
        ├─ 수정된 파일이 있다면
        │   ├─ git add [modified files]
        │   └─ git commit --amend --no-edit
        └─ 에러만 있다면
            └─ 사용자에게 수정 요청
```

### Amend 안전성 체크

```python
def is_safe_to_amend():
    # 1. 커밋이 이미 푸시되었는지 확인
    result = git("log origin/[branch]..[branch] --oneline")
    if not result:
        return False  # 이미 푸시됨, amend 위험

    # 2. 커밋 작성자가 현재 사용자인지 확인
    author = git("log -1 --format='%an %ae'")
    current_user = git("config user.name") + " " + git("config user.email")
    if author != current_user:
        return False  # 다른 사람의 커밋, amend 금지

    # 3. Pre-commit hook에 의한 자동 수정인지 확인
    # (이 경우 amend가 적절함)

    return True
```

### Exponential Backoff 구현

```python
import time

def push_with_retry(branch, max_retries=4):
    backoff_delays = [2, 4, 8, 16]

    for attempt in range(max_retries):
        result = execute_git_push(branch)

        if result.success:
            print(f"✓ Push successful on attempt {attempt + 1}")
            return True

        if attempt < max_retries - 1:
            delay = backoff_delays[attempt]
            print(f"⚠️  Push failed. Retrying in {delay}s... ({attempt + 1}/{max_retries})")
            time.sleep(delay)
        else:
            print(f"✗ Push failed after {max_retries} attempts")
            return False

    return False
```

### GitHub CLI PR 생성

```bash
gh pr create \
  --title "제목" \
  --body "본문 (HEREDOC 사용)" \
  --base main \
  --head feature-branch \
  --assignee @me \
  --reviewer team-member \
  --label enhancement \
  --draft  # 선택사항: 드래프트 PR
```

### 관련 파일

| 컴포넌트 | 파일 경로 |
|---------|----------|
| Commit-Push-PR 명령어 | `plugins/commit-commands/commands/commit-push-pr.md` |
| Commit 명령어 | `plugins/commit-commands/commands/commit.md` |
| allowed-tools 정의 | 명령어 YAML frontmatter |

### 핵심 개념

1. **allowed-tools**: 명령어가 사용할 수 있는 도구 제한
2. **HEREDOC**: 여러 줄 텍스트를 안전하게 셸에 전달
3. **Pre-commit Hook**: 커밋 전 자동 검증
4. **Commit Amend**: Hook 수정사항을 기존 커밋에 반영
5. **Exponential Backoff**: 네트워크 실패 시 재시도 전략
6. **Parallel Git Commands**: 독립적인 Git 명령어 동시 실행
7. **Commit Message Learning**: 프로젝트 스타일 학습 및 적용

---

이것이 Claude Code의 Git 워크플로우다. 단순한 자동화가 아니라, **지능적인 자동화**다.

커밋 메시지를 작성할 때는 프로젝트의 스타일을 학습한다.
에러가 발생하면 자동으로 수정하고 재시도한다.
네트워크가 불안정하면 인내심 있게 재시도한다.
PR 설명은 변경사항을 완벽히 분석하여 작성한다.

이 모든 것이 `/commit-push-pr` 한 줄로 시작된다.

이것이 바로 개발자가 코드 작성에 집중할 수 있도록 하는, Claude Code의 철학이다.
