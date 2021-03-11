## 9 - Data Augmentation
### Session:9  Advanced Image Augmentation Techniques: Albumentations, Richman's data augmentation and benchmarks

**week 9 contents:**

- [Relationship between Data and Validation Accuracy](./README.md/#datarelation)

- [Data Augmentation](./README.md/#dataaug)

- [Data Augmentation Strategies](./README.md/#strategies)

  - [PMDA - Poor Man's Data Augmentation Strategies](./README.md/#pmda)
  
            - Scale; Translation; Rotation; Blurring; Image Mirroring; Color Shifting / Whitening. 

  - [MMDA* - Middle-Class Man's Data Augmentation Strategies](./README.md/#mmda)
  
            1. ELASTIC DISTORTION - 2003
            
            2. CUTOUT - 29 Nov 2017
            
            3. MIXUP - 27 April 2018
           
            4. RICAP - 22 NOV 2018
            
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

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110744715-25591b00-8260-11eb-90f7-bac23bea04ce.png" />
</p>

- `Distortion related methods:`

          albumentations.GridDistortion
          
          albumentations.ElasticTransform

<p align = 'center'>
            <img src = "https://user-images.githubusercontent.com/42317258/110745349-1aeb5100-8261-11eb-825b-92afe9141c74.png" />
</p>

Affine distortions greatly improved results on the MNIST database. However,best results were obtained when we used elastic deformations. The imagedeformations were created by first generating randomdisplacement fields, that is ∆x(x,y) = rand(-1,+1) and ∆x(x,y)=rand(-1,+1), where rand(-1,+1) is a random number between -1 and +1, generated with a uniform distribution. The fields ∆x and ∆y are then convolved with a Gaussian of standard deviation σ (in pixels). If σ is large, the resulting values are very small because the random values average 0. If we normalize the displacement field (to a norm of 1), the field is then close to constant, with a random direction. If σ is small, the field looks like a completely random field after normalization (as depicted in Figure 2, top right). For intermediate σ values, the displacement fields look like elastic deformation, where σ is the elasticity coefficient.The displacement fields are then multiplied by a scaling factor α that controls the intensity of the deformation.

[ELASTIC DISTORTION - 2003](Papers/MMDA/ELASTIC_DISTORTION_2003/Elastic_Distortion.pdf)
