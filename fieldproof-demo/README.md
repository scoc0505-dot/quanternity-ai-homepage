# Handoff: FieldProof — 30초 프로덕트 데모 필름

## Overview

FieldProof는 퀀터니티에이아이(Quanternity AI)가 개발 중인 심사 워크플로우·증적 관리 SaaS입니다.
이 프로덕트를 소개하는 **30초 세로 스크립트 영상 (1920×1080, 브라우저 기반 애니메이션)** 의 디자인 참조 자료입니다.

영상의 목적: 처음 방문한 정보보호 담당자·품질책임자·법무 임원에게 다음 세 가지를 5개 컷에 걸쳐 증명합니다.
- 인증 컨설팅 견적서들이 서로 유사해서 담당자가 차별화를 느끼지 못한다는 문제 제기
- FieldProof는 "AI가 조항을 제안하고, 담당자가 승인"하는 원칙으로 심사 현장에서 증적을 남긴다
- 인증서 발급 이후의 정기심사 관리까지 하나의 원장에서 이어진다

**최종 목표**: 브라우저 기반 30초 재생 → 화면 녹화 도구로 mp4 추출 → 웹사이트/영업 자료/전시회 배너 등에 재활용.

---

## About the Design Files

이 번들의 HTML 파일은 **디자인 참조(레퍼런스)** 입니다 — 최종 룩앤필과 애니메이션 타이밍을 보여주는 프로토타입이며, 그대로 프로덕션에 넣는 코드가 아닙니다.

**개발자의 임무**: 이 HTML 디자인을 **타깃 코드베이스의 기존 환경** (React·Vue·Next.js·Astro·SwiftUI 등) 에 맞게 다시 구현하십시오. 코드베이스에 확립된 컴포넌트 라이브러리, 상태 관리 패턴, 애니메이션 라이브러리(GSAP·Framer Motion·Anime.js·Motion One 등)를 사용해 이 디자인을 재현합니다.

만약 신규 프로젝트라 프레임워크가 정해져있지 않다면 다음을 권장합니다.
- **React + Framer Motion** — 상태 기반 씬 전환, 각 컷을 독립 컴포넌트로 관리
- **Astro + CSS/JS 그대로** — 랜딩 페이지 임베드가 목적이면 정적 사이트 생성기가 가벼움
- **Remotion (React 기반 영상 렌더링)** — mp4 서버사이드 렌더링이 목표라면

이 HTML을 그대로 iframe으로 임베드해서 재생 후 화면 녹화하는 것도 유효한 딜리버리 경로입니다. 그 경우 별도 리팩터링 없이 이 파일을 사용하시면 됩니다.

---

## Fidelity

**High-fidelity (hifi)** — 최종 컬러, 타이포그래피, 스페이싱, 애니메이션 타이밍이 모두 확정된 픽셀-퍼펙트 목업입니다. 개발자는 이 디자인을 픽셀 단위까지 재현해야 합니다.

- 컬러: 퀀터니티에이아이 institutional B2B 디자인 시스템 (Deep Ink Navy #0B1220 + Signal Blue #0B3D91)
- 타이포그래피: Pretendard (300–700) + JetBrains Mono
- 스페이싱: 8px 그리드
- 반경: 최대 6px (institutional 톤)
- 애니메이션: cubic-bezier(0.2, 0, 0, 1) 이징 하나로 통일, 페이드 200ms 기본

---

## 무대 (Stage) 사양

- **캔버스**: 1920×1080px (16:9)
- **스케일링**: `#stage`는 고정 크기이며 부모(`#wrap`) 안에서 `transform: translate(-50%, -50%) scale(s)` 로 letterbox 스케일링. `s = min(vpw/1920, vph/1080)`.
- **배경**: `--gray-25` (#FBFAF7 오프화이트) — letterbox 여백 포함
- **길이**: 총 30.0초
- **컨트롤**: 재생/일시정지, 리셋(⟲), 스크럽 바, 스페이스/화살표/R 키보드 단축키
- **저장**: `localStorage["fieldproof-demo-v2-t"]` 에 재생 위치를 초 단위로 저장, 새로고침 후 이어보기

---

## 씬 (Scenes) — 5개 컷 + 엔드카드

씬은 `display: none / block` 토글로 전환 (opacity transition은 iframe timeline 이슈로 사용하지 않음 — 반드시 이 패턴 유지).

각 씬의 시간 배정:

| # | 씬 id | 시작 | 길이 | 이름 |
|---|---|---|---|---|
| 1 | `#cut1` | 0.0s | 5.0s | 견적서 3장 (문제 제기) |
| 2 | `#cut2` | 5.0s | 5.0s | 5구간 준비 프로그램 타임라인 |
| 3 | `#cut3` | 10.0s | 8.0s | **핵심 8초** — 현장 스마트폰 + AI 제안 → 담당자 확정 → 감사로그 |
| 4 | `#cut4` | 18.0s | 6.0s | SOP 12대 절차서 (8 운영중 · 4 미운영) |
| 5 | `#cut5` | 24.0s | 4.0s | 인증서 + D-85 정기심사 카운트다운 |
| — | `#endc` | 28.0s | 2.0s | 엔드카드 (다크 잉크, 로고 + 태그라인 + 3열 메타) |

### 씬 1 (0–5s) · 견적서 3장

**목적**: "인증 컨설팅 견적은 대부분 비슷해 보입니다" 문제 제기.

**레이아웃**:
- 좌측 (좌 128px 여백, 상 200px): 오버라인 "§ 문제 인식" + H1 "이 업체들, 뭐가 다르죠?" (64px, weight 600)
- 우측 (우 96px 여백, 상 200px): 3장의 견적 카드가 겹쳐서 부채꼴로 나열
  - 각 카드 340×620px, 24px 갭
  - 카드별 회전: q1 −3°, q2 +1° (약간 위로 튀어나옴, z-index 2), q3 +2.5°
  - 카드 진입 애니메이션: 0.3s → q1, 0.9s → q2, 1.5s → q3 (translateY 30px → 0, 380ms cubic-bezier)

**각 견적 카드 구성** (`<div class="qc q1/q2/q3">`):
1. 상단 메타: `QUOTATION` · `Q-2026-041` (mono 11px, letter-spacing 0.14em)
2. 제목 (24px, weight 600): "ISO/IEC 42001 인증 컨설팅" / "AI 경영시스템 구축 컨설팅" / "ISO 42001 인증 대응 프로젝트"
3. 벤더명 (mono 13px, fg-3): "A 컨설팅 그룹" / "B 어드바이저리" / "C 파트너스"
4. 라인 아이템 5행 (dashed border-bottom, 라벨 좌 · 금액 우 mono)
5. 합계 (mono 26px, tabular-nums): 42,000,000 / 43,000,000 / 42,000,000 원
6. 우하단 스탬프 "SUBMITTED" (회색 테두리, −8° 회전)

**포인트**: 3장 모두 금액이 42–43M 원으로 비슷하고 항목도 유사 → 시각적으로 "차별화 안 됨"이 즉시 읽힘.

### 씬 2 (5–10s) · 5구간 타임라인

**목적**: FieldProof의 준비 프로그램이 "하나의 화면에" 5구간을 모두 남긴다.

**레이아웃** (padding: 220px 128px 260px):
- 오버라인 (mono 13px, 5.1s): "FIELDPROOF · 준비 프로그램"
- H1 (48px, 5.35s): "현황진단부터 심사대응까지, 다섯 구간이 [하나의 화면에] 남습니다."
  - `[하나의 화면에]` 는 `<span class="kw">` — 하단 32% Signal Blue #E4ECF9 배경 라이트하이라이트
- 우상단 노트 (mono 12px, dashed border, 6.0s): "날짜·주차 표기 없음 · 인증 취득을 보장하지 않습니다"
- 하단 트랙 (2px, --gray-150):
  - 검은 진행 채움 5.5s에서 시작해 3.0s 동안 0 → 100%
  - 5개 스텝: 0.6s / 1.15s / 1.7s / 2.25s / 2.8s 마다 순차 등장 (translateY 6px → 0)
  - 각 스텝: 번호 (mono 13px), 이름 (32px weight 600), 조항 (mono 13px fg-3)
  - 스텝의 dot: 미도착 시 회색 링, 도착 시 검은 채움

**5개 스텝 데이터**:
| # | 번호 | 이름 | 조항 |
|---|---|---|---|
| 1 | 01 | 현황진단 | § 4 · Gap 분석 |
| 2 | 02 | 문서체계 | § 5–7 · 절차서 12종 |
| 3 | 03 | 운영·증적 | § 8 · A.6–A.10 |
| 4 | 04 | 내부심사 | § 9.1–9.2 |
| 5 | 05 | 심사대응 | § 9.3 · § 10 |

### 씬 3 (10–18s) · 스마트폰 현장 — **핵심 8초**

**목적 (요구사항)**: 4개 서브액션을 8초 안에 순차로 보여준다. 특히 14.5–16s 구간의 "담당자가 클릭해서 확정" 순간이 이 영상 전체에서 가장 중요한 1.5초. 이 동작이 없으면 "AI가 알아서 증적을 만든다"로 오독되어 심사 경험이 있는 결정권자의 신뢰를 잃음.

**레이아웃**: 좌측 720px = 폰 컬럼, 우측 = 감사로그 컬럼 (좌우 사이 1px hairline 세로 divider).

#### 좌측 · 스마트폰 (`#cut3 .phone`)

- 크기 440×900px, radius 56px, dark ink #0A0F1C 바디, 노치(110×30px)
- 스크린 안 (radius 44px):
  1. **Status bar** (46px, mono 14px): "09:41" | 시그널바 SVG + "88%"
  2. **App top** (border-bottom): ← back + 타이틀 "현장 증적 · 서버룸 A동" + 서브 "SYS-01 · CARDIOVISION AI"
  3. **Photo frame** (border, radius 8px, flex:1): 서버룸을 CSS로 그린 faux 사진
     - 배경: 반복 세로 그라디언트 (짙은 블루/네이비 스트라이프)
     - 상단 레이어: 랜덤 위치의 방사형 그라디언트 (블루/청록 조명 얼룩)
     - 좌하단 태그 (mono 10px): "2026-08-14 · 09:41 · 37.5236°N 127.0455°E"
     - 중앙 focus target (20%×20%, 흰 테두리): 10.4s에 등장, scale 1.6 → 1
  4. **Capture button** (72×72px, 하단 중앙): 11.2s에 press 애니메이션 (scale 0.88, 140ms)
  5. **Suggest sheet** (bottom slide-up, radius 24 24 0 0): 12.2s에 등장, 14.9s에 사라짐
     - 그래버 바
     - Eyebrow (mono 11px): 파란 AI 도트 + "FIELDPROOF · AI 제안 · 담당자 확정 필요"
     - 헤딩 (16px, fg-2): "사진·위치·시간 기반으로 다음 조항이 매핑됩니다."
     - **Clause chip**: 파란 테두리(#0B3D91), signal-50 배경(#F1F5FC)
       - 좌: 코드 `A.6.2.4` (mono 14px, 흰 배경 + 파란 테두리 박스)
       - 중: 설명 "AI 시스템 검증 · 물리적 환경 통제"
       - 우: 화살표 아이콘 (Lucide arrow-right)
  6. **Cursor SVG** (24×30px, 파란 화살표): 13.5s에 등장, 14.3s까지 (60, 780) → (220, 720) 로 이동, 14.45s에 chip press 애니메이션 트리거
  7. **Confirm toast** (하단 슬라이드업, ink-950 배경, 흰 텍스트): 15.0s에 등장, 17.9s에 사라짐
     - 초록 체크 아이콘 (24px 원, status-ok 배경)
     - 메시지 "A.6.2.4 조항에 증적이 확정되었습니다."
     - 서브 (mono 12px): "EVID-2026-0814-A · 감사로그 기록됨"

**타이밍 표 (컷 3 로컬 시간)**:
| lt | 동작 |
|---|---|
| 0.35–1.5 | Photo target pulse |
| 1.15–1.4 | Capture button press |
| 2.2–4.9 | Suggest sheet 슬라이드업/다운 |
| 3.5–5.4 | Cursor 등장/이동 |
| 4.45–4.63 | Chip press 애니메이션 |
| 5.0–7.9 | Confirm toast |
| 6.1 / 6.6 / 7.1 | 감사로그 3행 순차 등장 |

#### 우측 · 감사로그 (`#cut3 .logcol`)

- 좌 96px padding, 좌측에 1px hairline divider
- Eyebrow (mono 13px): "AUDIT LOG · 감사로그 · TENANT NORTHGATE"
- 타이틀 (38px weight 600): "모든 확정은 이 원장에 기록됩니다."
- 서브 (mono 15px, fg-3): "EVID → SOP → Baseline Diff"
- 로그 행 3개 (grid 100px / 140px / 1fr / auto):
  1. 09:38 | A.8.29 | "보안 로깅 정책 검토 · 배승우 정보보호팀장" | 확정
  2. 09:40 | A.7.4 | "학습데이터 출처 갱신 · 문세영 AI품질담당" | 확정
  3. 09:41 | A.6.2.4 | "AI 시스템 검증 · 물리 환경 · 강민석 CISO 승인" | 확정 **← 하이라이트 (signal-50 배경 + 좌측 3px signal-700 border)**
- 상태 뱃지 (mono 11px, status-ok bg): "확정"

### 씬 4 (18–24s) · SOP 12대 절차서

**목적**: 남은 문서와 담당자가 매일 보인다. "남은 것만" 보여주는 원칙.

**레이아웃** (padding: 160px 96px 200px):
- 헤더 (flex, 18.15s 등장):
  - 좌: 오버라인 "§ 문서체계 · 12대 절차서" + H2 "[남은 것]과, 그것을 맡을 사람이 매일 보입니다." (44px, kw 하이라이트)
  - 우: 3개 스탯 (좌측 1px border-left, 28px padding-left)
    - **8 / 12** — 운영중 · Active (of는 회색, 원본 크기의 절반)
    - **4** — 미운영 · Pending
    - **66.7 %** — 운영률
- 테이블 wrap (border, bg-surface, 18.5s 등장):
  - Head 6열: 문서(80px) · 조항(200px) · 제목 · 담당자(240px) · 최근 개정(180px) · 상태(140px)
  - 열 헤더 스타일: gray-50 배경, mono 12px, letter-spacing 0.14em, uppercase
  - 7개 행 데이터 (아래 표 참조)
  - 미운영 행은 `.pd` 클래스 → status-warn-bg (파스텔 노랑) 배경
- Highlight 프레임 (20.4s 등장): 절대 위치, 파란 3px border, 미운영 4개 행을 감쌈
  - 우상단 "MISSING · 4" 태그 (파란 배경, 흰 글자, mono 12px)

**SOP 행 데이터**:

| 문서 | 조항 | 제목 | 담당자 | 개정 | 상태 |
|---|---|---|---|---|---|
| SOP-06 | 7.2·7.3·7.4·7.5 | 역량·의사소통·문서관리 절차서 | 오하린 (인사·운영담당) | Rev. 1.0 · 2026-07-20 | 운영중 |
| SOP-07 | 8.2·A.6.2 | AI 시스템 수명주기 관리 절차서 | 유태경 (기술이사) | Rev. 1.1 · 2026-07-15 | 운영중 |
| SOP-08 | A.7·A.7.2·A.7.4 | AI 학습데이터 품질·출처 관리 절차서 | 문세영 (AI품질담당) | Rev. 1.0 · 2026-07-08 | 운영중 |
| SOP-09 | A.10·A.10.2·A.10.3 | 제3자·공급자 AI 관리 절차서 | 노가영 (구매·외주관리담당) | 미등록 · 초안 배정 필요 | **미운영** |
| SOP-10 | 9.1·9.2 | 성과 모니터링·내부심사 절차서 | 임도현 (내부심사 담당) | 미등록 · 초안 배정 필요 | **미운영** |
| SOP-11 | 9.3 | 경영검토 절차서 | 강민석 (CISO) | 미등록 · 초안 배정 필요 | **미운영** |
| SOP-12 | 10.1·10.2·A.10.4 | 부적합·시정조치 및 지속적 개선 절차서 | 배승우 (정보보호팀장) | 미등록 · 초안 배정 필요 | **미운영** |

### 씬 5 (24–28s) · 인증 개요 + D-85 카운트다운

**목적**: 인증서를 받은 다음날부터 다시 시작. 관리는 여기서부터.

**레이아웃** (padding 160px 96px 220px, grid 1fr 1fr, gap 64px):

#### 좌측 · 인증서 카드 (`.cert`, 24.2s 등장)

- 흰 배경, 1px hair border
- Eyebrow (mono 13px): "CERTIFICATE · 인증서 발행 완료"
- H3 (32px weight 600): "노스게이트 AI 시스템즈" / "ISO/IEC 42001"
- 상태 라인: 초록 pill "유효 · Handover Complete" + mono baseline "인정 인증기관 발행"
- 2×2 그리드 (mono 20px 값):
  - Baseline: 2026-05-02
  - Cert. Expiry: 2029-05-01
  - AI 시스템: 3 systems
  - Scheme: ISO/IEC 42001

#### 우측 · D-day 패널 (`.dday`, 24.4s 등장)

- Deep Ink Navy 배경, 8px 그리드 텍스처 (rgba 0.04 라인)
- Eyebrow (mono 13px, 옅음): "SURVEILLANCE · 정기심사까지"
- H3 (26px): "인증서를 받은 다음날부터 다시 시작됩니다."
- **카운트업 애니메이션**: 24.8s부터 1.2s 동안 0 → 85 (cubic ease-out)
  - "D −" (52px, 옅음) + **85** (mono 160px, tabular-nums, letter-spacing −0.04em)
- 서브: "Next Surveillance · 2026-11-14"
- Baseline Diff 3건:
  - #02 · AI 위험평가 임계점수 변경 · A.9.5.1 · HIGH (빨강 파스텔)
  - #01 · 보안 로깅 정책 v2.0 제정 · A.8.29 · MED (주황 파스텔)
  - #00 · Handover DB 무결성 검증 · 1,284건 · OK (초록 파스텔)

### 엔드카드 (28–30s) · `#endc`

- Deep Ink Navy 전체 배경, 8px 그리드 오버레이
- 로고 락업 (28.05s):
  - 방패 마크 SVG 72×72px (Lucide shield-check 기반)
  - 워드마크 "FieldProof" 96px weight 600 letter-spacing −0.035em
- **태그라인** (28.2s, 38px = 로고의 2/5):
  - "ISO 42001·27001 통제 항목과 조직관련 업무 산출물을 실시간 연결하는 증적 관리 플랫폼"
- 3열 메타 (28.44s, 1px 상단 divider):
  - **STANDARDS**: ISO/IEC 42001 / ISO/IEC 27001 / ISO 13485
  - **BY**: Quanternity AI + sm "퀀터니티에이아이"
  - **CONTACT**: quanternity.kr + sm "contact@qunternity.kr"

---

## 지속 표시 요소 (HUD)

**컷 2–5에서 항상 상단에 표시**, 컷 1과 엔드카드에서는 숨김:

- 좌: 방패 마크 SVG (32px) + "FieldProof" 이름 + "by Quanternity AI" 서브 (1px 좌측 divider)
- 중: **DEMO DATA 배지** (mono 12px, letter-spacing 0.14em, status-warn-bg #F7ECD4 배경, status-warn #8A5A00 텍스트, 좌측 깜빡이는 dot)
  - **필수**: 시드 JSON에서 "실제 고객사 데이터로 오인 방지" 목적으로 상시 노출 요구됨
- 우: "CUT ●●●●●" 인디케이터 (5개 도트, 현재까지 진행한 씬 수만큼 검게 채워짐)

**중요**: HUD는 `display: none/block !important` 토글로 표시. `opacity` transition은 iframe timeline 이슈로 stuck 됨 — 이 패턴을 반드시 유지.

---

## 자막 (Caption)

**위치**: 하단 (bottom 88px, left/right 64px). 컷 3에서는 폰이 좌측을 차지하므로 left를 850px로 밀어냄. 컷 4에서는 화면 헤딩 자체가 자막과 같은 메시지를 전달하므로 자막을 숨김. 엔드카드에서도 숨김.

**구조**:
- Eyebrow (mono 13px, letter-spacing 0.18em, uppercase, min-height 20px)
- Line A (48px weight 600, min-height 56px)
- Line B (48px weight 600, 12px margin-top) — 없는 경우 비움

**Signal Blue 강조**: `<strong>` 로 감싼 부분은 `color: --signal-700` + weight 700

**자막 타임라인**:

| at | eyebrow | line A | line B |
|---|---|---|---|
| 0.4 | CUT 01 · 문제 인식 | 이 업체들, 뭐가 다르죠? | — |
| 5.2 | CUT 02 · 준비 프로그램 | 준비 과정 전체가 **하나의 화면에** 남습니다. | — |
| 10.2 | CUT 03 · 현장에서 | 심사에 필요한 증적, | **현장에서 끝냅니다.** |
| 14.4 | CUT 03 · 현장에서 | AI는 제안하고, | **승인은 담당자가 합니다.** |
| 18.3 | (컷 4는 자막 숨김) | — | — |
| 24.2 | CUT 05 · 정기심사 | 인증을 받은 다음날부터 | **여기서부터 관리됩니다.** |
| 28.2 | (엔드카드는 자막 숨김) | — | — |

**중요**: 컷 3의 8초 안에 자막을 두 장 겹치지 말고 순차로 갈아끼워야 함. 앞 4초에 "심사에 필요한 증적, 현장에서 끝냅니다", 뒤 4초에 "AI는 제안하고, 승인은 담당자가 합니다."

---

## 타이머 (Timer)

우하단 (bottom 40px, right 64px):
- mono 13px 현재 시각 표시 (`00:00` 형식)
- 280×2px 진행 바 (--gray-150 배경, --ink-950 채움)
- "00:30" 총 시간 표시
- 엔드카드에서는 opacity 0으로 숨김

---

## 재생 컨트롤

**위치**: 뷰포트 하단 중앙 (viewport-fixed, `position: fixed`). Stage 밖에 있음.

**스타일**: rgba(11, 18, 32, 0.94) pill 배경, mono 12px 흰색 텍스트, radius 999px.

**요소**:
- ▶ 재생 / ❚❚ 일시정지 / ↻ 다시 재생 버튼
- ⟲ 리셋 버튼 (t = 0으로)
- `00:00.00 / 00:30` 시간 표시 (tabular-nums)
- 340×4px 스크럽 바 — 클릭·드래그로 시각 이동, 하얀 knob (진행률 %)

**키보드**:
- Space — 재생/일시정지
- R — 리셋
- ArrowRight — +0.5s
- ArrowLeft — −0.5s

---

## Design Tokens

전체 토큰은 `assets/colors_and_type.css` 참조. 핵심 값:

### Colors

```css
/* Brand */
--ink-950:    #0B1220   /* Deep Ink Navy — primary brand */
--ink-900:    #111A2E
--signal-700: #0B3D91   /* Signal Blue — single accent */
--signal-100: #E4ECF9
--signal-50:  #F1F5FC

/* Neutrals */
--gray-25:  #FBFAF7   /* Page canvas (off-white) */
--gray-50:  #F5F4EF
--gray-100: #EEEDE7
--gray-150: #E4E2DB   /* Borders (hair) */
--gray-200: #D6D3C9
--gray-300: #B9B5A7
--gray-400: #8F8B7C   /* Placeholder / disabled */
--gray-500: #6E6A5C   /* Meta text */
--gray-700: #3B3830   /* Body */

/* Status */
--status-ok:      #1F6B44
--status-ok-bg:   #E1EFE6
--status-warn:    #8A5A00
--status-warn-bg: #F7ECD4   /* DEMO DATA badge bg */
--status-risk:    #A02929
--status-risk-bg: #F5E1E1

/* Semantic */
--fg-1: #0B1220  /* primary text */
--fg-2: #3B3830  /* body */
--fg-3: #6E6A5C  /* meta */
--fg-on-ink: #F5F4EF
--fg-accent: #0B3D91
```

### Typography

- 본문: **Pretendard** 300 / 400 / 500 / 600 / 700
- 모노스페이스: **JetBrains Mono** 400 / 500 — 조항 번호, 시각, 라벨, 금액에 사용
- 캡션/자막: 48px weight 600 letter-spacing −0.02em
- 헤딩 (컷 내부): 44–64px weight 600
- 오버라인: 13px mono letter-spacing 0.18em uppercase
- 본문/설명: 15–17px line-height 1.55–1.7
- **자간(letter-spacing)**: 디스플레이·H1·H2에서만 미세하게 마이너스(−0.01~−0.02em), 본문 0
- **숫자**: 표·수치는 항상 `font-variant-numeric: tabular-nums`

### Spacing (8px 그리드)

```
4 · 8 · 12 · 16 · 24 · 32 · 48 · 64 · 96 · 128 (px)
```

### Radius

```
2 · 4 · 6 · 999 (pill for status only)
```
카드는 최대 6px. 컷 3의 phone bezel만 예외 (56px = 실제 디바이스 반경).

### Shadow

```
--shadow-1: 0 1px 0 0 rgba(11, 18, 32, 0.04)
--shadow-2: 0 1px 2px rgba(11, 18, 32, 0.06), 0 0 0 1px rgba(11, 18, 32, 0.04)
--shadow-3: 0 4px 16px rgba(11, 18, 32, 0.08), 0 0 0 1px rgba(11, 18, 32, 0.04)
--shadow-focus: 0 0 0 3px rgba(23, 88, 204, 0.28)
```

컷 1의 견적 카드만 사용: `0 24px 60px rgba(11,18,32,0.10)` — 종이가 떠있는 인상.

### Motion

```
--dur-fast: 120ms
--dur-base: 200ms
--dur-slow: 320ms
--ease-standard: cubic-bezier(0.2, 0, 0, 1)
```

**금지**: 스프링/바운스, 스크롤 페럴랙스, 커서 트레일, 컨페티. 어떤 씬 안에서도 cubic-bezier(0.2, 0, 0, 1) 하나만 사용.

---

## Interactions & Behavior

이 영상은 사용자 인터랙션이 없는 자동 재생 애니메이션입니다 (컨트롤 바 제외). 모든 애니메이션은 **재생 시각 t (0 ~ 30초)에 대해 idempotent** 하게 설계되어 스크럽 시 앞뒤로 스무스하게 표현됩니다.

**핵심 원칙**: 각 `animCutN(t)` 함수는 절대 시각 t를 받아 그 시각의 씬 상태를 계산 (transition은 CSS가 담당). rAF 루프가 매 프레임 `tick(curT)` 호출:

```js
function tick(t) {
  // 1) 현재 씬 결정 (시간 range 기반)
  // 2) showScene(id) — display 토글
  // 3) 모든 animCutN(t) 호출 (씬 안이면 화면에 반영)
  // 4) updateCaption(t)
  // 5) 타이머/스크럽 UI 업데이트
}
```

**스크럽 동작**: 사용자가 스크럽 바 드래그 시 playing = false, curT를 목표 시각으로 설정. loop에서 그대로 반영. 애니메이션 로직이 idempotent이므로 어떤 시각으로 점프해도 정확한 상태 표시.

**localStorage 위치 저장**: 재생 중 매 프레임 8% 확률로 curT를 저장. 새로고침 후 이어보기.

---

## State Management

전역 상태:
- `curT: number` — 현재 재생 시각 (초, 0–30)
- `playing: boolean` — 재생 중 여부
- `last: number` — 이전 프레임 timestamp (rAF dt 계산용)

DOM 상태 (모두 CSS 클래스 토글):
- `.scene.on` — 현재 씬 활성 (display: block)
- `.hud.on` — HUD 표시
- `.qc.on` — 견적 카드 등장 (컷 1)
- `.stp.on` — 타임라인 스텝 등장 (컷 2)
- `.target.on`, `.capbtn.press`, `.sheet.on`, `.chip.press`, `.toast.on`, `.lgr.on` — 컷 3 서브액션
- `.c4head.on`, `.tblwrap.on`, `.hlbox.on` — 컷 4
- `.cert.on`, `.dday.on` — 컷 5

**중요 함정**:
- `.scene`/`.hud`의 초기 상태는 `display: none !important`. `.on`이 붙으면 `display: block/flex !important`. **`opacity` transition은 iframe timeline 이슈로 stuck** → 반드시 display 토글 사용.
- `#endc { position: absolute; inset: 0 }`가 있으므로 특정성 문제로 `!important`가 필수.

---

## 데이터 소스

이 영상은 시드 JSON `fieldproof-demo-seed.json` 을 기반으로 하드코딩된 값들로 구성되어 있습니다. 실제 프로덕션에서 다른 회사의 데이터를 넣고 싶다면:

- **테넌트**: orgNameKo, workspaceLabel, accountableParty, certScheme, baselineDate, nextSurveillanceDate, daysToSurveillance
- **AI 시스템**: SYS-01/02/03 (name, nameKo, riskLevel)
- **컴플라이언스 티커**: severity, title, detail, date, ref (컷 5의 Baseline Diff 3건에 사용)
- **SOP 문서**: docId, clauses, title, owner, revision, lastUpdated, state (컷 4 테이블에 사용)

인명/조직명은 모두 가상입니다. 실존 인물·기관과 무관.

**법적 제약**:
- KAB-A 등 인정기구 실명은 사용하지 않음 → "인정 인증기관 발행"으로 표기
- 심사원·컨설턴트 직함은 고객사 테넌트 내 표기 금지 → "내부심사 담당" 등 내부 직책으로 대체
- DEMO DATA 배지는 실제 고객사 데이터 오인 방지 목적으로 **상시 노출 필수**
- ISO 로고·인정마크는 사용하지 않음. 텍스트 배지만
- "인증 취득 보장" 뉘앙스 문구 금지

---

## Assets

번들에 포함된 파일:
- `FieldProof Demo v2.html` — 메인 프로토타입 (단일 HTML, 모든 스타일/스크립트 인라인)
- `assets/colors_and_type.css` — 퀀터니티에이아이 디자인 토큰 (필수 임포트)
- `assets/fonts/*.woff2` — Pretendard 5 weights + JetBrains Mono 2 weights
- `assets/fieldproof-mark.svg` — 방패 마크 (임시안, CertReady 로고 기반)
- `fieldproof-demo-seed.json` — 원본 시드 데이터

**폰트 라이선스 주의**: 이 번들의 Pretendard는 jsDelivr @1.3.9 로컬 카피입니다. 프로덕션 배포 시:
1. `@fontsource/pretendard` npm 패키지 사용을 권장하거나
2. 자체 CDN에 호스팅하거나
3. Pretendard Std 라이선스를 재검토

**로고 자산 대체**: `assets/fieldproof-mark.svg` 는 임시안 (퀀터니티에이아이 CertReady 마크 기반). 실제 FieldProof 브랜딩이 확정되면 이 SVG를 교체하고, HTML 내부의 인라인 방패 SVG (헤드라인 워드마크와 엔드카드)도 함께 교체해야 합니다.

**아이콘 라이브러리**: Lucide (stroke-width 1.75px, 1.5–1.75px 표준). 현재는 필요한 아이콘을 인라인 SVG로 넣었습니다. 프로덕션에서는 `lucide-react` 또는 CDN 로드로 대체 가능.

---

## Files

- `FieldProof Demo v2.html` — 메인 프로토타입 (모든 컷 + 재생 로직)
- `assets/colors_and_type.css` — 토큰 CSS (반드시 함께 배포)
- `assets/fonts/Pretendard-Light.woff2` (300)
- `assets/fonts/Pretendard-Regular.woff2` (400)
- `assets/fonts/Pretendard-Medium.woff2` (500)
- `assets/fonts/Pretendard-SemiBold.woff2` (600)
- `assets/fonts/Pretendard-Bold.woff2` (700)
- `assets/fonts/JetBrainsMono-Regular.woff2` (400)
- `assets/fonts/JetBrainsMono-Medium.woff2` (500)
- `assets/fieldproof-mark.svg` — 방패 마크 SVG
- `fieldproof-demo-seed.json` — 원본 데이터

---

## 재구현 시 체크리스트

- [ ] 씬 전환은 반드시 **display none/block**. opacity transition은 iframe/오프스크린 상황에서 stuck 되므로 금지.
- [ ] 8px 그리드 준수 (4px는 half-step으로만).
- [ ] 컬러는 curated palette 안에서만 (특히 Signal Blue와 Deep Teal을 한 화면에 섞지 않기).
- [ ] 조항 번호·시각은 반드시 mono + tabular-nums.
- [ ] 컷 3의 클릭 확정 시퀀스 (14.5–16s 1.5초 구간) 는 사용자가 chip에 커서 이동 → press → toast 순서를 명확히 인지할 수 있어야 함. 이 순간이 흐릿하면 영상 전체의 신뢰가 무너짐.
- [ ] DEMO DATA 배지는 컷 2–5 상시 노출. 컷 1과 엔드카드에서는 다른 이유(집중도)로 숨김.
- [ ] 컷 4에서 자막을 숨기는 것은 의도된 결정. SOP-12 행과 겹치므로 화면 헤딩에 의존.
- [ ] 스크럽 시 아무 시각으로 점프해도 정확한 씬 상태가 보이도록 idempotent 유지.
- [ ] 원본 텍스트 (특히 조항 번호 A.6.2.4, EVID-2026-0814-A, D-85, 담당자 이름) 는 오탈자 없이 그대로 사용.
- [ ] mp4 렌더링이 필요하면 Remotion 이식을 고려. React 컴포넌트 트리 + 시각 t 기반 렌더 로직이 그대로 매핑됨.
