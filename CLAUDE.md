# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

김중기의 개인 포트폴리오/프로필 웹사이트. 순수 HTML, CSS, JavaScript로 제작된 단일 페이지 사이트로 별도의 빌드 시스템이나 프레임워크 없이 동작한다.

## Repository Structure

- `index.html` — 메인 페이지 (HTML + 인라인 CSS + 인라인 JS 포함)
- `profile/그림1.jpg` — 프로필 사진 이미지
- `.claude/settings.local.json` — Claude Code local permissions

## Tech Stack

- HTML5 / CSS3 / Vanilla JavaScript (ES2017+ async/await)
- Google Fonts: Noto Serif KR (제목), Noto Sans KR (본문)
- FormSubmit.co API (이메일 전송 서비스)
- 빌드 도구 없음, 패키지 매니저 없음, 외부 JS 라이브러리 없음

## Design System

### Color Theme (Dark Slate)

| Variable         | Value                                  | Description          |
|------------------|----------------------------------------|----------------------|
| `--bg`           | `#0f172a`                              | 딥 슬레이트 배경     |
| `--bg-surface`   | `#1e293b`                              | 입력 필드 배경       |
| `--bg-card`      | `#1e293b`                              | 카드/섹션 배경       |
| `--border`       | `#334155`                              | 기본 테두리          |
| `--border-hover` | `#475569`                              | Hover 테두리         |
| `--text`         | `#f8fafc`                              | 기본 밝은 텍스트     |
| `--text-secondary` | `#cbd5e1`                            | 보조 텍스트          |
| `--text-muted`   | `#94a3b8`                              | 흐린 텍스트          |
| `--accent`       | `#818cf8`                              | 인디고 포인트 색상   |
| `--accent-light` | `#a5b4fc`                              | 밝은 인디고          |
| `--accent-glow`  | `rgba(129, 140, 248, 0.12)`           | 인디고 글로우 효과   |
| `--blue`         | `#38bdf8`                              | 블루 보조 색상       |

### Typography

- 기본 폰트 크기: `18px` (태블릿 768px 이하: `16px`, 모바일 400px 이하: `14px`)
- 제목 (serif): `Noto Serif KR` — 400, 700, 900
- 본문 (sans): `Noto Sans KR` — 300, 400, 500, 700

### Layout

- 데스크탑 콘텐츠 최대 폭: `1200px` (hero-content, section-inner)
- 섹션 카드: `border-radius: 20px`, `border: 1px solid var(--border)`, 다크 박스 쉐도우

## Page Sections

1. **Navigation** — 고정 상단 네비게이션 (로고: "JK"), 스크롤 시 반투명 배경 + blur 효과, 모바일 햄버거 메뉴
2. **Hero** — 원형 프로필 사진 (140px, 그라디언트 보더), 이름 "김중기" (shimmer 텍스트 애니메이션), 소개 태그라인, CTA 버튼 2개 (메일 보내기 → #contact, 더 알아보기 → #about), 배경 orb + dot-grid 장식
3. **About (소개)** — 좌측 accent line + 자기소개 텍스트, 키워드 태그 6개 (AI 컨설팅, 바이브 코딩, 업무 자동화, 컨텐츠 자동화, 수익 구조 설계, 스타트업)
4. **Hobbies (취미)** — 3열 그리드 카드 (싸이클, 등산, 여행), SVG 아이콘, hover 시 translateY + 그림자 + 상단 accent line
5. **Contact (연락처)** — 이메일 전송 폼 (수신 이메일 표시, 이름, 이메일, 제목, 내용), FormSubmit.co API를 통한 실제 이메일 전송, 성공/실패 상태 화면
6. **Footer** — 저작권 표시 "&copy; 2025 김중기"

## Contact Form (FormSubmit.co)

### 구조
- **수신 이메일**: `admin@metantec.com` (고정, disabled 입력 필드로 표시)
- **폼 필드**: 이름 (`name`), 이메일 (`email`), 제목 (`_subject`), 내용 (`message`)
- **스팸 방지**: `_honey` 허니팟 필드, `_captcha: false`
- **이메일 템플릿**: `_template: table`

### API 연동
- **엔드포인트**: `https://formsubmit.co/ajax/admin@metantec.com`
- **방식**: `fetch` POST (JSON), `Accept: application/json`
- **성공 판별**: `response.ok && result.success === "true"`

### 상태 처리
- **전송 중**: 버튼에 `.loading` 클래스 → "전송 중..." 텍스트, 클릭 비활성화
- **성공**: 폼 숨김 → `#formSuccess` 표시 (체크 아이콘 + 성공 메시지 + Activation 안내)
- **실패**: 폼 숨김 → `#formError` 표시 (X 아이콘 + 에러 메시지)
- **리셋**: "새 메일 작성하기" / "다시 시도하기" 버튼 → 폼 복원 + `reset()`

### 최초 사용 시 주의
FormSubmit.co는 최초 전송 시 수신 이메일(`admin@metantec.com`)로 Activation 확인 메일을 발송함. 승인 후 정상 동작.

## Animations

| 이름          | 용도                         | 설명                                      |
|---------------|------------------------------|-------------------------------------------|
| `fadeUp`      | 히어로 요소 등장             | opacity 0→1, translateY 20px→0            |
| `fadeIn`      | 히어로 라인 등장             | opacity 0→1                               |
| `photoReveal` | 프로필 사진 등장             | opacity 0→1, translateY+scale 보정        |
| `shimmer`     | 이름 텍스트 반짝임           | background-position 0%→200%→0%            |
| `orbFloat1/2` | 배경 orb 부유 효과           | translate + scale 변화 (25s/30s 주기)     |
| `spin`        | (예비) 로딩 스피너           | rotate 0→360deg                           |
| `reveal`      | 스크롤 등장 (IntersectionObserver) | opacity 0→1, translateY 24px→0, delay 0.1~0.3s |

## Responsive Breakpoints

| 구간        | 폭             | 주요 변경                                                    |
|-------------|----------------|--------------------------------------------------------------|
| 데스크탑    | > 768px        | max-width 1200px, 3열 취미 그리드, 폰트 18px                |
| 태블릿      | ≤ 768px        | 햄버거 메뉴 (슬라이드 사이드바), 1열 그리드, 폰트 16px, CTA 세로 배치 |
| 모바일      | ≤ 400px        | 폰트 14px, 프로필 90px, 축소 패딩, 폼 1열, min-height auto  |

### 모바일 메뉴 동작
- 햄버거 버튼(`.nav-toggle`) → `.nav-links.open` (오른쪽 슬라이드 인)
- `.nav-overlay.show` (반투명 배경 오버레이)
- 메뉴 링크 클릭 또는 오버레이 클릭 시 `closeMenu()` 호출

## JavaScript 기능 요약

1. **Nav 스크롤 효과** — `window.scrollY > 40` 시 `nav.scrolled` 클래스 토글 (passive listener)
2. **스크롤 Reveal** — `IntersectionObserver` (threshold: 0.15, rootMargin: -40px) → `.visible` 클래스 추가
3. **모바일 메뉴** — 햄버거 토글, 오버레이 클릭 닫기, 링크 클릭 닫기
4. **Contact Form** — FormSubmit.co AJAX 전송, 로딩/성공/실패 상태 관리, 폼 리셋

## Development Notes

- 모든 HTML, CSS, JS는 `index.html` 내 인라인으로 포함 (단일 파일)
- 외부 의존성: Google Fonts CDN, FormSubmit.co API
- 이메일 수신 주소: `admin@metantec.com`
- CSS 커스텀 속성(`:root` 변수)으로 테마 관리 — 색상 변경 시 변수만 수정하면 전체 적용
- CSS 전환 곡선: `var(--ease)` = cubic-bezier(0.4, 0, 0.2, 1), `var(--ease-out)` = cubic-bezier(0, 0, 0.2, 1)
