# AI Agent Guidelines for Kusitms-DeepDive

이 저장소는 《Do it! AI 시대에 살아남는 프런트엔드 면접의 기술》 스터디 저장소입니다.

## 에이전트 스킬

- `study-chapter-pr`: 스터디원이 주차별 정리 파일(`N주차/<이름>.md`)을 올리거나 "PR 만들어줘", "1주차 정리 올려줘"라고 요청할 때 자동으로 브랜치를 따고 커밋·푸시 및 PR을 생성합니다.
- 상세 워크플로우: `.agents/skills/study-chapter-pr/SKILL.md`

## 규칙

- 모든 브랜치명은 `N주차/<이름>` 형식으로 생성합니다.
- PR 대상 브랜치는 항상 `main`입니다.
- 스터디 노트 이외의 불필요한 설정 파일이나 임시 파일은 스테이징하지 않습니다.
