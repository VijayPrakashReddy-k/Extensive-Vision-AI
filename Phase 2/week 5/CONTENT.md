<h1 align = 'center', id = 'applications'>
HPE Applications
</h1>

`It can be applied to many applications such as`

<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/91115931-e7701d00-e6a8-11ea-98e8-8d993ed41c69.jpg />
</p>

- **Action/Activity Recognition:**
<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/91112452-cdcad780-e6a0-11ea-9981-f791e16a1055.png />
</p>

[Open source Projects](https://awesomeopensource.com/projects/activity-recognition)

- **Action Detection:**

<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/91112898-e8518080-e6a1-11ea-8c3f-fd4126521511.png />
</p>

- **Human tracking in Movies and Animation:**

<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/91113396-1daa9e00-e6a3-11ea-934a-90ec5dacdfa0.jpg />
</p>

- **Human-Computer Interaction (HCI):**
 
<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/91115442-d70b7280-e6a7-11ea-8a36-c8934a11e53c.gif />
</p>

- **Video Surveillance, Medical assistance, Self-driving, Sports motion analysis, etc.**

<p align = 'center' id = 'challenges'>
      <img src = https://user-images.githubusercontent.com/42317258/91117076-69614580-e6ab-11ea-878a-7ec31433b1bd.png />
</p>

**Among the most significant challenges are:**

      (1) variability of human visual appearance in images,

      (2) variability in lighting conditions,

      (3) variability in the human physique,

      (4) partial occlusions due to self-articulation and layering of objects in the scene,

      (5) the complexity of human skeletal structure,

      (6) the high dimensionality of the pose, and

      (7) the loss of 3d information that results from observing the pose from 2d planar image projections
      
<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/91123587-de884700-e6ba-11ea-8646-db8281708fc9.jpg />
</p>

<p align = 'center' id = 'openpose'>
      <img src = https://user-images.githubusercontent.com/42317258/108200411-733ca080-7144-11eb-81d4-dd19206cda10.png />
</p>

![openpose](https://user-images.githubusercontent.com/42317258/108203452-89e4f680-7148-11eb-9435-c6366b6a198f.png)

- `OpenPose is the most popular open-source tool for body, foot, hand, and facial keypoint detection. It makes use of Part Affinity Fields (PAFs), a set of 2D vector fields to encode the location and orientation of limbs over the image domain.`

<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/108203898-1b546880-7149-11eb-899d-b28ab8e0f4d0.png />
</p>

As shown in the image F is passed through several convolutional layers to generate the PAFs (L) and confidence maps S for every joint location. The process is repeated for some iterations and the network refines its predictions at every stage. OpenPose is widely used in research projects. 

<p align = 'center'>
      <img src = https://user-images.githubusercontent.com/42317258/108204104-5fe00400-7149-11eb-8cc1-83493ab23992.png />
</p>

[OpenPose Paper](papers/OpenPose.pdf)

<p id = 'baseline'>
      <img src = https://user-images.githubusercontent.com/42317258/108232370-b6106f80-7168-11eb-9599-3476d6b2438f.png />
</p>

- `In this work, the authors implemented a lightweight and fast network able to process 300 frames per second. After extracting 2d joint location, due to the low dimensionality of 2d space, they use a simple neural network that has a small number of parameters, to estimate the coordinates of joints in 3d space.`

![3d-pose-estimation](https://user-images.githubusercontent.com/42317258/108232564-ebb55880-7168-11eb-80fa-331c6b2f744e.png)

[Effective-Baseline Paper](papers/Effective-Baseline.pdf)

<p id = 'densepose'>
      <img src = https://user-images.githubusercontent.com/42317258/108232393-bd377d80-7168-11eb-9019-2d723a792656.png />
</p>

- `DensePose adopts the architecture of MaskRCNN with the feature pyramid network features, and ROI-Align pooling so as to obtain dense part labels and coordinates with each of the selected regions. The method uses a fully convolutional network on top of ROI-pooling that is entirely devoted to generating per-pixel classification results for selection of surface part and regressing local coordinates within each part.`

![densepose](https://user-images.githubusercontent.com/42317258/108232577-f07a0c80-7168-11eb-9ef0-7131f3e1b8b4.png)

[DensePose Link](http://densepose.org/)

<p id = 'baseline-tracking'>
      <img src = https://user-images.githubusercontent.com/42317258/108232385-bb6dba00-7168-11eb-9cb8-e55e9c4ccf93.png />
</p>

![simple_pose](https://user-images.githubusercontent.com/42317258/108232614-fb34a180-7168-11eb-9ef7-9d7040db574a.png)

As other approaches have become complex,this work aimed to ease the problem by asking a question,**"how good could a simple method be?"**

- `This approach involves a few deconvolutional layers added on a backbone network, ResNet.This approach adds a few deconvolutional layers over the last convolution stage in the ResNet, called C5.`

- `By default, 3 Deconv layers with BN and ReLU as used.Each layer has 256 filters with 4x4 kernels.The stride is 2.`

- `A 1x1 convolutional layer is added at the last to generate predicted heatmaps for all k key points.MSE is used as the loss function.`

- `The targeted heatmap for join k is generated by applying a 2D gaussian centered on the kth joint's ground truth location.`

![simple_pose_bench](https://user-images.githubusercontent.com/42317258/108232620-fcfe6500-7168-11eb-97b3-75ff36011c80.png)

[Simple baseline for HPE and Tracking-paper](papers/Baseline-Tracking.pdf)
