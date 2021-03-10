## 9 - Data Augmentation
### Session:9  Advanced Image Augmentation Techniques: Albumentations, Richman's data augmentation and benchmarks

**week 9 contents:**

- [Relationship between Data and Validation Accuracy](./README.md/#data-relation)

- [Data Augmentation](./README.md/#data-aug)

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

<p align = 'center',id = 'data-relation'>
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

<p align = 'center',id = 'data-aug'>
            <img src = "https://user-images.githubusercontent.com/42317258/110662930-fd2fd480-81eb-11eb-8c91-f3f686741d89.png" />
</p>

`Data augmentation (DA) is an effective alternative to obtaining valid data, and can generate new labeled data based on existing data using "label-preserving transformations".`

- Designing appropriate DA policies requires a lot of expert experience and is time-consuming, and the evaluation of searching the optimal policies is costly. Moreover, the policies generated using DA policies are usually not reusable.

- [Source](./Papers/Revisiting Unreasonable Effectiveness of Data in Deep Learning Era.pdf) : we find that the performance on vision tasks increases logarithmically based on the volume of training data size

- Generally, the more data, the better deep neural networks can do. Insufficient data can lead to model over-fitting, which will reduce the generalization performance of the model on the test set. And Techniques such as:

    - DropOut
    
    - Batch Normalization
    
    - L1/L2 regularization
    
    - Layer normalization 
    
have been proposed to help combat over-fitting, but they will fall short if data is limited.
