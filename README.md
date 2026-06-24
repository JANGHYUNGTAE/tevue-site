# TeVue 홍보 사이트 (tevue.co.kr)

테슬라 미러링 앱 **TeVue**의 정적 홍보 랜딩 페이지. 백엔드 없이 HTML/CSS만으로 구성 → **GitHub Pages**로 무료 호스팅.

> ⚠️ **중요**: 이 사이트는 앱 소스 repo(`teslamirror`)와 **반드시 분리된 별도 public repo**에 올립니다.
> 앱 repo에는 외부에 공개하면 안 되는 내부 문서·히스토리가 있으므로 절대 public 전환하지 마세요.

## 구성
```
tevue-site/
├── index.html        랜딩 페이지 (단일 파일, CSS 인라인)
├── assets/
│   ├── icon.svg      앱 아이콘 (V 마크)
│   └── wordmark.svg  워드마크 로고
├── CNAME             커스텀 도메인 (tevue.co.kr)
└── .nojekyll         Jekyll 처리 비활성화
```

## 배포 (GitHub Pages)

1. **새 public repo 생성** (예: `tevue-web`) — 앱 repo와 별개.
2. 이 폴더 내용을 그대로 push:
   ```bash
   cd tevue-site
   git init && git add . && git commit -m "TeVue 홍보 사이트"
   git branch -M main
   git remote add origin https://github.com/<계정>/tevue-web.git
   git push -u origin main
   ```
3. GitHub repo → **Settings → Pages** → Source: `Deploy from a branch` → Branch `main` / `/ (root)` → Save.
4. 같은 화면 **Custom domain**에 `tevue.co.kr` 입력 → Save (CNAME 파일이 이미 있어 자동 인식).
5. DNS 전파 후 **Enforce HTTPS** 체크.

## DNS 설정 (도메인 등록기관에서)

`tevue.co.kr`은 서브도메인 없는 **apex 도메인**이므로 A 레코드(또는 ALIAS/ANAME) 필요.

**A 레코드 — apex (`tevue.co.kr` / 호스트 `@`)**, 아래 4개 모두 추가:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
(IPv6도 지원하려면 AAAA 레코드: `2606:50c0:8000::153` ~ `2606:50c0:8003::153`)

**CNAME 레코드 — www (`www.tevue.co.kr`)**:
```
www  →  <계정>.github.io
```
GitHub는 apex와 함께 www 서브도메인도 두는 걸 권장합니다(IP 변경에 영향받지 않아 더 안정적).

> DNS 변경은 최대 24시간 전파. `dig tevue.co.kr +noall +answer`로 위 IP가 나오는지 확인.

## 다운로드 버튼 연결
출시 후 `index.html`의 App Store / Google Play 링크(`href="#"`)를 실제 스토어 URL로 교체하세요.

## 로컬 미리보기
```bash
cd tevue-site && python3 -m http.server 8080
# http://localhost:8080
```
