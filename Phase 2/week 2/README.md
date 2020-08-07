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

Channel Shuffle
ShuffleNet Unit
ShuffleNet Architecture
Flops are not Reliable
MobileNet V2

ShuffleNet V2
Assignment
