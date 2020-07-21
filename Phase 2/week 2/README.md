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
      
### The advantages of SqueezeNet over Alexnet :
      
![squeezenet_alexnet_compare](https://user-images.githubusercontent.com/42317258/88101047-12071b80-cbbb-11ea-9930-4b3aa076a3d8.png)

  
<li>MobileNetV1
  
<li>Quantization
  
ShuffleNet
Channel Shuffle
ShuffleNet Unit
ShuffleNet Architecture
Flops are not Reliable
MobileNet V2
ShuffleNet V2
Assignment
