# A Study on Image Quality Optimization to Improve Object Recognition of Generated Images
<br>
<div align="center">
    
   **[생성 이미지에 대한 객체 인식 향상을 위한 화질 최적화 사례 연구]**
  
</div>

   Yolov5의 취약점 검사를 위해 COCO val 2017의 동물 객체 중 8가지를 카테고리로, Stable-diffusion 모델을 이용해 생성한 이미지를 데이터 셋으로 하여 정확도를 검사한다.
   도출된 취약점 개선을 위해 디노이징(NAFNET, PNGAN)으로 최적화 후 정확도 검사 연구를 진행한다.
  
   person, bird, dog, cat, horse, sheep, cow, elephant, bear, giraffe, zebra

</div>
<br>   

# 데이터셋
  > [Datset in Gdrive](https://drive.google.com/drive/folders/1KP1ZxGk0fJ_dSvetD0rYCNpINdC-yOdn?usp=sharing)



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
|"냉장고를 열고 <br>샌드위치를 꺼내는 소"|"a photo of a cow that opens the <br>refrigerator and takes out a sandwich"|<img src = "https://user-images.githubusercontent.com/94797349/203352353-0eea3a28-0bfc-413b-89bb-a11486a88128.png" width="250" height="200"/>|

COCO val 2017의 동물 객체 중 8가지를 카테고리를 주요 객체로 문장들을 생성하였다.

|giraffe|bear|elephant|sheep|
|---|---|------|---|
|A photo of a giraffe that throws a discus in a truck|A photo of a bear sitting on a chair and eating a sandwich|A photo of a Elephant looking at the clock while putting flowers in the pot|A photo of a sheep truckload of apples and oranges with a salad and wine|
|<img src = "https://user-images.githubusercontent.com/94797349/203360905-13407716-f8ed-41a1-83bf-0474dc834214.png" width="150" height="150"/>|<img src = "https://user-images.githubusercontent.com/94797349/203361010-a807b5c8-4bac-45c6-8590-4ced594eb644.png" width="150" height="150"/>|<img src = "https://user-images.githubusercontent.com/94797349/203361123-f411c47e-a6c0-4901-9d89-be51a41e8cc4.png" width="150" height="150"/>|<img src = "https://user-images.githubusercontent.com/94797349/203361198-d7638f1b-2cbe-4b88-b230-7fd2391c7c5f.png" width="150" height="150"/>|
|cow|horse|dog|cat|
|A photo of a cow that opens the refrigerator and takes out a sandwich|A photo of a horse wearing sunglasses and lying on a sunbed under a pararol|A photo of a dog tried on shoes at a shoe store|A photo of a cat putting on lipstick in front of the mirror|
|<img src = "https://user-images.githubusercontent.com/94797349/203352353-0eea3a28-0bfc-413b-89bb-a11486a88128.png" width="150" height="150"/>|<img src = "https://user-images.githubusercontent.com/94797349/203361292-128292fe-9502-4558-a7ea-9f5b26bc1351.png" width="150" height="150"/>|<img src = "https://user-images.githubusercontent.com/94797349/203361371-7fbb1ea3-31c8-4cd4-9b44-12c73d85660c.png" width="150" height="150"/>|<img src = "https://user-images.githubusercontent.com/94797349/203361443-59c4029b-36c1-4903-9f55-4b497ecef3a9.png" width="150" height="150"/>|

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
> <br> [NAFNET](https://github.com/megvii-research/NAFNet)

디노이징 툴인 NAFNET으로 데이터 이미지셋을 디노이징한 후, YOLOv5x로 다시 객체 인식해서 정확도 검사
<br><br>**NAFNET 프레임워크:**<br>
<img src="https://user-images.githubusercontent.com/94797349/205450910-f821d240-be41-4b8a-b130-664f6345faa5.jpg" width="400" height="150"/>
<img src="https://user-images.githubusercontent.com/94797349/205450934-e7e3b380-9192-4abc-b6c5-406feae56453.jpg" width="100" height="200"/>
<br>
|<img src = "https://user-images.githubusercontent.com/94797349/204239262-ed8409ac-fedf-4013-83d6-6648e7e88de3.png" width="250" height="250"/>|<img src = "https://user-images.githubusercontent.com/94797349/204239543-f334ae9f-35bf-4794-ac94-8593c78e6163.png" width="250" height="250"/>|
|--|--|
|데이터 이미지(Before denoising)|데이터 이미지(After denoising)|


> **디노이징**
> <br> [NAFNET](https://github.com/megvii-research/NAFNet)

디노이징 툴인 NAFNET으로 데이터 이미지셋을 디노이징한 후, YOLOv5x로 다시 객체 인식해서 정확도 검사
<br><br>**NAFNET 프레임워크:**<br>
<img src="https://user-images.githubusercontent.com/94797349/205450910-f821d240-be41-4b8a-b130-664f6345faa5.jpg" width="400" height="150"/>
<img src="https://user-images.githubusercontent.com/94797349/205450934-e7e3b380-9192-4abc-b6c5-406feae56453.jpg" width="100" height="200"/>
<br>
|<img src = "https://user-images.githubusercontent.com/94797349/204239262-ed8409ac-fedf-4013-83d6-6648e7e88de3.png" width="250" height="250"/>|<img src = "https://user-images.githubusercontent.com/94797349/204239543-f334ae9f-35bf-4794-ac94-8593c78e6163.png" width="250" height="250"/>|
|--|--|
|데이터 이미지(Before denoising)|데이터 이미지(After denoising)|


# conference

  > 회의록 : [회의록 DRIVE](https://docs.google.com/document/d/1fIRLpuA7V0Jb0l6fWg8KfU0ae6wXg9rNU_Z_M0-um4E/edit?usp=sharing)

<br>
