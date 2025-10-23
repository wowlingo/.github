# WowLingo

> 농난청인을 위한 AI 기반 한국어 학습 플랫폼

WowLingo는 청각 장애가 있는 학습자들이 음성 기반 인터랙티브 게임을 통해 한국어를 효과적으로 학습할 수 있도록 돕는 웹 애플리케이션입니다.

## 프로젝트 개요

WowLingo는 음성 합성 기술과 게임화된 학습 경험을 결합하여 농난청인을 위한 맞춤형 한국어 교육 솔루션을 제공합니다. 사용자는 다양한 게임 타입을 통해 한국어 단어와 문장을 듣고, 정답을 선택하며, 실시간 피드백을 받을 수 있습니다.

### 주요 특징

- 🎧 **음성 기반 학습**: 정상 속도와 느린 속도로 한국어 음성 재생
- 🎮 **4가지 게임 레이아웃**: 랜덤으로 선택되는 다양한 게임 타입으로 지루하지 않은 학습
- 🤖 **AI 기반 추천**: 학습자의 수준과 진행 상황에 맞는 맞춤형 학습 경로 제공
- 📊 **실시간 진행도 추적**: 문제별 정답/오답 및 소요 시간 기록
- 🎨 **직관적인 피드백**: 정답/오답에 따른 즉각적인 시각적 피드백
- 📱 **모바일 최적화**: 반응형 디자인으로 언제 어디서나 학습 가능

## 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│                    WowLingo Platform                    │
└─────────────────────────────────────────────────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
        ▼                   ▼                   ▼
┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│   Frontend   │   │   Backend    │   │      AI      │
│  (React +    │◄─►│  (NestJS +   │◄─►│   (Python)   │
│  TypeScript) │   │   MySQL)     │   │              │
└──────────────┘   └──────────────┘   └──────────────┘
```

## 저장소 구조

### 🎨 [wowlingo-client](https://github.com/wowlingo/wowlingo-client)

프론트엔드 애플리케이션 (React + TypeScript + Vite)

**주요 기능**:
- 4가지 학습 레이아웃 (케이크 스택, 고양이 스택, 카드 뒤집기 등)
- 음성 재생 (정상 속도, 느린 속도)
- 실시간 진행도 추적 및 결과 화면
- 반응형 디자인 (모바일 우선)

**기술 스택**:
- React 18, TypeScript
- Vite (빌드 도구)
- Tailwind CSS (스타일링)
- Zustand (상태 관리)
- React Router v6 (라우팅)

### 🔧 [wowlingo-be](https://github.com/wowlingo/wowlingo-be)

백엔드 API 서버 (NestJS + TypeORM + MySQL)

**주요 기능**:
- RESTful API 제공
- 퀘스트 및 문제 데이터 관리
- 사용자 학습 결과 저장 및 분석
- AI 서버와의 통신

**기술 스택**:
- NestJS (프레임워크)
- TypeORM (ORM)
- MySQL (데이터베이스)
- JWT (인증)

### 🤖 [wowlingo-ai](https://github.com/wowlingo/wowlingo-ai)

AI 기반 학습 추천 시스템 (Python)

**주요 기능**:
- 학습자 수준 분석
- 맞춤형 학습 경로 추천
- 난이도 조정
- 학습 패턴 분석

**기술 스택**:
- Python
- Machine Learning 라이브러리
- Apache 2.0 License

## 빠른 시작

### 전체 시스템 실행

#### 1. 백엔드 서버 실행

```bash
# wowlingo-be 디렉토리로 이동
cd wowlingo-be

# 의존성 설치
npm install

# 환경 변수 설정
cp .env.example .env
# .env 파일에서 데이터베이스 설정

# 데이터베이스 마이그레이션
npm run migration:run

# 개발 서버 실행
npm run start:dev
```

백엔드 서버가 http://localhost:3000 에서 실행됩니다.

#### 2. AI 서버 실행 (선택사항)

```bash
# wowlingo-ai 디렉토리로 이동
cd wowlingo-ai

# 가상 환경 생성 및 활성화
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 설치
pip install -r requirements.txt

# AI 서버 실행
python main.py
```

#### 3. 프론트엔드 실행

```bash
# wowlingo-client 디렉토리로 이동
cd wowlingo-client

# 의존성 설치
npm install

# 환경 변수 설정
echo "VITE_API_URL=http://localhost:3000/api" > .env.local

# 개발 서버 실행
npm run dev
```

프론트엔드가 http://localhost:5173 에서 실행됩니다.

## 학습 흐름

```
1. 홈 화면
   ↓
2. 퀘스트 선택
   ↓
3. 학습 인트로 (레이아웃 랜덤 선택)
   ↓
4. 문제 풀이 (10문제)
   ├─ 음성 듣기 (정상/느린 속도)
   ├─ 답변 선택
   ├─ 정답/오답 피드백
   └─ 다음 문제로 이동
   ↓
5. 결과 화면
   ├─ 정답 개수 및 정답률
   ├─ 총 소요 시간
   └─ 레이아웃별 완료 이미지
   ↓
6. 백엔드로 결과 전송
   ↓
7. AI 분석 (다음 학습 추천)
```

## 퀘스트 타입

### 📝 statement-question
문장과 질문을 듣고 정답 선택
- 예: "나는 학교에 갑니다" → "어디에 가나요?" → [학교 / 집 / 공원]

### 🔄 same-different
두 문장을 듣고 같은지 다른지 판단
- 예: "안녕하세요" vs "안녕히 가세요" → [같음 / 다름]

### ✅ choice
음성을 듣고 여러 선택지 중 정답 선택
- 예: "사과" → [사과 / 배 / 바나나 / 포도]

## 개발 환경 요구사항

### Frontend
- Node.js >= 18
- npm >= 9

### Backend
- Node.js >= 18
- MySQL >= 8.0
- npm >= 9

### AI
- Python >= 3.9
- pip

## 기여하기

WowLingo는 오픈 소스 프로젝트입니다. 기여를 환영합니다!

### 기여 방법

1. **이슈 생성**: 버그 리포트나 기능 제안을 이슈로 등록해주세요
2. **Fork & PR**: 저장소를 포크하고 Pull Request를 보내주세요
3. **코드 리뷰**: 다른 기여자의 PR을 리뷰해주세요

### 개발 가이드라인

- **코드 스타일**: 각 저장소의 ESLint/Prettier 설정을 따릅니다
- **커밋 메시지**: Conventional Commits 규칙을 따릅니다
  - `feat:` 새로운 기능
  - `fix:` 버그 수정
  - `docs:` 문서 변경
  - `refactor:` 코드 리팩토링
  - `test:` 테스트 추가/수정
- **브랜치 전략**: Git Flow를 따릅니다
  - `main`: 프로덕션 브랜치
  - `develop`: 개발 브랜치
  - `feature/*`: 기능 개발 브랜치
  - `fix/*`: 버그 수정 브랜치

## 라이선스

각 저장소의 라이선스를 참고하세요.

- **wowlingo-client**: 저장소 참고
- **wowlingo-be**: 저장소 참고
- **wowlingo-ai**: Apache 2.0 License

## 팀 & 문의

프로젝트에 대한 문의사항이나 버그 리포트는 각 저장소의 GitHub Issues를 이용해주세요.

## 데모

<!-- 데모 링크나 스크린샷을 여기에 추가하세요 -->

---

**WowLingo**로 더 나은 한국어 학습 경험을 만들어가고 있습니다. ⭐

[![GitHub stars](https://img.shields.io/github/stars/wowlingo?style=social)](https://github.com/wowlingo)
