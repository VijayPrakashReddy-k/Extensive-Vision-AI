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

- **Shallow or deep:** The full network has a group of 5 layers in the middle that you can leave out.

These settings can be used to make the network smaller — and therefore faster — but at the cost of prediction accuracy. (If you’re curious, the paper shows the effects of changing these hyperparameters on the accuracy.)

For the full network the total number of learned parameters is 4,221,032 (after folding the batch normalization layers). That’s certainly a lot less than VGGNet, which has over 130 million!
