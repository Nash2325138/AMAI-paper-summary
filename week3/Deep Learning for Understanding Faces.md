# [Paper reading] Deep Learning for Understanding Faces: Machines may be just as good, or better, than humans

Rajeev Ranjan, Swami Sankaranarayanan, Ankan Bansal, Navaneeth Bodla, Jun-Cheng Chen, Vishal M. Patel, Carlos D. Castillo, and Rama Chellappa

## Introduction
This is a survey paper that provides an overview of deep-learning methods for face recognition problem, including **face identification** and **verification** systems based on deep learning.

Tradictional methods degrades  significantly on data that have large variations in pose, illu-mination, resolution,  expression, age, background clutter, and occlusion, while deep learning trained with large amount is more robust to these variations and can extract more meaningful features.

Face recognition's procedure can factorized into the following steps
1. Face detection
2. Facial Landmarks localization (to align faces)
3. Feature descriptor (for similarity scores)

----

## Face detection
It's the first step in a face recognition system

### Region based
Propose several regions and classify whether or not a given proposal contains a face, e.g., faster R-CNN

Drawback:
- "Difficult faces" may not be captured on object proposal stage.
- Require additional computation on region proposal network

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

Other surveys on tradictional methods
- [Wang  et  al.](https://www.sciencedirect.com/science/article/pii/S0925231217308202) model-based methods
- [Chrysos  et  al.](https://link.springer.com/article/10.1007/s11263-017-0999-5) fiducial detec-tion methods

Here authors focus on methods based on DCNNs.

### Model based
- [Antonakos  et  al.](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Antonakos_Active_Pictorial_Structures_2015_CVPR_paper.html) modeling the appearance of the object using multiple  graph-based  pairwise  normal  distributions  (Gaussian  Markov  random  field)  between  patches  extracted  from  the  regions (fails in high variations data)
- [PIFA](http://openaccess.thecvf.com/content_iccv_2015/html/Jourabloo_Pose-Invariant_3D_Face_ICCV_2015_paper.html) 3-D face alignment, cascaded regression to predict the coefficients of a 3-D to 2-D projection matrix and the  base  shape  coefficients
- [Jour-abloo et  al.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Jourabloo_Large-Pose_Face_Alignment_CVPR_2016_paper.html) formulated  the  face  alignment  problem  as  a  dense 3-D model-fitting problem, where the camera projection matrix and 3-D shape parameters were estimated by a cascade of DCNN-based regressors

### Cascaded regression based
face  alignment  is  naturally  a  regression  problem
learn  a  model  that  directly maps the image appearance to the target output
performance  depends  on  local descriptors

- [Sun et al.](http://openaccess.thecvf.com/content_cvpr_2013/html/Sun_Deep_Convolutional_Network_2013_CVPR_paper.html) DCNNs  in  which,  at  each  level,  outputs  of  multiple  networks  are  fused  for  landmark  estima-tion  and  achieve  good  performance.
- [Zhang  et  al.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.702.1120&rep=rep1&type=pdf) coarse-to-fine autoencoder networks approach using successive  stacked  autoencoder  networks (SANs)
- [Kumar  et  al.](https://arxiv.org/abs/1601.07950) single DCNNs, but with better performance
- [Xiong et al.](http://openaccess.thecvf.com/content_cvpr_2015/html/Xiong_Global_Supervised_Descent_2015_CVPR_paper.html) suggested domain-dependent descent maps
- [Zhu et al.](http://openaccess.thecvf.com/content_cvpr_2016/html/Zhu_Unconstrained_Face_Alignment_CVPR_2016_paper.html) proposed  CCL to develop  head-pose-based  and  domain-selective  regressors  by  partitioning  the  optimization  domain  into multiple directions based on head pose and combining the results of multiple domain regressors through the composition estimator function
- [Trigeorgis et al.](http://openaccess.thecvf.com/content_cvpr_2016/html/Trigeorgis_Mnemonic_Descent_Method_CVPR_2016_paper.html)  combined and  jointly  trained  convolutional  recurrent  neural  network in  the  cascaded  regression  framework
- [Bulat et al.](http://eprints.nottingham.ac.uk/37236/) uses DCNN  features to roughly  localize facial landmarks, followed by a regression branch to refine the detection results.
- [Kumar et al.](https://ieeexplore.ieee.org/abstract/document/7961750/) iteratively estimates keypoint and predicts pose by  learning heat-map-based DCNN regressors for the face alignment.
- 300  Faces  in  the  Wild  data-base  (300  W) collects several datasets to provide 12,000 images annotated with  68  landmarks
- There are also several methods that apply multitask learning (MTL) by learning related tasks such as facial keypoint estimation for robustness, e.g. [Zhang et al.](https://ieeexplore.ieee.org/abstract/document/7553523/), [Chen et al.](https://link.springer.com/chapter/10.1007/978-3-319-46454-1_8), [Li et al.](https://link.springer.com/chapter/10.1007/978-3-319-46487-9_26), [HyperFace](https://ieeexplore.ieee.org/abstract/document/8170321/)

![](https://i.imgur.com/LcbpjWo.png)
Comparative performance evaluation of different algorithms for the task of facial keypoint estimation on the AFW [55]

----

## Face identification and verification
![](https://i.imgur.com/CmleZm1.png)
Two  major  components
1. Robust  face  representation
2. A discriminative  classification  model (face  identification) or  similarity  measure  (face  verification).

### Feature Learning
Tradictional methods: handcrafted features

#### Transfer learning
- [Huang et al.](https://ieeexplore.ieee.org/abstract/document/6247968) learns from an unlabeled images (unsupervised), and then transfers the learned representation to a identification/verification task through classification  models (e.g., SVM) and metric-learning approaches (e.g., OSS).

#### Deeper or wider networks
- [DeepFace](https://www.cv-foundation.org/openaccess/content_cvpr_2014/html/Taigman_DeepFace_Closing_the_2014_CVPR_paper.html) derives a face  representation  using  a  nine-layer  deep  neural  network (\~ 120M parameters)
- **DeepID frameworks** use ensemble of shallower and smaller deep  convolutional  networks to learn discriminative  and  informative  face  representation (first one that surpass human performance on LFW)

#### Embedding, unsupervised
- [FaceNet](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Schroff_FaceNet_A_Unified_2015_CVPR_paper.html) directly optimizes the embedding itself

#### New large scael dataset
- [CASIA-WebFace](https://arxiv.org/abs/1411.7923) collected 494,414 face images for 10,575 subjects from the IMDB website, which is widely  used  to  train  various  DCNN  models in the face recognition community.
- [VGGFace](http://cis.csuohio.edu/~sschung/CIS660/DeepFaceRecognition_parkhi15.pdf) consists  of  2.6  million  face  images  for  2,600  subjects. The  trained  DCNN model (triplet embedding) using VGGFace achieves comparable results on both still-face (i.e., LFW) and video-face [i.e., YouTube Faces ( Y T F )]data  sets  with  other SOTA

#### Data variation, augmentation
- [AbdAlmageed et  al.](https://ieeexplore.ieee.org/abstract/document/7477555) train separate DCNN models for different views to handle pose variations.
- [Masi  et  al.](https://link.springer.com/chapter/10.1007/978-3-319-46454-1_35) use 3D  morphable  models to augment  the  CASIA-WebFace  data  set

#### Improvement on loss function
- [Ding  et.  al.](https://ieeexplore.ieee.org/abstract/document/7917252) fuse  the  deep  features by a new triplet loss function
- [Wen  et.  al.](https://link.springer.com/chapter/10.1007/978-3-319-46478-7_31) proposed  a  new  loss  function that takes the centroid for each class into consideration and uses it as a regularization constraint to the softmax loss
- [Liu et al.](http://openaccess.thecvf.com/content_cvpr_2017/html/Liu_SphereFace_Deep_Hypersphere_CVPR_2017_paper.html) proposed a novel angular loss based on the modified softmax loss
- [Ranjan et al.](https://arxiv.org/abs/1703.09507) also trained with softmax loss  regularized  with  a  scaled  L-2norm  constraint

#### Aggregation or fusion
- [Yang et al.](http://openaccess.thecvf.com/content_cvpr_2017/html/Yang_Neural_Aggregation_Network_CVPR_2017_paper.html) proposed a neural aggregated network (NAN) to  perform  dynamically  weighted  aggregation on the features from multiple face images or face frames of a face video
- [Bodla et al.](https://ieeexplore.ieee.org/abstract/document/7926654) proposed a fusion network to com-bine face representations from two different DCNN models

### Metric learning
#### Supervised

####

## Implementation
Face recognition can be divided into 2 tasks
1. Face verification: determine if the two images if from the same person
2. Face identification: find the subject's identity

Face verification procedure
1. Face localization and normalization to the canonical coordinate.
2. Extract DCNN features
3. Measure similarity (L2 for cosine)

Face identification procedure
1. Store the DCNN features of each data in the gallery
2. Compute the feature representation and its similarity score with others in the database

## Training data

### Datasets comparison
![](https://i.imgur.com/w6cYuxi.png)

### Training data property analization
- [Bansal  et  al.](http://openaccess.thecvf.com/content_ICCV_2017_workshops/w37/html/Bansal_The_Dos_and_ICCV_2017_paper.html) studied found a combination of still images and video can help with DCNN compared to the one only trained on still images of only on video frames.

## Performance summary
![](https://i.imgur.com/abZHs14.png)
![](https://i.imgur.com/urbmfjE.png)
![](https://i.imgur.com/JKHLhsy.png)


## Results
