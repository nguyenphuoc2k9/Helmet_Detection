
1. Dowload the require data:
```bash

! gdown "1twdtZEfcw4ghSZIiPDypJurZnNXzMO7R"

! mkdir safety_helmet_dataset

!unzip -q "/content/Safety_Helmet_Dataset.zip"  -d "/content/safety_helmet_dataset"

```

  

2. Install YOLOv10:

  
```bash

!git clone https://github.com/THU-MIG/yolov10.git
```

  

3. Install the required dependencies:

  

```bash

! pip install -q -r requirements.txt

! pip install -e .

```

  

### Dowload pre-trained model:

  

Once everything is ready, you can launch the application by running:

  

```bash

!wget https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10n.pt

```
### Import pre-trained model:
```bash
from ultralytics import YOLOv10

MODEL_PATH  =  "yolov10n.pt"

model  = YOLOv10(MODEL_PATH)
```
### Fine-tunning model:
```bash
YAML_PATH  =  "../safety_helmet_dataset/data.yaml"
EPOCHS  =  50
IMG_SIZE  =  640
BATCH_SIZE  =  12
model.train(data=YAML_PATH,
epochs  =  EPOCHS ,
batch  =  BATCH_SIZE ,
imgsz  =  IMG_SIZE )
```
### Import outcome Module:
```bash
TRAINED_MODEL_PATH  =  "runs/detect/train/weights/best.pt"
model  = YOLOv10 ( TRAINED_MODEL_PATH )
model.val ( data  =  YAML_PATH ,
imgsz  =  IMG_SIZE ,
split  ="test")
```
### How to use :
1. Upload an image that you want to detect
2. Replace the image_url with your image path
```bash
from google.colab.patches import cv2_imshow
from ultralytics import YOLOv10
TRAINED_MODEL_PATH  =  "./runs/detect/train/weights/best.pt"

model  = YOLOv10(TRAINED_MODEL_PATH)

CONF_THREESHOLD  =  0.3

IMG_SIZE  =  640

image_url  =  "[Your image path]"
result  =  model.predict(source=image_url, conf=CONF_THREESHOLD, imgsz=IMG_SIZE)
annotated_img  =  result[0].plot()
cv2_imshow(annotated_img)
```