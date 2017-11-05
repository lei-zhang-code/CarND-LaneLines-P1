# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_proc]: processing_pipeline.png "Image Processing Pipeline"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 4 steps. 
1. Convert the images to grayscale and apply an gaussian smoothing filter.
2. Detect edges using Canny edge detector.
3. Apply mask to preserve only a trapezoidal region.
4. Detect line segments using Hough transform.
The pipeline is summarized in the the following figure.
![alt_text][image_proc]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as following:
1. Compute all line segments' Hough polar parameters rho and theta based on their end point.
2. Group lines into three groups: right lane (0.8 < theta < 1.2), left lane (-1.2 < theta < -0.8), outliers (other theta).
3. Fit a straight line over all the end points of the lines in each of the first and second groups.
4. Only draw the straight line between a user specified top and bottom y range.

### 2. Identify potential shortcomings with your current pipeline

Here are a list of short-comings:
1. Hard coded edge detection thresholds will fail when lighting is too bright or too dark.
2. Does not work with lanes consist of only dots.
3. Does not work at sharp turn since Hough transformation parameters are hard coded.
4. Does not work when vehicle changes lane since region of interest is hard coded.
5. Does not work when there are complicated markings on the road, such as bike and pedestrain crossing markers.
6. Does not work when the road color has a sudden change due to shadow, bridge or newly paved road section. Like what happened in 3~4 second in the challenge video.

### 3. Suggest possible improvements to your pipeline

Potential improvement:
1. To improve for different lighting conditions, one can adjust the edge contrast by histogram equalization.
2. Using end-to-end machine learning method with labeled data to train a more sophisticate model to avoid having to manually engineer each corner cases.
