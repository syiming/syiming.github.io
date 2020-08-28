---
layout: post
title:  "Google Summer of Code with TensorFlow Model Garden"
date:   2020-08-24 15:07:19
excerpt: "A ton of text to test readability."
categories: [Tech]
comments: true
image:
  feature: posts/gsoc.png
---

> This blog post serves as a report of Yiming’s 2020 Google Summer of Code student project.

## Mentor

TF Model Garden: Jaeyoun Kim (jaeyounkim@)

Object Detection team: Vivek Rathod (rathodv@), Shan Yang (shanyang@) 

## Faster/Mask R-CNN FPN in Object Detection API
### Goal

The goal for this project is adding a Resnet FPN feature extractor for faster RCNN. The work I have done including:
* Add Resnet FPN feature extractor.
* Add multilevel crop and resize function.
* Modify faster RCNN meta architecture to accept multilevel features.
* Modify proto files such that feature extractor can accept more args.

The class diagram for the Resnet FPN feature extractor is shown below.

![class_diagram](/img/posts/class_diagram.png)

### Results

Before adding FPN to the Faster RCNN with Resnet50 as backbone, the model reaches mAP 29.3 on COCO dataset. After adding FPN to the Faster RCNN with Resnet50 as backbone, the model reached mAP 31.6.


IoU       | area  | maxDets | Average Precision
----------|-------|---------|------------------
0.50:0.95 | all   | 100     | 0.316
0.50      | all   | 100     | 0.551
0.75      | all   | 100     | 0.335
0.50:0.95 | small | 100     | 0.107
0.50:0.95 | medium| 100     | 0.274
0.50:0.95 | large | 100     | 0.457


IoU       | area  | maxDets | Average Recall
----------|-------|---------|------------------
0.50:0.95 | all   | 1       | 0.285
0.50:0.95 | all   | 10      | 0.458
0.50:0.95 | all   | 100     | 0.497
0.50:0.95 | small | 100     | 0.269
0.50:0.95 | medium| 100     | 0.477
0.50:0.95 | large | 100     | 0.641

Type                                       | Loss
-------------------------------------------|-------
Loss/RPNLoss/localization_loss             | 0.080119
Loss/RPNLoss/objectness_loss               | 0.021327
Loss/BoxClassifierLoss/localization_loss   | 0.272600
Loss/BoxClassifierLoss/Classification_loss | 0.3121138
Loss/regularization_loss                   | 0.271487
Loss/total_loss                            | 0.954237

### Pull Request
The related pull request for this project is listed in the following table.

Title                                      | Link
-------------------------------------------|-------
Add Faster RCNN Resnet V1 FPN Keras feature extractor | [#8716](https://github.com/tensorflow/models/pull/8716), [#8762](https://github.com/tensorflow/models/pull/8762)
Add multilevel crop and resize functions              | [#8746](https://github.com/tensorflow/models/pull/8746)
Move to keraslayers fasterrcnn fpn keras feature extractor   | [#8893](https://github.com/tensorflow/models/pull/8893)
moving fpn message to fpn.proto | [#8894](https://github.com/tensorflow/models/pull/8894)
Adjust frcnn meta arch to multilevel rpn feature | [#8895](https://github.com/tensorflow/models/pull/8895)
add config file for faster rcnn resnet 50 fpn on dataset coco17 using tpu-8                          | [#9055](https://github.com/tensorflow/models/pull/9055)
Add fpn to context rcnn | [#9078](https://github.com/tensorflow/models/pull/9078)



## Community Support for TF2 Object Detection API (GitHub issues)
### Goal
Collect all issues (bugs, new features, docs) for Object Detection API since it upgraded to TF2 and help resolve Object Detection API issues. 

The issues that I have collected and help is listed in this [sheet](https://docs.google.com/spreadsheets/d/1q8t4TO455IWHbMsb9AKlsUxgogLwCqqhe73DXi82B8Y/edit?usp=sharing).

### Pull Request
The related pull request for this project is listed in the following table.

Title                                      | Link
-------------------------------------------|-------
frozen inference graphs tf 1 documentation update | [#8984](https://github.com/tensorflow/models/pull/8984)
remove unused import within image_resizer.proto | [#8954](https://github.com/tensorflow/models/pull/8954)
fix links for research/object_detection/colab_tutorials/object_detection_tutorial.ipynb | [#8985](https://github.com/tensorflow/models/pull/8985)
fix object_detection_tutorial.ipynb instance segmentation example error | [#8978](https://github.com/tensorflow/models/pull/8978)



## Panoptic Feature Pyramid Networks

### Goal
Implement CVPR 2019 paper - [Panoptic Feature Pyramid Networks](https://arxiv.org/abs/1901.02446).

### Current Progress
* Read paper and Detectron2 implementation for Panoptic Feature Pyramid Networks.
* Reading code in TensorFlow official computer vision modeling library.
* Waiting for updates in official library and will start implementing as soon as changes are released. Will continue working on this project in the following months.




