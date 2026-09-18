# WORKLOG

## 2026-09-18

### 작업 목적

실제 개발 저장소와 원본 참고 저장소를 명확히 구분하고 세션 간 작업 기록 체계를 추가한다.

### 작업 기준

- 실제 작업: ryujmin97/v1 / ryu-v1
- 원본 참고: ryujmin97/openpilot / carrot-ryu-v1

### 변경 파일

- PROJECT_GUIDELINES.md
- docs/WORKLOG.md

### 주요 변경 내용

- 실제 작업 저장소와 원본 참고 저장소를 명확히 구분
- 개발 및 안전 관련 기본 원칙 정의
- 변경 후 검증 및 Git 작업 원칙 정의
- 세션 간 인수인계를 위한 WORKLOG 규칙 정의

### 테스트 및 결과

- 문서 생성 후 git diff --check 확인 예정
- 코드 기능 변경 없음

### 발생한 문제

- 최초 heredoc 입력이 완료되지 않음
- git config 명령 입력 과정에서 오타 발생

### 미해결 사항

- 문서 commit 및 push 필요

### 다음 작업

1. 문서 확인
2. git diff --check
3. commit
4. push
5. 최종 git status 확인

## 2026-09-19

### 작업 목적

우측 경로 안내의 교통정보 배지 내부에 `sdi_descr` 텍스트(예: `과속방지턱`)가 배지 안에 정상적으로 들어가도록 위치를 수정한다.

### 변경 파일

- openpilot/selfdrive/ui/onroad/hud_renderer.py
- docs/WORKLOG.md

### 주요 변경 내용

- `sdi_descr` 배지 높이를 텍스트 높이 기준으로 여유 있게 계산
- `left_bottom` 정렬 기준 baseline을 배지의 세로 중앙에 맞춰 텍스트가 배지 내부에 표시되도록 수정
- 기존 배지의 좌우 위치와 회전 안내 레이아웃은 유지

### 테스트 및 결과

- GitHub 브랜치의 변경 코드 확인 완료
- 실제 차량/화면 렌더링 테스트는 아직 수행하지 않음

### 발생한 문제

- 기존 baseline(`badge_y + size.y + 2`)이 배지 높이와 맞지 않아 `과속방지턱` 텍스트가 배지 내부에 제대로 들어가지 않는 문제가 있었음

### 미해결 사항

- 실기기에서 배지 내부 수직 정렬과 주변 요소 간격 확인 필요

### 다음 작업

1. 실기기/렌더링 화면에서 `과속방지턱` 표시 확인
2. 필요하면 badge padding 및 y 위치 미세 조정
3. 관련 UI 변경에 대한 diff/test 검증


### 추가 수정 — 2026-09-19

실차 스크린샷에서 이전 baseline 보정이 실제 렌더링의 텍스트 위치 문제를 해결하지 못한 것을 확인했다. left_bottom 대신 left_center 정렬을 사용하고 draw_text_ui_style의 6px y_offset을 보정하여 배지 중앙에 텍스트를 직접 배치하도록 수정했다.

- v1 커밋: d5c91ab0
- 실제 렌더링 테스트: 미실행
