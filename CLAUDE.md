# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

김중기의 개인 포트폴리오/프로필 웹사이트. 순수 HTML, CSS, JavaScript로 제작된 단일 페이지 사이트로 별도의 빌드 시스템이나 프레임워크 없이 동작한다.

## Repository Structure

- `index.html` — 메인 페이지 (HTML + 인라인 CSS + 인라인 JS)
- `profile/그림1.jpg` — 프로필 사진 이미지
- `.claude/settings.local.json` — Claude Code local permissions

## Tech Stack

- HTML5 / CSS3 / Vanilla JavaScript
- Google Fonts: Noto Serif KR, Noto Sans KR
- 빌드 도구 없음, 패키지 매니저 없음

## Design System

### Color Theme (Light)

| Variable         | Value                          |
|------------------|--------------------------------|
| `--bg`           | `#f0f0f3` (연한 회색 배경)     |
| `--bg-card`      | `#ffffff` (카드 배경)          |
| `--text`         | `#1a1a2e` (본문 텍스트)       |
| `--accent`       | `#6c5ce7` (보라색 포인트)     |
| `--accent-light` | `#a29bfe` (밝은 보라색)       |

### Typography

- 기본 폰트 크기: `18px` (768px 이하 `16px`, 480px 이하 `15px`)
- 제목: Noto Serif KR (세리프)
- 본문: Noto Sans KR (산세리프)

## Page Sections

1. **Navigation** — 고정 상단 네비게이션, 스크롤 시 배경 블러 효과, 모바일 햄버거 메뉴
2. **Hero** — 원형 프로필 사진, 이름, 소개 태그라인, CTA 버튼 2개 (메일 보내기 / 더 알아보기)
3. **About (소개)** — 자기소개 텍스트, 키워드 태그 목록
4. **Hobbies (취미)** — 3열 그리드 카드 (싸이클, 등산, 여행)
5. **Contact (연락처)** — 이메일 링크 및 메일 보내기 버튼
6. **Footer** — 저작권 표시

## Key Features

- **반응형 디자인**: 768px / 480px 브레이크포인트, 모바일 슬라이드 사이드바 메뉴
- **애니메이션**: 스크롤 reveal (IntersectionObserver), 히어로 fadeUp, 프로필 사진 등장 효과, orb 배경 floating
- **그림자 효과**: 카드, 버튼, 프로필 사진에 보라색 계열 box-shadow 적용
- **인터랙션**: 카드 hover 시 translateY + 그림자 확대, 버튼 hover glow 효과

## Development Notes

- 모든 스타일과 스크립트는 `index.html` 내 인라인으로 포함
- 외부 의존성은 Google Fonts CDN만 사용
- 이메일 주소: `admin@metantec.com`
