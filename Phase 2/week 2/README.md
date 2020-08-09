### 2.MobileNet & Other Edge DNNs:

   *`Training a DNN for EDGE Deployment from scratch. Understanding MobileNets and ShuffleNets.`*

**Session 2 - EMBEDDED DEVICES** <br>

**`Week 2 Contents:`**
<ul>
<li>Cloud vs Mobile Neural Nets
  
  ![Cloud vs Mobile NN](https://user-images.githubusercontent.com/42317258/87967718-e150b480-cadc-11ea-8ab8-a1c81906b91d.png)


<li>Simple Old Tricks
  
  ![old trics](https://user-images.githubusercontent.com/42317258/87968141-94b9a900-cadd-11ea-87a1-13dbfe61fefa.png)

  
<li>SqueezeNet
  
  ![squeezenet](https://user-images.githubusercontent.com/42317258/87968590-4a84f780-cade-11ea-9baf-b8c3353fbe94.png)

**The main ideas of SqueezeNet are:**

      Using 1x1(point-wise) filters to replace 3x3 filters, as the former only 1/9 of computation.
      
      Using 1x1 filters as a bottleneck layer to reduce depth to reduce computation of the following 3x3 filters.
      
      Downsample late to keep a big feature map.
      
[more about squeezenet](./CONTENT.md#squeeze_nets)
      
### The advantages of SqueezeNet over Alexnet :
      
![squeezenet_alexnet_compare](https://user-images.githubusercontent.com/42317258/88101047-12071b80-cbbb-11ea-9930-4b3aa076a3d8.png)

  
<li> MobileNetV1 <br>

[Paper](https://github.com/VijayPrakashReddy-k/Extensive-Vision-AI/files/5017307/MobileNets.Efficient.Convolutional.Neural.Networks.for.Mobile.Vision.pdf)

- A class of efficient models for mobile and embedded vision applications
- Based on depth-wise separable convolutions
 

*`Author: For MobileNets the depthwise convolution applies a single filter to each input channel. The pointwise convolution then applies a 1×1 convolution to combine the outputs of the depthwise convolution. A standard convolution both filters and combines inputs into a new set of outputs in one step. The depthwise separable convolution splits this into two layers, a separate layer for filtering and a separate layer for combining. This factorization has the effect of drastically reducing computation and model size.`* 

                                   Normal Convolution
                                   
![Normal](https://user-images.githubusercontent.com/42317258/89209152-60fd7980-d5db-11ea-991f-45e7b662f08d.gif)

                                   Depthwise Separable Convolution

![depthwise_convs](https://user-images.githubusercontent.com/42317258/89256757-75289180-d642-11ea-8be3-116d696fe7d9.gif)

[mobilenet v1 architecture](./CONTENT.md#mobilenet_v1)

<li>Quantization <br>
  
*As we want more and more accurate predication, and as networks grows deeper and deeper, the memory size of network becomes a problem, especially on mobile devices. Typically, mobile phones are equipped with 4GB memory (as of early 2019), which is expected to be able to support multiple applications at one time. Models of large size make phones short of memory since they may take 1GB memory away if three or more models at one time which is usually the case.*

*The model size is not only a memory usage problem, it’s also a memory bandwidth problem. Weights of model is walked every time for each predication, and image related applications usually need to process data in real time, which means at least 30 FPS (Frame per Second). So, if deploying ResNet-50 to classify objects, which is relatively small, 3GB/s memory bandwidth is required for the model regardless other media processing.*

**`Memory, CPU and battery burn the device when network is runing. We cannot afford such a expensive effort to get a device a bit smarter.`**

##### So,to optimize the scheme of deep learning things, Researches basically lie in two aspects:

- *`Designing more effecient network architecture which maintains reasonable accuracy with relative smaller model size. MobileNet and SequeezeNet are such attempts.`*

![model-sizes](https://user-images.githubusercontent.com/42317258/89674545-f82d3e80-d905-11ea-8e93-f37bc927a459.png)

- *`Reducing network size by means of compression, encoding and so on. Quantization is one of the most widely adopted compression methods.`*

***`Quantization itself, conceptly, converts floating-point arithmetic of neural networks into fixed-point, and makes real time inference possible on mobile phones as well as benefits cloud applications.`***

![quntization-concept](https://user-images.githubusercontent.com/42317258/89675203-2cedc580-d907-11ea-9aa6-6c0b037a71a3.png)

    The quantized MobileNetV1 of TensorFlow is only 4.8MB, such models can be easily deployed on any mobile platforms.
    
[deep-dive-quantization](./CONTENT.md#quantization)
 
<li> ShuffleNet <br>

[Paper](https://github.com/VijayPrakashReddy-k/Extensive-Vision-AI/files/5017309/ShuffleNet.An.Extremely.Efficient.Convolutional.Neural.Network.for.Mobile.pdf)

`Megvii Inc (a.k.a Face++) introduces an extremely computation-efficient CNN architecture named ShuffleNet, which is designed especially for mobile devices with very limited computing power (e.g. 10-150 MFLOPs).` <br>

Most focus on **pruning, compressing, or low-bit representation.** <br>

The ShuffleNet utilizes **pointwise group convolution** *(Pointwise convolution actually is the 1×1 convolution to change the dimension)* and **channel shuffle** to reduce computation cost while maintaining accuracy.

Experiments on *ImageNet classification* and *MS COCO object detection* demonstrate the superior performance of ShuffleNet over other structures, *e.g. lower top-1 error (absolute 7.8%) than MobileNet on ImageNet classification task, under 40MFLOPs. ShuffleNet is 13x faster than AlexNet while maintaining comparable accuracy.*

Xception and ResNeXt architectures are awesome but become less efficient in extremely small networks because of the costly dense (1x1) convolutions. **They proposed using pointwise group convolutions to reduce the computation complexity of 1x1 convolutions.**

- For each residual unit in ResNeXt, the pointwise convolutions occupy 93.4% multiplication-adds (cardinality 32). 

***Problem : Expensive pointwise group convolutions result in limited number of channels to meet the complexity constraint, which might significantly damage accuracy.***
 
***Solution :*** *`To overcome the side effects brought by group convolutions, they come up with a novel `* **channel shuffle operation** *`to help the information flowing across feature channels.`*
 
- Hence, ShuffleNet allows more feature map channels, which helps to encode more information and is especially critical to the performance of very small networks. 

In the below figure, the group convolutions are given as examples to demonstrate its capability in reducing computation cost.

![channel-shuffle](https://user-images.githubusercontent.com/42317258/89733332-65f67900-da72-11ea-936b-9d8705fbdc98.png)

*Figure 1(a) illustrates a situation of two stacked group convolution layers, which has twofold properties, blocking the information flow between channel groups and weakening representations.*

*Figure 1(b) shows that the group convolution is allowed to obtain input data from different groups. Notice that the input channels are fully related to the output ones.*

*Figure 1(c) sets up the feature map from the previous group layer, which is then implemented by a channel shuffle operation. Channel shuffle operation is able to construct more powerful structures with multiple group convolutional layers.*

**But there is a drawback, output from a certain channel is only derived from a small fraction of input channels. How do we fix this problem?**

If we allow group convolutions to obtain input data from different groups (b), the input and output channels will be fully related. Specifically, for the feature map generated from the previous group layer, we can first divide the channels in each group into several subgroups, then feed each group in the next layer with different groups. This can be efficiently and elegantly implemented by a channel shuffle operation. 

- *`Suppose a convolutional layer with g groups whose output has g×n channels; we first reshape the output channel dimension into (g, n), transposing, and then flattening it back as the input of the next layer.`*

[Visualize Channel Shuffle](./CONTENT.md#channel-shuffle)

- [ShuffleNet Unit](./CONTENT.md#shufflenet-unit) is designed for small networks.

- [ShuffleNet Architecture](./CONTENT.md#shufflenet-architecture) is a stack of ShuffleNet units grouped into three stages.

- [comparison](./CONTENT.md#comparison) between channel shuffle and No shuffle.

- [model comparison](./CONTENT.md#model-comparison) between ShuffleNet vs MobileNet on ImageNet classification

<li>Flops are not Reliable <br>
  
*`To measure the computation complexity, a widely used metric is the number of float-point operations or FLOPS. However, FLOPs are an indirect metric. It is an approximation of, but usually not equivalent to the direct metric that we rarely care about, such as the speed of latency. Such discrepancy has been noticed in many networks.`*

For example, MobileNet V2 is must faster than NASNET, but they have comparable FLOPs. 

![graphs](https://user-images.githubusercontent.com/42317258/89735573-25522c00-da81-11ea-980e-66a2a72d5895.png)

 Measurement of accuracy (ImageNet classification on validation set), speed, and FLOPs of four network architectures on two hardware platforms with four different levels of computation complexities (see text for details). (a, c) GPU results, batch size = 8. (b, d) ARM results, batch size = 1. The best performing algorithm, our proposed ShuffleNet v2, is on the top right region, under all cases.
 
 **There are three reasons for this discrepancy:** <br>

- *First, several important factors that have a considerable effect on speed are not taken into account by FLOPs. One such factor is memory access cost (MAC). Such cost constitutes a large portion of run time in certain operations like group convolutions. It could be a bottleneck on devices with strong computation power (like GPUs).* <br>
- *Another one is the degree of parallelism. A model with a high degree of parallelism could be much faster than another one with low.*<br>
- *Finally, operations with the same FLOPs could have different running times, depending on the platform.*

![pie-graph](https://user-images.githubusercontent.com/42317258/89735575-27b48600-da81-11ea-82d6-6287a8169243.png)

***With these observations, we propose that two principles should be considered for effective network architecture design.*** <br>

- First, the direct metric (e.g., speed) should be used instead of the indirect ones (e.g., FLOPs). <br>
- Second, such metrics should be evaluated on the target platform. In this work, we follow the two principles and propose a more effective network architecture.

<li> MobileNet V2
  
`MobileNetV2 builds upon the ideas from MobileNetV1, using depthwise separable convolution as efficient building blocks. However, V2 introduces two new features to the architecture:`

- `1) linear bottlenecks between the layers, and` <br>
- `2) shortcut connections between the bottlenecks

![mobilenetv2-architecture](https://user-images.githubusercontent.com/42317258/89737158-79164280-da8c-11ea-8572-efdae8b0bb70.png)

`Overview of MobileNetV2 Architecture. Blue blocks represent composite convolutional building blocks as shown above.`

The intuition is that the bottlenecks encode the model’s intermediate inputs and outputs while the inner layer encapsulates the model’s ability to transform from lower-level concepts such as pixels to higher level descriptors such as image categories. Finally, as with traditional residual connections, shortcuts enable faster training and better accuracy.

[Inverted Residuals](./CONTENT.md#inverted-residuals) enables faster training and better accuracy,[Linear Bottlenecks](./CONTENT.md#bottlenecks) encodes models intermediate inputs and outputs, Smaller Memory Footprint. Mobilenet V2 is Faster,Smaller and Uses [ReLU6](./CONTENT.md#relu6).`
 
 

ShuffleNet V2

Assignment
