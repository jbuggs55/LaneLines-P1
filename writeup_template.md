# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
1. Convert to gray scale. Gray scale will allow us to associate rapid changes in pixel colors to gradients.
2. Remove unnecessary noise by applying gaussian blur to the gray scale image. While the guassian blur is embedded in hough transform, this enhances the image even more and gives us flexibility to adjust parameters if needed(kernel size)
3. Feed the enhanced image into the canny edge detection function. This gives us a binary image(white pixels are associated to gradients above the threshold. Additionally, the white pixels also represent those pixels whose gradient is in the middle of the low and high thresholds AND are connected to the above gradient threshold pixels. These white pixesl represent edges and these edges will help use identify lines.
4. After identifying the edges, we identify the section of the image which we want to focus our attention on. We do so by establishing hard coded points or vertices and draw a polygon(on a separate image) with these vertices. We combine the separate image and the original image to select points of interest.
5. With our focus on an a specified area of the image, we identify all lines in this section using the hough transform function. After getting a list of lines from the hough transform function, we feed the x1,y1,x2,y2 components into a for loop to identify left lane lines and right lane lines. If the slope of these points is above/below a threshold, and x2-x1 doesn't = 0, the points are appended to an left lane or right lane array. After all points of all lines found within the hough transform function are put into the right or left lane array, we calculate the average of these points. In turn, we calculate the average slope of these points. Finally, we draw a single line on the left and right using the average slope, hardcoded x point and calculated y value.


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


Potential shortcomings include:
1. Lanes fall outside our region of interest
2. Hardcoded x1,x2, value when drawing left and right lanes


### 3. Suggest possible improvements to your pipeline

possible improvement include:
1. Adjusting our region of interest so that the horizon is a horizontal line across the image
2. Dynamically calculating the x1,x2 values based on average values of the previous lines.

