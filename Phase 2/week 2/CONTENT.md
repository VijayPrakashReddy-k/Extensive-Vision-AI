## Model Architectures

<section id="squeeze_nets">
<h2>Squeeze Net</h2>
</section>

![squeeze_expand](https://user-images.githubusercontent.com/42317258/88203885-1b9a8d00-cc68-11ea-9572-c522eceb5902.png)
![squeezenet_architecture](https://user-images.githubusercontent.com/42317258/88203902-20f7d780-cc68-11ea-8577-08bb12757ab8.png)
![squeeze_ratio](https://user-images.githubusercontent.com/42317258/88203915-23f2c800-cc68-11ea-8f37-d15d411e9feb.png)

<section id="mobilenet_v1">
<h2>Mobilenet v1</h2>
</section>

#### Depthwise Separable Convolution:

    Depthwise separable convolution is a depthwise convolution followed by a pointwise convolution as follows:

![depthwise-separable-convs](https://user-images.githubusercontent.com/42317258/89290942-4082fd00-d677-11ea-9154-0b5160ca7f13.png)

`Depthwise convolution is the` ***channel-wise DK×DK spatial convolution***. `Suppose in the figure above, we have 5 channels, then we will have 5 DK×DK spatial convolution.`***Pointwise convolution*** `actually is the` ***1×1 convolution*** `to change the dimension.`<br>

the cost for above operation is:      ![math1](https://user-images.githubusercontent.com/42317258/89291394-1251ed00-d678-11ea-988e-7ddf716e0349.png)

    Depthwise Separable Convolution Cost: Depthwise Convolution Cost (Left), Pointwise Convolution Cost (Right)
    
where,

                        M: Number of input channels, 
                        
                        N: Number of output channels,
                
                        DK: Kernel size, and
                        
                        DF: Feature map size.
         
the cost for standard convolution,is:

![math2](https://user-images.githubusercontent.com/42317258/89291398-13831a00-d678-11ea-8032-144f5f719d34.png)

                        Standard Convolution Cost

Thus, the computation reduction is:

![math3](https://user-images.githubusercontent.com/42317258/89291401-141bb080-d678-11ea-8f44-014179658404.png)

                Depthwise Separable Convolution Cost / Standard Convolution Cost
                
- ***`When DK×DK is 3×3, 8 to 9 times less computation can be achieved, but with only small reduction in accuracy.`***

#### Architecture:

*`MobileNetV1 is from Google. Depthwise Separable Convolution is used to reduce the model size and complexity. It is particularly useful for mobile and embedded vision applications.`*

- *Smaller model size: Fewer number of parameters*
- *Smaller complexity: Fewer Multiplications and Additions (Multi-Adds)*

![Architecture@2x](https://user-images.githubusercontent.com/42317258/89277098-04916d00-d662-11ea-9014-78634b4652b2.png)

    The full MobileNets network has 30 layers. The design of the network is quite straightforward:

![mobilenet-arch](https://user-images.githubusercontent.com/42317258/89278444-bd0be080-d663-11ea-99aa-8e050aba53e2.png)

    - convolutional layer with stride 2
    - depthwise layer
    - pointwise layer that doubles the number of channels
    - depthwise layer with stride 2
    - pointwise layer that doubles the number of channels
    - depthwise layer
    - pointwise layer
    - depthwise layer with stride 2
    - pointwise layer that doubles the number of channels and so on…

After the very first layer (a regular convolution), the depthwise and pointwise layers take turns. Sometimes the depthwise layer has a stride of 2, to reduce the width and height of the data as it flows through the network. Sometimes the pointwise layer doubles the number of channels in the data. All the convolutional layers are followed by a  Batch Normalization (BN) and ReLU activation function.

![BN_relu_conv](https://user-images.githubusercontent.com/42317258/89286054-29401180-d66f-11ea-94ec-f7c1f8f6a56b.png)

      Standard Convolution (Left), Depthwise separable convolution (Right) With BN and ReLU
      
This goes on for a while until the original 224×224 image is shrunk down to 7×7 pixels but now has 1024 channels. After this there’s an *`average-pooling layer`* that works on the entire image so that we end up with a 1×1×1024 image, which is really just a vector of 1024 elements.

![global_average_pooling](https://user-images.githubusercontent.com/42317258/89289131-5ba03d80-d674-11ea-8dfe-8343d3898a60.png)

        Global Average Pooling

If we’re using MobileNets as a classifier, for example on ImageNet which has 1000 possible categories, then the final layer is a fully-connected layer with a softmax and 1000 outputs. If you wanted to use MobileNets on a different dataset, or as a feature extractor instead of classifier, you’d use some other final layer instead.

Even though MobileNets is designed to be pretty fast already, it’s possible to use a reduced version of this network architecture. There are three hyperparameters you can set that determine the size of the network:

- **Width multiplier (the paper calls this “alpha”):** This shrinks the number of channels. If the width multiplier is 1, the network starts off with 32 channels and ends up with 1024.

`Width Multiplier α for Thinner Models:`
Width Multiplier α(alpha) is introduced to control the **input width of a layer**, which makes M become αM. And the depthwise separable convolution cost become:

![alpha-thinner layers](https://user-images.githubusercontent.com/42317258/89324755-6921eb80-d6a5-11ea-9d10-5bb21f571e93.png)

        Depthwise Separable Convolution Cost with Width Multiplier α
`where α is between 0 to 1, with typical settings of 1, 0.75, 0.5 and 0.25. When α=1, it is the baseline MobileNet. And the computational cost and the number of parameters can be reduced quadratically by roughly α².`

![alpha-results](https://user-images.githubusercontent.com/42317258/89324743-67582800-d6a5-11ea-9fe2-c2610af7f7bf.png)

        Different Values of Width Multiplier α

**Accuracy drops off smoothly from α=1 to 0.5 until α=0.25 which is too small.**

- **Resolution multiplier (“rho” in the paper):** This shrinks the dimensions of the input image. The default input size is 224×224 pixels.

`Resolution Multiplier ρ for Reduced Representation:`
Resolution Multiplier ρ(rho) is introduced to control the **input image resolution of the network**, with Resolution Multiplier ρ, the cost become:

![rho-input-dimensions](https://user-images.githubusercontent.com/42317258/89325904-18ab8d80-d6a7-11ea-9af8-a6f0099f64a3.png)

        Depthwise Separable Convolution Cost with Both Width Multiplier α and Resolution Multiplier ρ
        
`where ρ is between 0 to 1. And the input resolution is 224, 192, 160, and 128. When ρ=1, it is the baseline MobileNet.`

![rho-results](https://user-images.githubusercontent.com/42317258/89325909-1a755100-d6a7-11ea-95c2-48f31e157e2a.png)

**Accuracy drops off smoothly across resolution from 224 to 128.**

![Width-and-resolution-multiplier](https://user-images.githubusercontent.com/42317258/89438032-f0369880-d765-11ea-9152-5f1c5e9a64dd.png)

- **Shallow or deep:** The full network has a group of 5 layers in the middle that you can leave out.

These settings can be used to make the network smaller — and therefore faster — but at the cost of prediction accuracy. (If you’re curious, the paper shows the effects of changing these hyperparameters on the accuracy.)

For the full network the total number of learned parameters is 4,221,032 (after folding the batch normalization layers). That’s certainly a lot less than VGGNet, which has over 130 million!

![model-results](https://user-images.githubusercontent.com/42317258/89438049-f462b600-d765-11ea-9771-10349795c75d.png)

<section id="quantization">
<h2>Quantization</h2>
</section>

#### Quantization has several other terminologies which could be similar in technique or concept.

**1. Low precision or half precision floating point:** <br>
Low precision could be the most generic concept. As normal precision uses FP32 (floating point of 32 bits which is single precision) to store model weights, low precision indicates numeric format such as FP16 (half precision floating point), INT8 (fixed point integer of 8 bits) and so on.<br>
There is a tend that low precision means INT8 these days.

![half-precision](https://user-images.githubusercontent.com/42317258/89677037-4c3a2200-d90a-11ea-902b-8dcf7bd3e8de.png)

**2.Mixed Precision:**
Mixed precision utilizes both FP32 and FP16 in model. FP16 reduces half of the memory size (which is a good thing), but some parameters/operators have to be in FP32 format to maitain accuracy.
**Steps:**

        1.Make an FP16 copy of the weights
        2.Forward propagate using FP16 weights and activations
        3.Multiply the resulting loss by the scale factor S
        4.Backward propagate using FP16 weights, activations, and their gradients
        5.Multiply the weight gradients by 1/S
        6.Optionally process the weight gradients (gradient clipping, weight decay, etc.)
        7.Update the master copy of weights in FP32

**3.Quantization:**
Quantization is basically INT8. Still, it has sub-categories depending on how many bits it takes to store one weight element. For example:

- **Binary Neural Network:** Neural networks with binary weights and activations at run-time and when computing the parameters’ gradient at train-time.
- **Ternary Weight Networks:** Neural networks with weights constrained to +1, 0 and -1.
- **XNOR Network:** the filters and the input to convolutional layers are binary. XNOR-Networks approximate convolutions using primarily binary operations.

***`Quantization process can be divided into two parts:`*** 

    1.Converting model from FP32 to INT8, and 
    
![training-inferencing](https://user-images.githubusercontent.com/42317258/89678049-1f870a00-d90c-11ea-9cad-f09a45d89cb8.png)

    2.Inferencing with INT8.
    
In 8 bit quantization, FP32 is replaced by INT8 during inference, while training is still FP32.

![Quantized-model](https://user-images.githubusercontent.com/42317258/89678210-712f9480-d90c-11ea-84d0-9437e62dea65.png)

### Training with Quantization:

- learn ranges during training
- forward pass - quantized values
- backward pass - float values

[Reference](https://jackwish.net/2019/neural-network-quantization-introduction.html)

## ShuffleNet:

<section id="channel-shuffle">
<h3>Channel Shuffle</h3>
</section>

Let's understand, by example:
<ol>
<li>Let Gr = 3,  and N = 4 (channels in each group) </li>
    
        1.RRRR GGGG BBBB
        
<li>Reshape to (Gr, N)
    
        1.RRRR
        2.GGGG
        3.BBBB
    
<li>Transpose to (N, Gr) </li>

        1.RGB
        2.RGB
        3.RGB
        4.RGB
        
<li>Flatten (not x, y, but channels, don't forget) </li>

        1.RGB RGB RGB RGB
        
<li>Convert back to Gr = 3 and N = 4 </li>

        1.RGBR GBRG BRGB

![shuffling-channels](https://user-images.githubusercontent.com/42317258/89733923-76105780-da76-11ea-8dbb-c474715b57ff.png)

<section id="shufflenet-unit">
<h3>ShuffleNet Unit</h3>
</section>

![shufflenet unit](https://user-images.githubusercontent.com/42317258/89734080-69d8ca00-da77-11ea-99bb-1360528720ad.png)

*(a) bottleneck unit with depthwise convolution (DWConv), (b) ShuffleNet unit with pointwise group convolution (GConv) and channel shuffle,* **The purpose of the second pointwise group convolution is to recover the channel dimension to match the shortcut path.** *(c) ShuffleNet unit with stride = 2.*

- **(a) Bottleneck Unit:** This is a standard residual bottleneck unit, but with depthwise convolution used. (Depthwise convolution is used in [MobileNetV1 source](https://towardsdatascience.com/review-mobilenetv1-depthwise-separable-convolution-light-weight-model-a382df364b69)) With 1×1 then 3×3 DW then 1×1 convolutions used, it can be also treated as a bottleneck type of depthwise separable convolution used in [MobileNetV2](https://towardsdatascience.com/review-mobilenetv2-light-weight-model-image-classification-8febb490e61c) <br>
- **(b) ShuffleNet Unit:** The first and second 1×1 convolutions are replaced by group convolutions. A channel shuffle is applied after the first 1×1 convolution.<br>
- **(c) ShuffleNet Unit with Stride=2:** When stride is applied, a 3×3 average pooling on the shortcut path is added. Also, the element-wise addition is replaced with channel concatenation, which makes it easy to enlarge channel dimension with little extra computation cost.
- ReLU is not applied to 3x3 DWConv (Depthwise convolutions) <br>
- Given the input c×h×w, and bottleneck channels m, [ResNet](https://towardsdatascience.com/review-resnet-winner-of-ilsvrc-2015-image-classification-localization-detection-e39402bfa5d8) unit requires hw(2cm+9m²) FLOPs and [ResNeXt](https://towardsdatascience.com/review-resnext-1st-runner-up-of-ilsvrc-2016-image-classification-15d7f17b42ac) requires hw(2cm+9m²/g) FLOPs, while **ShuffleNet only requires hw(2cm/g+9m) FLOPs** where g is the number of group convolutions.<br>
- In other words, given a computational budget, **ShuffleNet can use wider feature maps**. We find this is **critical for small networks**, as tiny networks usually have an insufficient number of channels to process the information.<br>

<section id="shufflenet-architecture">
<h3>ShuffleNet Architecture</h3>
</section>

![shufflenet-architecture](https://user-images.githubusercontent.com/42317258/89734752-ab6b7400-da7b-11ea-91e8-bcc99700631a.png)

- The proposed network is mainly composed of a stack of ShuffleNet units grouped into three stages.<br>
- The number of bottleneck channels is set to 1/4 of the output channels for each ShuffleNet unit. <br>
- A scale factor s is applied on the number of channels. The networks in the above table is denoted as “ShuffleNet 1×”, then ”ShuffleNet s×” means scaling the number of filters in ShuffleNet 1× by s times thus overall complexity will be roughly s² times of ShuffleNet 1×. <br>

![model-complexity](https://user-images.githubusercontent.com/42317258/89734893-7ad80a00-da7c-11ea-9d8d-4838988a2ba6.png)

- With g = 1, i.e. no pointwise group convolution.
- Models with group convolutions (g > 1) consistently perform better than their counterparts without pointwise group convolutions (g = 1).
- Smaller models tend to benefit more from groups.
- For example, for ShuffleNet 1× the best entry (g = 8) is 1.2% better than the counterpart, while for ShuffleNet 0.5× and 0.25×, the gaps become 3.5% and 4.4% respectively.
- For some models (e.g. ShuffleNet 0.5×) when **group numbers become relatively large (e.g. g = 8), the classification score saturates or even drops. With an increase in group number (thus wider feature maps), input channels for each convolutional filter become fewer, which may harm representation capability.**


<section id="comparision">
<h2 align = 'center'>Channel Shuffle vs No shuffle</h2>
</section>

![comparision](https://user-images.githubusercontent.com/42317258/89735162-364d6e00-da7e-11ea-8182-15f40a8b0e9c.png)

- `Channel shuffle consistently boosts classification scores for different settings, which shows the importance of cross-group information interchange.`
