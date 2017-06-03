# **Finding Lane Lines on the Road** 


[//]: # (Image References)

[iamge0]: ./test_images/solidWhiteCurve.jpg "Input Image"
[image1]: ./writeup/grayscale.png "Grayscale"
[image2]: ./writeup/grayblur.png "Grayscale Blurred"
[image3]: ./writeup/canny.png "Canny"
[image4]: ./writeup/cannymask.png "Masked Canny"
[image5]: ./writeup/result.png "Result" 
[image6]: ./writeup/problem.png "Problem"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consist of 5 steps

##### Input Image
![Input Image][iamge0]
##### Step 1 Convert to grayscale
![Grayscale][image1]
##### Step 2 Gaussian Blur
Apply Gaussian blur to the gray scale image to surpress noise and spurious gradient.
![Grayscale Blurred][image2]
##### Step 3 Canny Transform
Apply Canny transform to the blurred image to locate all pixels of edges (strong gradient).
![Canny][image3]
##### Step 4 Masked Canny Transform
Apply a trapezoidal image mask to filter our irrelavent edges and only leave the ones that are most likely belong to lane lines.
![Masked Canny][image4]
##### Step 5 Probablistic Hough Line Transform
Apply Probablistic Hough Line Transform to find all the start and end points of line segments.

Here is the final result superimposed onto the original image.
![Result][image5]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first fitting a straight line on to each paire of the start and end points and then filtering out lines with slopes that are either too flat or too steep and only keep the ones that have slope coefficient between 0.1 and 100. Then the fitted lines were separated into two groups one with positive slope and one with negative slop. Finally, the coefficent of the final lany line is calcuated from the weighted average of the coefficent by length of each line segments, and the start and end point of each lane line is the max and min points in each group.


### 2. Identify potential shortcomings with your current pipeline


Here are the potential short comings:

- sharp turns may not be correctly identified
- faded lane lines may not be correctly identified if the gradient (change in grayscale pixel value) is small                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    
- the parameters are hard coded to work well under direct sunlight and may not work well under other weather/lighting conditions 
- may not work well in heavy traffic conditions where many of the lane line segments are occluded
- does not work well when there are other marks with in the masked area, one example shown below, where a horizontal line crossing with one of the lane line
![Problem][image6]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   


### 3. Suggest possible improvements to your pipeline

Possible improvements:
- collect photos from many different weather/lighting conditions and dynamically adjust parameters (i.e. canny threshold values, hough line transform params)
- use information from adjacent frames to help locate lane
