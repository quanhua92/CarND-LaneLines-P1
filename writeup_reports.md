#**Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image01_masked]: ./examples/01_masked_image.png "Masked Image"
[image02_pipeline]: ./examples/02_pipeline.png "Pipeline"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a Gaussian Blur Kernel with the size of 3. Then, I used a Canny Edges Detector with low threshold of 50 and high threshold of 100.

I use a poly mask image to remove unnecessary edges. The result image is as follows:

![alt text][image01_masked]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by using the slope and positions of each lines. Besides, I also discard lines which are out of some fixed ranges of slopes. For example, a line on the right is counted only if the x1 and x2 is larger than half of image width and the slope is between 0.35 and 0.7. The same rule is apply to lines on the left.

Then, I will calculate the average x, y and slope for the line of the left and right separately. The avarage values are computed with weights which are their line lengths.

In order to create the left line and right line, I use the average x, y, slope to compute the x position for 2 points: mid point(y=height / 2) and bottom point( y = height). Then, I draw a line through these 2 points.

Here is how my pipeline works:


![alt text][image02_pipeline]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when:

- The position of the lines are out of my fixed masked image.

Another shortcoming could be:

- The slope of the lines are out of the fixed ranges.
- Too many shadows which create many false edges.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to:
- Use a linear regression model to create a function of the left and right lines.

Another potential improvement could be to :
- Use a classifier to decide if a line is a street line or a shadow line.