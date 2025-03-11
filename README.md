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
import cv2
import numpy as np
import matplotlib.pyplot as plt

me = cv2.imread('facepic.png')
glass = cv2.imread('sunglass.png', cv2.IMREAD_UNCHANGED)

left_eye = (62, 64)
right_eye = (93, 65)

eye_width = right_eye[0] - left_eye[0] + 40
eye_height = int(eye_width * (glass.shape[0] / glass.shape[1]))

glass = cv2.resize(glass, (eye_width, eye_height), interpolation=cv2.INTER_AREA)

glassBGR = glass[:, :, 0:3]
glassMask = glass[:, :, 3]

glassMask = cv2.merge((glassMask, glassMask, glassMask)) / 255

x_offset = left_eye[0] - 20
y_offset = left_eye[1] - int(eye_height / 2)

roi = me[y_offset:y_offset + eye_height, x_offset:x_offset + eye_width]

if roi.shape[:2] == glassBGR.shape[:2]:
    maskedFace = roi * (1 - glassMask)
    maskedGlasses = glassBGR * glassMask
    roiFinal = np.uint8(maskedFace + maskedGlasses)
    me[y_offset:y_offset + eye_height, x_offset:x_offset + eye_width] = roiFinal

display_size = (150, 175)
me_small = cv2.resize(me, display_size, interpolation=cv2.INTER_AREA)

plt.figure(figsize=(5, 5))
plt.imshow(me_small[:, :, ::-1])
plt.title("Face with Sunglasses")
plt.show()

## Output:

![image](https://github.com/user-attachments/assets/05229718-f7ce-4612-bf0f-74cfb4fde768)

![image](https://github.com/user-attachments/assets/42fcb259-9227-448a-8599-6571642dc4a5)


