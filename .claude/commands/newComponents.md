---
description: "새로운 컴포넌트 생성 (컴포넌트 파일, 스타일 파일, 테스트 파일)"
allowed-tools:
  [
    "Bash(*)",
    "Write(*)",
    "Read(*)",
  ]
---

# Claude 명령어: newComponents

새로운 React 컴포넌트를 생성합니다. 컴포넌트 파일, 스타일 파일, 테스트 파일을 자동으로 생성합니다.

## 사용법

```
/newComponents {컴포넌트이름}
```

**예시:**
```
/newComponents Button
/newComponents UserCard
/newComponents Modal
```

## 생성 파일

컴포넌트명이 `Button`일 경우:

1. **Button.tsx** - React 컴포넌트 파일
   - TypeScript 타입 정의
   - 기본 Props 인터페이스
   - 함수형 컴포넌트

2. **Button.style.ts** - Tailwind CSS 스타일 파일
   - 스타일 유틸리티 함수 (선택사항)
   - 상수 정의

3. **Button.test.ts** - Vitest 테스트 파일
   - 기본 렌더링 테스트
   - 테스트 구조

## 생성 위치

`components/` 디렉토리 내에 생성됩니다.

```
components/
├── Button.tsx
├── Button.style.ts
└── Button.test.ts
```

## 프로세스

1. 컴포넌트 이름 유효성 검사
2. 세 개의 파일 생성
   - React 컴포넌트 (TypeScript)
   - 스타일 파일
   - 테스트 파일
3. 기본 코드 템플릿으로 초기화

## 규칙

- PascalCase 이름 필수 (e.g., `Button`, `UserCard`)
- TypeScript 사용
- Tailwind CSS 스타일
- Vitest 테스트 프레임워크
