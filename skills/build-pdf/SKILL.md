---
name: build-pdf
description: "마스킹된 이력서 Markdown을 실제 개인정보로 치환하고 PDF로 변환하는 방법을 안내합니다. 'PDF 만들어줘', 'PDF 빌드', '이력서 출력' 등의 요청 시 사용합니다."
argument-hint: "[이력서 MD 파일 경로]"
allowed-tools: Read, Bash, Glob
---

이력서 Markdown 파일의 마스킹 토큰을 실제 개인정보로 치환하고, PDF로 변환하는 방법을 안내합니다.

---

## 단계 1: 마스킹 토큰 치환

이력서 Markdown에는 개인정보가 마스킹 토큰으로 대체되어 있습니다:

| 토큰 | 용도 |
|------|------|
| `[마스킹:성명]` | 지원자 이름 |
| `[마스킹:연락처]` | 전화번호 |
| `[마스킹:이메일]` | 이메일 주소 |
| `[마스킹:주소]` | 거주지 주소 |
| `[마스킹:생년월일]` | 생년월일 |

### 방법 A: 수동 치환 (간편)

1. 이력서 MD 파일을 열어 마스킹 토큰을 직접 실제 값으로 바꿉니다
2. 예: `[마스킹:성명]` → `홍길동`

### 방법 B: personal_info.json 자동 치환 (권장)

1. 이력서 MD 파일과 같은 디렉토리에 `personal_info.json`을 생성합니다:

```json
{
  "성명": "홍길동",
  "연락처": "010-1234-5678",
  "이메일": "hong@example.com",
  "주소": "서울시 강남구",
  "생년월일": "1990.01.01"
}
```

2. 다음 명령으로 치환합니다:

```bash
# sed를 사용한 치환 예시 (bash)
sed -e 's/\[마스킹:성명\]/홍길동/g' \
    -e 's/\[마스킹:연락처\]/010-1234-5678/g' \
    -e 's/\[마스킹:이메일\]/hong@example.com/g' \
    이력서_최적화.md > 이력서_최종.md
```

> `personal_info.json` 파일이 없으면 위 템플릿을 생성하고 사용자에게 값을 입력하도록 안내하세요.

---

## 단계 2: PDF 변환

### 방법 A: pandoc 사용 (간편, 권장)

```bash
# pandoc이 설치되어 있는 경우
pandoc 이력서_최종.md -o 이력서_최종.pdf --pdf-engine=xelatex -V mainfont="맑은 고딕"
```

pandoc이 없다면:
```bash
# 설치 (Windows)
winget install --id JohnMacFarlane.Pandoc

# 설치 (macOS)
brew install pandoc
```

### 방법 B: 브라우저 인쇄 (가장 간편)

1. Markdown을 HTML로 변환합니다:
```bash
pandoc 이력서_최종.md -o 이력서_최종.html
```

또는 VS Code에서 Markdown Preview로 열기

2. 브라우저에서 HTML을 열고 `Ctrl+P` → "PDF로 저장"

### 방법 C: build_resume.py 사용 (고급)

> 이 방법은 `job_expert` 프로젝트를 보유한 경우에만 사용 가능합니다.

```bash
# job_expert 프로젝트 디렉토리에서 실행
cd /path/to/job_expert
python build_resume.py
```

요구사항:
- Python 3.10+
- Playwright + Chromium (`playwright install chromium`)
- `personal_info.json` 파일
- `02_output/` 하위에 이력서 MD 파일 배치

이 스크립트는 마스킹 치환 + MD→HTML→PDF 변환을 자동으로 수행합니다.
CSS 기반 이력서 디자인 템플릿이 적용됩니다.

---

## 개인정보 보호 경고

- `personal_info.json`은 **절대 외부에 전송하지 않습니다** (로컬 실행 전용)
- 치환 후 생성된 최종 파일(MD/HTML/PDF)에는 실제 개인정보가 포함되므로 **공유 시 주의**하세요
- 마스킹된 버전(원본)은 별도로 보관하세요
- Git에 커밋할 때 `personal_info.json`과 최종 파일은 `.gitignore`에 추가하세요
