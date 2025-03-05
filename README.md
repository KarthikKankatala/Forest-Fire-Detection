<h1 align="center"><span>YOLOv5/YOLOv9 for Fire Detection</span></h1>

Fire detection task aims to identify fire or flame in a video and put a bounding box around it. This repo includes a demo on how to build a fire detector using YOLOv5/YOLOv9. 

<p align="center">
  <img src="results/result.gif" />
</p>

## 🛠️ Installation
1. Clone this repo 
``` shell
# Clone
git clone https://github.com/KarthikKankatala/Forest-Fire-Detection.git
cd Yolov5-Fire-Detection
```

2. Install [YOLOv5](https://github.com/ultralytics/yolov5). 
``` shell
git clone https://github.com/ultralytics/yolov5.git 
cd yolov5
pip install -r requirements.txt
```

3. Or install [YOLOv9](https://github.com/WongKinYiu/yolov9.git)
``` shell
git clone https://github.com/WongKinYiu/yolov9.git
cd yolov9
pip install -r requirements.txt
```

## 🏋️ Training
I set up ```train.ipynb``` script for training the model from scratch. To train the model, download [Fire-Dataset](https://www.kaggle.com/datasets/atulyakumar98/fire-and-gun-dataset) and put it in ```datasets``` folder. I filtered out images and annotations that contain fire and guns as well as images with low resolution, and then changed fire annotation's label in annotation files.

- YOLOv5
```
python train.py --img 640 --batch 16 --epochs 10 --data ../fire.yaml --weights yolov5s.pt --workers 0
```

- YOLOv9
```
python train_dual.py --workers 4 --device 0 --batch 16 --data ../fire.yaml --img 640 --cfg models/detect/yolov9-c.yaml --weights '' --name yolov9-c --hyp hyp.scratch-high.yaml --min-items 0 --epochs 50 --close-mosaic 15
```

## 🌱 Inference

- YOLOv5
  
If you train your own model, use the following command for detection:
``` shell
python detect.py --source ../input.mp4 --weights runs/train/exp/weights/best.pt --conf 0.2
```
Or you can use the pretrained model located in ```model``` folder for detection as follows:
``` shell
python detect.py --source ../input.mp4 --weights ../model/yolov5s_best.pt --conf 0.2
```

