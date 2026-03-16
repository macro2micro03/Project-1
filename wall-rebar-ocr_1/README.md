# 벽체 배근일람도 OCR 추출기

아파트 벽체 배근일람도 PDF에서 배근 데이터를 자동으로 추출하여 Excel(.xlsx)로 저장하는 웹 앱입니다.

## 주요 특징

- **API 키 불필요** — 완전 무료, 브라우저에서만 동작
- **Tesseract.js OCR** — 영어 전용 모드로 빠른 초기화 (철근 표기는 모두 영문/숫자)
- **다중 파일 처리** — 여러 PDF 동시 업로드 및 처리
- **Excel 출력** — 도면별 시트 + 전체통합 시트 자동 생성
- **보안** — 파일이 외부 서버로 전송되지 않음 (브라우저 로컬 처리)

## 추출 데이터

| 항목 | 예시 |
|------|------|
| 출처 도면 | S42-001 |
| 벽체 기호 | W41, CW2, HW1, MW3 |
| 층 범위 | 7F ~ 29F, B2F ~ B1F |
| 두께(mm) | 220, 250, 350 |
| 수직철근 | SHD10 @300, UHD16 @150(*) |
| 단부보강근 | 10 - UHD16(*), 8 - SHD13 |
| 수평철근 | SHD10 @280 |

> `(*)` 표기 = S41-402 상세도 횡방향 띠철근 설치 필요 벽체

## 사용 방법

### 방법 1 — 바로 열기 (로컬)

```bash
git clone https://github.com/YOUR_USERNAME/wall-rebar-ocr.git
cd wall-rebar-ocr
# index.html을 브라우저에서 직접 열기
open index.html        # macOS
start index.html       # Windows
xdg-open index.html   # Linux
```

### 방법 2 — GitHub Pages로 배포

1. 이 저장소를 Fork 또는 Clone
2. GitHub 저장소 → **Settings → Pages**
3. Source: `Deploy from a branch` → Branch: `main` / `/ (root)` → Save
4. `https://YOUR_USERNAME.github.io/wall-rebar-ocr/` 로 접속

### 방법 3 — 로컬 서버 실행

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .
```

브라우저에서 `http://localhost:8080` 접속

## 사용 순서

1. PDF 파일 드래그&드롭 또는 클릭해서 선택
2. 렌더링 해상도 선택 (기본: 표준 200dpi)
3. **OCR 분석 시작** 클릭
4. 결과 확인 후 **Excel 다운로드**

## 기술 스택

| 라이브러리 | 버전 | 용도 |
|-----------|------|------|
| [Tesseract.js](https://github.com/naptha/tesseract.js) | 5.x | 브라우저 OCR |
| [PDF.js](https://mozilla.github.io/pdf.js/) | 3.11 | PDF → 이미지 변환 |
| [SheetJS (xlsx)](https://sheetjs.com/) | 0.18 | Excel 파일 생성 |

## 도면 형식

본 도구는 아래 컬럼 구조의 벽체 배근일람표를 대상으로 합니다.

```
WALL기호 | 층 | 두께(mm) | 수직철근 | 단부보강근 | 수평철근
```

지원 벽체 타입: `W`, `CW`, `HW`, `MW`

## 파일 구조

```
wall-rebar-ocr/
└── index.html   # 단일 파일 앱 (HTML + CSS + JS 포함)
```

## 주의사항

- OCR 정확도는 PDF 화질과 폰트에 따라 달라질 수 있습니다
- 스캔 이미지 PDF보다 텍스트 삽입 PDF에서 더 정확합니다
- 처음 실행 시 Tesseract 영어 언어팩(약 4MB) 다운로드가 필요합니다

## 라이선스

MIT License
