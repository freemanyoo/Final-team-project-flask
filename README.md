# Final-team-project-flask

AI 기반 음식 이미지 분석 서버 - Flask AI 서버

## 개발환경

Java 17, Spring Boot 3.5.4, Flutter SDK 3.9.2, MariaDB, MongoDB, QueryDSL 5.0.0, JWT, Flask 2.3.0, PyTorch 2.0.0, Google Maps API, YouTube API v3, OAuth2 (Google, Naver)

## 개요

Flask 기반 AI 서버로, EfficientNet 딥러닝 모델을 사용하여 음식 이미지를 분석하고 Top-3 예측 결과를 제공하는 REST API 서버입니다.

## 주요 기능

### 🤖 음식 이미지 분석
- EfficientNet-B0 모델을 사용한 음식 분류
- Top-3 예측 결과 및 신뢰도 제공
- BiRefNet을 활용한 배경 제거 (선택적)

### 📊 지원 음식 클래스
현재 5가지 음식 클래스를 지원합니다:
- 감바스
- 숯불치킨
- 양념치킨
- 파스타
- 후라이드치킨

## 기술 스택

- **Flask 2.3.0**: 웹 프레임워크
- **PyTorch 2.0.0**: 딥러닝 프레임워크
- **Torchvision 0.15.0**: 이미지 전처리
- **Transformers 4.30.0**: BiRefNet 배경 제거 모델
- **Pillow 10.0.0**: 이미지 처리

## API 엔드포인트

### POST /analyze
음식 이미지를 분석하여 예측 결과를 반환합니다.

**요청:**
- Content-Type: `multipart/form-data`
- 파라미터: `image` (이미지 파일)
- 쿼리 파라미터: `remove_bg` (선택, 기본값: false)

**응답:**
```json
{
  "class": "파스타",
  "confidence": 95.5,
  "top3": [
    {"class": "파스타", "confidence": 95.5},
    {"class": "감바스", "confidence": 3.2},
    {"class": "양념치킨", "confidence": 1.3}
  ]
}
```

### POST /classify
테스트용 이미지 분류 API (웹 인터페이스용)

## 설치 및 실행

### 1. 의존성 설치

```bash
pip install -r requirements.txt
```

### 2. 모델 파일 준비

프로젝트 루트에 `efficientnet_finetuned_best.pth` 모델 파일이 필요합니다.

### 3. 서버 실행

```bash
python app.py
```

서버는 기본적으로 `http://localhost:5001`에서 실행됩니다.

## 설정

### 포트 변경
`app.py`의 `FLASK_PORT` 변수를 수정하여 포트를 변경할 수 있습니다.

### 배경 제거 활성화/비활성화
`ENABLE_BACKGROUND_REMOVAL` 변수를 `True`/`False`로 설정:
- `True`: BiRefNet을 사용한 배경 제거 (느리지만 정확도 향상)
- `False`: 배경 제거 없이 처리 (빠른 처리)

### 디바이스 설정
자동으로 사용 가능한 디바이스를 감지합니다:
- Apple Silicon (MPS)
- CUDA GPU
- CPU

## Spring Boot 연동

이 Flask 서버는 Spring Boot 백엔드 서버에서 호출됩니다:
- Spring Boot의 `AIAnalysisService`가 `/analyze` 엔드포인트를 호출
- 분석 결과를 JSON 형식으로 반환

## 주의사항

- 모델 파일(`efficientnet_finetuned_best.pth`)이 프로젝트 루트에 있어야 합니다
- GPU가 있는 경우 자동으로 사용하지만, CPU만으로도 동작 가능합니다
- 배경 제거 기능은 메모리를 많이 사용하므로 필요시 비활성화하세요

## 라이선스

이 프로젝트는 팀 프로젝트입니다.
