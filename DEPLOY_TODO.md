# 터미널 재시작 후 배포 작업 순서

## 1. GitHub Pages 활성화

터미널에서 순서대로 실행:

```bash
gh api repos/dju99/NAKWHA/pages -X POST -f build_type=workflow
```

> 이미 Pages가 생성된 경우 위 명령이 실패하면 아래로 대체:
> ```bash
> gh api repos/dju99/NAKWHA/pages -X PUT -f build_type=workflow
> ```

---

## 2. 워크플로우 실행

```bash
gh workflow run deploy.yml --repo dju99/NAKWHA
```

---

## 3. 배포 완료 확인

```bash
gh run list --repo dju99/NAKWHA --limit 1
```

`conclusion: success` 가 뜨면 배포 완료.

---

## 4. 접속 확인

배포 완료 후 아래 URL에서 확인:

```
https://dju99.github.io/NAKWHA/
```

---

## 참고

- 이후 `main` 브랜치에 push하면 자동으로 재배포됨
- `index.html`의 `og:url`이 `https://dju99.github.io/spring-live-2026/` 으로 되어 있어 실제 배포 URL과 다름 → 추후 수정 필요
