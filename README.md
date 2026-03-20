# PRISM — 감사 리스크 인텔리전스 대시보드

> 모두의연구소 AIFFELTHON 참가 프로젝트 (감사합니다팀)  
> Original Repository: [jinheeus/AIFFEL_QUEST](https://github.com/jinheeus/AIFFEL_QUEST)

공공기관 감사 결과 및 리스크 데이터를 시각화하고,  
RAG 기반 AI 챗봇과 감사 보고서 자동 생성을 지원하는 통합 인텔리전스 대시보드입니다.

---

## 본인 기여 내용 (My Contribution)

- **데이터 정제**: 감사 데이터 전처리 및 정제 작업 일부 담당 (risk_category)
- **프롬프트 튜닝**: RAG 챗봇의 응답이 실제 문서 내용을 정확하게 반영하도록 프롬프트 개선
- **응답 품질 검토**: 생성된 응답의 정확도와 일관성을 수기로 검토하며 품질 개선

---

## 기술 스택

`Python` `Streamlit` `RAG` `FastAPI` `LangChain`

---

## 실행 방법

1. 레포지토리 클론 후 가상환경 생성
2. 패키지 설치: `pip install -r requirements.txt`
3. 실행: `streamlit run app_final.py`

> AI 검색 기능은 로컬 환경(http://localhost:8000)에 RAG 백엔드 서버 구동 필요
