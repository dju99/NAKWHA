# 팀 소개 페이지 디자인 스펙

> Spring Live 2026 메인(`index.html`)과 디자인 시스템을 공유하는 개별 팀 소개 페이지  
> 각 팀당 1개 HTML 파일 생성 — `band1.html` / `band2.html` / `band3.html`

---

## 1. 디자인 시스템 (index.html 공유)

### 폰트
- 헤드라인: `Bebas Neue` (Google Fonts)
- 본문: `Noto Sans KR` (Google Fonts) — weight 300 / 400 / 700 / 900

### 팀별 컬러 팔레트

| 팀 | 라이트 그라데이션 | 다크 그라데이션 |
|----|-----------------|----------------|
| 01 | `#fce4ec → #f9c6e0 → #e8b4f8` (벚꽃 핑크) | `#4a0e2a → #6d1f55 → #3d1569` |
| 02 | `#e8d5fb → #c4b5fd → #a5d8f7` (라벤더) | `#1e0a4e → #2d1a6b → #0a2550` |
| 03 | `#d1fae5 → #a7f3d0 → #c4b5fd` (민트) | `#0a2e1e → #0f4535 → #1a1060` |

### 공통 변수
```css
--bg-light:   #fdf6fb
--bg-dark:    #0d0518
--text-light: #2e1f2e
--text-dark:  #f0e6ff
--accent:     #c084fc
--gradient:   linear-gradient(90deg, #f472b6, #c084fc, #818cf8)
```

### 다크모드
- `<html data-theme="dark">` 토글 방식 (index.html 동일)
- `localStorage` 키: `springlive_theme`

---

## 2. 파일 구조

```
/
├── index.html
├── band1.html
├── band2.html
├── band3.html
└── (og-image-band1.png 등 이미지는 추후 추가)
```

---

## 3. 페이지 레이아웃 (섹션 순서)

```
[NAV]
[HERO]          — 팀 이름 대형 타이포 + 장르 뱃지 + 공연 날짜
[INTRO]         — 팀 소개 한 문단 + 키워드 태그
[MEMBERS]       — 멤버 카드 그리드 (이름 / 포지션 / 한마디)
[SETLIST]       — 트랙 리스트 (번호 / 곡명 / 원곡 아티스트)
[GALLERY]       — 사진 그리드 (placeholder 포함)
[BACK]          — 메인으로 돌아가기 버튼
[FOOTER]        — index.html 동일
```

---

## 4. 섹션별 상세 스펙

### 4-1. NAV

index.html NAV 완전 동일하게 재사용.  
로고 클릭 시 `index.html`로 이동.  
링크 목록: `소개 / 멤버 / 세트리스트 / 갤러리` (앵커 링크).

---

### 4-2. HERO

**레이아웃**
- `min-height: 100vh`
- 팀별 그라데이션 배경 (섹션 1 팔레트 참조)
- 벚꽃 blob 4개 float 애니메이션 (index.html 동일 코드 재사용)
- 벚꽃 꽃잎 파티클 (index.html 동일)

**콘텐츠 (중앙 정렬)**
```
[장르 pill 뱃지]          ← 예: "K-POP COVER"
[팀 이름]                 ← Bebas Neue, clamp(5rem, 18vw, 13rem), 흰색
[팀 슬로건 한 줄]          ← Noto Sans KR 300, 흰색 88% 투명도
[공연 날짜 / 장소 뱃지 행]  ← index.html hero-badges 동일 컴포넌트
[SNS 링크 버튼 행]         ← Instagram / YouTube 아이콘 포함 rounded 버튼
```

**뒤로가기 버튼** (좌상단 고정, NAV 아래)
```
← Spring Live  (흰색, 반투명 pill 버튼)
```
> position: fixed, top: 5rem, left: 2rem, z-index: 150  
> 클릭 시 index.html#bands로 이동

**스크롤 큐** — index.html 동일 (하단 중앙 "Scroll" + 선)

---

### 4-3. INTRO

**레이아웃**: 배경 `var(--bg-light)`, 최대 너비 760px, 중앙 정렬

```
[eyebrow 라벨]   "About"  — 보라색 소문자
[제목]           "우리가 <팀이름>이에요"  — s-title 클래스 동일
[본문 단락]      팀 소개 2–3문장 (font-weight 300, line-height 1.9)
[키워드 태그 행] 예: #봄밤  #커버밴드  #K-POP  #에너지
```

**키워드 태그 스타일**
- 배경: 팀 컬러 20% 투명도
- 테두리: 팀 컬러 40% 투명도
- border-radius: 999px
- 클릭 불가(장식용)

---

### 4-4. MEMBERS

**레이아웃**: 배경 `linear-gradient(180deg, var(--bg-light), #f5eeff)`, 섹션 패딩 6rem

**멤버 카드 그리드**
- `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))`
- `gap: 1.2rem`
- 최대 너비: 900px, 중앙 정렬

**멤버 카드 구조**
```
┌─────────────────────┐
│  [사진 영역]         │  ← 원형, 120×120px
│                     │    없을 경우: 이니셜 + 팀 컬러 그라데이션 배경
│  [이름]             │  ← font-weight 700
│  [포지션/악기]       │  ← 작은 pill 뱃지 (예: "보컬", "기타", "드럼")
│  [한마디 멘트]       │  ← font-size 0.82rem, 300, 이탤릭
└─────────────────────┘
```

**카드 스타일**
- background: `#fff` (다크: `#1a0835`)
- border-radius: 24px
- border: 1.5px solid 팀 컬러 15% 투명도
- hover: `translateY(-6px)` + box-shadow
- `.appear` 등장 애니메이션 (index.html 동일 IntersectionObserver)

---

### 4-5. SETLIST

**레이아웃**: 배경 팀 컬러 그라데이션 (index.html ticket-section과 유사), 패딩 7rem

**헤더**
```
[eyebrow] "Set List"
[제목]    "우리가 부를 <span>곡들</span>"  — 흰색
[서브]    "공연 당일 순서가 변경될 수 있습니다"  — 흰색 70%
```

**트랙 테이블** (최대 너비 640px, 중앙 정렬)
```
┌──┬────────────────────────┬──────────────┐
│번호│ 곡명                   │ 원곡 아티스트  │
├──┼────────────────────────┼──────────────┤
│ 1 │ 곡 이름                │ 아티스트      │
│ 2 │ 곡 이름                │ 아티스트      │
│...│                        │              │
└──┴────────────────────────┴──────────────┘
```

**행 스타일**
- 홀수 행: 흰색 5% 투명도 배경
- hover: 흰색 12% 투명도로 변화 (transition 0.2s)
- border-bottom: 흰색 8% 투명도
- 번호: Bebas Neue, 흰색 30% 투명도
- 곡명: font-weight 600, 흰색
- 아티스트: font-size 0.8rem, 흰색 55% 투명도

**배경 패턴** — `radial-gradient` dot 패턴 (index.html ticket-section::before 동일)

---

### 4-6. GALLERY

**레이아웃**: 배경 `var(--bg-light)`, 패딩 6rem

**그리드**
- `columns: 3` (masonry-like), `gap: 0.8rem`
- 모바일(600px 이하): `columns: 2`
- 최대 너비: 980px, 중앙 정렬

**이미지 카드**
- border-radius: 18px
- overflow: hidden
- hover: `scale(1.02)` + box-shadow (transition 0.3s)

**플레이스홀더** (이미지 없을 경우)
- 팀 컬러 그라데이션 배경
- aspect-ratio: 4/3 또는 3/4 (번갈아)
- 중앙에 🌸 이모지

**총 플레이스홀더 수**: 6개 (나중에 실제 이미지로 교체)

---

### 4-7. BACK TO MAIN 버튼

섹션 없이 단독 버튼 — GALLERY 하단, FOOTER 위

```
[← 메인 페이지로 돌아가기]
```

- 스타일: index.html `btn-main` 동일 (gradient, rounded)
- 텍스트: "← 메인 페이지로"
- href: `index.html#bands`
- `display: block; text-align: center; max-width: 280px; margin: 0 auto 5rem;`

---

### 4-8. FOOTER

index.html footer 완전 동일.

---

## 5. 반응형 브레이크포인트

| 뷰포트 | 변화 |
|--------|------|
| `≤ 700px` | NAV 햄버거 메뉴 활성화 |
| `≤ 600px` | HERO 뱃지 세로 스택, 멤버 카드 2열, 갤러리 2열 |
| `≤ 400px` | 갤러리 1열 |

---

## 6. 인터랙션 & 애니메이션

| 기능 | 스펙 |
|------|------|
| `.appear` 등장 | IntersectionObserver, threshold 0.12, translateY(28px)→0, opacity 0→1, 0.75s |
| 벚꽃 파티클 | index.html 동일 (hero 내부) |
| 커서 벚꽃 이펙트 | index.html 동일 (mousemove) |
| 다크모드 토글 | index.html 동일 (localStorage 공유) |
| 햄버거 메뉴 | index.html 동일 |
| 갤러리 hover | `transform: scale(1.02)`, `box-shadow`, transition 0.3s |

---

## 7. SEO / OG 태그

각 파일 `<head>`에 아래 태그 포함:

```html
<meta property="og:title"       content="[팀이름] — Spring Live 2026">
<meta property="og:description" content="[팀 슬로건]">
<meta property="og:image"       content="og-image-band[N].png">
<meta property="og:url"         content="https://dju99.github.io/NAKWHA/band[N].html">
<title>[팀이름] | Spring Live 2026</title>
```

---

## 8. 데이터 플레이스홀더 (개발 시 교체)

아래 값들은 TBD — 개발 시 주석으로 명확히 표시할 것.

```
BAND_NAME        = "팀 이름 TBD"
BAND_GENRE       = "장르 TBD"
BAND_SLOGAN      = "슬로건 TBD"
BAND_INSTAGRAM   = "#"
BAND_YOUTUBE     = "#"
MEMBERS          = [] (이름, 포지션, 멘트, 사진경로)
SETLIST          = [] (번호, 곡명, 아티스트)
```

---

## 9. index.html 연동

**band card에 링크 추가** (index.html 수정 필요):
```html
<!-- 기존 bc-links 아래에 추가 -->
<a href="band1.html" class="bc-link">🔍 자세히 보기</a>
```

각 `band-card`에 `cursor: pointer` 유지, 카드 전체 클릭 시 `band[N].html`로 이동 (또는 "자세히 보기" 링크만).
