<div align="center">
  
# 🌉 복지이음 *(Bokji-Eum)*  
### AI 기반 개인 맞춤형 복지 추천 서비스  
**WeBridge | 2025 새싹 해커톤 – AI 서비스 부문**

<br/>

<img src="https://img.shields.io/badge/AI-RAG%20Engine-blue?style=for-the-badge"/>
<img src="https://img.shields.io/badge/Frontend-React-61DAFB?style=for-the-badge&logo=react&logoColor=white"/>
<img src="https://img.shields.io/badge/Backend-Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"/>
<img src="https://img.shields.io/badge/AI%20Server-FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
<img src="https://img.shields.io/badge/VectorDB-ChromaDB-orange?style=for-the-badge"/>

<br/><br/>

**“누구나 말만 하면 받을 수 있는 복지 혜택을 알려주는 서비스”**

</div>

---

<br/>

## 📌 **서비스 개요**

**복지이음(Bokji-Eum)** 은 사용자의 **음성·텍스트 입력**을 이해하고  
개인의 **연령, 소득, 가구 구조, 상황 정보**에 따라 가장 적합한 복지 프로그램을 추천하는  
**AI 대화형 복지 서비스**입니다.

- 🗣 **음성 기반 설문 (Whisper STT)**
- 🔍 **LLM + RAG 기반 의미 검색 추천**
- 📄 **복지 안내서 PDF → 자동 JSON 구조화**
- 🎧 **프로그램 설명 음성 안내(TTS)**
- ⭐ **게스트 모드 + 즐겨찾기 저장 기능**

<br/>

---

## 🧠 **AI 추천 엔진 구조**

### 🚀 RAG 기반 추천 흐름
```

사용자 입력(음성/텍스트)
↓
STT(Whisper) / 설문 JSON화
↓
LLM 전처리 & Embedding 생성
↓
ChromaDB 의미 기반 검색 (70%)
↓
Keyword 보조 검색 (30%)
↓
Rule-based 필터링(연령·소득·가구형태)
↓
최종 매칭 점수 계산
↓
복지 프로그램 추천 결과

```

- Embedding 모델: `text-embedding-3-small`
- Vector DB: ChromaDB
- AI 분석: GPT-3.5/4  
- Category 추론: Few-shot Learning

<br/>

---

## 🎨 **주요 화면 (UI/UX)**

복지이음은 음성 기반 접근성과 시니어 친화 UI를 중심으로  
누구나 쉽게 복지 추천을 받을 수 있도록 설계되었습니다.

---

### 🏠 1. 홈 화면 (Landing)
- 서비스 소개
- 회원가입 없이 바로 시작 가능한 **게스트 모드**

### 📝 2. 설문 입력 (Assessment)
- 연령, 가구 형태, 소득 등 기본 정보 입력
- 선택한 카테고리(생계·취업·보건·임신 등)에 따라 질문 자동 변경

### 🎤 3. 음성 설문 (Voice Assessment)
- Whisper 기반 음성 인식
- 말한 내용을 즉시 텍스트로 변환하여 확인 가능
- ‘다시 말하기 / 확인’ 기능 제공

### ✔️ 4. 정보 확인 (Confirmation)
- 입력 정보 요약 카드 표시
- 수정 후 다시 제출 가능

### 🎯 5. 추천 결과 (Results)
- AI 기반 맞춤형 복지 프로그램 추천
- 프로그램 설명, 자격 사유, 신청 방법 요약 제공
- 음성 안내(TTS), 저장 기능 포함

### 📄 6. 프로그램 상세 (Program Details)
- 지원 내용 · 자격 · 혜택 · 문의처 정리
- 태그 기반 추가 정보(연령대/소득/지역 등)
- 전체 내용을 음성으로 읽어주기

### ⭐ 7. 저장 목록 (Saved Programs)
- 로그인 시 관심 프로그램 저장/관리 가능

<br/>

---

# 🗂 **데이터 파이프라인**

### 📄 원본 데이터
| 데이터 | 출처 | 형식 |
|--------|--------|-------|
| 나에게 힘이 되는 복지서비스 2024 | 보건복지부 | PDF |
| 나에게 힘이 되는 복지서비스 2025 | 보건복지부 | PDF |
| 중위소득 기준 | 보건복지부 | JSON |
| 복지 프로그램 | LangChain 파싱 | JSON |

### 🔧 자동 처리 과정
```

PDF → 텍스트 파싱 → JSON 구조화 → 속성 태깅 → 임베딩 생성 → ChromaDB 저장

````

<br/>

---

## 🏗 **전체 시스템 아키텍처**

```text
[ React Web (설문·음성 입력, UI) ]
          ↓ REST API
[ Spring Boot 서버 ]
  ├─ JWT 인증 / 회원관리
  ├─ 설문 저장
  ├─ 음성(STT) 처리 (Whisper API)
  └─ 추천 요청 중계
          ↓ HTTP
[ FastAPI AI 서버 ]
  ├─ LangChain RAG Engine
  ├─ GPT 기반 분석
  └─ ChromaDB Vector Search
````

<br/>

---

## 🗄 **데이터베이스 구조 (MySQL)**

### 핵심 테이블

* `users` – 회원 정보
* `user_profile` – 연령/가구형태/소득 등
* `saved_benefits` – 즐겨찾기
* `welfare_policies` – 파싱된 복지프로그램
* `policy_tags` – 연령·소득·지역 등 태그
* `user_responses` – 사용자의 설문
* `questionnaire_questions` – 카테고리별 질문

<br/>

---

## 💻 **기술 스택**

### ✔ Frontend

* React (Vite)
* Typescript
* TailwindCSS + shadcn/ui
* React Router
* Browser SpeechSynthesis(TTS)

### ✔ Backend

* Spring Boot
* Spring Security + JWT
* MySQL
* Whisper API (STT)

### ✔ AI Server

* FastAPI
* LangChain
* OpenAI GPT-3.5/4
* ChromaDB

<br/>

---

## 📈 **기대 효과**

### ✔ 사회적 효과

* 디지털 약자를 위한 음성 기반 복지 안내
* 복지 사각지대 해소
* 방대한 PDF 문서를 검색할 필요 없음

### ✔ 경제적 효과

* 복지 신청률 상승 → 예산 미집행 감소
* 가구 단위 생활 안정 및 지역경제 활성화

<br/>

---

# 👥 **Team WeBridge**

| 이름  | 역할                |
| --- | ----------------- |
| 이현주 | AI 모델 |
| 한지원 | 백엔드 |

<br/>

---

<div align="center">

💡 *더 나은 복지 정보 접근을 위한 첫걸음, 복지이음.*

</div>
