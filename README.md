# vibecoding-practice

홍길동의 1페이지 자기소개 정적 웹 페이지. 외부 라이브러리 없이 **단일 HTML 파일** 안에 HTML과 CSS만으로 작성된 에디토리얼 다크 테마 포트폴리오입니다.

> Single-file static profile page · Editorial dark aesthetic · No build step required

---

## 개요

본 프로젝트는 학술적이면서 화려한 인상을 주는 1페이지 정적 자기소개 사이트입니다. 잉크 블랙 배경에 골드 강조색, 가변 세리프(Fraunces) 타이포그래피, 그라디언트 메쉬와 SVG 그레인 텍스처가 결합된 매거진/저널 스타일을 지향합니다.

**핵심 정보**

| 항목 | 값 |
| --- | --- |
| 이름 | 홍길동 |
| 소속 | 삼육대학교 인공지능융합학부 |
| 관심 분야 | LLM · 멀티에이전트 · 인지심리학 |
| 연락처 | example@syusw.ac.kr |

---

## 기술 스택

- **HTML5** — 시맨틱 마크업 (`<header>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`)
- **CSS3** — 인라인 `<style>` 한 곳에 정의. 사용한 주요 기능:
  - CSS Custom Properties (디자인 토큰)
  - CSS Grid · Flexbox 비대칭 레이아웃
  - `clamp()` 기반 유체 타이포그래피
  - `@keyframes` 애니메이션 7종
  - `radial-gradient` 다중 레이어 메쉬
  - `mask-image` 그라디언트 마스킹
  - `mix-blend-mode: overlay` 그레인 합성
  - `font-variation-settings` 가변 폰트 축 제어
- **SVG** — 인라인 `<feTurbulence>` 필터 기반 노이즈/그레인 텍스처
- **Google Fonts** — Fraunces · Noto Serif KR · JetBrains Mono (CDN)

빌드 도구, 번들러, JavaScript 프레임워크 모두 사용하지 않습니다.

---

## 파일 구조

```
vibe-practice/
├── about.html        # 메인 페이지 (HTML + CSS 단일 파일, ~700 lines)
└── README.md         # 이 문서
```

---

## 시작하기

### 로컬에서 열기

```bash
git clone https://github.com/bskang-openbus/vibecoding-practice.git
cd vibecoding-practice
open about.html              # macOS
xdg-open about.html          # Linux
start about.html             # Windows
```

빌드 단계가 없으므로 브라우저에서 바로 열리며, Google Fonts는 첫 로드 시 자동으로 받아옵니다.

### 로컬 서버로 띄우기 (선택)

```bash
python3 -m http.server 8000
# 브라우저에서 http://localhost:8000/about.html
```

또는

```bash
npx serve .
```

---

## 디자인 시스템

### 컬러 토큰

`:root`에 CSS 변수로 정의되어 있어 한 곳에서 일괄 변경할 수 있습니다.

| 변수 | 값 | 용도 |
| --- | --- | --- |
| `--bg` | `#0a0d14` | 메인 배경 (잉크 블랙) |
| `--bg-2` | `#11151f` | 보조 배경 |
| `--ink` | `#ede4d3` | 본문 텍스트 (크림) |
| `--ink-2` | `#cfc4ad` | 보조 텍스트 |
| `--ink-dim` | `#7d7461` | 흐린 메타 텍스트 |
| `--gold` | `#d4a574` | 강조 색상 (앤티크 골드) |
| `--gold-bright` | `#f1c894` | 하이라이트 골드 |
| `--blue` | `#6ab7ff` | 보조 액센트 (블루) |
| `--orange` | `#ff5b3a` | 상태 표시 액센트 (오렌지) |
| `--border` | `rgba(237,228,211,0.12)` | 기본 구분선 |
| `--border-strong` | `rgba(237,228,211,0.28)` | 강조 구분선 |

### 타이포그래피

세 가지 서체를 역할별로 페어링합니다.

- **Fraunces** — 가변 세리프(variable font). `opsz`, `wght`, italic 축을 적극적으로 활용. 큰 디스플레이 텍스트와 영문 캡션에 사용.
- **Noto Serif KR** — 한글 본문 및 굵은 헤드라인. Black(900) 무게로 "홍길동" 등 시그니처 타이틀에 사용.
- **JetBrains Mono** — 메타 정보, 섹션 번호, 테이블, 푸터 등 기술적/저널적 디테일에 사용.

이름 "홍길동"의 가운데 글자 "길"은 Fraunces italic + 골드 그라디언트 텍스트로 처리하여 한 글자만 시그니처 포인트로 부각됩니다.

### 레이아웃

- **최대 너비**: 1280px, 가운데 정렬
- **사이드 패딩**: 데스크톱 56px, 모바일 28px
- **히어로 그리드**: `1fr 280px` 비대칭 2단 (좌측 본문 + 우측 메타 카드)
- **관심 분야 그리드**: 데스크톱 3단, 모바일 1단
- **연락처 그리드**: `1.4fr 1fr` 비대칭 2단

### 애니메이션

| 이름 | 길이 | 트리거 | 효과 |
| --- | --- | --- | --- |
| `mesh` | 28s | 자동 무한 alternate | 배경 그라디언트가 천천히 드리프트 |
| `pulse` | 2s | 자동 무한 | 상태 도트(오렌지)에서 ripple |
| `scroll` | 44s | 자동 무한 | 마퀴 텍스트 좌측 이동 |
| `reveal` | 1.2s | 페이지 로드 | 9단계 stagger로 섹션 페이드인 |
| `name-up` | 1.4s | 페이지 로드 | "홍길동" 한 글자씩 위로 슬라이드 |
| 카드 hover | 0.7s | 마우스 호버 | translateY(-8px) + 골든 글로우 + 보더 변색 |
| 링크 hover | 0.55s | 마우스 호버 | 밑줄 `scaleX` 0→1, 화살표 우측 이동 |

### 배경 레이어 4겹

z-index 순서대로 쌓입니다.

1. `.bg-mesh` (z:0) — 4개의 `radial-gradient`로 만든 컬러 메쉬, 28초 드리프트 애니메이션
2. `.bg-grid` (z:1) — 80px 격자, `mask-image`로 중앙만 보이도록 페이드
3. `.bg-grain` (z:2) — SVG `feTurbulence` 노이즈 필터, `mix-blend-mode: overlay`로 합성
4. `.bg-vignette` (z:3) — 중앙은 투명, 모서리로 갈수록 어둡게

콘텐츠는 `z-index: 10`의 `.stage` 안에 배치되어 모든 배경 레이어 위에 놓입니다.

---

## 페이지 구조

### 1. Top Strip (상단 스트립)

좌측에 인덱스 라벨(`※ INDEX / 自己紹介`)과 발행 정보(VOL. 01 · ED. 2026.05), 우측에 상태 표시(`AVAILABLE` + pulse 도트)와 위치(SEOUL · KR · KST)가 배치됩니다.

### 2. Hero (히어로)

- `§ 001 — Profile · 인물` 섹션 태그
- 거대 한글 이름 "홍길동" (clamp 4.5rem ~ 12rem)
- 이탤릭 영문 표기 "Hong, Gil-dong"
- 골드 좌측 보더를 가진 한 줄 소개
- 우측 메타 카드: NO. / YEAR / FIELD / STATUS / LANG 5개 행
- 좌상단·우하단 모서리 골드 ornament

### 3. Marquee (마퀴)

좌우로 무한 스크롤되는 키워드 띠. `Large Language Models ✦ Multi-Agent Systems ✦ Cognitive Psychology ✦ Emergence ✦ Reasoning ✦ Attention` 반복.

### 4. Current Foci (관심 분야)

- 섹션 헤딩: "현재의 관심사 / Current Foci" + 우측 메타(`§ 002`, 03 ENTRIES)
- 3개의 카드 그리드: LLM · 멀티에이전트 · 인지심리학
- 각 카드: 번호(◦ 01) · 한글 제목 · 영문 부제(이탤릭 골드) · 설명문
- 호버 시 카드 상승 + 골든 그라디언트 글로우 + 보더 색상 변경

### 5. Correspondence (연락처)

- 섹션 헤딩: "연락처 / Correspondence" + 우측 메타(`§ 003`, DIRECT CHANNEL)
- 좌측: 거대 이탤릭 이메일 링크 `→ example@syusw.ac.kr` (호버 시 골드 + 밑줄 + 화살표 이동)
- 우측: 점선 테이블 (Protocol / Timezone / Languages / Response)

### 6. Footer (푸터)

좌측 저작권, 가운데 콜로폰(사용한 폰트 표기), 우측 파일 메타.

---

## 커스터마이징 가이드

### 1. 본인 정보로 바꾸기

`about.html`에서 다음 부분을 수정하세요.

```html
<!-- 이름 (한 글자씩 span으로 감싸야 stagger 애니메이션 동작) -->
<h1 class="hero-name" aria-label="당신이름">
  <span>당</span><span class="gilo">신</span><span>이름</span>
</h1>

<!-- 영문 표기 -->
<div class="hero-en">Your, Name</div>

<!-- 한 줄 소개 -->
<p class="hero-tagline">소속과 한 줄 소개</p>

<!-- 관심 분야 3개 (article.interest) -->
<!-- 이메일 (mailto + 텍스트 둘 다 변경) -->
<a class="contact-link" href="mailto:you@example.com">
  <span class="contact-arrow">→</span>you@example.com
</a>
```

### 2. 컬러 변경

`:root`의 변수를 바꾸면 전체 톤이 일괄 변경됩니다.

```css
:root {
  --gold: #d4a574;  /* 강조색을 다른 색으로 변경 */
  --bg: #0a0d14;    /* 배경을 다른 어두운 색으로 */
}
```

라이트 테마로 전환하려면 `--bg`를 밝은 색(`#f5f0e6`)으로, `--ink`를 어두운 색(`#1a1a1a`)으로 바꾸고 `mix-blend-mode: overlay`를 `multiply`로 조정하면 됩니다.

### 3. 폰트 교체

`<link>` 태그의 Google Fonts URL과 `body { font-family: ... }`를 함께 수정하세요. Fraunces 대신 다른 가변 세리프(예: Newsreader, Cormorant)를 사용해도 잘 어울립니다.

### 4. 관심 분야 개수 조정

`.interests` 그리드 카드 수를 변경하려면:

```css
.interests {
  grid-template-columns: repeat(3, 1fr);  /* 4개라면 repeat(4, 1fr) */
}
```

---

## 브라우저 호환성

- Chrome / Edge 105+
- Safari 15.4+
- Firefox 110+

가변 폰트, CSS `clamp()`, `mask-image`, `mix-blend-mode`를 사용하므로 최신 브라우저에서 가장 잘 동작합니다. IE는 지원하지 않습니다.

### 접근성

- 의미 있는 시맨틱 태그 사용
- `aria-label`, `aria-labelledby`, `aria-hidden` 적절히 부여
- 키보드 포커스: `:focus` 스타일 (이메일 링크)
- 색상 대비: 본문(`#ede4d3` on `#0a0d14`) 약 13:1 — WCAG AAA 통과
- 다만 마퀴 애니메이션은 `prefers-reduced-motion` 미대응 상태 (개선 여지)

---

## 변경 이력

- **v2** (현재) — 에디토리얼 다크 테마로 전면 리뉴얼. 가변 폰트, 마퀴, 비대칭 그리드, 그레인 텍스처, 인터랙티브 카드 도입.
- **v1** — 흰 배경 + 짙은 남색 강조의 깔끔한 학술 톤 초기 버전.

---

## 라이선스

개인 학습 및 자기소개 용도. 코드는 자유롭게 참고/수정 가능합니다.
