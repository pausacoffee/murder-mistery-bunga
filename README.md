# 머더 미스터리 GM 플랫폼

여러 머더 미스터리 게임을 정적 웹앱으로 운영하기 위한 GM 플랫폼입니다. TV/빔 화면에서 GM이 진행 보조 도구로 사용할 수 있도록 설계되어 있습니다.

## 실행 방법
1. `index.html`을 브라우저로 엽니다.
2. 좌우 화살표 버튼(또는 키보드 좌우키)으로 페이지를 이동합니다.

## 현재 구성
- 카탈로그 기반 게임 검색
- 게임별 독립 패키지 로딩
- 현재 샘플 게임: `분가`

## 핵심 기능
- 슬라이드 네비게이션 (버튼/키보드/스와이프)
- 다중 타이머 위젯 (시작/일시정지, ±1분, 종료 오버레이)
- 규칙 팝업 (탭형 + 페이지별 `i` 버튼 연결)
- 파트 전환 확인 모달
  - 이야기 카드 A 공개 확인 -> 파트 2 진입
  - 이야기 카드 B 공개 확인 -> 파트 3 진입

## 타이머 사용 방법
기본 타이머는 아래처럼 사용합니다.

```html
<div class="timer-widget" data-timer-widget data-initial-seconds="180">
```

- `data-initial-seconds`: 기본 시간(초)

플레이어별 타이머는 아래처럼 사용합니다.

```html
<div
  class="timer-widget"
  data-timer-widget
  data-timer-type="per-player"
  data-player-count="6"
  data-initial-seconds="60"
>
```

- `data-timer-type="per-player"`: 플레이어별 탭 타이머 활성화
- `data-player-count`: 생성할 플레이어 탭 수
- `data-initial-seconds`: 각 플레이어에게 동일하게 적용할 기본 시간(초)
- 선택된 플레이어 탭은 검은 글자, 종료된 플레이어 탭은 회색 글자로 표시됩니다.
- 현재 플레이어 시간이 끝나면 해당 탭은 종료 상태가 되고, 다음 남은 플레이어 탭으로 자동 이동합니다.

## 문서
- [GM 운영 가이드](docs/GM-PLAYBOOK.md)
- [규칙 팝업 매핑](docs/RULES-MAPPING.md)
- [문구/표기 가이드](docs/UI-WRITING-GUIDE.md)

## 파일 구조
- `data/catalog.json`: 검색용 게임 카탈로그
- `games/<id>/game.json`: 게임 실행 패키지 엔트리
- `games/<id>/slides.html`: 현재 슬라이드 본문
- `index.html`: 뷰/모달 마크업
- `styles.css`: 카탈로그/슬라이드 스타일
- `app.js`: 카탈로그/게임 로더, 슬라이드/타이머/모달 로직

## 패키지 작성 원칙
- 카탈로그에는 검색과 프리뷰에 필요한 최소 정보만 둡니다.
- 게임 실행 데이터는 각 `games/<id>/` 폴더 아래에 둡니다.
- 현재는 `slides.html` 기반이지만, 신규 게임은 장기적으로 `slides.json` 기반 전환을 목표로 합니다.
