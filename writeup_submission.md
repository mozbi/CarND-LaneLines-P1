# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---


### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

1) Convert image from RBG to HSV and from RBG to grayscale to generate an image mask for detection of both yellow as well as white lanes.
2) Perform Gaussian Blur and Canny Edge detection to generate an image with the edges of lanes.
3) Apply a region of interest on the image. This region of interest region is of a tripezium shape and will be based on the image size and contain the two lanes of interest.
4) Generate hough lines by supplying finely tuned hough parameters and drawing the hough lines.
5) Blend the hough lines image with the original image to generate the original image with the lane lines overlayed in red.

The draw_lines() function was modified using these steps:
1) Compute gradients and intercepts for every line segment from the hough_lines() output.
2) Determine line segment with the max slope and min slope. 
These slopes will allow us to have a reference point from which to bucket all the other line segments to decide which ones are to form the left lane line and which to form the right lane line. The max slope, which is positive will be the reference point for the left lane line bucket and the opposite can be said for the right lane line bucket.
3) Determine which line segments belong to the left lane line bucket and which on the right based on the values in 2), in combination with a tolerance factor.
4) Find the average slope and intercept in each bucket.
5) Generate end points for the left lane line and the right lane line given the average slope and intercepts for each bucket.

# Reflections

1) One of the initial short comings of the pipeline was not being able to detect yellow lanes.
Previously, I had only come up with a grayscale mask. Upon further investigation, I learned that converting from RBG to HSV would allow for the generation of a yellow mask.

2) The lines being drawn in the draw_lines() function do not handle curved lines nor does it completely follow the length of the lines on the road. This is a result of both the algorithm used as well as the fact that an ROI is in play.

3) When playing videos, the lines being drawn seem to be "vibrating" with every frame. More can be done to smooth this out.
For example, the line being drawn in the previous frame or image can be saved and used in coming up with the line to be drawn for the next frame. This way, the lines drawn in the video can be made to look smoother.

