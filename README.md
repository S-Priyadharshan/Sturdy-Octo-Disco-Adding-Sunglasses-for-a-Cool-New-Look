# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Code:

```python

import cv2
import numpy as np
import matplotlib.pyplot as plt

me = cv2.imread('me.jpg')
plt.imshow(me[:,:,::-1])
plt.title("Face")

glass = cv2.imread('glass.png',-1)
plt.imshow(glass[:,:,::-1])
plt.title("glass")

glass = cv2.resize(glass,(110,45))
print(glass.shape)

glassbgr = glass[:,:,0:3]
glassMask1 = glass[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121)
plt.imshow(glassbgr[:,:,::-1])
plt.subplot(121)
plt.imshow(glassMask1,cmap='grey')

glassFace = me.copy()
glassFace[100:145,72:182]=glassbgr
plt.imshow(glassFace[...,::-1])

glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
glassFacemath = me.copy()
eyeROI = glassFacemath[100:145,72:182]
maskedEye = cv2.multiply(eyeROI,(1-glassMask))
maskedGlass = cv2.multiply(glassbgr,glassMask)
eyeROIFinal = cv2.add(maskedEye,maskedGlass)

plt.figure(figsize=[20,20])
plt.subplot(131)
plt.imshow(maskedEye[...,::-1])
plt.title("Masked Eye Region")

plt.subplot(132)
plt.imshow(maskedGlass[...,::-1])
plt.title("Masked Coolers Region")

plt.subplot(133)
plt.imshow(eyeROIFinal[...,::-1])
plt.title("Augmented eye and glasses")

glassFacemath[100:145,72:182]=eyeROIFinal
plt.figure(figsize=[10,10])
plt.subplot(121)
plt.imshow(me[:,:,::-1])
plt.title("Original Me")

plt.subplot(122)
plt.imshow(glassFacemath[:,:,::-1])
plt.title("Cool Me")

```

## Output:
![image](https://github.com/user-attachments/assets/b13e88d7-3c37-40c6-8ef7-5283551f9081)

## Result:
My image has been made to look even more cooler successfully.

