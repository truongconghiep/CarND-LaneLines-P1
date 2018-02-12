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


---

### Reflection

### 1. Pipeline

My pipeline consisted of 6 steps. 

1. Color masking

2. Gaussian blurring 

3. Edge extraction

4. Region masking to extract the region of interest 

5. Hough Transform - Average lines

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
After filtering all pixels of lanelines the result images of the 3 steps above are combined together to have an gray image, which despites the lanelines in the original image.
![alt text][image5]

#### Gaussian blurring

The purpose o this step is to cut down on visual noise and ensure that only the sharpest edges get through in edge detection step.
![alt text][image6]

#### Edge extraction
In this step, canny edge detection algorithm is applied to detect all edges in the gray image from the previous step.
![alt text][image7]

#### Region masking to extract the region of interest
By applying this step we can ignore the pixels, where lane lines shouldn't be. In this step a fixed region in the image is chosen before performing hough transform. All pixels in
this region are preserved, the others outside this region will be removed.
![alt text][image8]



#### Hough Transform - Average lines

#### Draw lines




In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
