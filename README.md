📘 Noise-Robust License Plate Recognition with YOLOv10
📌 프로젝트 개요

이 프로젝트는 노이즈 환경에서의 한국 번호판 문자 인식 성능 개선을 목표로 합니다.
기존 번호판 인식 모델들은 깨끗한 환경에서는 높은 성능을 보였지만, 눈·흙·오염 등으로 번호판 일부가 가려진 경우 인식률이 급격히 저하되는 문제가 있었습니다.

본 연구에서는 YOLO 계열 모델(YOLOv3, YOLOv4s, YOLOv10n)을 비교하고, **데이터 증강·confidence threshold 조정·자모음 기반 후처리(post-processing)**를 적용하여 성능을 개선했습니다

69eb4ee7-6111-44d8-8301-743476b…

.

🚀 연구 목표

경량 YOLO 모델 비교: YOLOv3, YOLOv4s, YOLOv10n 성능 및 연산 효율성 분석

노이즈 학습 데이터 생성: 실제 오염 영역을 합성해 노이즈 포함 학습 데이터 제작

Confidence Threshold 조정 + 후처리: 미검출을 줄이고, 증가한 오검출은 IoU 기반 후처리로 제거

자모음 기반 후처리 제안: 음절뿐 아니라 자음·모음까지 검출 후 신뢰도를 결합해 최종 인식률 개선

69eb4ee7-6111-44d8-8301-743476b…

🏗 모델 구조 요약

YOLOv3: Darknet-53, 약 48M 파라미터, 95 GFLOPs (높은 연산량)

YOLOv4s: CSPDarknet-53, 약 6.5M 파라미터, 22 GFLOPs (경량화)

YOLOv10n: RepVGG 기반, 약 2.3M 파라미터, 6.7 GFLOPs (가장 효율적)

69eb4ee7-6111-44d8-8301-743476b…

📊 실험 결과
모델	학습 데이터	Confidence	후처리	성능 요약
YOLOv3	노이즈X	0.25	X	미검출 많음
YOLOv4s	노이즈X	0.25	X	오검출 많음
YOLOv10n	노이즈X	0.25	X	상대적으로 안정적
YOLOv10n (70 classes)	노이즈 포함	0.1	✅ 제안 후처리	최고 성능 달성 (FN=5, FP=0, 오류=11)

69eb4ee7-6111-44d8-8301-743476b…

➡️ **YOLOv10n (70 클래스 + 제안 후처리)**가 노이즈 환경에서 가장 강인한 성능을 보였음.

🎯 결론

YOLOv10n은 적은 파라미터와 연산량으로 임베디드 환경에 적합하면서도 높은 성능을 달성함

제안된 자모음 기반 후처리 기법을 적용하면 노이즈 환경에서도 인식 성능이 크게 향상됨

최종적으로, 노이즈 환경 한국 번호판 인식 문제에 대한 실용적 해결책을 제시함

69eb4ee7-6111-44d8-8301-743476b…

⚙️ 실행 방법 (예시: Colab)
# 저장소 클론
git clone https://github.com/yourusername/NoiseRobust-LPR-YOLOv10.git
cd NoiseRobust-LPR-YOLOv10

# 패키지 설치
pip install -r requirements.txt

# 학습 실행
python train.py --model yolov10n --data dataset.yaml --epochs 800 --imgsz 640

# 추론 실행
python detect.py --weights runs/train/exp/weights/best.pt --source test_images/

👤 저자

이동관 (DongGwan Lee), Hongik University

김재민 (Jaemin Kim), Hongik University

69eb4ee7-6111-44d8-8301-743476b…# NoiseAware-License-Plate-Recognition
