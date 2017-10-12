# **Finding Lane Lines on the Road** 


### 1. Approach

Here I designed a lane detector using low-level computer vision techniques. I will illustrate the steps of my algorithmic approach using the sample image below.

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_1_raw_solidyellow.png)

First, we convert the RGB image to grayscale and apply canny edge detector (low_thres=50, high_thres=150) on an image that is Gaussian blurred with kernel_size=5

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_2_canny.png)

Because the camera is upright and facing forward, we can assume the vanishing point law for the lanes, and mask the image with a trapezoid to get rid of details that do not belong to lanes.

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_3_canny_mask.png)

We then apply a line detector based on Hough transform. For the Hough transform parameters, I used threshold=3, min_line_length=100, and max_line_gap=100

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_4_hough_raw.png)

Since our aim is to determine one left (or right) lane, we aggregate all left (or right) lanes detected by previous step, and average their end coordinates to generate a single filtered line. The left/right determination was done by looking at the slope of individual lines. If(y2-y1)/(x2-x1) was greater than 0.3, we called it a candidate right lane, and if(y2-y1)/(x2-x1) was less than -0.3, we call it a candidate left lane. Note that a margin was forced in the slope check step to reject false lane detections.

Also, the single left and right lanes then were corrected to touch the bottom and near-center of image. This was done by applying simple linear extrapolation.

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_5_hough_filt_ex.png)

Finally, we overlay our lane detection results on the original image.

![alt text](https://github.com/willtopower/project_1-lane_detection_using_low_level_CV/blob/master/imgs/img_6_overlay.png)


### 2. Shortcomings and how to improve

A shortcoming of the current approach is that is it complete based on rules that we gathered from ideal driving scenarios. Few challenging natural scenarios that violate the rules of the algorithm would be road with illumination variations from signs, other cars making lane changes, etc, and a lot of false lanes would be generated. To address those situations, we can modify the algorithm in two ways
* modifiable lane length to gain precision
* incorporate temporal information

