---
date: 2021-08-11
title: "AI Boostcamp Day 8"
categories: 
 - Naver AI Boostcamp Diary
tags:
 - Convolution
 - Python
author: Hyeong
description: Basic concept of convolution, 
---
### What I studied today:
1. How Kernerls Work
    - Input size, kernel size, output size
    - Knowing only two above the above, can tell the size of the other
2. The Larger the Parameter Size, the Less Robust the Model Is
3. Padding
    - Enlarging the input size with additional slots e.g. zero padding
4. Stride
    - The space that the kernel takes when it slides over the input
5. 1 x 1 Convolution
    - Reducing Dimension
    - Decreasing the number of parameters and increasing the depth
    - e.g. 128x128x128 --(Kenerl:1x1x128x16)--> 128x128x16
6. Trend of CNN
    - Lesser parameter, deeper layers, better performance
    - AlexNet:
        - 11*11 Kernel. Larger receptive field, but leads to too large parameter
    - VGGNet:
        - 3x3 Kernel. Why? Two 3x3 layers = One 5x5 layer. Two 3x3 layer has less parameter. Larger receptive field with less parameter
    - GoogLeNet:
        - Inception Block (1x1 Kernel). Performs channel-wise dimension reduction. Performing 1x1 kernel convolution before another convolution as such 3x3 kernel operation can reduce the number of parameters significantly
        - Deeper layer and significantly ligther
    - ResNet:
        - Deeper layers did not train after certain number of operations
        - Channeling the input to the output channel directly with or without inception block. The layer aims to train on x + f(x)
    - DenseNet:
        - DenseNet is similar with ResNet, but it concatenates instead of adding. The channel increases geometrically, thus need to use 1x1 kernel convolution
7. Segmentation
    - Fully Convolutional Network (convolutionalization):
        - Removing the dense layer and replacing it with convolutional layer
        - Number of the pararmeters are the same
        - Result layer small. Need to size up (deconvolution)
        - Not the other way around of deconvolution because the lost information due to small scale does not come back
    - R-CNN:
        - Many random bounding box + CNN
        - Run the nn for every bounding box, slow
    - SPPNet:
        - Run the nn only one time for one image. Use on;y the corresponding weights of that bounding box
    - Fast R-CNN:
        - SSPNet + bouding box regression (how to move the bb)
    - Faster R-CNN:
        - Network also selects the bounding box
        - Region Proposal Network + Fast R-CNN -> Faster R-CNN
    - Region Proposal Network?
        - Anchor Boxes: presized detection boxes
        - Anchor Boxes: the nn decides what size range, how much the size should change, and whether the box is useful
    - YOLO
        - extremely fast object dectection (bounding box)
        - No discrete region proposal network, thus faster
        - Divides the input image into NxN grid
        - Each bounding box is reponsible for selecting five cells and classifying the class
        - Output: NxNx5xC
