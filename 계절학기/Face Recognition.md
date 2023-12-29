# 0. 학습 목표
- Google Colab의 기본적인 사용법을 익힌다.
- OpenCV API를 사용하여 이미지 처리를 해본다.
- face recognition를 사용하여 얼굴인식 기능 개발을 해본다.

# 1. Google Colab이란?
> 구글이 제공하는 클라우드 기반 Jupyter Notebook 환경
- 머신 러닝, 딥 러닝, 데이터 분석에 사용한다.
- 무료이며, 구글 드라이브와 연동하여 노트북 파일을 저장하고 공유할 수 있다.
- 구글 클라우드 플랫폼과 연동되어 GPU나 TPU 같은 하드웨어 가속기를 사용할 수 있다. 이를 통해 대용량 데이터셋을 처리하거나, 복잡한 모델을 학습하는 등의 작업을 빠르게 처리할 수 있다.
- TensorFlow, PyTorch, Keras, NumPy, Pandas 등 다양한 라이브러리들이 이미 설치되어 있어 사용자들은 추가적인 설치나 설정 없이 바로 사용할 수 있다.


# 2. 기본 과제
## 코드 스니펫
> 재사용 가능한 소스 코드, 기계어, 텍스트의 작은 부분

- `도움말 > 코드 스니펫 검색`    
<img src="https://github.com/namoo1818/TIL/assets/50236187/c6000fa6-2d30-4ff7-ac83-625ac28648e9" width=300>

- `Visualization: Linked Brushing in Altair` 검색
<img src="https://github.com/namoo1818/TIL/assets/50236187/120b8524-464b-47a3-bbd8-7ebfb59a7ce4" width=500>

## Visualization: Linked Brushing in Altair
> 맞춤형 히스토그램을 만들기 위한 다양한 연산 작업을 제공
- 아래 예시는 나라별 가속-MSG, 마력-MSG 그래프
```python
# load an example dataset
from vega_datasets import data
cars = data.cars()

import altair as alt

interval = alt.selection_interval()

base = alt.Chart(cars).mark_point().encode(
  y='Miles_per_Gallon',
  color=alt.condition(interval, 'Origin', alt.value('lightgray'))
).properties(
  selection=interval
)

base.encode(x='Acceleration') | base.encode(x='Horsepower')
```
![Visualization](https://github.com/namoo1818/TIL/assets/50236187/8882e669-1083-4ec9-93cd-3d211979b27d)

## Google Drive 연동
```python
from google.colab import drive
drive.mount('/gdrive')
```

## matplotlib 와 OpenCV 의 Drawing API 를 이용하여 도형 그리기
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

image = np.full((512, 512, 3), 255, np.uint8)
image = cv2.rectangle(image, (20, 20), (255, 255), (255, 0, 0), 3)

plt.imshow(image)
plt.show()
```
<br>
<img src="https://github.com/namoo1818/TIL/assets/50236187/dd85c3b2-af64-4eee-b5d6-ad5be9de1543" width=300>

```python
image = np.full((512, 512, 3), 255, np.uint8)
image = cv2.circle(image, (255, 255), 30, (255, 0, 0), 3)

plt.imshow(image)
plt.show()
```
<br>
<img src="https://github.com/namoo1818/TIL/assets/50236187/192d8090-b84d-4b6c-98a0-4700942befab" width=300>

# 3. 심화 과제
## Face recognition
> 얼굴을 포함하는 입력 정지 영상 또는 비디오에 대해 얼굴 영역의 자동적인 검출 및 분석을 통해 해당 얼굴이 어떤 인물인지 판별해 내는 기술로 패턴인식 및 컴퓨터 비전 분야에서 오랫동안 연구되어 온 분야

### face_recognition 패키지의 HOG 모델을사용해 얼굴감지를 해보자
```python
from google.colab import drive
drive.mount('/content/drive')

import cv2, os
import face_recognition as fr
from IPython.display import Image, display
from matplotlib import pyplot as plt

image_path = "/content/drive/MyDrive/colab/nmixx.jpg"

image = fr.load_image_file(image_path)
face_locations = fr.face_locations(image)

for(top, right, bottom, left) in face_locations:
  cv2.rectangle(image, (left, top), (right, bottom), (0,255,0),3)

# 이미지 버퍼 출력
plt.rcParams['figure.figsize'] = (16,16)
plt.imshow(image)
plt.show()
```
![nmixx](https://github.com/namoo1818/TIL/assets/50236187/3073646a-6a30-40cc-b079-7b68baed0b54)

### face_locations() 함수를 사용하여 사진에서 얼굴을 찾는 기능을 구현해보자
- 인물 사진에서 얼굴 인식하여 encoding한다
<br><img src="https://github.com/namoo1818/TIL/assets/50236187/714a9fb2-d4b7-4881-ad55-f31667092139" width=600><br>
- 2장의 사진에서 encoding된 2개의 얼굴 데이터를 face_distance()의 파라메터로 전달하여 두 사진 간의 distance를 얻어낸다
- 보통 distance 값이 0.6 이상이면 타인, 0.6 미만이면 동일인
<br><img src="https://github.com/namoo1818/TIL/assets/50236187/3f584fea-12d5-493a-a404-cd97f15a7a5e" width=600><br>
- 4명의 인물 사진과 비교할 인물 사진 한장을 준비한다
<br><img src="https://github.com/namoo1818/TIL/assets/50236187/1c8b2620-e324-452e-af3e-9d662edaa9d0" width=500>

```python
plt.rcParams["figure.figsize"] = (1,1)

# 이미지 파일을 로드하여 known_person_list 리스트 생성
known_person_list = []
known_person_list.append(fr.load_image_file("/content/drive/MyDrive/colab/person1.jpg"))
known_person_list.append(fr.load_image_file("/content/drive/MyDrive/colab/person2.jpg"))
known_person_list.append(fr.load_image_file("/content/drive/MyDrive/colab/person3.jpg"))
known_person_list.append(fr.load_image_file("/content/drive/MyDrive/colab/person4.jpg"))
known_person_list.append(fr.load_image_file("/content/drive/MyDrive/colab/person5.jpg"))

# 얼굴을 인식하여 감지된 부분을 잘라낸 다음 known_face_list에 저장
known_face_list = []
for person in known_person_list:

  # 얼굴좌표를 알아내서 잘라낸다
  top, right, bottom, left = fr.face_locations(person)[0]
  face_image = person[top:bottom, left:right]

  # known_face_list에 잘라낸 face_image를 저장
  known_face_list.append(face_image)

# known_face_list에 저장된 얼굴들 출력
for face in known_face_list:
  plt.imshow(face)
  plt.show()
```
![4](https://github.com/namoo1818/TIL/assets/50236187/430823a1-b903-4d16-bb53-f4a68fa05293)

```python
# 기존리스트에 없는 새로움 파일을 열어서
unknown_person = fr.load_image_file("/content/drive/MyDrive/colab/unknown.jpg")

# 얼굴좌표를 알아내서 잘라낸다
top, right, bottom, left = fr.face_locations(unknown_person)[0]
unknown_face = unknown_person[top:bottom, left:right]

# unknown_face이라는 타이틀을 붙여서 표시
plt.title("unknown_face")
plt.imshow(unknown_face)
plt.show()
```
![5](https://github.com/namoo1818/TIL/assets/50236187/b50c971a-79f3-430a-bcaa-38dc836816b3)

```python
# 등록된 얼굴 리스트를 비교
for face in known_face_list:

  # 등록된 얼굴을 128-dimensional face 인코딩
  enc_known_face = fr.face_encodings(face)

  # 등록된 얼굴과 새로운 얼굴의 distance를 얻기
  distance = fr.face_distance(enc_known_face, enc_unknown_face[0])

  # distacne 수치를 포함한 얼굴 출력
  plt.title("distance: " + str(distance))
  plt.imshow(face)
  plt.show()
```
![6](https://github.com/namoo1818/TIL/assets/50236187/f9f2cced-1e57-47c9-ae35-008067a585ee)


# 4. 과제 소감
- 개인적으로 Colab을 공부한 적이 있었는데 이번 과제를 하면서 기본 문법을 다시 공부할 수 있어서 좋았습니다.
- 친절한 가이드 코드 덕분에 쉽게 할 수 있었고 얼굴 인식 결과가 바로 보여서 즐거웠습니다.
- 기회가 된다면 얼굴 인식을 활용한 프로젝트를 해보고싶습니다.
