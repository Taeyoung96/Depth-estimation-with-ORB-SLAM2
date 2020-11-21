# Depth estimation with ORB-SLAM2

광운대학교 로봇학부 학술소모임 **'BARAM'** 20년도 후반기 Toy Project에 대한 소스코드입니다.  

## 개발 환경
|OS|사용 언어|사용 IDE|
|:---:|:---:|:---:|
|Ubuntu 18.04|C++|Qt Creator|

## 프로젝트 개발 동기

- [ORB-SLAM2](https://github.com/raulmur/ORB_SLAM2) 구동을 통한 Visual SLAM의 구조를 이해해 보고 싶었습니다.  
  최근 Mono depth estimation 관련 연구 및 논문들이 많이 나온 상태에서,  
  실제 센서에서 나온 Depth data 대신에  
  Depth estimation model을 이용해 구한 Depth data를 이용하여  
  SLAM에 적용하면 어떤 성능이 나오는지 궁금하였습니다.  

## 프로젝트 개요
1. [ORB-SLAM2](https://github.com/raulmur/ORB_SLAM2) 코드를 웹캠으로 돌릴 수 있도록 변경.  
2. [Sequence 'freiburg1_xyz'](https://vision.in.tum.de/data/datasets/rgbd-dataset/download#freiburg1_xyz) Dataset을 이용하여 ORB-SLAM2 구동.  
3. 'Monocular Depth Estimation with Transfer Learning pretrained MobileNetV2'([Github](https://github.com/alinstein/Depth_estimation))를 이용하여 RGB Image Sequence에서 Depth Prediction Sequence를 얻음. (Colormap = 'gist_yrag' 사용) 
4. 실제 센서 값에서 얻은 Depth Data와 비슷한 수치를 얻기 위해서 Normalization 작업을 통해 실제 Depth data와 비슷한 값을 얻음.
> - [Matching-timestamp-and-Image](https://github.com/Taeyoung96/Matching-timestamp-and-Image) : Timestamp 값과 Image Sequence를 매칭시켜주기 위해 사용.
> - [Image-Min-Max-Normalization](https://github.com/Taeyoung96/Image-Min-Max-Normalization) : 실제 Depth 값과 비슷한 수치를 갖도록 Normalization을 위해 사용.

## System Architecture
<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99869659-2104e580-2c10-11eb-9ebf-ae5fa683d77c.png" width="600px"></p>  


### Code Overview  
- 대부분 소스코드는 ORB-SLAM2와 동일  
- `/Examples/Monocular/mono_tum.cc` : 조건부 컴파일 '#ifdef'를 이용하여 웹캠을 이용할 때와 Sequence 파일을 이용할 때 두 가지 Mode로 구동.  
- `/Examples/RGB-D/rgbd_tum.cc` : 조건부 컴파일 '#ifdef'를 이용하여 'Realsense D435'을 이용할 때와 Sequence 파일을 이용할 때 두 가지 Mode로 구동.  
- `datasets/Depth-prediction-dataset/` : Depth prediction model을 이용하여 구한 Depth data와 그에 맞는 `associations.txt`이 존재.

### Project scenario

1. [블로그에 쓴거]를 참고하여 개발환경을 Setting 해줍니다.  
2. 터미널에서 `cd Depth-estimation-with-ORB-SLAM2`를 입력합니다.
3. 만약 단일 카메라를 이용하여 'Real time Monocular Mode' 프로젝트를 실행하고 싶을 경우,  
    `/Examples/Monocular/mono_tum.cc`에 `#define UsingWebCam`을 활성화하고,  
    터미널 창에 `sh. build.sh`를 입력합니다.  
    빌드가 끝나면 터미널 창에 `./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt ./Examples/Monocular/d435.yaml`를 입력합니다.
    
4. 만약 Realsense D435를 이용하여 'Real time RGB-D Mode' 프로젝트를 실행하고 싶을 경우,  
    `/Examples/RGB-D/rgbd_tum.cc`에 `#define UsingWebCam`을 활성화하고,  
    터미널 창에 `sh. build.sh`를 입력합니다.  
    빌드가 끝나면 터미널 창에 `./Examples/RGB-D/rgbd_tum Vocabulary/ORBvoc.txt ./Examples/RGB-D/d435.yaml`를 입력합니다.

5. 만약 Depth prediction Sequence를 이용하여 ORB-SLAM2를 실행하고 싶을 경우,  
    `/Examples/RGB-D/rgbd_tum.cc`에 `#define UsingWebCam`을 비활성화하고(주석 처리),  
    터미널 창에 `sh. build.sh`를 입력합니다.  
    빌드가 끝나면 터미널 창에 `./Examples/RGB-D/rgbd_tum Vocabulary/ORBvoc.txt ./Examples/RGB-D/TUM1_deep.yaml datasets/Depth-prediction-dataset/ /datasets/Depth-prediction-dataset/associations.txt`를 입력합니다.

## 프로젝트 결과

<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99868840-84d7e000-2c09-11eb-919f-9499515c70ce.gif" width="500px"></p>  
<p align="center"> < ORB-SLAM2 (Monocular Mode)> </p>  

<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99868841-8dc8b180-2c09-11eb-8701-1aedd399ea28.gif" width="500px"></p>  
<p align="center">< ORB-SLAM2 (RGB-D Mode with Depth Data Sequence)></p>  

<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99868842-9620ec80-2c09-11eb-8b9c-aec62ce3d89d.gif" width="500px"></p>  
<p align="center">< ORB-SLAM2 (RGB-D Mode with Depth Estimation Sequence)></p>  

