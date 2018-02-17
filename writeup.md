# **Finding Lane Lines on the Road** 

## Writeup Template

---

**Finding Lane Lines on the Road**


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./debug/solidYellowCurve2_masked.png "croped gray scale"
[image3]: ./debug/solidYellowCurve_canny.png "canny edge applied"
[image4]: ./debug/solidYellowCurve_canny_enha.png "canny edge croped"
[image5]: ./debug/solidYellowCurve_hough.png "hough transform applied"
[image6]: ./test_images_output/solidYellowCurve.png "final output"

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps.
1. Make a copy if the input image for precessing the mask while keeping the original input for merging at the final step
2. Convert the image to gray scale and apply Gaussian blur to remove the noise
3. Mask the intrest zone the contains the lane lines first to apply later algorthins only there based on an input paramter(and measure if it saves time or not)
![alt text][image2]
4. apply the canny edge detection 
![alt text][image3]
5. whether or not step 3 was need remasking is required because the edges intrduced by step 3 would be identified as lines so a crop with 5 pixel offest less than the original area of intrest is applied to the output of step 4
![alt text][image4]
6. Hough transform applied with a modifiction to get all the lines and fit them using numpy function polyfit and draw two straight lines
![alt text][image5]

7. merge the generated image from the pipeline with the original to mark the lane lines
![alt text][image6]

### 2. Identify potential shortcomings with your current pipeline


1. Time optimization can be improved to get higher throughput specially for video
2. colours filtering was not used , need to be introduced for better accuracy on the cost of computation power
3. The "solidYellowLeft" video has an issue that in some frames the lines are not correct
update:
third issue was fixed by introducing a reject filter for lines from one side changing the slope for the oppsoite side
there was an idea of using a 3 point average filter by averaging the obtained sloped with 2 previous samples; could be used in the future perhaps with the challenge video


### 3. Suggest possible improvements to your pipeline

1. Time optimization
2. curvy lines to be handled 
3. fix an issue where the lines in same frame are not correctly displayed ( maybe paramters tweaking)
