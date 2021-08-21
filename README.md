# GSoC-ignite

This Repository contains the work done during Google Summer of Code 2021 for the Metric Enhancement Project in Pytorch-Ignite.

## 1. My Project

### 1.a Ignite

Ignite is a high-level library to help with training and evaluating neural networks in PyTorch flexibly and transparently. Ignite's Distributed Module is one of the greatest attraction of the library. It works on an Engine and Events based setup. The Metric module is an enhancement to this module to provide commonly used metrics out of the box with Ignite. 

Read more about Ignite at Ignite Github - https://github.com/pytorch/ignite

### 1.b My Proposal

My proposal is mainly based on enhancing the metrics module. I proposed to add four new metrics to Ignite, namely, Frechet Inception Distance (FID), Inception Score (IS), Perceptual Path Length (PPL) and Mean Average Precision (mAP). The initial idea was add GAN evaluation metrics (FID and IS), PPL which has great application in Style Transfer for Feature and Style Loss Calculation and mAP for Object Detection model evaluation like Fast-RCNN. Link to the original proposal - https://summerofcode.withgoogle.com/serve/5981180681256960/

## 2. The Work

### 2.a Inception Score

Inception Score (IS) is an objective metric for evaluating the quality of generated images, specifically synthetic images output by generative adversarial network models. It is the average of the overall KL Divergence of the features of two images. It uses a pre-trained Inceptionv3 model to calculate these features. Since KL Divergence is calculated featurewise, so it is difficult to calculate it in a distributed setting using the algorithm implemented in the original paper. A different algorithm needed to be devised which could adapt and work well in the ignite distributed setting. You can find more Inception Score in the paper found [here](https://arxiv.org/pdf/1801.01973.pdf). 

### 2.b Frechet Inception Distance

Frechet Inception Distance (FID) is a metric that calculates the distance between feature vectors calculated for real and generated images. Like IS, it also uses a pre-trained Inceptionv3 model. It uses the mean and covariance between the real and generated images' feature vectors to measure performance of a GAN. Similar to IS, FID uses mean and covariances over all samples to calculate the final result. While calculating online mean is easy, the covariance calculation needed to be modified to a more online implementation. The implementation is inline with the Pytorch-FID package found [here](https://github.com/mseitzer/pytorch-fid).You can find more about Frechet Inception Distance in the paper found [here](https://arxiv.org/pdf/1706.08500.pdf).

### 2.c Perceptual Path length

Perceptual Path Length (PPL) is mathematical formula which could be used as both a loss and an evaluation metric. It measures the difference between consecutive images (their VGG16 embeddings) when interpolating between two random inputs. Since the calculation of this distance can be slightly variable on a case by case basis so it is not suitable to be standarized as a metric. It has a wide array of application including Garment Transfer, Augmented Reality. It's greatest application however lies in style transfer. An ignite based Style Transfer example is implemented for the same. You can find more about Perceptual Path Length in the paper found [here](https://arxiv.org/abs/1603.08155)

### 2.d Mean Average Precision

Mean Average Precision (mAP) is a popular metric used to measure the performance of models doing object detection tasks. The mAP metric tries to greedily match detections with ground truths based on confidence scores and measures the Precision value for these matches at a given set of recall values. The average of all the recorded precisions is called Average Precision. The mean of these Average precision over all classes is called mean Average Precision. To implement a distributed mAP metric for ignite, the input had to be changed from per detection to per image as it would be difficult to keep track of imagwise detection in an online distributed setting. The implementation also provides all six flavours of mAP (3 based on Intersection over Union thresholds, 3 based on Detection Box Area) aviavlable in pycocotools. The implementation is inline with the pycocotools implementation found [here](https://github.com/cocodataset/cocoapi). You can find more about Mean Average Precision in the paper found [here](https://homepages.inf.ed.ac.uk/ckiw/postscript/ijcv_voc09.pdf).

## 3. Conclusion

Working on distributed metric in Ignite has been a wonderful experience so far. I got to learn a lot about working open source, contributing to existing projects, writing standardized tests and documentations amoung other things. It has been a great experience learning and working with my mentor to realize my proposal and contribute something meaningful to the Pytorch Ignite Community.

## Repository Structure

The Repository is divided into three folders, namely, metrics, examples and tests.

The metric folder contain the distributed implementation and documentation of three metrics, Frechet Inception Distance, Inception Score and mean Average Precision.
- FID PR (merged) - https://github.com/pytorch/ignite/pull/2049/files
- IS PR (merged) - https://github.com/pytorch/ignite/pull/2053/files
- Further work on FID and IS (merged) - https://github.com/pytorch/ignite/pull/2061/files , https://github.com/pytorch/ignite/pull/2094/files
- PPL - a pull request for the PPL has not been made since it is a case specific metric and does not have a more generalized implementation. An example and blog post showing implementation of the same in ignite can be found in the Examples listed below.
- mAP PR (Open) - https://github.com/pytorch/ignite/pull/2130

The tests folder contain the tests written for the above three metrics to test there functionality and compatibility with ignite.

The examples folder contain the Google Colab Notebook examples written for the above three metrics using pytorch-ignite.
- FID/IS Example (Completed) - https://colab.research.google.com/drive/1bMmIbS13y3UCpkl0BwaNiQISXGV5pbxL?usp=sharing
- PPL Example (In progress) (It has been left incomplete as mAP is a higher priority and needs to be done first.) - https://colab.research.google.com/drive/1uqGmxMiEO7iDorrsZd7ccQfwMoGsqmoZ?usp=sharing
- mAP Example (In progress) - https://colab.research.google.com/drive/1SdcNZ57OWPuo_XhNsipIMgFu9o5P51ga?usp=sharing

Note: Further work is being done on PPL Example, mAP PR and mAP Example. This work will be done in the same PR/ Notebook shared here. All three things mentioned above are functionally working and will give results inline with implementation they are being compared/ tested against. Future work is to be done on design and polishing.