# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidYellowCurve.jpg "solidYellowCurve"
[image2]: ./test_images/rgb_y.jpg "rgb_y"
[image3]: ./test_images/rgb_w.jpg "rgb_w"
[image4]: ./test_images/hls_y.jpg "hls_y"
[image5]: ./test_images/color_threshold.jpg "color_threshold"
[image6]: ./test_images/Gassian_Blur.jpg "Gassian_Blur"
[image7]: ./test_images/Canny_Edges.jpg "Canny_Edges"
[image8]: ./test_images/Region_Of_Interest.jpg "Region_Of_Interest"
[image9]: ./test_images/lines_edges.jpg "lines_edges"

lines_edges
---

### Reflection

### 1. Pipeline

My pipeline consisted of 6 steps. 

1. Color masking

2. Gaussian blurring 

3. Edge extraction

4. Region masking to extract the region of interest 

5. Hough Transform

6. Draw lines

Let's use the image below as our original:
![alt text][image1]

#### Color masking

Since most of lanelines are yellow or white, we can firstly filter out the pixels in a picture, which roughly represent the lanelines on the road.
To do that, first yellow thresholds are applied to the original image in BGR color space to determine the pixels of yellow lanelines. Other pixels are removed from the image.
Then the result is then converted to gray scale. The result image of yellow threshold in RGB color space is shown below.

![alt text][image2]

The next step of color masking is filer out white pixels, which represent while lanelines. Very similar to filtering out yellow pixels, white thesholds are applied to the original image
to filter out white pixels. The result image of white threshold in RBG color space is shown in the image below.

![alt text][image3]

Because yellow thresholding in the first step is not as effective as filtering while pixels, an additional filtering step is required to extract yellow pixels. In this step the yellow pixels are 
extracted in HLS color space. This method provides a very reliable result. The input image is first converted into HLS color space, then yellow thresholds are applied to filter the yellow pixels.
The result image of yellow threshold in RGB color space is shown below.

![alt text][image4]

After filtering all pixels of lanelines the result images of the 3 steps above are combined together to have an gray image, which depicts the lanelines in the original image.

![alt text][image5]

#### Gaussian blurring

The purpose of this step is to cut down on visual noise and ensure that only the sharpest edges get through in edge detection step.

![alt text][image6]

#### Edge extraction
In this step, canny edge detection algorithm is applied to detect all edges in the gray image from the previous step.

![alt text][image7]

#### Region masking to extract the region of interest
By applying this step we can ignore the pixels, where lane lines shouldn't be. In this step a fixed region in the image is chosen before performing hough transform. All pixels in
this region are preserved, the others outside this region will be removed.

![alt text][image8]

#### Hough Transform
After we have our regioned-out edges from the Canny algorithm, we pass the image through a Hough Transform. The Hough transform results lines detected from the edge image. The lines can
belong to the lane lines, they also can be geometric properties of other objects on the road, which appear in the region of interest.

#### Draw lines
In this step, based on the lines detected by hough transform 2 lines will be drawn on the original image to represent left and right lane lines in front of the vehicle. To draw these two lines 
slope and center of all hough lines must be calculated with following formulas:

slope = (y2 - y1)/(x2 - x1)

center = [(x1 + x2)/2, (y1 + y2)/2]

Based on the calculated slope the lines will be separated in 2 groups: left and right. If slop is positive then put it in the right group, else put it in the left group. Here a slop threshold can
be introduced to filter out the lines, which should not represent any lane lines. For example lines, which have very small slope. After that an average slope and center for each group will be 
calculated. These slop and center represent the left and right land lines in the original image. Unfortunately, with slope and center we can still not draw the lines on the original image, thus
we must find out 2 end points of the line. To determine these 2 points we just give 2 y-coordinates and calculate the corresponding x-coordinates with following formula:

x = x_center - (y_center - y_given)/slope

Hence we have 2 end points of the line, we can draw it on original image.
![alt text][image9]


### 2. The Pipeline’s Shortcomings

One potential shortcoming would be the function *Draw_Lines*. This function cannot draw horizontal lines, because their slopes are infinity.

Another shortcoming could be the fixed vertices by determining the region of interest. The coordinates of the region of interest were hard-coded, therefore it cannot react to any terrace changes, 
for example when car is cresting a hill or coming out of a valley.


### 3. Possible Pipeline Improvements

A possible improvement would be to determine the region of interest dynamically.

Detected lines of a previous frame can be used in the current frame to detect the current lane lines. The old lines help to average changes in the current frame and play a roll of low pass filter 
to stabilize the detection of lane lines

Another potential improvement could be to ...
