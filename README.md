# Image-Restoration
# 1. Introduction

This project aims to restore and enhance the quality of old photographs using advanced image processing techniques to breathe new life into deteriorated or faded images, preserving cherished memories. The project's benefits lie in the restoration and enhancement of old photographs and improving their quality to preserving memories.

# 2. Objective

The objective of this project is to develop a system that can automatically restore and enhance old photographs. The focus is on addressing common issues such as noise, scratches, color fading, blurriness, and other artifacts.

# 3. Methodology
![Image Restoration and enhancement Methodology 2](https://github.com/SidElias/Image-Restoration/assets/83931879/03646416-3598-4f7f-aa5f-de0f523afa49)


# 4. Code breakdown

1. Read and downsample the image:
The code reads an image file named "Test Image.png" using the "io.imread" function from the skimage library and downsamples it by a factor of 0.5 using the "cv2.resize" function from OpenCV.

The downscaled image is then displayed using matplotlib. 

<img width="300" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/2d892292-4278-4a1e-8fa6-693a35361881">

2. Convert the image into grayscale:

The "color.rgb2gray" function from skimage is used to convert the RGB image ("im1") into a grayscale image ("gray").

The grayscale image is displayed using matplotlib. 

<img width="300" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/44d7aa30-5ba8-4ffe-90dd-5ddcda144c7d">

3. Gradient Magnitude Calculation:
Two Sobel filters are defined ("sobel_x" and "sobel_y") for calculating horizontal and vertical gradients, respectively.

The horizontal gradient ("gx") is obtained by convolving the grayscale image with "sobel_x" using the "cv2.filter2D" function from OpenCV.
The vertical gradient ("gy") is obtained by convolving the grayscale image with "sobel_y" using the same "cv2.filter2D" function. 
The gradient magnitude ("mg") is calculated as the element-wise square root of the sum of squares of "gx" and "gy". 

The gradient magnitude image is displayed using matplotlib. 

<img width="300" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/51fe940d-fba1-4bec-8e79-171bfe758435">


4. Threshold the Gradient Magnitude:
The gradient magnitude image ("mg") is thresholded using the 17th percentile of its maximum value, which means that only edges with magnitudes higher than 17% of the maximum magnitude will be retained.

The thresholded binary image ("mgBw") is displayed using matplotlib. 

<img width="300" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/5a0bb7a3-0158-4113-a860-570febcd5178">


5. Apply Morphological Operation Closing:
A morphological closing operation is applied to the binary image ("mgBw") using a diskshaped structuring element of size 3x3. This operation helps to close small gaps and smooth the binary regions. 
The resulting binary image ("mgBw") after the morphological closing is displayed using matplotlib. 

<img width="300" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/1ac8b8bd-9ca0-41a3-a39e-1955c6552661">


6. Apply Connected Component Labeling (CCL) or Particle Analysis:
The "morphology.remove_small_objects" function from skimage is used to perform
connected component labeling (CCL) on the binary image ("mgBw"). 
All connected components (particles) smaller than the minimum size (500 pixels) areremoved, and the resulting binary image after CCL ("CCL") is displayed using matplotlib. 

 <img width="300" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/b0829406-7225-4b80-9320-19490890a6f8">

7. Prepare the mask for inpainting:
The "CCL" image obtained from the previous step is used as the mask for inpainting. 
The mask is resized to match the size of the original RGB image ("im1") by padding with zeros, resulting in "mask_resized."

8. Convert the image to RGB format:
The original downscaled image ("im1") is converted from BGR format (OpenCV default) to RGB format using "cv2.cvtColor."

9. Perform inpainting using TELEA and NS techniques:
Inpainting is performed using two different techniques: "cv2.INPAINT_TELEA" and
"cv2.INPAINT_NS."
The "cv2.inpaint" function from OpenCV is used to inpaint the image using the "mask_resized" as the binary mask and a specified inpainting radius of 5 pixels.
The inpainted images ("output1" and "output2") are displayed together with the original image and the mask using matplotlib.

10. Save the results:
The inpainted images obtained using the TELEA and NS techniques are saved as
"TELEA.jpg" and "NS.jpg," respectively, using "cv2.imwrite" function from OpenCV. 
 
 
# 5. Results
Image Restoration: 

<img width="500" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/154f1b40-e92b-41b2-ade8-80393cf60321">


Noise Reduction:

<img width="500" alt="image" src="https://github.com/SidElias/Image-Restoration/assets/83931879/22988964-d3c8-469c-9ec9-e64f538b3704">
