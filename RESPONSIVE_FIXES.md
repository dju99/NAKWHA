# 반응형 디자인 수정 사항

## 1. 카운트다운 구분자(`:`) 모바일 미조정 — 🔴 우선순위 높음

**문제**  
320px 화면에서 카운트다운 아이템 4개 + 구분자 3개의 최소 너비 합이 ~380px를 초과해 가로 스크롤이 발생할 수 있음.

**원인**  
`@media (max-width: 600px)`에서 `.cd-item`은 조정됐지만 `.cd-sep`의 `font-size: 2.2rem`은 그대로.

**수정 위치** `index.html` — line 680~683

```css
/* 현재 */
@media (max-width: 600px) {
  .cd-item { min-width: 64px; padding: 0.75rem 0.8rem; }
  .cd-num { font-size: 2rem; }
}

/* 수정 후 */
@media (max-width: 600px) {
  .cd-item { min-width: 64px; padding: 0.75rem 0.8rem; }
  .cd-num { font-size: 2rem; }
  .cd-sep { font-size: 1.6rem; padding-top: 0.65rem; }
}
```

---

## 2. hero-title clamp 최솟값 — 🟡 우선순위 중간

**문제**  
`clamp(5.5rem, 18vw, 15rem)` — 320px 뷰포트에서 18vw = 57.6px < 88px(5.5rem)이므로 최솟값 88px로 고정. 좌우 padding(2rem × 2 = 64px) 제외 시 가용 너비 256px에서 Bebas Neue "SPRING" 88px가 빠듯.

**수정 위치** `index.html` — line 159

```css
/* 현재 */
font-size: clamp(5.5rem, 18vw, 15rem);

/* 수정 후 */
font-size: clamp(4rem, 18vw, 15rem);
```

---

## 3. 태블릿 브레이크포인트 부재 — 🟡 우선순위 중간

**문제**  
현재 브레이크포인트가 600px / 700px 두 개뿐. 768px~1024px 태블릿 구간에서 bands-grid가 2열로 뭉칠 때 카드 비율이 어색하게 늘어날 수 있음.

**수정 위치** `index.html` — 기존 미디어쿼리 아래에 추가

```css
@media (max-width: 900px) {
  .bands-grid {
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1.2rem;
  }
  .hero-inner { max-width: 700px; }
}
```

---

## 4. 타임라인 — 초소형 화면(≤360px) 여백 — 🟢 우선순위 낮음

**문제**  
320px 화면에서 `padding-left: 80px` + 본문 너비 192px가 경계선. `.tl-body` 텍스트가 긴 경우 줄바꿈이 많이 발생.

**수정 위치** `index.html` — line 622~630 미디어쿼리 내부

```css
@media (max-width: 400px) {
  .timeline { padding-left: 68px; }
  .timeline::before { left: 56px; }
  .tl-time { left: -68px; width: 54px; font-size: 0.7rem; }
}
```

---

## 5. tc-seats 데드 CSS 정리 — 🟢 우선순위 낮음

**문제**  
`.tc-seats`, `.tc-seats-bar`, `.tc-seats-fill`, `.tc-seats-label` CSS가 정의되어 있지만 HTML ticket-card 안에 해당 마크업이 없어 실제로 렌더링되지 않는 데드 코드.

**처리 방법**  
- 좌석 바 기능을 추후 사용할 계획이면 → 해당 HTML 마크업 추가
- 사용하지 않을 계획이면 → CSS 삭제 (line 1017~1043)

---

## 수정 우선순위 요약

| # | 항목 | 우선순위 | 작업 |
|---|------|----------|------|
| 1 | 카운트다운 `.cd-sep` 모바일 조정 | 🔴 높음 | CSS 한 줄 추가 |
| 2 | hero-title clamp 최솟값 축소 | 🟡 중간 | 값 수정 |
| 3 | 태블릿 브레이크포인트 추가 | 🟡 중간 | 미디어쿼리 추가 |
| 4 | 타임라인 초소형 화면 여백 | 🟢 낮음 | 미디어쿼리 추가 |
| 5 | tc-seats 데드 CSS 정리 | 🟢 낮음 | 삭제 또는 마크업 추가 |
