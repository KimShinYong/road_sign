# YOLOv8 기반 도로 표지판(Object Detection) 실습 과제
Kaggle **Road Sign Detection** 데이터셋을 YOLO 포맷으로 변환한 뒤, **YOLOv8** 모델로 학습하고 예측 결과 이미지를 저장/정리한 실습입니다.

- Dataset: Kaggle Road Sign Detection (andrewmvd/road-sign-detection)
- Model: YOLOv8s
- Classes(4): `trafficlight`, `stop`, `speedlimit`, `crosswalk`

---

## 0. 실습 환경

- Google Colab
- Python 3.x
- Ultralytics YOLOv8

설치:
```bash
pip install ultralytics
```
# (1) 데이터셋 준비
### 1-1. 데이터셋 다운로드/압축 해제

Kaggle에서 받은 zip(roadSign.zip)을 Colab에 업로드 후 압축 해제
> 데이터셋 이미지 개수: 877장 (png)
### 1-2. YOLO 학습 가능한 폴더 구조 구성

```
road_sign_datasets/
└── SIGN/
    ├── images/
    │   ├── train2007/
    │   ├── val2007/
    │   └── test2007/
    └── labels/
        ├── train2007/
        ├── val2007/
        └── test2007/
```
### 1-4. XML → YOLO 라벨 변환 (수업 방식: convert2Yolo)

수업 실습 방식과 동일하게 convert2Yolo를 사용
### 1-5. train/val/test 랜덤 분할 + 이미지 복사

전체 877장
랜덤 분할(seed=42) 결과: train: 615 / val: 175 / test: 87

### 1-6. .yaml 작성

```
path: /content/road_sign_datasets/SIGN
train: images/train2007
val: images/val2007
test: images/test2007

nc: 4
names: ['trafficlight', 'stop', 'speedlimit', 'crosswalk']
```

# (2) YOLOv8 학습 (loss, metrics 확인)
### 2-1. 학습 실행 (YOLOv8s)
<img width="2400" height="1200" alt="results" src="https://github.com/user-attachments/assets/7f7ba24f-0a6c-4cb4-8bb6-c6af72511fd7" />

### 2-2. 학습 로그(loss/metrics) 시각화
<img width="543" height="773" alt="image" src="https://github.com/user-attachments/assets/b943a7fe-a8bf-43a3-9679-51ca0c5cb967" />

# (3) 객체 탐지 테스트
예측 수행

# (4) 결과 정리 (캡처)
예측 결과에서 표지판을 바운딩 박스로 탐지하는 것을 확인했습니다.
![val_batch0_pred](https://github.com/user-attachments/assets/5bfeede2-f0f8-49f0-9ed3-6443cc0a1023)
![val_batch1_pred](https://github.com/user-attachments/assets/d69a796b-f3e8-462b-8af0-cdd3835c8fbc)
![val_batch2_pred](https://github.com/user-attachments/assets/23cc570b-1ec0-4a40-9cb4-d05ba6b02574)


