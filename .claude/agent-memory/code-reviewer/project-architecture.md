---
name: project-architecture
description: Next.js 15/React 19 스타터킷 프로젝트의 전체 아키텍처, 기술 스택, 디렉토리 구조 요약
metadata:
  type: project
---

# 프로젝트 아키텍처

Next.js 15(실제로는 next@16.2.6 사용 중), React 19, Tailwind CSS v4, shadcn/ui 기반 랜딩 페이지 스타터킷.

## 기술 스택 (package.json 기준)
- next: 16.2.6 (주의: hero/faq 등 컴포넌트에 "Next.js 16"이라고 하드코딩되어 있음)
- react: 19.2.4
- tailwindcss: ^4 (postcss 방식)
- radix-ui: ^1.4.3 (통합 패키지, @radix-ui/* 개별 패키지 아님)
- shadcn/ui 스타일 커스텀 컴포넌트 (ui/ 폴더)
- next-themes: ^0.4.6
- zod: ^3.22.4
- date-fns: ^4.4.0
- class-variance-authority (cva) + tailwind-merge + clsx

## 디렉토리 구조
- app/ : AppRouter 페이지 (layout.tsx, page.tsx, docs/about/blog/contact page.tsx)
- components/layout/ : Header, Footer, MobileMenu, ThemeToggle
- components/sections/ : HeroSection, FeaturesSection, StatsSection, CtaSection, FaqSection
- components/ui/ : shadcn 스타일 기본 UI 컴포넌트들
- lib/ : utils.ts, format.ts, string.ts, validators.ts, constants.ts
- providers/ : ThemeProvider (next-themes 래퍼)
- types/ : index.ts (공통 인터페이스)

## 주요 설계 결정
- Server Component 우선: Header/Footer/sections 모두 서버 컴포넌트
- 클라이언트 컴포넌트: ThemeToggle, MobileMenu (인터랙션 필요), UI 기본 컴포넌트들
- 타입 정의 중앙화: types/index.ts
- 상수 중앙화: lib/constants.ts (SITE_CONFIG, NAV_ITEMS, FOOTER_LINKS)
- React import 없이 JSX 사용 (react-jsx transform)

**Why:** 스타터킷으로 설계되어 확장 가능한 구조를 목표로 함
**How to apply:** 새 컴포넌트 추가 시 서버/클라이언트 경계 고려, 타입은 types/index.ts에 추가
