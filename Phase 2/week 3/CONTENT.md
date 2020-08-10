<section id="usecases">
<h2>Use Cases of Facial detection</h2>
</section>

### 1. Landmark Detection:
- `There are two kinds of facial landmark detectors, that are provided by the Dlib are - new, faster, smaller 5-point facial landmark detector and the original 68-point facial landmark detector.`<br>

![5-68 points](https://user-images.githubusercontent.com/42317258/89811653-987ca080-db5c-11ea-818b-cbb51a4fa01f.png)

- `The 68-point detector localizes regions along the eyes, eyebrows, nose, mouth, and jawline, the 5-point facial landmark detector reduces this information to: 2 points for the left eye, 2 points for the right eye and 1 point for the nose`

[facial_landmarks_68markup](https://github.com/VijayPrakashReddy-k/Extensive-Vision-AI/blob/master/Phase%202/week%203/Images/facial_landmarks_68markup.jpg)
The 68 facial landmark coordinates from the iBUG 300-W dataset,which the dlib facial landmark predictor was trained on.

- `dlib’s 5-point facial landmark detector is 8-10% faster than the original 68-point facial landmark detector.A 8-10% speed up is significant; however, what’s more important here is the size of the model.The original 68-point facial landmark is nearly 100MB, weighing in at 99.7MB.The 5-point facial landmark detector is under 10MB, at only 9.2MB — this is over a 10x smaller model`

`The use case for the 5-point facial landmark detector is` **`face alignment`**, `and` **`face recognition`** `is for 68-point facial landmark detector`

**References:** - [5 and 68 points detector](https://www.pyimagesearch.com/2018/04/02/faster-facial-landmark-detector-with-dlib/) and [face alignment](https://www.pyimagesearch.com/2017/05/22/face-alignment-with-opencv-and-python/)
