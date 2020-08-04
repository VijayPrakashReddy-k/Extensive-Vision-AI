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
      
This goes on for a while until the original 224×224 image is shrunk down to 7×7 pixels but now has 1024 channels. After this there’s an average-pooling layer that works on the entire image so that we end up with a 1×1×1024 image, which is really just a vector of 1024 elements.

If we’re using MobileNets as a classifier, for example on ImageNet which has 1000 possible categories, then the final layer is a fully-connected layer with a softmax and 1000 outputs. If you wanted to use MobileNets on a different dataset, or as a feature extractor instead of classifier, you’d use some other final layer instead.

Note: The paper actually states that between each convolution and the ReLU there is a batch normalization layer. For our purposes we can ignore those layers as they’re only used during training. Since the convolution operation is a linear transform and so is batch normalization, we can multiply the weights learned by batch normalization with the weights of the convolution layer before it. This saves on multiply operations at inference time.

Even though MobileNets is designed to be pretty fast already, it’s possible to use a reduced version of this network architecture. There are three hyperparameters you can set that determine the size of the network:

Width multiplier (the paper calls this “alpha”): this shrinks the number of channels. If the width multiplier is 1, the network starts off with 32 channels and ends up with 1024.

Resolution multiplier (“rho” in the paper): this shrinks the dimensions of the input image. The default input size is 224×224 pixels.

Shallow or deep. The full network has a group of 5 layers in the middle that you can leave out.

These settings can be used to make the network smaller — and therefore faster — but at the cost of prediction accuracy. (If you’re curious, the paper shows the effects of changing these hyperparameters on the accuracy.)

For the full network the total number of learned parameters is 4,221,032 (after folding the batch normalization layers). That’s certainly a lot less than VGGNet, which has over 130 million!
