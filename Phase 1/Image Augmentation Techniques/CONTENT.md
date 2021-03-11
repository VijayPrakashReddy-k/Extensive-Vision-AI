<p align = 'center',id = 'distortion'>
            <img src = "https://user-images.githubusercontent.com/42317258/110744715-25591b00-8260-11eb-90f7-bac23bea04ce.png" />
</p>

- `Distortion related methods:`

          albumentations.GridDistortion
          
          albumentations.ElasticTransform

![distortion-transform](https://user-images.githubusercontent.com/42317258/110752863-d31df700-826b-11eb-8ddc-b22c85c184ac.jpeg)

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110745349-1aeb5100-8261-11eb-825b-92afe9141c74.png" />
</p>

Affine distortions greatly improved results on the MNIST database. However,best results were obtained when we used elastic deformations. The imagedeformations were created by first generating randomdisplacement fields, that is ∆x(x,y) = rand(-1,+1) and ∆x(x,y)=rand(-1,+1), where rand(-1,+1) is a random number between -1 and +1, generated with a uniform distribution. The fields ∆x and ∆y are then convolved with a Gaussian of standard deviation σ (in pixels). If σ is large, the resulting values are very small because the random values average 0. If we normalize the displacement field (to a norm of 1), the field is then close to constant, with a random direction. If σ is small, the field looks like a completely random field after normalization (as depicted in Figure 2, top right). For intermediate σ values, the displacement fields look like elastic deformation, where σ is the elasticity coefficient.The displacement fields are then multiplied by a scaling factor α that controls the intensity of the deformation.

[ELASTIC DISTORTION - 2003](Papers/MMDA/ELASTIC_DISTORTION_2003/Elastic_Distortion.pdf)

<p align = 'center',id = 'cutout'>
            <img src = "https://user-images.githubusercontent.com/42317258/110753016-019bd200-826c-11eb-8c36-9e0a213f2ef4.png" />
</p>

- `Cutout related methods:`
 
      albumentations.Cutout <-- It is deprecated.
      albumentations.CoarseDropout
      
***CutOut: Image speaks better on what it is. It adds square sized mask to images for data augmentation. CNN need to learn target label by "watching" part of the images.***

      Original image
      Cutout(num_holes=8, max_h_size=8, max_w_size=8, fill_value=0, p=1)
      Cutout(num_holes=10, max_h_size=20, max_w_size=20, fill_value=0, p=1)
      Cutout(num_holes=30, max_h_size=30, max_w_size=30, fill_value=64, p=1)
      Cutout(num_holes=50, max_h_size=40, max_w_size=40, fill_value=128, p=1)
      Cutout(num_holes=100, max_h_size=50, max_w_size=50, fill_value=255, p=1)
    
![Cutout](https://user-images.githubusercontent.com/42317258/110753366-80910a80-826c-11eb-967a-b79cbdd82e16.jpg)

### Cutout function parameters:
![cutout-function](https://user-images.githubusercontent.com/42317258/110754930-5f311e00-826e-11eb-85b2-03af8de91a2b.png)

### Cutout Results:
![cutout-results](https://user-images.githubusercontent.com/42317258/110754095-6a377e80-826d-11eb-894b-6fcc1a383cb3.png)

[CUTOUT - 29 Nov 2017](Papers/MMDA/CUTOUT/Cutout.pdf)

<p align = 'center',id = 'mixup'>
            <img src = "https://user-images.githubusercontent.com/42317258/110755970-97852c00-826f-11eb-980b-ca0983f86dd4.png" />
</p>

`Mixup alpha-blends two images to construct a new training image. Mixup can train deep CNNs on convex combinations of pairs of training samples and their labels and enables deep CNNs to favor a simple linear behavior in between training samples. This behavior makes the prediction confidence transit linearly from one class to another class, thus providing smoother estimation and margin maximization. Alpha-blending not only increases the variety of training images but also works like adversarial perturbation. Thereby, mixup makes deep CNNs robust to adversarial examples and stabilizes the training of generative adversarial networks. In addition, it behaves similarly to class label smoothing by mixing class labels with the ratio λ : 1 − λ.`

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110755994-9fdd6700-826f-11eb-929f-56348da22d3e.png" />
</p>

[MIXUP - 27 April 2018](Papers/MMDA/MIXUP_2018_27_04/mixup-BEYOND-EMPIRICAL-RISK-MINIMIZATION.pdf)

<p align = 'center',id = 'ricap'>
            <img src = "https://user-images.githubusercontent.com/42317258/110757113-0616b980-8271-11eb-9bc5-d916b32e4d0a.png" />
</p>

`RICAP crops four training images and patches them to construct a new training image; it selects images and determines the cropping sizes randomly, where the size of the final image is identical to that of the original image.  RICAP also mixes class labels of the four images with ratios proportional to the areas of the four images like label smoothing in mixup. Compared to mixup, RICAP has three clear distinctions: it mixes images spatially, it uses partial images by cropping, and it does not create features that are absent in the original dataset except for boundary patching.`

### RICAP process:

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110757140-0f078b00-8271-11eb-8589-2fbd8ba2c94b.png" />
</p>

### RICAP results:

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110757147-10d14e80-8271-11eb-8286-9e921a737ba6.png" />
</p>

### RICAP output:

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110757153-12027b80-8271-11eb-8c1d-ac996430787f.png" />
</p>

[RICAP - 22 NOV 2018](Papers/MMDA/RICAP_2018_22_11/RICAP.pdf)
