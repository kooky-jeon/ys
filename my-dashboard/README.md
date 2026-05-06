# 기업 재무건강 체크 대시보드

재무 데이터를 입력하면 주요 지표(유동비율, 부채비율, ROE, 이자보상배율)를 자동 계산하고,
업종 평균과 비교해 신호등 형태로 시각화하며 Claude AI가 진단 코멘트를 생성합니다.

---

## 폴더 구조

```
my-dashboard/
├── api/
│   └── analyze.js      ← Vercel 서버리스 함수 (API 키 보관)
├── index.html          ← 대시보드 프론트엔드
├── vercel.json         ← Vercel 설정
├── .gitignore
└── README.md
```

---

## 배포 방법

### 1단계 — GitHub 저장소 생성 및 Push

```bash
git init
git add .
git commit -m "첫 배포"
git remote add origin https://github.com/your-id/my-dashboard.git
git push -u origin main
```

### 2단계 — Vercel 배포

1. [vercel.com](https://vercel.com) 접속 후 GitHub 계정으로 로그인
2. **Add New Project** → 방금 Push한 저장소 선택
3. **Deploy** 클릭 (별도 설정 불필요)

### 3단계 — API 키 환경변수 등록

1. Vercel 대시보드 → 프로젝트 선택 → **Settings → Environment Variables**
2. 아래 값 입력 후 **Save**

| Name | Value |
|------|-------|
| `ANTHROPIC_API_KEY` | `sk-ant-xxxxxxxxxxxxxxxx` |

3. **Deployments → Redeploy** 클릭 (환경변수 적용)

### 4단계 — 접속 확인

`https://your-project.vercel.app` 주소로 접속하면 완료입니다.

---

## API 키 발급

[console.anthropic.com](https://console.anthropic.com) → **API Keys** → **Create Key**

---

## 주요 기능

- 6개 업종 벤치마크 비교 (제조업, IT, 유통, 금융, 건설, 의료)
- 신호등 분석: 초록(양호) / 노랑(주의) / 빨강(위험)
- 레이더 차트: 내 기업 vs 업종 평균 시각화
- Claude AI 자동 재무 진단 코멘트
- 다크모드 자동 지원

---

## 보안 주의사항

- `ANTHROPIC_API_KEY`는 절대 `index.html`이나 소스코드에 직접 입력하지 마세요.
- `.env` 파일은 `.gitignore`에 포함되어 GitHub에 업로드되지 않습니다.
- API 키는 Vercel 환경변수에만 저장하며, 서버 함수(`api/analyze.js`)에서만 사용됩니다.
