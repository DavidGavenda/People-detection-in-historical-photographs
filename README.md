# People-detection-in-historical-photographs
Master thesis on topic of People detection in historical photographs

Author : Bc. Dávid Gavenda <br />
Supervisor: Ing. Zuzana Rábeková <br />

[Link to Master's thesis in CRZP (slovak language)](https://opac.crzp.sk/?fn=detailBiblioForm&sid=EC7951772ACC837B5F7DC5A56A1E)

## Abstract 

The thesis delves into the issue of detecting individuals in digitized historical photographs. It examines the challenging factors that distinguish historical photographs from regular ones, on which detection is typically conducted and existing detectors are trained. It contrasts the performance of current detectors on our own labeled collection of historical photographs, which encapsulate scenes from everyday life. The thesis also investigates methods of photo restoration and the influence of such restoration on detection models. Furthermore, it explores the transfer learning of existing models with the aim of achieving better results, and it includes an analysis of the findings obtained. 

## Top 10 models

The analysis of the top 10 models on the validation set (see table below) clearly demonstrated that the most effective way to fine-tune models is to use original photos. The YOLOv8l-custom model, which was trained on these original photos, achieved a precision of 0.749, a recall of 0.724, and an F1 score of 0.737, which was superior compared to the other models in the table. When evaluating the other models, we can observe that the best models achieved precision values ranging from 0.742 to 0.886, recall values ranging from 0.555 to 0.724, and F1 scores ranging from 0.668 to 0.737.

| Model                           | Precision | Recall | F1    |
|---------------------------------|-----------|--------|-------|
| YOLOv8l-custom                  | 0.749     | 0.724  | 0.737 |
| YOLOv8x6-custom                 | 0.78      | 0.647  | 0.708 |
| YOLOv7-D6                       | 0.868     | 0.579  | 0.695 |
| YOLOv7-E6                       | 0.876     | 0.573  | 0.693 |
| YOLOv7-E6E                      | 0.873     | 0.566  | 0.687 |
| YOLOv7-W6                       | 0.886     | 0.555  | 0.683 |
| YOLOv8l                         | 0.792     | 0.598  | 0.681 |
| faster-rcnn-R-101-FPN-3x        | 0.742     | 0.612  | 0.671 |
| faster-rcnn-X-101-32x8d-FPN-3x  | 0.749     | 0.608  | 0.671 |
| YOLOv8l-cyclegan                | 0.755     | 0.6    | 0.668 |

In total 70+ models were tested and their results and confusion matrices can be found withing this repository 

[Access the Custom models](https://drive.google.com/drive/folders/1SU0OsNtJ4glwEIKVc9N8b3yXbCZomf2c?usp=share_link)

## Restoration

We found that Deoldify almost always worsened the results. Even though the images are more colorful and pleasing to the eye, the overall quality did not improve. The GFP-GAN was able to improve overall results the best, and even though precision decreased, the F1 value increased the most. The solution from Microsoft achieved the second-best results at the highest settings. The dataset size increased by 460%, while the resolution remained the same, but the format changed to .png. The best results were achieved by restoring photos using GFP-GAN, but it is still only a minor improvement.

| Type                        | Size Change (%) | Precision Change | Recall Change | F1 Change |
| ----------------------------|-----------------|------------------|---------------|-----------|
| Deoldify-Artistic           | 39%             | 0                | -0.02         | -0.02     |
| Deoldify-Standard           | 39%             | 0.004            | -0.02         | -0.02     |
| **GFP-GAN**                 | 93%             | -0.01            | 0.016         | 0.012     |
| GFP-GAN-Deoldify-Standard   | 39%             | 0.004            | -0.02         | -0.02     |
| GFP-GAN-Deoldify-Artistic   | 39%             | 0                | -0.02         | -0.02     |
| Microsoft-AI                | 461%            | -0.002           | 0.012         | 0.01      |
| Microsoft-AI-HR             | 460%            | -0.002           | 0.012         | 0.01      |

* all changes were difference based on model YOLOv8l with confidence = 0.15 which resulted in highest F1 value 


## Graph comparing all increments of confidence between 0.05 and 0.95 for YOLOv8l model

![Diagram](yolov8lconfidence.png)

## Graph comparing best F1 values based on best model for respective resolution

![Diagram](graphbyresolution.jpg)

## Graph comparing best F1 values and speed based on best model for respective year

![Diagram](graphbyspeedandyear.jpg)

Testing was done on Nvidia RTX 3060 Ti and Ryzen 5600x with 64GB of RAM.

# Project Overview

Currently, rapid advancements in the field of computer vision and deep learning are leading to significant progress in the detection of objects in images. Current models achieve excellent results across a broad spectrum of benchmark databases. However, the success of these models can be limited when applied to lower-quality photos, such as digitized historical photographs.

This work focuses on exploring the possibilities of using modern computer vision methods for object detection, specifically people, in historical photographs. The aim is to determine how current models handle such a task and identify opportunities for improving their performance in this particularly challenging task.

The theoretical part is dedicated to studying the issues of people detection using deep learning methods, encompassing the exploration of current approaches, techniques, and models used in object detection. This part of the work will include the theoretical foundations of machine learning, deep learning, neural networks, and convolutional neural networks.

## Practical Part

In the practical part, we are engaged in:

- Identifying and creating a suitable database of labeled digitized historical photographs, which serves as the basis for training and testing models. For this purpose, we used our own set of historical photos, obtained from the Fortepan collection and photographs from the life of Milan Rastislav Štefánik. We labeled these photos using the CVAT tool so that we could use our own photo database for training models and testing their success. The work will also be devoted to the analysis of the quality and characteristics of such a dataset.
- Verifying existing solutions for the given problem, including testing current state-of-the-art (SOTA) models on the selected database. This part of the work will focus on a wide range of models, such as Haar Cascade, HOG, R-CNN, SSD, Mask R-CNN, RetinaNet, MobileNet, CenterNet, EfficientDet, and YOLO. It will also pay attention to the latest versions of these models, such as YOLOv7 and YOLOv8.
- Testing existing models on the obtained dataset is also part of the work. This part includes the evaluation of models, analysis of single-stage and two-stage models, as well as the examination of problematic photos, on which the models may struggle with object detection. Various models, such as YOLO models, single-stage models (e.g., SSD), and two-stage models (e.g., R-CNN), will be examined within the testing.
- Finally, the work will include an analysis of the obtained results, identification of areas where there are possibilities for improving the performance of current models for detecting people in historical photographs, and a discussion about possible next steps and research directions in this field.

## Project Aim

The main aim of this work is to explore the possibilities of using modern methods and models of computer vision for object detection, specifically people, in historical photographs. The work focuses on testing current state-of-the-art (SOTA) models on digitized historical photographs and analyzing their performance in this particularly challenging task, to find out how current models handle such a task and identify opportunities for improving their results in this area.

This work will provide a detailed overview and analysis of current methods and models used in the field of computer vision and deep learning for object detection, focusing on the detection of people in historical photographs. The results of this work will contribute to a better understanding of the possibilities and limitations of current approaches, as well as the identification of potential opportunities for improving the detection of people in digitized historical photographs.

# Conclusion 

In this work, we focused on detecting people in historical photographs and thoroughly examined current machine learning methods, including deep learning and deep convolutional neural networks. We concentrated on various object detection models. Additionally, we looked into GAN networks and their application in the artificial aging process of photographs.

In the theoretical part of our work, we focused on an overview of machine learning methods, with an emphasis on deep convolutional neural networks, which are the basis for detecting people in photographs. We presented various models based on these networks, such as Haar Cascade, HOG, Faster R-CNN, SSD, Mask R-CNN, RetinaNet, CenterNet, EfficientDet, and YOLO. Additionally, we devoted ourselves to GAN networks, which are a significant tool for modifying and reconstructing image data, including historical photographs. The theoretical part provided us with a solid basis for the experimental part, where we tested and compared various models and methods.

In the practical part, we compiled a database of historical photographs and evaluated their quality. Based on our analysis, we tested the performance of existing models of person detection, identifying problematic photos. We examined the possibilities of improving the results through photo restoration and transfer learning on our own sets and through artificial aging of photos using CycleGAN or by adjusting photos by adding filters.

Although we achieved some improvement in the results of detecting people in historical photographs thanks to transfer learning and artificial aging of photos, the results are still not ideal, and there is room for further research and improvement. In the future, it would be interesting to explore new techniques, models, and approaches that could lead to better detection of people in these fascinating and historically valuable images.

Based on the knowledge gained from our work, we can suggest several possible research directions, such as the development of new models and multimodal approaches for detecting people in historical photographs, exploring generative adversarial networks for more efficient photo modifications, and the impact of various factors on detection. We recommend increasing the amount of historical photographs in our dataset, training GAN networks for a longer time on a larger number of photos with higher resolution, and considering the use of transfer learning or meta-learning to make model training more efficient. It is important to consider the high GPU demand of GAN networks and consider options for optimization and efficiency of training to reduce the demands on computational resources and enable wider use of these methods in practice.

In conclusion, detecting people in historical photographs is an interesting and significant area of research that offers many opportunities for future development and innovation. Although we have achieved certain improvements in our work, it is necessary to continue looking for new approaches and techniques that could lead to even better results and allow us to better understand and analyze these valuable historical resources.





