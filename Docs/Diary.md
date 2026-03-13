# 📋 BidNow 홈페이지 개발 일지

## 📅 2026년 3월 8일 (토)

---

## 1. 홈페이지 기획 및 개발 환경 구성

### 작업 내용
- 프로젝트 기획서 검토 및 기술 스택 확정
  - **HTML5 + Tailwind CSS (CDN) + Vanilla JS** 조합으로 결정
  - 별도 빌드 도구 없이 정적 파일만으로 구동되는 구조
- 디자인 컨셉 확정: 다크 네이비 + 네온 블루 테마, 글래스모피즘, 마이크로 애니메이션
- 폴더 구조 생성: `assets/css`, `assets/js`, `assets/images`

### Lessons Learned
- 간단한 랜딩 페이지는 프레임워크(React, Next.js) 없이도 충분히 고퀄리티 구현 가능
- Tailwind CDN + 커스텀 CSS 조합이 빠른 프로토타이핑에 최적

---

## 2. 랜딩 페이지 핵심 구현

### 작업 내용
- **Hero 섹션**: 메인 카피, CTA 버튼, AI 생성 배경 이미지 적용
- **Pain Points 섹션**: 3단 카드 레이아웃 (끝없는 검색 노가다, 문서 해석 늪, 뒤늦은 공고 확인)
- **Features 섹션**: AI 요약, 키워드 필터링, 텔레그램 알림 (스마트폰 목업 포함)
- **Process 섹션**: 5단계 워크플로우 시각화
- **Apply 섹션**: 문의 폼 (이름, 업체명, 연락처, 텔레그램ID, 키워드, 메시지)
- **Navigation**: 반응형 GNB + 모바일 햄버거 메뉴
- **애니메이션**: IntersectionObserver 기반 fadeUp, hover 효과, 펄스 애니메이션

### Lessons Learned
- `IntersectionObserver`는 스크롤 기반 애니메이션 처리에 퍼포먼스와 구현 편의성 모두 우수
- Phosphor Icons (CDN)를 활용하면 별도 아이콘 에셋 없이 빠르게 아이콘 적용 가능
- 글래스모피즘 효과는 `backdrop-blur` + 반투명 배경 + 보더 조합으로 구현

---

## 3. 텍스트 수정 및 브랜딩 작업

### 작업 내용
| 변경 전 | 변경 후 |
|---|---|
| AI Bidding Master | **BidNow** |
| 나라장터 | **KAPT** |
| AI 비딩 서비스 신청하기 | **BidNow 서비스 신청하기** |
| 복잡한 HWP는 | **복잡한 공고문서는** |
| 아쉬운 타이밍 미스 | **뒤늦은 공고 확인** |
| Feature/Process 상세 문구 다수 | 사용자 요청에 맞게 수정 |

### Lessons Learned
- 브랜딩 변경 시 로고, 네비게이션, 푸터, 버튼, 봇 이름 등 **모든 곳**을 체크리스트로 정리해야 누락 방지 가능
- 한글 파일 경로에서 `grep` 검색이 안 될 수 있음 → `view_file`로 직접 확인 필요

---

## 4. Process 섹션 리디자인

### 작업 내용
- 기존 5단계 원형 아이콘 나열 → **좌우 분할 레이아웃**으로 전면 재설계
  - **좌측**: "✋ 대표님이 하실 일" — 키워드 등록 카드 (예시 태그 포함)
  - **→ 화살표** (모바일: ↓ 전환)
  - **우측**: "🤖 BidNow가 자동으로 처리" — 공고 수집 → AI 분석 → 텔레그램 알림
  - **하단**: ✅ "대표님은 받아보신 요약으로, 입찰 여부만 결정하세요."
- "사용자는 키워드만 등록하면 나머지는 BidNow가 해결" 메시지 강조

### Lessons Learned
- 프로세스 표현에서 **사용자 역할 vs 시스템 역할**을 시각적으로 분리하면 서비스 가치가 직관적으로 전달됨
- `lg:flex-row` + `flex-col` 조합으로 데스크톱은 좌우, 모바일은 상하 배치를 자연스럽게 전환 가능

---

## 5. Formspree 이메일 연동

### 작업 내용
- **Formspree** 서비스를 활용하여 문의 폼 → `bidnow.admin@gmail.com` 이메일 전송 연동
- Form 태그에 `action="https://formspree.io/f/xyknzpqa"` 추가
- `script.js`의 mock submission → 실제 `fetch` API 호출로 교체
- 성공/실패 시 버튼 색상 + 텍스트 피드백 구현

### Lessons Learned
- 정적 사이트에서 폼 전송은 **Formspree**(간단, 월 50건) 또는 **EmailJS**(커스텀 템플릿, 월 200건) 활용
- Formspree는 첫 제출 시 수신 이메일로 **인증 메일**을 보냄 → Confirm 필수
- `fetch` + `Accept: application/json` 헤더를 사용하면 Formspree가 JSON 응답을 반환하여 JS에서 처리 가능

---

## 6. GitHub 배포

### 작업 내용
- Git 저장소 초기화 → `https://github.com/jeonghunkim942/bidnow` 에 push
- 브랜치: `main`
- 커밋 이력:
  1. `1eb4f26` — Initial commit: BidNow landing page
  2. `cf14d67` — Update: 텍스트 수정, Formspree 연동, Process 리디자인

### Lessons Learned
- PowerShell에서 `&&` 연산자가 작동하지 않음 → 명령어를 개별 실행하거나 `;`으로 연결해야 함

---

## 7. Cloudflare Pages 배포 및 도메인 연결

### 작업 내용
- **Cloudflare Pages**에 GitHub 저장소 연동 → 자동 배포 설정
  - Build command: 없음 (정적 사이트)
  - Build output: `/`
- 가비아에서 구매한 `bidnow.kr` 도메인을 Cloudflare에 등록
- 가비아 네임서버를 Cloudflare 제공 네임서버로 변경
- **Custom domains** 설정:
  - `bidnow.kr` ✅ 접속 확인
  - `www.bidnow.kr` ✅ 접속 확인

### Lessons Learned
- Cloudflare Pages 커스텀 도메인 연결 시 **DNS 레코드를 수동 추가하면 안 됨** → Pages의 Custom domains 기능에서 추가하면 DNS가 자동 생성됨
- 수동 CNAME + Pages 추가를 동시에 하면 **"This domain is already in use"** 에러 발생
- `www` 서브도메인을 수동 CNAME만 하고 Pages에 등록 안 하면 **Error 1014 (CNAME Cross-User Banned)** 발생
- 가비아 → Cloudflare 네임서버 전환은 보통 10분~30분 내 적용

---

## 📊 최종 산출물 요약

| 항목 | 내용 |
|---|---|
| **GitHub** | https://github.com/jeonghunkim942/bidnow |
| **Live URL** | https://bidnow.kr |
| **www URL** | https://www.bidnow.kr |
| **이메일 수신** | bidnow.admin@gmail.com (Formspree) |
| **주요 파일** | `index.html`, `assets/css/styles.css`, `assets/js/script.js` |
| **호스팅** | Cloudflare Pages (무료) |
| **도메인** | 가비아 (bidnow.kr) + Cloudflare DNS |
