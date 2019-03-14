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

----

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

----

## Finding crucial facial keypoints and head orientation
important  preprocessing  component
- Facial  keypoints such as eye centers, nose tip, mouth corners: align the face into canonical coordinates
- Head-pose  estimation: pose-based face  analysis

Other survey on tradictional methods
- [Wang  et  al.](https://www.sciencedirect.com/science/article/pii/S0925231217308202): model-based methods
- [Chrysos  et  al.](https://link.springer.com/article/10.1007/s11263-017-0999-5): fiducial detec-tion methods

Here authors focus on methods based on DCNNs.

### Model based
- [Antonakos  et  al.](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Antonakos_Active_Pictorial_Structures_2015_CVPR_paper.html): modeling the appearance of the object using multiple  graph-based  pairwise  normal  distributions  (Gaussian  Markov  random  field)  between  patches  extracted  from  the  regions (fails in high variations data)
- [PIFA](http://openaccess.thecvf.com/content_iccv_2015/html/Jourabloo_Pose-Invariant_3D_Face_ICCV_2015_paper.html): 3-D face alignment, cascaded regression to predict the coefficients of a 3-D to 2-D projection matrix and the  base  shape  coefficients
- [Jour-abloo et  al.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Jourabloo_Large-Pose_Face_Alignment_CVPR_2016_paper.html): formulated  the  face  alignment  problem  as  a  dense 3-D model-fitting problem, where the camera projection matrix and 3-D shape parameters were estimated by a cascade of DCNN-based regressors

### Cascaded regression based
face  alignment  is  naturally  a  regression  problem
learn  a  model  that  directly maps the image appearance to the target output
performance  depends  on  local descriptors

- [Sun et al.](http://openaccess.thecvf.com/content_cvpr_2013/html/Sun_Deep_Convolutional_Network_2013_CVPR_paper.html): DCNNs  in  which,  at  each  level,  outputs  of  multiple  networks  are  fused  for  landmark  estima-tion  and  achieve  good  performance.
- [Zhang  et  al.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.702.1120&rep=rep1&type=pdf): coarse-to-fine autoencoder networks approach using successive  stacked  autoencoder  networks (SANs)
- [Kumar  et  al.] (https://arxiv.org/abs/1601.07950): single DCNNs, but with better performance

----

## Face identification and verification
### Feature learning
### Metric learning

## Problem Setting 

## Method

### Architecture
## Results
