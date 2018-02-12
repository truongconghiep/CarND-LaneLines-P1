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
Then the result is then converted to gray scale
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]




In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
