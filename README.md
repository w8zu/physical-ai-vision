# Physical AI Vision

YOLOv8을 사용한 실시간 웹캠 기반 컴퓨터 비전 프로젝트입니다.

## 📋 목차
- [기능](#기능)
- [설치](#설치)
- [사용법](#사용법)
- [작동원리](#작동원리)
- [파일 설명](#파일-설명)

## 🎯 기능

### 1. **Object Detection (객체 탐지)**
- 실시간으로 웹캠에서 객체를 감지
- 바운딩 박스와 신뢰도 점수 표시
- 사람, 자동차, 동물 등 80개 클래스 감지 가능

### 2. **Classification (분류)**
- 웹캠 프레임을 이미지 카테고리로 분류
- ImageNet 데이터셋 기반의 1,000개 클래스 지원

### 3. **Segmentation (분할)**
- 픽셀 단위의 정확한 객체 경계 감지
- 각 객체를 다른 색상으로 마스크 표시
- 배경과 객체의 명확한 구분

### 4. **Object Tracking (객체 추적)**
- 프레임 간 객체의 이동 경로 추적
- 각 객체에 고유 ID 부여
- 객체의 일관된 추적으로 움직임 분석 가능

## 📦 설치

### 필수 패키지
```bash
pip install ultralytics opencv-python
```

또는 requirements.txt 사용:
```bash
pip install -r requirements.txt
```

## 🚀 사용법

### 1. Object Detection 실행
```bash
python webcam_detection.py
```

### 2. Classification 실행
```bash
python webcam_classification.py
```

### 3. Segmentation 실행
```bash
python webcam_segmentation.py
```

### 4. Object Tracking 실행
```bash
python webcam_tracking.py
```

### 프로그램 종료
- 웹캠 창에서 **'q' 키** 누르기
- 또는 터미널에서 **Ctrl + C** 입력

## 🔧 작동원리

### YOLOv8 (You Only Look Once v8)
- **실시간 객체 감지 모델**: 이미지를 한 번에 스캔해서 객체 위치와 클래스 예측
- **장점**: 매우 빠르고 정확한 성능
- **용도**: 자율주행차, 보안 시스템, 산업용 검사 등

### 각 모델의 차이

| 모델 | 파일명 | 특징 |
|------|--------|------|
| Detection | yolov8n.pt | 일반적인 객체 감지, 빠른 속도 |
| Classification | yolov8n-cls.pt | 전체 이미지의 카테고리 분류 |
| Segmentation | yolov8n-seg.pt | 객체의 정확한 경계선 감지 |
| Tracking | yolov8n.pt + track() | Detection에 ID 추적 기능 추가 |

### 작동 흐름
```
웹캠 입력 → YOLOv8 모델 → 결과 처리 → 화면 표시 → 반복
```

1. **웹캠 프레임 캡처**: OpenCV로 웹캠에서 실시간 프레임 수집
2. **모델 추론**: YOLOv8 모델이 프레임 분석
3. **결과 시각화**: 감지된 객체에 박스, 마스크, 또는 ID 표시
4. **화면 출력**: OpenCV imshow()로 결과 표시
5. **반복**: 'q' 키 입력까지 계속 반복

### 성능 지표
```
Speed: [전처리시간] preprocess, [추론시간] inference, [후처리시간] postprocess
```
- 일반적으로 **전체 처리 시간 = 15-30ms** (초당 30-60 프레임)

## 📁 파일 설명

### Python 스크립트
| 파일 | 설명 |
|------|------|
| `webcam_detection.py` | 객체 탐지 (Object Detection) |
| `webcam_classification.py` | 이미지 분류 (Classification) |
| `webcam_segmentation.py` | 픽셀 분할 (Segmentation) |
| `webcam_tracking.py` | 객체 추적 (Object Tracking) |

### 모델 파일
| 파일 | 크기 | 설명 |
|------|------|------|
| `yolov8n.pt` | ~6.3MB | Nano 모델 (가장 빠름) |

## 💡 팁

### 성능 최적화
- **더 빠른 속도**: `yolov8n.pt` 사용 (기본값)
- **더 높은 정확도**: `yolov8m.pt` 또는 `yolov8l.pt` 사용 (더 큼)

### 트러블슈팅
- **웹캠이 열리지 않음**: `cv2.VideoCapture(0)` 번호를 변경 (1, 2, ...)
- **느린 성능**: 화면 해상도 축소 또는 더 빠른 모델 선택
- **GPU 가속**: CUDA 지원 GPU가 있으면 자동으로 사용됨

## 📚 참고 자료
- [YOLOv8 공식 문서](https://docs.ultralytics.com/)
- [OpenCV 문서](https://docs.opencv.org/)

---

**작성자**: Claude AI  
**라이선스**: MIT
