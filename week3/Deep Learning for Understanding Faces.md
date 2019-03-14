# [Paper reading] Deep Learning for Understanding Faces: Machines may be just as good, or better, than humans

Rajeev Ranjan, Swami Sankaranarayanan, Ankan Bansal, Navaneeth Bodla, Jun-Cheng Chen, Vishal M. Patel, Carlos D. Castillo, and Rama Chellappa

## Introduction
Survey paper

In this article, we provide an overview of deep-learning methods used for  face  recognition.  We  discuss  different  modules  involved  in  designing an automatic face recognition system and the role of deep  learning  for  each  of  them

In  this  article,  we  present  an  overview  of  recent  automatic  **face identification** and **verification** systems based on *deep learning*.

Traditional:
1. face detector
2. localize the important facial landmarks -> align faces
3. feature descriptor -> similarity scores
work well on images, degrades  significantly  on face images or videos that have large variations in pose, illu-mination,  resolution,  expression,  age,  background  clutter,  and  occlusion.

Deep learning:
large amount of training data represents significant variations in pose, illumination, expression, and occlusion, which enables the DCNNs to be robust to these variations and extract meaningful features required for the task.

## Face detection
first step in an automatic face recognition system
traditional methods (e.g. HOG) do not capture salient facial information when variation is high (resolution, viewpoint, illumination...)
DCNN pretrained with a large generic  data  set  can  be  used  as  a  meaningful  feature  extractor

### Region based
classify whether or not a given proposal contains a face

- Faster R-CNN

Drawback:
- difficult faces are hard to capture in any object proposal
- additional computation on RPN

### Sliding-window based
bounding-box coordinates at every location in a feature map at a given scale
can be implemented using just a convolution operation that works in a sliding-window fashion

- Single-shot detector (SSD)
utilizes  the  inbuilt  pyramid  structure  present  in  DCNNs
overall  computation  time  of  SSD  is  lower  than  faster  R-CNN

### unconstrained face detection datasets
- FDDB: 2,845 images containing a total of 5,171 faces col-lected from news articles on yahoo.com
- MALF: 5,250 high-resolution images containing a total of 11,931 faces (collected from Flickr and an image search service provided by Baidu, Inc)
- WIDER Face:  32,203  images,  with  50%  samples  for  training  and  10%  for  validation (larger variation, Face  detectors  trained  on  this  data  set  have  achieved  improved  performance  [19],  [23],  [28],  [29],  [32],  [33]) (results  for  this  data  set  reveal  that  finding  small  faces  in  the  crowd  is  still  challeng-ing.)

## Finding crucial facial keypoints and head orientation
important  preprocessing  component
- Facial  keypoints such as eye centers, nose tip, mouth corners: align the face into canonical coordinates
- Head-pose  estimation: pose-based  face  analysis

### Model based
### Cascaded regression based

## Face identification and verification
### Feature learning
### Metric learning

## Problem Setting 

## Method

### Architecture
## Results
