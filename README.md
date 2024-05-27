# ml-workshops

Original model:

https://github.com/Megvii-BaseDetection/YOLOX


<!-- 
Original data:

https://github.com/ucuapps/top-view-multi-person-tracking
 -->


Data converted to COCO format:

https://drive.google.com/file/d/1c9Ni8-eQNxEEULtKuvvLkj6mYkCCVf81/view?usp=sharing

Fine-tuned ckpts:

https://drive.google.com/drive/folders/16qs4_58hXvWzZx0FX5BC1btoRGKLb0mY?usp=sharing

## How to run

Installation (required for all actions):
```
# recommended python 3.9

cd YOLOX-0.3.0
pip install -r requirements.txt
pip install -v -e .
```

Test on single image (works on cpu):
```
# first download best_ckpt.pth from gdrive and place it in YOLOX-0.3.0/

cd YOLOX-0.3.0
python tools/demo.py image -n yolox-s -c best_ckpt.pth --path test.jpg --conf 0.25 --nms 0.45 --tsize 640 --save_result --device cpu
```

Fine-tune from pretrained ckpt (requires gpu):
```
# download chosen weights from main yolox repo: https://github.com/Megvii-BaseDetection/YOLOX
# for example yolo-s weights (smallest model): https://github.com/Megvii-BaseDetection/YOLOX/releases/download/0.1.1rc0/yolox_s.pth

# download dataset: https://drive.google.com/file/d/1c9Ni8-eQNxEEULtKuvvLkj6mYkCCVf81/view?usp=sharing
# unpack and set environment variable to the place containing 'COCO' folder, for example: 
export YOLOX_DATADIR=data/

# run training (checkpoint yolox_s.pth, 1 gpu device, 8 batch size):
cd YOLOX-0.3.0
python -m yolox.tools.train -n yolox-s -c yolox_s.pth -d 1 -b 8 --fp16 -o
```
