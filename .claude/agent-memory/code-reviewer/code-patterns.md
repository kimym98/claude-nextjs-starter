---
name: code-patterns
description: 프로젝트에서 발견된 코딩 패턴, 공통 이슈, 개선 포인트 목록
metadata:
  type: project
---

# 코드 패턴 및 공통 이슈

## 잘 작성된 패턴
- typography.tsx: cva + forwardRef 조합으로 재사용 가능한 Heading/Text 컴포넌트 구현
- ThemeToggle: mounted 상태로 hydration 불일치 방지 (suppressHydrationWarning와 함께 사용)
- MobileMenu: NavItem 타입을 props로 받아 재사용성 확보
- validators.ts: Zod 스키마를 개별 export하여 조합 가능하게 설계
- lib/format.ts: date-fns/locale ko 적용, try-catch로 안전한 날짜 포맷
- constants.ts: SITE_CONFIG, NAV_ITEMS를 타입 지정하여 export

## 발견된 이슈들

### Major
1. **배열 인덱스를 key로 사용** - features.tsx(idx), stats.tsx(idx), faq.tsx(idx)
   - FEATURES, STATS, FAQS 배열은 정적이라 큰 문제는 아니지만 title/question 필드를 key로 쓰는 것이 올바름

2. **stats.tsx의 렌더링 로직 복잡성** - stat.label === "%" 조건이 반복되고 데이터 구조가 label과 description을 혼용
   - StatItem 타입과 실제 데이터가 불일치 (label에 단위를, description에 설명을 넣고 렌더링 시 label로 분기)
   - formatNumber import가 있지만 stats.tsx에서 사용되지 않음 (미사용 import)

3. **콘텐츠에 버전 불일치** - hero.tsx와 faq.tsx에 "Next.js 16", "Tailwind CSS v4"가 하드코딩됨
   - 실제 package.json에는 next@16.2.6이 있으나 공식 Next.js 최신은 15.x

4. **외부 링크 rel 속성 누락** - hero.tsx의 GitHub 버튼에 rel="noopener noreferrer" 없음
   - cta.tsx의 GitHub Clone 버튼도 동일 문제

5. **Footer의 currentYear 계산** - 서버 컴포넌트에서 new Date()를 직접 사용
   - 빌드 타임에 고정됨 (정적 사이트라면 문제, 동적이면 괜찮음)

### Minor
6. **주석 부재** - 모든 파일에 한국어 주석이 없음 (CLAUDE.md 규칙 위반)
7. **types/index.ts에 React import 없음** - FeatureItem 인터페이스에 React.ComponentType 사용하지만 React import 없음
8. **플레이스홀더 페이지들** - about/blog/contact/docs 페이지가 "준비 중입니다" 상태
   - <main> 태그를 중첩 사용 (layout.tsx의 <main>과 각 page의 <main>)
9. **stats.tsx에서 formatNumber 미사용** - import했지만 실제 사용 안 함
10. **sheet.tsx의 Close 버튼 텍스트** - "Close"가 영어로 하드코딩 (다른 곳은 한국어)

## UI 컴포넌트 패턴
- radix-ui 통합 패키지 사용 (Dialog as SheetPrimitive, Accordion as AccordionPrimitive)
- data-slot 속성으로 컴포넌트 식별
- data-[state] 대신 data-open/data-closed 사용 (Tailwind v4 방식)
- forwardRef 없이 함수 컴포넌트로 직접 작성 (최신 shadcn 패턴)

**How to apply:** 코드 리뷰 시 위 이슈들을 기준으로 체크, 새 컴포넌트 작성 시 주석 추가 권장
