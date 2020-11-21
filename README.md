# Depth estimation with ORB-SLAM2

광운대학교 학술소모임 BARAM 20년도 후반기 Toy Project에 대한 소스코드입니다.  

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
- `소스코드1` : 이것을 의미합니다.
- `소스코드2` : 이것도 의미하구요.
- `소스코드3` : 저것도 의미합니다.

### Project scenario

1. 처음에 이거하고  
2. 두번째 저거하고  
3. 세번째 이거합니다. 여기 사진 넣어줘도 좋겠죠?  

## 프로젝트 결과

<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99868840-84d7e000-2c09-11eb-919f-9499515c70ce.gif" width="500px"></p>  
<p align="center"> < ORB-SLAM2 (Monocular Mode)> </p>  

<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99868841-8dc8b180-2c09-11eb-8701-1aedd399ea28.gif" width="500px"></p>  
<p align="center">< ORB-SLAM2 (RGB-D Mode with Depth Data Sequence)></p>  

<p align="center"><img src="https://user-images.githubusercontent.com/41863759/99868842-9620ec80-2c09-11eb-8b9c-aec62ce3d89d.gif" width="500px"></p>  
<p align="center">< ORB-SLAM2 (RGB-D Mode with Depth Estimation Sequence)></p>  

