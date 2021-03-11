## 9 - Data Augmentation
### Session:9  Advanced Image Augmentation Techniques: Albumentations, Richman's data augmentation and benchmarks

**week 9 contents:**

- [Relationship between Data and Validation Accuracy](./README.md/#datarelation)

- [Data Augmentation](./README.md/#dataaug)

- [Data Augmentation Strategies](./README.md/#strategies)

  - [PMDA - Poor Man's Data Augmentation Strategies](./README.md/#pmda)
  
            - Scale; Translation; Rotation; Blurring; Image Mirroring; Color Shifting / Whitening. 

  - [MMDA* - Middle-Class Man's Data Augmentation Strategies](./README.md/#mmda)
            
            - We have 2 beautiful Libraries for MMDAs:

                  1. ALBUMENTATIONS
                  
                  2. IMGAUG

  - [RMDA* - Rich Man's Data Augmentation Strategies](./README.md/#rmda)
  
            1. Reinforcement learning or AutoAugment 24th May 2018

            2. Population-Based Augmentation

            3. Patch Gaussian Augmentation 6 June 2019

- [Strategy Results](./README.md/#results)

- [Global Average Pooling](./README.md/#gap)

- [GradCam](./README.md/#cam)

- [Diagnosing DNN](./README.md/#dnn)

- [Assignment](./README.md/#assignment)

<p align = 'center',id = 'datarelation'>
            <img src = "https://user-images.githubusercontent.com/42317258/110660713-d4a6db00-81e9-11eb-9047-4d65fd26042f.png" />
</p>

- **`One easy way of increasing accuracy is increasing the Receptive Field:`**

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110661261-657db680-81ea-11eb-9201-2104101e834f.png" />
</p>

- **`But IF we increase the receptive field of a network, we see heavy over-fitting (performing good at training and failing at validation.)`**

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110662151-3e73b480-81eb-11eb-9647-db8df98879a1.png" />
</p>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110661275-67477a00-81ea-11eb-961b-45429755f86f.png" />
</p>

- `As we can see above graph, it is exponential (As data getting increased, the average precision also getting increased exponentially).`

<p align = 'center',id = 'dataaug'>
            <img src = "https://user-images.githubusercontent.com/42317258/110662930-fd2fd480-81eb-11eb-8c91-f3f686741d89.png" />
</p>

`Data augmentation (DA) is an effective alternative to obtaining valid data, and can generate new labeled data based on existing data using "label-preserving transformations".`

- Designing appropriate DA policies requires a lot of expert experience and is time-consuming, and the evaluation of searching the optimal policies is costly. Moreover, the policies generated using DA policies are usually not reusable.

[Source](Papers/Revisiting-Unreasonable-Effectiveness-of-Data-in-Deep-Learning-Era.pdf) : we find that the performance on vision tasks increases logarithmically based on the volume of training data size.

- Generally, the more data, the better deep neural networks can do. Insufficient data can lead to model over-fitting, which will reduce the generalization performance of the model on the test set. And Techniques such as:

    - DropOut
    
    - Batch Normalization
    
    - L1/L2 regularization
    
    - Layer normalization 
    
have been proposed to help combat over-fitting, but they will fall short if data is limited.

- *So,we have Data Augmentation Strategies to Increase the size of the data are:*

      PMDA - Poor Man's Data Augmentation Strategies

      MMDA* - Middle-Class Man's Data Augmentation Strategies

      RMDA* - Rich Man's Data Augmentation Strategies

<p align = 'center',id = 'pmda'>
            <img src = "https://user-images.githubusercontent.com/42317258/110740365-f7bca380-8258-11eb-83e1-58c978d61290.png" />
</p>

- `Scale; Translation; Rotation; Blurring; Image Mirroring; Color Shifting / Whitening.`

Simple Stuff which most probably is in-built in Pytorch. 

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110740248-c348e780-8258-11eb-96a8-281b68a286aa.jpg" />
</p>

<p align = 'center',id = 'mmda'>
            <img src = "https://user-images.githubusercontent.com/42317258/110740754-947f4100-8259-11eb-9c6e-39d331d33978.png" />
</p>

- `ALBUMENTATIONS is easy to integrate with PyTorch.`

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110740913-d01a0b00-8259-11eb-98ea-22d043cdfaa6.png" />
</p>

- `It has some nearly everything we'd want:`

![albumentation-exaples](https://user-images.githubusercontent.com/42317258/110740916-d14b3800-8259-11eb-8eb0-e5e3385ee026.jpeg)

- `And smart way of handling Annotations`

![albumentation-annotations](https://user-images.githubusercontent.com/42317258/110740929-d4debf00-8259-11eb-9e53-f8908ad1f163.jpeg)

- **`Some of the MMDAs are already included in Albumentations. But let's see some of the important ones.`**

  [1. ELASTIC DISTORTION - 2003](./CONTENT.md/#distortion)

  [2. CUTOUT - 29 Nov 2017](CONTENT.md/#cutout)

  [3. MIXUP - 27 April 2018](./CONTENT.md/#mixup)

  [4. RICAP - 22 NOV 2018](CONTENT.md/#ricap)

<p align = 'center',id = 'rmda'>
            <img src = "https://user-images.githubusercontent.com/42317258/110774161-81816680-8283-11eb-9c04-fd40d6b28288.png" />
</p>

### AutoAugment:

**Pros:**

    Can be applied directly on the dataset
    Learned policies can be transferred to a new dataset
    Achieves State-of-art for ImageNet, CIFAR10, and CIFAR100
    NAS took CIFAR10 error to 2% (cannot be beaten by humans), AutoAugment with NAS took this number to 1.5%

**Cons:**

    Takes 5000 P100 GPU hours for CIFAR and 15000 GPU hours for ImageNet

![AutoAugment](https://user-images.githubusercontent.com/42317258/110774645-0d938e00-8284-11eb-9023-dccc003cec99.png)

[Reinforcement learning or AutoAugment 24th May 2018](/Papers/RMDAs/AutoAugment.pdf)

### Population-Based Augmentation:

(PBA), which generates nonstationary augmentation policy schedules instead of a fixed augmentation policy.

![PBA2](https://user-images.githubusercontent.com/42317258/110774690-197f5000-8284-11eb-8286-017d7231f5c6.png)

[Population-Based Augmentation14 May 2019](/Papers/RMDAs/Population-Based-Augmentation.pdf)

### PATCH GAUSSIAN:

`Prior work has argued that there is an inherent trade-off between robustness and accuracy, which is exemplified by standard data augment techniques such as Cutout, which improves clean accuracy but not robustness, and additive Gaussian noise, which improves robustness but hurts accuracy. To overcome this trade-off, we introduce Patch Gaussian, a simple augmentation scheme that adds noise to randomly selected patches in an input image. Models trained with Patch Gaussian achieve state of the art on the CIFAR-10 and ImageNet.`

![PatchGuassian](https://user-images.githubusercontent.com/42317258/110774754-27cd6c00-8284-11eb-8633-83632f6f6d36.png)

[Patch Gaussian Augmentation 6 June 2019](/Papers/RMDAs/Patch-Gaussian-Augmentation.pdf)

<p align = 'center',id = 'results'>
            <img src = "https://user-images.githubusercontent.com/42317258/110780573-daa0c880-828a-11eb-9b69-e1650fd3c6e3.png" />
</p>

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110780628-e8eee480-828a-11eb-8688-9862e02f8663.png" />
</p>
<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110780619-e7252100-828a-11eb-8818-6432ca5bdb63.png" />
</p>
