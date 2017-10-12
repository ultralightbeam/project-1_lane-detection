# **Finding Lane Lines on the Road** 


### 1. Approach

Here I designed a lane detector using low-level computer vision techniques. I will illustrate the steps of my algorithmic approach using the sample image below.

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_1_raw_solidyellow.png)

First, we convert the RGB image to grayscale and apply canny edge detector (low_thres=50, high_thres=150) on an image that is Gaussian blurred with kernel_size=5


![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_2_canny.png)




### 2. Shortcomings and how to improve

A possible improvement would be to ...

Another potential improvement could be to ...
