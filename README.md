# Kick-Detection-and-pose-estimation
This project is used to detect and count number of kicks in a sample video. It uses Mediapipe for Pose detection and drawing the landmarks over it, it also uses Yolov3 to tackle a problem of multiple person detection which occurs with Mediapipe. A Machine learning model is trained on a dataset for "Kicking" and "Standing" and uses it for detection.
<br />
Note: To run this project on local system download the files and follow the steps mentioned in the notebook

## Clone darknet folder and Load YOLOv3 model
```
!git clone https://github.com/pjreddie/darknet
```
## Download the weights and make the file
``` 
!make
```
```
!wget https://pjreddie.com/media/files/yolov3.weights
```
### With mediapipe there's a problem that it can detect and perform pose landmark detection over a single person, but our project aim was to perfrom kick detection over multiple person so we integrated Yolov3 object detection model to solve this problem.
<br />
## The Yolov3 model in our project is used to detect "Person" which has class=0 in Yolo and draw a box over them so that to run mediapipe on each person and run our model over it

## After Person detection 
<img width="530" alt="Screenshot 2023-05-19 at 1 20 03 PM" src="https://github.com/pachauriyash/Kick-Detection-and-pose-estimation/assets/86353193/cbcc5ae5-c405-4c28-b2be-b6fabbc84d3f">
<br />
There's this problem of multiple boxes around each person so to get a box and dimensions with highest confidence we use a concept of Non Maximum Suppression (NMS)

## After applying NMS
<img width="535" alt="Screenshot 2023-05-19 at 1 22 57 PM" src="https://github.com/pachauriyash/Kick-Detection-and-pose-estimation/assets/86353193/b0a8744d-b0eb-4c07-85c1-1a2619140a5e">

## Applying Mediapipe Pose landmark detection
<img width="533" alt="Screenshot 2023-05-19 at 1 27 57 PM" src="https://github.com/pachauriyash/Kick-Detection-and-pose-estimation/assets/86353193/ece6e394-9ad1-49fd-b8c4-fef0fae3f55b">

## Training a custom dataset of "Kicking" and "Standing" class using mediapipe and storing the data in a output CSV file
To directly use this model refer to the "fitness_poses_csvs_out.csv" file otherwise create your custom dataset for your different class for example pushup, punch or jump using the steps mentioned in the notebook.

## Apply the tranied model and use it to on detected multiple person to detect and count number of kicks
Here is the attached output rendered video with the model run on it

https://github.com/pachauriyash/Kick-Detection-and-pose-estimation/assets/86353193/3665fd25-7875-4e05-a141-11614103ff2f

### This is the performance graph with Processing time vs Frames

![graph for btp](https://github.com/pachauriyash/Kick-Detection-and-pose-estimation/assets/86353193/96b237a2-fb7f-44e8-aa4b-aff83e995fe7)

## References
https://developers.google.com/mediapipe/solutions/vision/pose_landmarker/python
https://github.com/google/mediapipe/blob/master/docs/solutions/pose.md
https://github.com/nachi-hebbar/Object-Detection-Yolo-V3-Darknet/blob/main/YOLO_V3.ipynb
https://shawntng.medium.com/multi-person-pose-estimation-with-mediapipe-52e6a60839dd
https://colab.research.google.com/drive/19txHpN8exWhstO6WVkfmYYVC6uug_oVR?authuser=2&hl=ko
