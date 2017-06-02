# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[grayscale]: ./writeup/grayscale.png "Grayscale"
[grayblur]: ./writeup/grayblur.png "Grayscale Blurred"
[canny]: ./writeup/canny.png "Canny"
[cannymask]: ./writeup/cannymask.png "Masked Canny"
[result]: ./writeup/result.png "Result" 
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale. then I applyed Gaussian Blur with to surpress noise and spurious gradient. And thirdly, I applied Canny Edge Detector to the blurred image to locate all pixels of edges (strong gradient). Fourthly, I apply a trapezoidal image mask to filter our irrelavent edges and only leave the ones that are most likely belong to lane lines. Finally, I applied Probablistic Hough Line Transform to find all the start and end points of line segments.  

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Grayscale][grayscale]
![Grayscale Blurred][grayblur]
![Canny][canny]
![Masked Canny][cannymask]
![Result][result]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
