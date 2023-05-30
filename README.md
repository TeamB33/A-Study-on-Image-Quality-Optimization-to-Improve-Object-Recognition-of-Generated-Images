# Performance Evaluation of Denoising and Object Detection on Generated Images
   ### 생성 이미지에 대한 객체 인식과 디노이징 성능 평가


   YOLOv5의 취약점 검사를 위해 COCO val 2017의 동물 객체 중 8가지를 카테고리로, Stable-diffusion 모델을 이용해 생성한 이미지를 데이터 셋으로 하여 정확도를 검사한다.
   도출된 취약점 개선을 위해 디노이징(NAFNet, PNGAN)으로 최적화 후 정확도 검사 연구를 진행한다.
  
</div>
<br>   

# Dataset
  > [dataset](https://drive.google.com/drive/folders/1KP1ZxGk0fJ_dSvetD0rYCNpINdC-yOdn?usp=sharing)



<br>
    
# Tool
  [<img src="https://img.shields.io/badge/Python-3766AB?style=flat-square&logo=Python&logoColor=white"/>](https://www.python.org/)
  [<img src="https://img.shields.io/badge/StableDiffusion-412991?style=flat-square&logo=Python&logoColor=white"/>](https://stablediffusionweb.com/)
  [<img src="https://img.shields.io/badge/Google Colab-F9AB00?style=flat-square&logo=Python&logoColor=white"/></a>](https://colab.research.google.com/drive/1gjUVQBpd7Ib5NlojBwcZRh3B2MkRicc7#scrollTo=q2T8J68g11da)

<br>

# Technology
<br>

> **Stable-diffusion**
> <br>[<img src="https://img.shields.io/badge/StableDiffusion-412991?style=flat-square&logo=Python&logoColor=white"/>](https://stablediffusionweb.com/)

적대적 공격 사례에 활용되는 이미지들은 현실에 존재하는 이미지를 생성한 것이다. 그러므로 Stable-diffusion을 활용하여 이미지를 생성할 때 작화 형식이 아닌 실제 현실과 유사한 사진 형식으로 이미지를 생성하기 위해 'A photo of'구문을 문장의 앞에 삽입하였다.
<br>

|한글|영어로 번역|Stable-Diffusion으로 생성한 이미지|
|------|---|---|
|"꽃밭을 걷는 곰 사진"|"A photo of a bear walking through the flowers"|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/bb047a64-cb9c-4b9b-ae8c-d54edb1051fd" width="200" height="200"/></div>|
<br>

COCO val 2017의 카테고리 중 주요 객체인 person, bird, dog, cat, horse, sheep, cow, elephant, bear, giraffe, zebra에 대한 문장을 생성하고, 생성된 문장을 이용하여 이미지셋을 생성하고자 하였다.



|giraffe|bear|elephant|sheep|
|-----|-----|-----|-----|
|A photo of a giraffe looking at the night sky|A photo of a bear walking through the flowers|A photo of an elephant standing in front of a bookshelf|A photo of a sheep walking on the beach|
|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/f666335a-904d-4368-89f9-c8a4bbc5e1d0" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/bb047a64-cb9c-4b9b-ae8c-d54edb1051fd" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/e5a4e9f0-9ac8-45ae-a427-b512a75f8a1f" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/abbc72a7-6631-4a27-9be8-7c692bbfc9f7" width="200" height="200"/></div>|
| <div align="center"> **cow** </div> |<div align="center"> **horse** </div>|<div align="center"> **dog** </div>|<div align="center"> **cat** </div>|
|A photo of a cow running in the meadow|A photo of a horse staring a car|A photo of a dog driving a car|A photo of a cat wearing a glasses|
|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/8aa8f9bf-8e0e-4ddb-9552-52cfe9311ac6" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/6e3cea4c-8dcd-4c31-a600-f8e3d7b8a63d" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/a8a4009c-0121-4df8-93d7-61c11a485d6f" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/111479186/65edc666-ffd9-412a-8bcd-c078a96eb184" width="200" height="200"/></div>|
|<div align="center"> **zebra** </div>|<div align="center"> **bird** </div>|<div align="center"> **person** </div>||
|A photo of a zebra running through the field|A photo of a bird in a bathtub covered in a towel|A photo of a person sitting on a bed||
|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/916a56d5-35cc-429b-aac5-7d50cad779f0" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/79df4b04-48b5-4ff0-9cc5-4f3ba046f866" width="200" height="200"/></div>|<div align="center"><img src = "https://github.com/TeamB33/A-Study-on-Image-Quality-Optimization-to-Improve-Object-Recognition-of-Generated-Images/assets/110325367/14cfffe0-a218-468c-a65b-069013d10afd" width="200" height="200"/></div>||



<br><br>

> **Yolov5x**
> <br>: [YOLOv5](https://github.com/ultralytics/yolov5)

stable diffusion에서 생성한 이미지를 YOLOv5의 pretrained 모델 중 mAP 값이 높아서 성능이 좋다고 평가된 YOLOv5x 모델에 넣어 정확도를 평가하였다.

<br><br>**YOLOv5 프레임워크:**<br>
<img src="https://user-images.githubusercontent.com/94797349/205436140-42c89d27-ae63-4b63-91ae-cbc71b1c273d.png" width="600" height="200"/>
<br>
|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/57c52bdf-57f4-4647-bc43-5df19d2e8e21" width="250" height="250"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/a298c7e1-b533-4001-a565-34d9222b8398" width="250" height="250"/>|
|--|--|
|데이터 이미지|YOLOv5x로 돌린 후(바운딩 박스 생성)|


<br><br>

> **디노이징**
> <br>: [NAFNet](https://github.com/megvii-research/NAFNet), [PNGAN](https://github.com/caiyuanhao1998/PNGAN)


<br>**NAFNET 프레임워크:**<br>
<img src="https://user-images.githubusercontent.com/94797349/205450910-f821d240-be41-4b8a-b130-664f6345faa5.jpg" width="400" height="150"/>
<img src="https://user-images.githubusercontent.com/94797349/205450934-e7e3b380-9192-4abc-b6c5-406feae56453.jpg" width="100" height="200"/>
<br>


<br><br>**PNGAN 프레임워크:**<br><br>
<img src="https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/01ac0cb7-6ebb-4aea-9017-bbb5cfb46a87" width="600" height="200"/>
<br><br><br>

디노이징 툴인 NAFNET으로 데이터 이미지셋을 디노이징한 후, YOLOv5x로 다시 객체 인식해서 정확도 검사

|original|PNGAN|NAFNet
|----|----|----|
|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/7026e594-707e-49f4-826c-7c0f2d6e14ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/9050e377-85e5-4a47-8531-be41dbcb70ea" width="150" height="150"/>|<img src = "https://github.com/TeamB33/Performance-Evaluation-of-Denoising-and-Object-Detection-on-Generated-Images/assets/110325367/1cb297aa-476c-4e6e-9c53-36a1c8553dd4" width="150" height="150"/>|


<br><br>

# 실험 결과 
각각의 카테고리에 대한 객체 인식률은 아래의 표와 같다.


|카테고리|original|NAFNet|PNGAN|
|-------|--------|------|-----|
|person  |99.5    |97.7  |99.0 | 
|bird    |96.2    |94.2  |**96.5** | 
|dog     |99.2    |98.1  |95.3 | 
|cat     |96.3    |93.3  |94.8 | 
|horse   |96.9    |94.0  |94.8 | 
|sheep   |85.7    |**86.3**  |83.6 | 
|cow     |94.8    |91.4  |87.3 | 
|elephant|96.8    |92.9  |87.3 | 
|bear    |95.6    |86.3  |81.8 | 
|giraffe |99.8    |98.9  |99.7 | 
|zebra   |100.0   |98.5  |100.0| 
|total   |96.4    |93.8  |92.7 | 


<br>일부 객체에서는 디노이징 이후 객체 인식률이 소폭 상향 되었으나, 객체 인식률이 오히려 더 떨어지는 결과가 발생하기도 하였다.
<br>디노이징 모델이 생성 이미지 데이터 셋에 대한 객체 인식률을 높이는데 효과적이지 않다는 것을 알 수 있었다.

   
