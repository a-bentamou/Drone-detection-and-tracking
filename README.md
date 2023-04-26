# yolov7 Drone Detection and tracking

## Steps to run Code

- Go to the root folder.
```
cd DroneDetection_ICIP2023
```
- Create a virtual envirnoment (Recommended, If you dont want to disturb python packages)
```
### For Linux Users
python3 -m venv yolov7Dronetracking
source yolov7Dronetracking/bin/activate

### For Window Users
python3 -m venv yolov7Dronetracking
cd yolov7Dronetracking
cd Scripts
activate
cd ..
cd ..
```
- Upgrade pip with mentioned command below.
```
pip install --upgrade pip
```
- Install requirements with mentioned command below.
```
pip install -r requirements.txt
```

## Inference
- Run the code with mentioned command below.

### for detection only
```
python detect.py --weights runs/train/cluster/weights/best.pt --source "your image.jpg or your video.mp4" 
```
### for detection only on several images or videos
```
python detect.py --weights runs/train/cluster/weights/best.pt --source "your image folder or your video folder"
```

### for detection only with distortion detection
```
python detect.py --weights runs/train/cluster/weights/best.pt --source "your image.jpg or your video.mp4" --classify
```

- Output file will be created in the ```working-dir/runs/detect/Drone_detection``` with original filename

### Jupyter

We provide a Jupyter notebook "Inference.ipynb" that you can use for drone vs bird detection and distortion type detection.

### for drone tracking
```
python detect_and_track.py --weights runs/train/cluster/weights/best.pt --source "your video.mp4 or your video folder"
```


### for colored tracks 
```
python detect_and_track.py --weights runs/train/cluster/weights/best.pt --source "your video.mp4" --colored-trk
```

### for saving tracks centroid, track id and bbox coordinates
```
python detect_and_track.py --weights runs/train/cluster/weights/best.pt --source "your video.mp4" --save-txt --save-bbox-dim
```

- Output file will be created in the ```working-dir/runs/tracking/Drone_tracking``` with original filename

## Testing

```
python test.py --weights runs/train/cluster/weights/best.pt --data data/IR_data.yaml --img 640 --batch 16 --conf 0.001 --iou 0.6 --device 0
```
- Output file will be created in the ```working-dir/runs/test/yolov7_640``` with original filename

## Training

### Single GPU training

```
# train models
python train.py --workers 8 --device 0 --batch-size 32 --data data/IR_data.yaml --img 640 640 --cfg cfg/deploy/yolov7.yaml --weights 'weights/yolov7.pt'
```
- Output file will be created in the ```working-dir/runs/train/exp``` with original filename

### Multiple GPU training

```
# train models
python -m torch.distributed.launch --nproc_per_node 4 --master_port 9527 train.py --workers 8 --device 0,1,2,3 --sync-bn --batch-size 128 --data data/IR_data.yaml --img 640 640 --cfg cfg/deploy/yolov7.yaml --weights 'weights/yolov7.pt'
```

## Results
<table>
  <tr>
    <td>Drone vs bird Detection </td>
    <td>Distortion type detection</td>
  </tr>
  <tr>
    <td>mAP = 92.6 %</td>
    <td>Accuracy = 92%</td>
  </tr>
 </table>


## References
 - https://github.com/WongKinYiu/yolov7
 - https://github.com/RizwanMunawar/yolov7-object-tracking
