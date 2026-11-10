# 연구의 기록 | Medical AI Lab

의료 AI 연구의 실험 조건, 평가 결과와 연구 노트를 관리하는 한국어 웹앱입니다.

## 주요 기능

- GP-Regularized Critic-Guided Diffusion, ALS 음성 사전탐지, Fundus 3-class, Brain MRI 종양 합성 프로젝트 관리
- 데이터셋, 모델 구조, 학습 조건과 실험 버전 기록
- 성능 지표 추가·숨기기·순서·비교 방향 커스터마이징
- 지표 원본 문자열 보존, 비교표와 그래프, 동일 평가 조건의 회귀 점검
- 최종 채택 모델 지정, 연구 노트와 변경 이력
- 보고서·발표용 요약, CSV/Markdown 내보내기, JSON 백업·복원
- 사용자별 서버 저장과 동시 수정 충돌 보호

## 기술 구성

React 19, TypeScript, Vinext/Vite, Cloudflare Workers, D1(SQLite), Drizzle.

## 로컬 실행

Node.js 22.13 이상이 필요합니다.

```sh
npm run install:ci
npm run build
node --import ./scripts/sites-env.mjs ./node_modules/wrangler/bin/wrangler.js d1 execute DB --local --config dist/server/wrangler.json --persist-to .wrangler/state --file drizzle/0000_chubby_expediter.sql
npm run dev
```

터미널에 표시되는 주소를 열고, 로컬 로그인 링크 `/signin-with-chatgpt?return_to=/`로 접속하면 테스트 계정으로 저장 기능을 사용할 수 있습니다. 데이터베이스 준비는 새 로컬 환경에서 한 번 수행합니다.

## 검증

```sh
npx tsc --noEmit
npm run build
```

## 배포

이 프로젝트는 서버 API와 D1 저장소를 사용하는 Sites 앱입니다. GitHub Pages의 정적 호스팅만으로는 저장·로그인 기능을 실행할 수 없습니다. `.openai/hosting.json`은 기존 Sites 프로젝트와 DB 바인딩을 가리킵니다. 다른 Sites 프로젝트로 배포할 경우 새 프로젝트 ID를 설정해야 합니다. Sites 외부에 배포하려면 D1 연결 및 사용자 인증 처리를 별도로 구성해야 합니다.

자세한 개발 환경과 로컬 D1 안내는 [DEVELOPMENT.md](DEVELOPMENT.md)를 참고하세요.

## 포함 범위

앱 소스, 패키지 잠금 파일, 스키마와 마이그레이션, 개발·빌드 설정을 포함합니다. 실제 연구 입력 데이터, 비밀 키, 로그인 세션, 로컬 테스트 DB, node_modules, 빌드 출력은 포함하지 않습니다.
