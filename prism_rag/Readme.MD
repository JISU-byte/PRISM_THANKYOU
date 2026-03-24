# PRISM - 공공 데이터 기반 AI 감사 분석 시스템

> **PRISM** (Public Risk Intelligence & Smart Management)  
> 공공기관 감사 결과 및 리스크 데이터를 시각화하고, RAG 기반 AI 챗봇과 감사 보고서 자동 생성을 지원하는 통합 인텔리전스 대시보드입니다.

---

## 📁 디렉터리 구조

```
PRISM_THANKYOU/
│
├── AURA/                           # 이전 기수 RAG 시스템 (참고용)
├── EvaluationMetric/               # RAG 평가 지표
├── metadata/                       # 감사 데이터 메타데이터
├── prism_rag/                      # RAG 백엔드 서버
│   ├── common/                     # 공통 설정 및 유틸리티
│   ├── rag/agentic_rag_v2/         # RAG 파이프라인
│   │   └── modules/                # 검색, 생성, 평가 모듈
│   └── web_app/
│       ├── backend/main.py         # FastAPI 백엔드
│       └── frontend/app_final.py   # Streamlit 대시보드
├── streamlit/                      # Streamlit 버전별 히스토리
├── data/                           # 데이터셋 (별도 공유)
├── _crew/                          # 팀원 소개
├── .env.example                    # 환경변수 예시
└── requirement.txt                 # 패키지 목록
```

---

## 🛠 기술 스택

| 분류 | 내용 |
|------|------|
| Frontend | Streamlit |
| Backend | FastAPI |
| AI / RAG | LangChain, Milvus, BM25 |
| Database | Milvus (Vector DB), Redis |
| Infra | Docker |

---

## 🚀 실행 방법

### 1. 레포 클론

```bash
git clone https://github.com/JISU-byte/PRISM_THANKYOU.git
cd PRISM_THANKYOU
```

### 2. 가상환경 설정

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate

pip install -r requirement.txt
```

### 3. 환경변수 설정

`.env.example`을 복사해서 `.env` 파일 생성 후 API 키 입력

```bash
cp .env.example .env
```

### 4. Docker로 Milvus 실행

```bash
cd prism_rag
docker-compose up -d
```

확인:
```bash
docker ps
# milvus-standalone, milvus-etcd, milvus-minio 3개가 Up 상태여야 합니다
```

### 5. Milvus 데이터 업로드 (최초 1회)

```bash
python prism_rag/upload_to_milvus.py
```

### 6. 백엔드 서버 실행

```bash
python prism_rag/web_app/backend/main.py
```

정상 실행 시:
```
✅ BM25 Index Ready
🔹 VectorRetriever Ready!
INFO: Uvicorn running on http://0.0.0.0:8000
```

### 7. Streamlit 대시보드 실행

새 터미널에서:
```bash
streamlit run prism_rag/web_app/frontend/app_final.py
```

브라우저에서 `http://localhost:8501` 접속 후 **AI 분석** 탭에서 테스트

---

## ⚠️ 주의사항

- `data/` 폴더의 데이터셋은 용량 문제로 별도 공유 (구글 드라이브)
- `.env` 파일은 절대 깃허브에 올리지 마세요 (API 키 포함)

---

## ❗ 자주 발생하는 오류

| 오류 | 원인 | 해결 |
|------|------|------|
| `MilvusException: Fail connecting` | Docker 꺼짐 | `docker-compose up -d` 재실행 |
| `address already in use` | 포트 8000 충돌 | `kill $(lsof -t -i:8000)` 후 재시작 |
| `Failed to load corpus` | BM25 캐시 오류 | `bm25_cache.pkl` 삭제 후 재시작 |
| `audit_v10.json not found` | 데이터셋 없음 | 데이터셋 별도 요청 |

---

## 📌 시스템 정보

| 항목 | 값 |
|------|-----|
| 백엔드 포트 | 8000 |
| 프론트엔드 포트 | 8501 |
| Milvus 포트 | 19530 |
| 데이터셋 | audit_v10.json |
| RAG 모듈 | agentic_rag_v2 |
