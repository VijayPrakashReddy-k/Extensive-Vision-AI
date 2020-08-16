## 3 - Face Recognition Part I

**`Facial Landmarks, Alignment and Applications`**

### Session 3 : Face Detection and Detection Strategies

**week 3 contents:**
<ul>
 
<li>Detection Pipeline

![Facial-detection-pipeline](https://user-images.githubusercontent.com/42317258/89808415-b98ec280-db57-11ea-8c92-8043c22329af.jpg)

**`Transform :`** is to straightening the tilted image

[use cases](./CONTENT.md#usecases)

<li>Dlib
 
![dlib](https://user-images.githubusercontent.com/42317258/90091541-501fd700-dd44-11ea-8606-6c08d22d246a.png)

**`Dlib is an open-source Machine Learning library written in C++ with python binding. It is extremely portable and can be used on multiple platforms (including mobiles). Written by`** [Davis King](./Images/davis_king.jpg)

**DLib functionalities :**

      GUI
      Optimization
      Data Structures
      Machine Learning
            deep learning
            structured prediction
            regression
            clustering
      Text Parsing
      Linear Algebra
      Networking
      Image Processing
            image io
            object detection
            feature extraction
            filtering
 
 ![facial-landmark-detection](https://user-images.githubusercontent.com/42317258/90092380-6c247800-dd46-11ea-9572-5f004805c397.png)

- Here, will go step by step over the code for facial landmark detection on an image and save the results to disk.
            
 ![dlib-68points](https://user-images.githubusercontent.com/42317258/90091906-30d57980-dd45-11ea-908b-dc766557cbf4.png)
 
The image below shows all the landmarks and their corresponding indices in Dlib’s array. In many applications, we are concerned with using only a few facial landmarks. In those cases, the figure below can be used for quick reference. Here, we will show how to detect these points, plot them on a face image, and save them to file.

![68pointModel](https://user-images.githubusercontent.com/42317258/90092116-b6f1c000-dd45-11ea-8268-4e20a0133b15.jpg)

[Dlib's 68 points model](./Images/facial_landmarks_68markup.jpg)

<li> Facial landmark detection,one of the Facial Detection Pipeline usecase with Dlib
 
