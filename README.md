# Image Alignment and Panorama using OpenCV

This project demonstrates how to align images and create panoramic views using **OpenCV**.  
It combines two powerful computer vision techniques — **Image Alignment (Homography estimation)** and **Automatic Panorama Stitching** — to produce seamless wide-angle or rectified image results.

---

## Overview

In many real-world applications such as document scanning, aerial mapping, or landscape photography, it’s often necessary to align multiple images or merge them into one unified view.  
This project shows how to:

- Align images of the same scene using **feature matching** and **homography**.
- Automatically stitch multiple overlapping images into a seamless panorama using **OpenCV’s Stitcher API**.
- Understand the role of **keypoints**, **descriptors**, **feature matching**, and **RANSAC** in geometric transformations.

---

## Project Workflow

### Image Alignment

Image alignment ensures that two images of the same scene (for example, a scanned form and its original template) match perfectly by estimating a **homography matrix** between them.

#### Steps:
1. **Load Template and Scanned Image**  
   Convert both to grayscale for feature detection.

2. **Detect ORB Keypoints**  
   Identify stable corner-like features using the **ORB (Oriented FAST and Rotated BRIEF)** algorithm.

3. **Match Features**  
   Use the **BruteForce-Hamming matcher** to find corresponding features between both images.

4. **Estimate Homography**  
   Compute a 3×3 transformation matrix using **RANSAC** to eliminate outliers and get accurate alignment.

5. **Warp Image**  
   Apply the computed homography to align one image with the other using `cv2.warpPerspective()`.

---

### Panorama Stitching

Panorama stitching combines multiple overlapping images into a single continuous, wide-angle view.

#### Steps:
1. **Read Input Images**  
   Load all images in sequence and convert them to RGB format.

2. **Feature Detection and Matching**  
   Automatically detect keypoints and establish correspondences across adjacent images.

3. **Estimate Pairwise Homographies**  
   Compute transformations between overlapping image pairs.

4. **Blend and Stitch Images**  
   Use **OpenCV’s Stitcher class** to blend and merge all images seamlessly.

#### Core Code Example:
```python
stitcher = cv2.Stitcher_create()
status, result = stitcher.stitch(images)

if status == 0:
    plt.imshow(result)
    plt.axis("off")
    plt.title("Panorama Result")
    plt.show()

```
## Algorithms Used

1. ORB (Oriented FAST and Rotated BRIEF) — for keypoint detection and feature description

2. Brute-Force Hamming Matcher — for binary descriptor matching

3. RANSAC (Random Sample Consensus) — for robust homography estimation

4. OpenCV Stitcher API — for automatic panorama generation

## Results
### Before Stitching
<img width="2186" height="790" alt="download" src="https://github.com/user-attachments/assets/77547ed7-1f39-42f7-bb1c-1d1e73d51224" />

### After Stitching
<img width="2381" height="626" alt="download" src="https://github.com/user-attachments/assets/cc8506e3-c286-444a-abb0-63dfbb777dee" />

## Acknowledgment

This project is inspired by LearnOpenCV tutorials and OpenCV Bootcamp lessons.
It is intended purely for educational purposes to help beginners understand feature-based image alignment and panorama creation.

# If you found this project helpful, don’t forget to star the repo!
