# cannyedgedetection
canny edge detection algorithm
 
Phase 1: Compute smoothed gradients: 
 
a) Load an image, convert it to float format, and extract its luminance as a 2D array. Alternatively, you may also convert the input image from color to gray-scale if required. 
 
b) Find the x and y components Fx and Fy of the image gradient after smoothing with a Gaussian (for the Gaussian, you can use σ = 1). There are two ways to go about doing this: either (A) smooth with a Gaussian using a convolution, followed by computation of the gradient; or (B) convolve with the x and y derivatives of the Gaussian. 
 
c) At each pixel, compute the edge strength F (gradient magnitude), and the edge orientation D = atan(Fy/Fx). Include the gradient magnitude and direction images in your report.  
 
Phase 2: Non-maximal Suppression 
 
Create a "thinned edge image" I[y, x] as follows: 
 
a) For each pixel, find the direction D* in (0, π/4, π/2, 3π/4) that is closest to the orientation D at that pixel. 
 
b) If the edge strength F[y, x] is smaller than at least one of its neighbors along the direction D*, set I[y, x] to zero, otherwise, set I[y, x] to F[y, x]. Note: Make a copy of the edge strength array before thinning, and perform comparisons on the copy, so that you are not writing to the same array that you are making comparisons on. 

 
After thinning, your "thinned edge image" should not have thick edges any more (so edges should not be more than 1 pixel wide). Include the thinned edge output in your report. 
 
Phase 3: Hysteresis thresholding:  
 
a) Assume two thresholds: T_low, and T_high (they can be manually set or determined automatically). 
 
b) Mark pixels as "definitely not edge" if less than T_low. 
 
c) Mark pixels as "strong edge" if greater than T_high. 
 
d) Mark pixels as "weak edge" if within [T_low, T_high]. 
 
e) Strong pixels are definitely part of the edge. Whether weak pixels should be included needs to be examined. 
 
f) Only include weak pixels that are connected in a chain to a strong pixel. How to do this?  
 
Visit pixels in chains starting from the strong pixels. For each strong pixel, recursively visit the weak pixels that are in the 8 connected neighborhood around the strong pixel, and label those also as strong (and as edge). Label as "not edge" any weak pixels that are not visited by this process. Hint: This is really a connected components algorithm, which can be solved by depth first search. Make sure to not revisit pixels when performing your depth first search! 
