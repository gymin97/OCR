# OCR
OCR for traditional Han-gul.

- Normally, OCR projects are carried out Object Detection and Classification sequentially, but due to time constraints, the project was carried out only Object Detection. 
Classification is currently in progress.

To apply the OCR to the ancient Korean literature, follow these procedures

1. Data preprocessing 
2. Object Detection (yolov3)

## 1. preprocessing 
1. Data label convert to yolo label || Referenced [GitHub](https://github.com/ssaru/convert2Yolo)

   - My data was downloaded from this [link](https://aihub.or.kr/aidata/30753), and I had to convert it because the annotation is different from yolo.
   - In OCR, Object Detection model only needs to know the character location, but it also contains the code to create the name file used by yolo.          

## 2. Object Detection (yolov3)
#### 0) Environment
 ```
 Ubuntu 18.04
 cuda 10.1
 cudnn 7.6.5
 opencv 3.4.2  (build)
 ```
#### 1) Git CLone darknet(AlexeyAB)
  ```
 git clone https://github.com/AlexeyAB/darknet.git
 ```
 #### 2) Make 
- Move to darknet folder and modify Makefile:     
GPU = 1, CUDNN = 1, OPENCV=1
```
make
```
#### 3) Make a 'custom' folder in darknet folder 
- Modify the data, names, cfg files provided by DarkNet and put them in the custom folder.
- 'custom.data', 'custom.names', 'custom_yolov3.cfg' 
- Please refer to the following [blog](https://blog.naver.com/rudals2901/222425780667) for information on how to modify the files.

#### 4) Test
```
./darknet detector test custom/custom.data custom/custom_yolov3_test.cfg backup/custom_yolov3_best.weights
Enter Image: 
```
<img src="https://user-images.githubusercontent.com/76406136/127340393-2b990faa-417f-4f8c-871d-1c1b6f3826a8.jpg"  width="300" height="430"> 
Using less data, but getted High Accuracy         

![image](https://user-images.githubusercontent.com/76406136/127341174-bd34ce84-d4d0-41a8-a6fd-eaabb4f388cc.png)
It also showed high accuracy in distinguishing between '판본'(a straight handwriting) and '필사체' (scrawl)

