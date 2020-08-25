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
- Most important models:

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

![key-problems](https://user-images.githubusercontent.com/42317258/91117076-69614580-e6ab-11ea-878a-7ec31433b1bd.png)

- `Human pose estimation is one of the key problems in computer vision that has been studied for well over 15 years. The reason for its importance is the abundance of applications that can benefit from such technology.`

- For example, human pose estimation allows for higher-level reasoning in the context of human-computer interaction and activity recognition; it is also one of the basic building blocks for *`marker-less motion capture (MoCap) technology`.*

- Motion capture implies *recording the movement of head and body but no facial or finger data*, whereas Performance Capture includes hands, fingers and face.MoCap technology is useful for applications ranging from character animation to clinical analysis of gait pathologies.

Despite many years of research, however, pose estimation remains a very difficult and still largely unsolved problem.[Here, are the most significant challenges](./CONTENT.md/#challenges)

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
