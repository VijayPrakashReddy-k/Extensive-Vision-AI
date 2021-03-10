## 5. Human Pose Estimation, State of Art HPE and Human Localization

### Session 5 - Monocular Human Pose Estimation And ONNX Models

**week 5 contents:**

- [Human Pose Estimation](./README.md/#HPE)

- [Key problems in Pose estimation](./README.md/#problems)

- [HPE Method Categories](./README.md/#methods)

            1. Generative vs Discriminative
            
            2. Top-down vs Bottom-up
            
            3. Regression vs Detection
            
            4. One-stage vs Multi-stage
            
- [Human Pose Models](./README.md/#models)
- [HPE Benchmarks and Datasets](./README.md/#datasets)
- [HPE Evaluation Metrics](./README.md/#metrics)
- [Most important models](./README.md/#work):

            1. OpenPose
            
            2. A simple yet effective baseline
            
            3. DensePose
            
            4. Simple baseline for HPE and tracking
            
- [Open Neural network Exchange (ONNX)](./README.md/#onnx)

[Awesome HPE Reference](https://github.com/wangzheallen/awesome-human-pose-estimation)

<h1 align = 'center',id = "HPE">Human Pose Estimation</h1>

- `Human pose estimation is the process of estimating the configuration of the body (pose) from a single, typically monocular, image.`
- `It represents the orientation of a person in a graphical format. Essentially, it is a set of coordinates that can be connected to describe the pose of the person. Each co-ordinate in the skeleton is known as a` ***part (or a joint, or a keypoint).*** `A valid connection between two parts is known as` ***a pair (or a limb).***

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/91109601-1c747380-e699-11ea-98ea-f27226353d01.gif" />
</p>

[Applications](./CONTENT.md/#applications)

<p id = 'problems'>
            <img src = "https://user-images.githubusercontent.com/42317258/91117076-69614580-e6ab-11ea-878a-7ec31433b1bd.png" />
</p>

- `Human pose estimation is one of the key problems in computer vision that has been studied for well over 15 years. The reason for its importance is the abundance of applications that can benefit from such technology.`

- For example, human pose estimation allows for higher-level reasoning in the context of human-computer interaction and activity recognition; it is also one of the basic building blocks for **marker-less motion capture (MoCap) technology.**

- Motion capture implies *recording the movement of head and body but no facial or finger data*, whereas Performance Capture includes hands, fingers and face.MoCap technology is useful for applications ranging from character animation to clinical analysis of gait pathologies.

Despite many years of research, however, pose estimation remains a very difficult and still largely unsolved problem.[Here, are the most significant challenges](./CONTENT.md/#challenges)

<p id = 'methods'>
            <img src = "https://user-images.githubusercontent.com/42317258/91124284-979b5100-e6bc-11ea-8d73-4b0500bd731d.png" />
</p>

## i. Generative and Discriminative (3D Single Person)

            Generative - human body model-based
            
            Discriminative - human body model-free
            
**`The main difference between generative and discriminative methods is whether a method uses human body models or not`**.

- Based on the different representations of human body models, **generative methods can be processed in different ways such as prior beliefs about the structure of the body model, geometrically projection from different views to 2D or 3D space, high-dimensional parametric space optimization in regression manners.**

- **Discriminative methods directly learn a mapping from input sources to human pose space (learning-based) or search in existing examples (example-based) without using human body models. Discriminative methods are usually faster than generative methods but may have less robustness for poses never trained with.**
            
## ii. Top-down and Bottom-up (Multi-Person)

            Top-down - from high-level abstraction to low-level pixel evidence

            Bottom-up - from low-level pixel evidence to high-level abstraction
            
`The bottom-up approach first finds the keypoints and then maps them to different people in the image, while the top-down approach first uses a mechanism to detect people in an image, put a bounding box area around each person instance and then estimate keypoint configurations within the bounding boxes.`
            
- **For multi-person pose estimation, HPE methods can generally be classified as top-down and bottom-up methods according to the starting point of the prediction: high-level abstraction or low-level pixel evidence. Topdown methods start from high-level abstraction to first detect persons and generate the person locations in bounding boxes. Then pose estimation is conducted for each person.**

- **In contrast, bottom-up methods first predict all body parts of every person in the input image and then group them either by human body model fitting or other algorithms. Note that body parts could be joints, limbs, or small template patches depending on different methods. With an increased number of people in an image, the computation cost of top-down methods significantly increases, while keeps stable for bottom-up methods. However, if there are some people with a large overlap, bottom-up methods face challenges to group corresponding body parts.**

## iii. Regression and Detection based (Single Person)

            Regression - directly mapping from input images to body joint points

            Detection - generating intermediate image patches or heatmaps of join-locations
            
- **Based on the different problem formulations, deep learning-based human pose estimation methods can be split into regression-based or detection-based methods. The regression-based methods directly map the input image to the coordinates of body joints or the parameters of human body models. The detection-based methods treat the body parts as detection targets based on two widely used representations: image patches and heatmaps of joint locations.**

- **Direct mapping from images to joint coordinates is very difficult since it is a highly nonlinear problem, while small-region representation provides dense pixel information with stronger robustness.  Compared to the original image size, the detected results of small-region representation limit the accuracy of the final joint coordinates.**

## iv. One-stage and Multi-stage:

            One-stage : end-to-end training

            Multi-stage : stage-by-stage training
            
- **The deep learning-based one-stage methods aim to map the input image to human poses by employing end-to-end networks, while multi-stage methods usually predict human pose in multiple stages and are accompanied by intermediate supervision. For example, some multiperson pose estimation methods first detect the locations of people and then estimate the human pose for each detected person.**

- **Other 3D human pose estimation methods first predict joint locations in the 2D surface, then extend them to 3D space. The training of one-stage methods is easier than multi-stage methods, but with less intermediate constraints.**

<p id="models", align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108172879-63f92b00-7123-11eb-9a52-2839fc054308.png" />
</p>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108173153-c81bef00-7123-11eb-8146-75bba259817d.jpg" />
</p>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108175040-411c4600-7126-11eb-88cc-cfede995f5b5.png" />
</p>

<p id="datasets", align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108174176-20072580-7125-11eb-8820-c743d84084a3.png" />
</p>

<h2 align = 'center'>Summary of 2D Single person HPE</h2>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108174496-84c28000-7125-11eb-8ca3-83115dcb05ca.png" />          
</p>

<h2 align = 'center'>Summary of 2D Multi person HPE</h2>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108174490-83915300-7125-11eb-8913-6ce02748fcb8.png" />
</p>

<h2 align = 'center'>Datasets</h2>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108175495-d9b2c600-7126-11eb-9fdd-cd527483e966.jpg" />
</p>

<p id="metrics", align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108187028-0f11e080-7134-11eb-9857-e2ae77bb035a.png" />
</p>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108187057-15a05800-7134-11eb-9810-4e0640914166.png" />
</p>

            OKS = Object Keypoint Similarity

            PCK = Percentage of Correct Keypoint

            PCKh = The PCKh performance metric is the percentage of joints with predicted locations that are no further than half of the head segment length from the ground truth.
            
<p id="work", align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/108200411-733ca080-7144-11eb-81d4-dd19206cda10.png" />
</p>      

[1.OpenPose](./CONTENT.md/#openpose)

[2.A simple yet effective baseline](./CONTENT.md/#baseline)

[3.DensePose](./CONTENT.md/#densepose)

[4.Simple baseline for HPE and Tracking](./CONTENT.md/#baseline-tracking)

<p id="onnx">
            <img src = "https://user-images.githubusercontent.com/42317258/91028889-b8f83080-e61b-11ea-983b-825f88b0a10e.png" />
</p>

| - ***`The Open Neural Network Exchange (ONNX) is an open standard for representing machine learning models. The biggest advantage of ONNX is that it allows interoperability across different open source AI frameworks, which itself offers more flexibility for AI frameworks adoption.`*** | ![download](https://user-images.githubusercontent.com/42317258/91035264-f2349e80-e623-11ea-9e6b-307262455967.png) |

-  ONNX defines a common set of operators - the building blocks of machine learning and deep learning models - and a common file format to enable AI developers to use models with a variety of frameworks, tools, runtimes, and compilers.

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/91035221-e47f1900-e623-11ea-8447-3e6e4cbd426e.png" />
</p>

- With ONNX, AI developers can more easily move models between state-of-the-art tools and choose the combination that is best for them. ONNX is developed and supported by a community of partners such as **Microsoft, Facebook and AWS.**

![ONNX](https://user-images.githubusercontent.com/42317258/91035278-f660bc00-e623-11ea-866a-5eac59d00aa3.png)

- Apart from bringing interoperability across deep learning frameworks, ONNX promises optimized execution of neural network graph depending on the availability of hardware. *The ONNX Runtime abstracts various hardware architectures such as AMD64 CPU, ARM64 CPU, GPU, FPGA, and VPU.*

- `ONNX Runtime is a performance-focused engine for ONNX models,which inferences efficiently across multiple platforms and hardware (Windows, Linux, and Mac and on both CPUs and GPUs).ONNX Runtime has proved to considerably increase performance over multiple models.`

![onnx-runtime](https://user-images.githubusercontent.com/42317258/91034458-a7665700-e622-11ea-90f8-dc104df2d208.jpg)

![deploy](https://user-images.githubusercontent.com/42317258/108237733-34bbdb80-716e-11eb-9ad7-6feea26d61bf.png)

![frameworks-1](https://user-images.githubusercontent.com/42317258/108237762-38e7f900-716e-11eb-963c-2ee7d691879c.png)

### Practice ONNX:

- [PyTorch YoloV4 ONNX](https://github.com/Tianxiaomo/pytorch-YOLOv4)

- [AlexNet to ONNX](https://michhar.github.io/convert-pytorch-onnx/)

- [ResNet to ONNX](https://colab.research.google.com/github/bentoml/gallery/blob/master/onnx/resnet50/resnet50.ipynb)

- [SuperResolution to ONNX](https://pytorch.org/tutorials/advanced/super_resolution_with_onnxruntime.html)

[ONNX.js](https://microsoft.github.io/onnxjs-demo/#/)

![HPE-assignment](https://user-images.githubusercontent.com/42317258/108237213-aa737780-716d-11eb-8eaf-555bc1979335.png)

[Simple Baseline for HPE and tracking](https://arxiv.org/pdf/1804.06208.pdf)

[paper](https://github.com/Microsoft/human-pose-estimation.pytorch)

[models](https://onedrive.live.com/?authkey=%21AFkTgCsr3CT9%2D%5FA&id=56B9F9C97F261712%2110709&cid=56B9F9C97F261712)
