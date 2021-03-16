### Resource Links:

#### Data Augmentation:

[Albumentation-kaggle](https://www.kaggle.com/corochann/bengali-albumentations-data-augmentation-tutorial)

[Albumentation-github-official](https://github.com/albumentations-team/albumentations)

[Data Augmentation Blog](https://towardsdatascience.com/when-conventional-wisdom-fails-revisiting-data-augmentation-for-self-driving-cars-4831998c5509)

[PyTorch and Albumentations for image classification](https://albumentations.ai/docs/examples/pytorch_classification/)

[Albumentations_examples](https://github.com/albumentations-team/albumentations_examples)

[Data Augmentation](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-019-0197-0/figures/2)

[Examples](https://sourcecodequery.com/example-method/albumentations.GridDistortion)

[Albumentation docmentation](https://albumentations.ai/docs/api_reference/augmentations/transforms/#albumentations.augmentations.transforms.Cutout)

#### Grad-CAM:

[Gradient Class Activation Maps Excellent Blog](https://glassboxmedicine.com/2020/05/29/grad-cam-visual-explanations-from-deep-networks/)

[Another Good Blog](https://medium.com/@stepanulyanin/implementing-grad-cam-in-pytorch-ea0937c31e82)

[Grad-CAM: Gradient-weighted Class Activation Mapping](http://gradcam.cloudcv.org/)

[Grad-CAM github repo](https://github.com/ramprs/grad-cam)

[Grad-CAM youtube](https://www.youtube.com/watch?time_continue=129&v=COjUB9Izk6E&feature=emb_logo)

#### Trainable vs. Post-Hoc Attention Mechanisms

`When training an image model, we want the model to be able to focus on important parts of the image. One way of accomplishing this is through trainable attention mechanisms. In this post we will first discuss the difference between post-hoc vs. trainable attention and soft vs. hard attention.`

**Note: attention is also used extensively in natural language processing. The focus of this post is attention in computer vision tasks.**

**`What is Attention?`**

- `definition (1): trainable attention: a group of techniques that help a “model-in-training” notice important things more effectively` and

- `definition (2): post-hoc attention: a group of techniques that help humans visualize what an already-trained model thinks is important`

![grad-cam-etc-tree-1](https://user-images.githubusercontent.com/42317258/111259001-1699ac00-8644-11eb-8913-f8055f1a12bf.png)

#### Summary:

- `Trainable attention mechanisms have attention weights that are learned during training, which help the model focus on key parts of images important for the task;`

- `Post-hoc attention mechanisms are techniques applied after a model is finished training, and are intended to provide insight into where the model is looking when it makes predictions;`

- `Hard attention is image cropping and can be trained using REINFORCE. Soft attention produces “hazier” focus region(s) and can be trained using regular backpropagation.`

- `“Learn to Pay Attention” is an interesting paper demonstrating how soft trainable attention can improve image classification performance and highlight key parts of images.`
