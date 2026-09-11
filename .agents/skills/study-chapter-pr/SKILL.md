---
name: study-chapter-pr
description: >-
  Commits study chapter notes (single or multiple md files, folders) and opens a pull request for this repository.
  Use whenever the user asks to commit chapter summaries, push study notes,
  create a branch like 0N주차/이름, or open a PR for 주차/챕터 정리 — even if they
  only say "올려줘", "PR 만들어줘", or mention files under 0N주차/* or N주차/*.
---

# Study Chapter PR

이 저장소의 스터디 정리 파일(단일 md 파일, 복수 md 파일 또는 폴더 형태)을 브랜치에 커밋하고 `main`으로 Pull Request를 생성한다. 파일 개수에는 제한이 없다.

## When to use

- `0N주차/<이름>.md`, `0N주차/<이름>_*.md`, 또는 `0N주차/<이름>/` 하위 정리본들을 커밋·푸시·PR 할 때
- 브랜치명 `0N주차/<이름>` 패턴으로 올리라고 요청할 때
- 주차별 스터디 노트 / 면접 Q&A 정리 PR 요청일 때

## Preconditions

- `gh` CLI로 이 저장소에 접근 권한이 있어야 한다.
- 커밋은 사용자가 명시적으로 요청했거나 스터디 정리 발행 요청일 때만 진행한다.
- `.DS_Store`, 임시 파일 등 스터디 노트와 무관한 파일은 절대 스테이징하지 않는다.

## Workflow

### 1. 대상 주차 및 작성자 파악

대상 경로 또는 변경사항에서 주차 번호와 작성자를 추출한다.

- 지원 경로 형태:
  - 단일 파일: `0N주차/<이름>.md` (예: `01주차/이만재.md`)
  - 복수 파일: `0N주차/<이름>_*.md` (예: `01주차/이만재_1장.md`, `01주차/이만재_2장.md`)
  - 폴더 형태: `0N주차/<이름>/**` (예: `01주차/이만재/1장.md`, `01주차/이만재/2장.md`)
- 만약 사용자가 `1주차/...`처럼 한 자리 숫자로 입력하더라도 레포지토리의 `01주차/...` 포맷을 우선 확인하고 통일한다.
- 챕터/주제 제목은 다음 우선순위로 결정한다:
  1. 사용자가 직접 언급한 주제
  2. 작성된 md 파일 상단의 `# 제목` 헤딩
  3. `README.md` 로드맵에 기재된 주제 (있는 경우)
  4. 알 수 없으면 `[이름] 0N주차 정리` 기본형 사용

### 2. 브랜치 생성 및 동기화

`main`을 최신 상태로 갱신한 뒤 주차별 브랜치를 생성한다.

```bash
git checkout main
git pull --ff-only origin main
git checkout -b "0N주차/<이름>"
```

이미 존재하는 로컬/원격 브랜치라면 해당 브랜치로 체크아웃하여 작업을 진행한다.

### 3. 스테이징과 커밋

해당 주차/작성자의 스터디 관련 파일들(단일/복수 md 파일, 이미지 등)을 스테이징한다.

```bash
# 파일 형태에 맞춰 스테이징 (예시)
git add "0N주차/<이름>.md" 2>/dev/null || true
git add "0N주차/<이름>"* 2>/dev/null || true

git commit -m "0N주차 <이름> 정리 추가"
```

### 4. 원격 푸시

```bash
git push -u origin HEAD
```

### 5. PR 생성

PR 제목 규칙: `[이름] 0N주차: <선정 주제 또는 챕터>`  
(예: `[이만재] 01주차: 1장 HTML과 웹 기본 구조`)

```bash
gh pr create --base main --title "[이름] 0N주차: 챕터 주제" --body "$(cat <<'EOF'
## 📌 Summary
- **주차**: 0N주차
- **작성자**: <이름>
- **정리 파일**: `0N주차/<이름>...`

## 💡 주요 다룬 내용
- 

## 💬 토론 & 질문 포인트
- 

---
> *스터디 세션 전까지 상호 리뷰 및 코멘트 환영합니다!*
EOF
)"
```

### 6. 완료 보고

생성된 PR URL을 사용자에게 제공하고, 정상적으로 스터디 정리 파일들이 포함되었는지 확인한다.

## Done criteria

- 원격에 `0N주차/<이름>` 브랜치가 생성되어 푸시되었다.
- `main` ← `0N주차/<이름>` PR이 열려 있고 URL을 사용자에게 안내했다.
- PR 변경사항에 오직 스터디 노트 및 관련 리소스 파일만 포함되었다.

