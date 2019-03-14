# [Paper reading] Deep Learning for Understanding Faces: Machines may be just as good, or better, than humans

Rajeev Ranjan, Swami Sankaranarayanan, Ankan Bansal, Navaneeth Bodla, Jun-Cheng Chen, Vishal M. Patel, Carlos D. Castillo, and Rama Chellappa

## Introduction
This is a survey paper that provides an overview of deep-learning methods for face recognition problem, including **face identification** and **verification** systems.

Traditional methods degrade significantly on data that have large variations in pose, illumination, resolution,  expression, age, background clutter, and occlusion, while deep learning trained with large amount is more robust to these variations and can extract more meaningful features.

Face recognition's procedure can be factorized into the following steps
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
Use bounding-box instead of proposed regions on a feature map to classify. It can be implemented using convolution operation (therefore it's usually faster)
- [Single-shot detector (SSD)](https://link.springer.com/chapter/10.1007/978-3-319-46448-0_2) utilized natural pyramid structure in DCNNs

### Unconstrained face detection datasets
- FDDB: 2,845 images containing a total of 5,171 faces collected from news articles on yahoo.com
- MALF: 5,250 high-resolution images containing a total of 11,931 faces (collected from Flickr and an image search service provided by Baidu, Inc)
- WIDER Face: 32,203 images, with 50% samples for training and 10% for validation.

----

## Finding facial key points and head orientation
It's an important preprocessing step to align the face into canonical coordinates and pose-based face analysis. It can be classified into model-based and regression-based approaches.

Other surveys on traditional methods
- [Wang et al.](https://www.sciencedirect.com/science/article/pii/S0925231217308202) for model-based methods
- [Chrysos et al.](https://link.springer.com/article/10.1007/s11263-017-0999-5) for fiducial detection methods

Here authors focus on those based on DCNNs.

### Model based
- [Antonakos et al.](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Antonakos_Active_Pictorial_Structures_2015_CVPR_paper.html) models the appearance of the object using multiple graph-based pairwise normal distributions between patches extracted from the regions (but failed in high variations data)
- [PIFA](http://openaccess.thecvf.com/content_iccv_2015/html/Jourabloo_Pose-Invariant_3D_Face_ICCV_2015_paper.html) performs 3D face alignment with cascaded regression to predict the coefficients of a 3D to 2D projection matrix.
- [Jour-abloo et al.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Jourabloo_Large-Pose_Face_Alignment_CVPR_2016_paper.html) formulated the face alignment problem as a dense 3-D model-fitting problem, where the camera projection matrix and 3-D shape parameters were estimated by a cascade of DCNN-based regressors.

### Cascaded regression based
Face alignment is naturally a regression problem, hence there are learn  a  model that  directly maps the image appearance to the target output

#### Works that introduce DCNN to solve the regression problems
- [Sun et al.](http://openaccess.thecvf.com/content_cvpr_2013/html/Sun_Deep_Convolutional_Network_2013_CVPR_paper.html) fused multiple DCNNs for landmark estimation.
- [Zhang et al.](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.702.1120&rep=rep1&type=pdf) design a coarse-to-fine autoencoder networks using successively stacked autoencoder networks (SANs)
- [Kumar et al.](https://arxiv.org/abs/1601.07950) used only single DCNNs, but with better performance.

#### Architecture or training techniques improvements
- [Xiong et al.](http://openaccess.thecvf.com/content_cvpr_2015/html/Xiong_Global_Supervised_Descent_2015_CVPR_paper.html) suggested domain-dependent descent maps.
- [Zhu et al.](http://openaccess.thecvf.com/content_cvpr_2016/html/Zhu_Unconstrained_Face_Alignment_CVPR_2016_paper.html) developed head-pose-based and domain-selective regressors.
- [Trigeorgis et al.](http://openaccess.thecvf.com/content_cvpr_2016/html/Trigeorgis_Mnemonic_Descent_Method_CVPR_2016_paper.html) jointly trained convolutional recurrent NN in the cascaded regression framework.
- [Bulat et al.](http://eprints.nottingham.ac.uk/37236/) uses DCNN features to roughly localize facial landmarks, followed by a regression branch to refine the detection results.
- [Kumar et al.](https://ieeexplore.ieee.org/abstract/document/7961750/) iteratively estimates keypoint and predicts pose by learning heat-map-based DCNN regressors for the face alignment.

#### A New large dataset
- 300 Faces in the Wild data-base (300  W) combined several datasets to provide 12,000 images annotated with  68  landmarks

#### Multitask learning
- There are also several methods that apply multitask learning (MTL) by learning related tasks such as facial keypoint estimation for robustness, e.g. [Zhang et al.](https://ieeexplore.ieee.org/abstract/document/7553523/), [Chen et al.](https://link.springer.com/chapter/10.1007/978-3-319-46454-1_8), [Li et al.](https://link.springer.com/chapter/10.1007/978-3-319-46487-9_26), [HyperFace](https://ieeexplore.ieee.org/abstract/document/8170321/)

![](https://i.imgur.com/LcbpjWo.png)
Comparative performance evaluation of different algorithms for the task of facial keypoint estimation on the AFW [55]

----

## Face identification and verification
![](https://i.imgur.com/CmleZm1.png)
Two  major  components
1. Robust  face  representation
2. A discriminative classification model (face identification) or similarity measure  (face verification).

### Feature Learning
Traditional methods: handcrafted features

#### Transfer learning
- [Huang et al.](https://ieeexplore.ieee.org/abstract/document/6247968) learns from unlabeled images (unsupervised) and then transfers the learned representation to an identification/verification task through classification/metric-learning models.

#### Deeper or wider networks
- [DeepFace](https://www.cv-foundation.org/openaccess/content_cvpr_2014/html/Taigman_DeepFace_Closing_the_2014_CVPR_paper.html) used a nine-layer deep neural network to obtain face representation (\~ 120M parameters)
- **DeepID frameworks** use ensemble of shallower and smaller deep convolutional networks to learn face representation (the first one that surpasses human performance on LFW)

#### Embedding, unsupervised
- [FaceNet](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Schroff_FaceNet_A_Unified_2015_CVPR_paper.html) directly optimizes the embedding itself

#### New large scael dataset
- [CASIA-WebFace](https://arxiv.org/abs/1411.7923) has 494,414 face images for 10,575 subjects from the IMDB website.
- [VGGFace](http://cis.csuohio.edu/~sschung/CIS660/DeepFaceRecognition_parkhi15.pdf) consists of 2.6 million face images for 2,600 subjects. The  trained  DCNN model (triplet embedding) using VGGFace achieves comparable results on both still-face (i.e., LFW) and video-face (i.e., YTF) datasets with other SOTAs.

#### Data variation, augmentation
- [AbdAlmageed et al.](https://ieeexplore.ieee.org/abstract/document/7477555) train separate DCNN models for different views to handle pose variations.
- [Masi et al.](https://link.springer.com/chapter/10.1007/978-3-319-46454-1_35) use 3D morphable models to augment the CASIA-WebFace dataset.

#### Improvement on loss function
- [Ding et. al.](https://ieeexplore.ieee.org/abstract/document/7917252) fuse the deep features by a new triplet loss function.
- [Wen  et.  al.](https://link.springer.com/chapter/10.1007/978-3-319-46478-7_31) proposed a new loss function that takes the centroid for each class into consideration and uses it as a regularization constraint to the softmax loss
- [Liu et al.](http://openaccess.thecvf.com/content_cvpr_2017/html/Liu_SphereFace_Deep_Hypersphere_CVPR_2017_paper.html) proposed a novel angular loss based on the modified softmax loss
- [Ranjan et al.](https://arxiv.org/abs/1703.09507) also trained with softmax loss  regularized  with  a  scaled  L-2norm  constraint

#### Aggregation or fusion
- [Yang et al.](http://openaccess.thecvf.com/content_cvpr_2017/html/Yang_Neural_Aggregation_Network_CVPR_2017_paper.html) proposed a neural aggregated network (NAN) to  perform  dynamically  weighted  aggregation on the features from multiple face images or face frames of a face video
- [Bodla et al.](https://ieeexplore.ieee.org/abstract/document/7926654) proposed a fusion network to combine face representations from two different DCNN models

### Metric learning
#### Supervised methods
- [Hu et al.](http://openaccess.thecvf.com/content_cvpr_2014/html/Hu_Discriminative_Deep_Metric_2014_CVPR_paper.html) starts to learn a deep metric
- [Schroff et al.](https://www.cv-foundation.org/openaccess/content_cvpr_2015/html/Schroff_FaceNet_A_Unified_2015_CVPR_paper.html) and [Parkhi et al.](http://cis.csuohio.edu/~sschung/CIS660/DeepFaceRecognition_parkhi15.pdf) use triplet loss to learn a better embedding.
- [S. Sankaranarayanan](https://ieeexplore.ieee.org/abstract/document/7791205/) learned a low-rank embedding.
- [Song et al.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Song_Deep_Metric_Learning_CVPR_2016_paper.html) considers the full pairwise distances between samples.
#### Unsupervised or semi-supervised methods
- [Yang et al.](https://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Yang_Joint_Unsupervised_Learning_CVPR_2016_paper.html) jointly train the deep representations and image clusters iteratively until the number of clusters reaches the predefined value.
- [Zhang et al.](https://link.springer.com/chapter/10.1007/978-3-319-46487-9_15) clusters face images in videos by alternating between deep representation adaption and clustering.
- [Tri-georgis et al.](https://ieeexplore.ieee.org/abstract/document/7453156) applies nonnegative matrix factorization on the deep features.
- [Lin et al.](https://ieeexplore.ieee.org/abstract/document/7961755) presents an unsupervised clustering algorithm which utilizes the samples' neighborhood structures.

####

## Implementation
Face recognition can be divided into 2 tasks.
1. Face verification: determine if the two images if from the same person.
2. Face identification: find the subject's identity.

Face verification procedure
1. Face localization and normalization to the canonical coordinate.
2. Extract DCNN features.
3. Measure similarity (L2 for cosine)

Face identification procedure
1. Store the DCNN features of each data in the gallery.
2. Compute the feature representation and its similarity score with others in the database.

## Training data

### Datasets comparison
<img src="https://i.imgur.com/w6cYuxi.png" width=500>

### Training data property analyzation
- [Bansal et al.](http://openaccess.thecvf.com/content_ICCV_2017_workshops/w37/html/Bansal_The_Dos_and_ICCV_2017_paper.html) studied and found a combination of still images and video can help with DCNN compared to the one only trained on still images of only on video frames.

## Performance summary
![](https://i.imgur.com/abZHs14.png)
![](https://i.imgur.com/urbmfjE.png)
![](https://i.imgur.com/JKHLhsy.png)
