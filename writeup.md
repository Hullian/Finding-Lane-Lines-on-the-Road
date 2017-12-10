# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My method to obtain first countoured lanes and then averaged, extrapolated value of those contours consits of following steps:
  1) convert image to greyscale
  2) apply gaussian filter to reduce noise of the image as the derivative is amplifies any noise
  3) apply canny transform in order to calculate the gradient and in this way detect the edges
  4) apply mask to the image to focus only on the part where lanes are
  5) apply hough transform to calculate the coordinates of the lines of lanes
  6) draw aproximate lines and apply them to the image
  
The part I would like to focus more is calculation and extrapolation of the linear function that consists of lane points. In the adapted draw_lines function I divide my masked picture with a line that is in the middle of original picture. Next step is to calculate distance of x points from the middle line and check their relative position. If the distance between x and middle line is negative it means this point is part of right lane and vice versa. Also I look for x point that has smallest distance to the middle line from each side. This is how x1_left and x1_right is calculated. Then I'm looking for respectively x with highest value, as the point (0,0) is in the top left of the image it means it will be x2 point of the right lane, and x with the smallest value will be x2 point of left lane. Then I calculate slope a of the line connecting x1 and x2 and intercept b. Last step is to make y1 same on both lanes. Finally the lines are drawn with certain aproximation in the picture


### 2. Identify potential shortcomings with your current pipeline


As already seen with challenge video there are problems with curved lanes. 
Also the way I aproximate the lines coordinate is not perfect. 
One can also imagine a case when there is some white object on the road that is not filtered out.


### 3. Suggest possible improvements to your pipeline

The extrapolation method could be improved with some better calculations of x1 and x2 points. The aproximation with linear function is not optimal in case of curved lanes, so in order to fix that the lanes could be split into smaller parts to calculate linear function for them, in similar manner as integral considers infinitesmall parts of the function. Or one could use some 2nd order polynominal in order to calculate the aproximate function of the lane. I also wish that I had more time :)
