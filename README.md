# Road-Lane-Detection--Opencv

## Introduction
When we drive, we use our eyes to decide where to go. The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle. Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

## Approach
   - The first step to working with our images will be to convert them to grayscale. This is a critical step to using the Canny Edge Detector inside of OpenCV. I’ll talk more about what canny() does in a minute, but right now it’s important to realize that we are collapsing 3 channels of pixel value (Red, Green, and Blue) into a single channel with a pixel value range of [0,255]. gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
   - Before we can detect our edges, we need to make it clear exactly what we’re looking for. Lane lines are always yellow and white. Yellow can be a tricky color to isolate in RGB space, so lets convert instead to Hue Value Saturation or HSV color space. You can find a target range for yellow values by a Google search. The ones I used are below. Next, we will apply a mask to the original RGB image to return the pixels we’re interested in.
   - We are almost to the good stuff! We’ve certainly processed quite a bit since our original image, but the magic has yet to happen. Let’s apply a quick Gaussian blur. This filter will help to suppress noise in our Canny Edge Detection by averaging out the pixel values in a neighborhood.
   
### Canny Edge Detection
We’re ready! Let’s compute our Canny Edge Detection. A quick refresher on your calculus will really help to understand exactly what’s going on here! Basically, canny() parses the pixel values according to their directional derivative (i.e. gradient). What’s left over are the edges — or where there is a steep derivative in at least one direction. We will need to supply thresholds for canny() as it computes the gradient. John Canny himself recommended a low to high threshold ratio of 1:2 or 1:3.
