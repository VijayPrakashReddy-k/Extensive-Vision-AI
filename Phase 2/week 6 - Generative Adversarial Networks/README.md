## 6. GANs: Generative Adversarial Network and Variants

### [Session 6 - GANs](https://www.youtube.com/watch?v=k5_nTSHpKv8)

**week 6 contents:**

- [What Are GANS?](./README.md/#gan_intro)

- [Deep Generative Models](./README.md/#dgm)

- [Overview of different Generative Models](./README.md/#overview)

- [GENERATIVE ADVERSARIAL NETWORKS](./README.md/#gan)

- [Generative VS Discriminative Algorithms](./README.md/#algos)

- [GAN Internals](./README.md/#gan_internals)

- [GANS, AUTOENCODERS AND VAES](./README.md/#gan_vaes)

- [GAN via code](./README.md/#code)

- [Types of GANS](./README.md/#types)

    - [DEEP CONVOLUTIONAL GAN (DCGAN)](./README.md/#dcgan)

    - [CONDITIONAL GAN](./README.md/#cgan)

    - [AUXILLARY GANS](./README.md/#agan)

    - [INFOGANS](./README.md/#infogan)

    - [PIXELGANS](./README.md/#pixelgan)

    - [CYCLEGANS](./README.md/#cyclegan)

- [GAN Problems](./README.md/#problems)

- [Assignment](./README.md/#assignment)

<h1 id=gan_intro align='center'>What Are GANS? </h1>

**`Adversarial: (of a trial or legal proceedings) in which the parties in a dispute have the responsibility for finding and presenting evidence.`**

- GANs are DNNs comprised of two nets, pitted one against the other (thus adversarial)

- Generative Adversarial Networks are deep neural net architectures comprised of two neural networks, competing one against the other (adversarial = competing).

- GANs are neural networks that are trained in an adversarial manner to generate data mimicking some distribution.

[GAN Applications](./CONTENT.md/#applications)

## Two great practical examples of GAN use are:

**Google Brain Project for Creating a Method of Encryption :**

    The project was to send an encrypted message which cannot be intercepted by anyone. 

**Drug Research :**

    Drug Research, can be trained on existed drugs and suggest new synthetic chemical structures that improve upon existing drugs.
 

## There are two kinds of models in machine learning:

**`Discriminative model:`**
   
- They discriminate between two classes of data (for example hot-dog, not-hot-dog, i.e. 0/1). They fall into the category of classification problems. 
    
**`Generative models:`**

- They are trained on training data X sampled from a distribution D, which given some random distribution z produces a distribution D' which is close to D according to some closeness metrics. 

<h1 id=dgm align='center'> Deep Generative Models </h1>

- AutoEncoders

- Variational AutoEncoders

- Ganerative Adversarial Networks
    
        Adversarial AutoEncoders

        VAE/GAN

        Adversatial Domain Adaption

<h1 id=overview align='center'> Overview of different Generative Models </h1>

<h2 align='center'> Auto Encoders </h2>

![Auto Encoders](./Images/AutoEncoders.jpg)

<h2 align='center'> Variational Auto Encoders </h2>

![Variational Auto Encoders](./Images/VAE.jpg)

<h2 align='center'> GANs </h2>

![GANs](./Images/GAN.jpg)
