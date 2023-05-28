# Performance Evaluation of Denoising and Object Detection on Generated Images
<br>
<div>
    
   ### 생성 이미지에 대한 객체 인식과 디노이징 성능 평가
  
</div>

   Yolov5의 취약점 검사를 위해 COCO val 2017의 동물 객체 중 8가지를 카테고리로, Stable-diffusion 모델을 이용해 생성한 이미지를 데이터 셋으로 하여 정확도를 검사한다.
   도출된 취약점 개선을 위해 디노이징(NAFNET, PNGAN)으로 최적화 후 정확도 검사 연구를 진행한다.
  
</div>
<br>   

# 데이터셋
  > [Dataset in Gdrive](https://drive.google.com/drive/folders/1KP1ZxGk0fJ_dSvetD0rYCNpINdC-yOdn?usp=sharing)



<br>
    
# Tool
  [<img src="https://img.shields.io/badge/Python-3766AB?style=flat-square&logo=Python&logoColor=white"/>](https://www.python.org/)
  [<img src="https://img.shields.io/badge/StableDiffusion-412991?style=flat-square&logo=Python&logoColor=white"/>](https://stablediffusionweb.com/)
  [<img src="https://img.shields.io/badge/Google Colab-F9AB00?style=flat-square&logo=Python&logoColor=white"/></a>](https://colab.research.google.com/drive/1gjUVQBpd7Ib5NlojBwcZRh3B2MkRicc7#scrollTo=q2T8J68g11da)

<br>

## technology
<br>

> **Stable-diffusion**
> <br>[<img src="https://img.shields.io/badge/StableDiffusion-412991?style=flat-square&logo=Python&logoColor=white"/>](https://stablediffusionweb.com/)

적대적 공격 사례에 활용되는 이미지들은 현실에 존재하는 이미지를 생성한 것이다. 그러므로 Stable-diffusion을 활용하여 이미지를 생성할 때 작화 형식이 아닌 실제 현실과 유사한 사진 형식으로 이미지를 생성하기 위해 'A photo of'구문을 문장의 앞에 삽입하였다.
<br>

|한글|영어로 번역|Stable-Diffusion으로 생성한 이미지|
|------|---|---|
|"꽃밭을 걷는 곰 사진"|"A photo of a bear walking through the flowers"|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/bb047a64-cb9c-4b9b-ae8c-d54edb1051fd" width="250" height="200"/>|
<br>

COCO val 2017의 카테고리 중 주요 객체인 person, bird, dog, cat, horse, sheep, cow, elephant, bear, giraffe, zebra에 대한 문장을 생성하고, <br>
생성된 문장을 이용하여 이미지셋을 생성하고자 하였다.

|bear|zebra|horse|giraffe|
|----|----|----|----|
|A photo of a bear walking through the flowers|A photo of a zebra running through the field|A photo of a horse staring a car|A photo of a giraffe looking at the night sky|
|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/bb047a64-cb9c-4b9b-ae8c-d54edb1051fd" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/916a56d5-35cc-429b-aac5-7d50cad779f0" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/6e3cea4c-8dcd-4c31-a600-f8e3d7b8a63d" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/f666335a-904d-4368-89f9-c8a4bbc5e1d0)" width="150" height="150"/>|


|dog|bird|person|cow|
|----|----|----|----|
|A photo of a dog driving a car|A photo of a bird in a bathtub covered in a towel|A photo of a person sitting on a bed|A photo of a cow running in the meadow|
|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/a8a4009c-0121-4df8-93d7-61c11a485d6f" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/79df4b04-48b5-4ff0-9cc5-4f3ba046f866" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/14cfffe0-a218-468c-a65b-069013d10afd" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/8aa8f9bf-8e0e-4ddb-9552-52cfe9311ac6" width="150" height="150"/>|

|elephant|sheep|cat|
|----|----|----|
|A photo of an elephant standing in front of a bookshelf|A photo of a sheep walking on the beach|A photo of a cat wearing a glasses|
|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/e5a4e9f0-9ac8-45ae-a427-b512a75f8a1f" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/abbc72a7-6631-4a27-9be8-7c692bbfc9f7" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/f3705ac4-cdc1-4d53-a7ed-f9e6148a1668" width="150" height="150"/>|<img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/8aa8f9bf-8e0e-4ddb-9552-52cfe9311ac6" width="150" height="150"/>|

<br>

> **Yolov5x**
> <br>: [YOLOv5](https://github.com/ultralytics/yolov5)

stable-diffusion에서 생성한 이미지를 YOLOv5의 pretrained 모델 중 mAP 값이 높아서 성능이 좋다고 평가된 YOLOv5x 모델에 넣어 정확도를 평가
<br><br>**YOLOv5 프레임워크:**<br>
<img src="https://user-images.githubusercontent.com/94797349/205436140-42c89d27-ae63-4b63-91ae-cbc71b1c273d.png" width="600" height="200"/>
<br>
|<img src = "https://user-images.githubusercontent.com/94797349/203380581-4a9f2a73-c6fb-4612-a84b-386517da3181.png" width="250" height="250"/>|<img src = "https://user-images.githubusercontent.com/94797349/203380664-2dc2a0cc-1b14-4ad5-872e-cdc10a8c3268.jpg" width="250" height="250"/>|
|--|--|
|데이터 이미지|YOLOv5x로 돌린 후(바운딩 박스 생성)|


<br>

> **디노이징**
> <br> [NAFNet](https://github.com/megvii-research/NAFNet) , 
> [PNGAN](https://github.com/caiyuanhao1998/PNGAN)

디노이징 툴인 NAFNET으로 데이터 이미지셋을 디노이징한 후, YOLOv5x로 다시 객체 인식해서 정확도 검사


|original|PNGAN|NAFNet
|----|----|----|
|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/7026e594-707e-49f4-826c-7c0f2d6e14ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/9050e377-85e5-4a47-8531-be41dbcb70ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/1cb297aa-476c-4e6e-9c53-36a1c8553dd4" width="150" height="150"/>|


ㅇ
|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/7026e594-707e-49f4-826c-7c0f2d6e14ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/9050e377-85e5-4a47-8531-be41dbcb70ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/1cb297aa-476c-4e6e-9c53-36a1c8553dd4" width="150" height="150"/>ㅇ
|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/7026e594-707e-49f4-826c-7c0f2d6e14ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/9050e377-85e5-4a47-8531-be41dbcb70ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/1cb297aa-476c-4e6e-9c53-36a1c8553dd4" width="150" height="150"/>ㅇ
|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/7026e594-707e-49f4-826c-7c0f2d6e14ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/9050e377-85e5-4a47-8531-be41dbcb70ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/1cb297aa-476c-4e6e-9c53-36a1c8553dd4" width="150" height="150"/>


<img width="443" alt="스크린샷 2023-05-28 오후 3 45 17" src="https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/84899706/26b15c49-6a39-4493-8fb6-74535e6921e9">

<img width="434" alt="스크린샷 2023-05-28 오후 3 45 02" src="https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/84899706/41f40df6-38ff-4fb1-bb4d-6fe8683b1c10">
