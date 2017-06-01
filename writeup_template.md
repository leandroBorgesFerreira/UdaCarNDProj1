


# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection


My pipeline consisted of 5 steps. First, I converted the images to grayscale so colors wouldn't matter in my solution. Then I added a Gaussian blur to make the derivate more smooth and avoid disturbances. After that, I added Canny edge detection. And then, I cut off the region that was not of my interest. 

It is important to do not use Canny edge detection after the region of interest cut, because the bounds of the region are going to appear as an edge if you do so. 

Then i had to apply Hough Lines in the new image and then combine the initial image with the the one containing the lines.

Then, I got this: 
![enter image description here](https://lh3.googleusercontent.com/-EWpxYPD3_no/WTAll3V0enI/AAAAAAAAMCY/e8zq903RuXsv8tJrvGxJmHYlww_B1jj7QCLcB/s500/Screen+Shot+2017-06-01+at+11.24.06.png "Screen Shot 2017-06-01 at 11.24.06.png")

(I changed the color from red to blue... I think it is easier to see this way) 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to find the average line that is closer as possible of all blue point in the image. Then I extrapolated the lines until it reaches the bottom of the image. 

The result:
![enter image description here](https://lh3.googleusercontent.com/-PgoLemsTfgk/WTAm__ipq_I/AAAAAAAAMCo/7AQCkK-dwNkWJXCrTDUJlS6bKNqK_D8eQCLcB/s500/Screen+Shot+2017-06-01+at+11.36.11.png "Screen Shot 2017-06-01 at 11.36.11.png")

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the car finds a shadow or another big disturbance in the road. I don't believe that the algorithm is robust to disturbances because it is completely statical. It never remembers what was processed before the current image so it can't use previous images to help with the current one. The results should the integrated the help with the decisions about the lines, like a PI (or PID) controller. Right now, it works only as a proportional controller. 

Another shortcoming could be when the car is not aligned with road because to the region of interest cuts a big part of the image. As it is completely statical, when the car is in strange positions in relation to the road, the algorithm can present bad results. The same problem goes when the car finds a curve.

Also, white cars are mixed with lines.


### 3. Suggest possible improvements to your pipeline

Keep previous results to help to evaluate the current image. 

Work with curves instead of line can be a better approach to the problem. 

Detect cars. 
