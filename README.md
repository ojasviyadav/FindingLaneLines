# FindingLaneLines
 • Designed a lane-finding algorithm which identified lane lines • Employed OpenCV, Hough Transform, Canny edge detection, Gaussian blurring, object interpolation • Successfully applied the algorithm on sample video shot from a camera in a car

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road




### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline does these functions in a sequence to find lane lines :
1. Gets the image as an input
2. Applies grayscale
3. Applies some Gaussian blurring to smooth out pixels in order to
filter out sharp edges
4. Marks all the edges as white and everything else as black using
Canny edge detection
5. Applies hough transform to find the lines in the image space by
detecting intersections in the hough space. It also calls the 
function which classifies these lines into left and right lines 
and then draws them (draw_lines())
6.The lines and the image are superimposed on each other and
returned as output

Here’s how the draw_lines() function works
1. Declares x,y arrays for both left and right lanes
2. Runs a for loop to go through all the elements given to it by
hough_transform() function. In this loop,
	A. A slope variable m is defined as (y2-y1)/(x2-x1)
	B. According the the sign of the slope, positive or negative, it’s
	classified as a left or a right lane point and appended 
	into the suitable array
3. A variable L stores the slope and intercept of the Left lane points
gathered in step 2
4. A variable R stores the slope and intercept of the right lane points
gathered in step 3
5. The number 540, which is the y value of the lowest pixel row in the
image, is appended in the array which already contains the detected y
points of left and right lane. This is done to consider the position where the drawn
lines are to be extended till.
6. The prediction is made using the polyval function. A line which
passes through the detected x,y points for both the lanes is extended up to the base of 
the image because it also had to make a prediction based on the given line for it.
7. The predicted points and detected points are then drawn

### 2. Identify potential shortcomings with your current pipeline

1.If the lane goes out of the region of interest then the hough
transform work
2. If the lane has different colours it might cause issues
3. If there is a car crossing lanes then it would block the view to get
lanes
4. Going up or down a terrain will cause the region of interest to be
insufficient
5. taking left or right turns will alsu cause region of interest to be
insufficient

### 3. Suggest possible improvements to your pipeline

1. The region of interest should be flexible, it should expand until the
lanes are found
2. Using supervised learning we can train the pipeline to know what a
turn looks like
3. We can transform and warp the image to enhance the knowledge 
of a curvature.
