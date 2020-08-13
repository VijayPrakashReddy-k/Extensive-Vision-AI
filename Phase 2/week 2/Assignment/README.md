### Mobinet V2 Training and Deployment for Custom Dataset on AWS with Serverless open source framework:

Lambda URL after deployment : `https://ly1yaeusha.execute-api.ap-south-1.amazonaws.com/dev/mobilenetV2-classify-flying-objects`

![S2_result](https://user-images.githubusercontent.com/42317258/90090921-d9360e80-dd42-11ea-8d60-383ab771ad4b.png)

#### Data Collection:
- 21,824 images have been collected via group effort over four classes:

             Flying Birds with count : 8378
             
             Small QuadCopters with count : 3624
             
             Large QuadCopters with count : 4163
                      
             Winged Drones with count : 5659

`Images here are different in sizes and types.
Dataset is divided into train and validation set with ratio of 8:2`

#### Data Augmentation:

To solve the huge variation in image size, all image have been resized to 250, and then random crop of 224 x 224. <br>

*Augmentation techniques used:*

              Resize
              RandomRotation
              Horizontal and Vertical flip
              Random Erasing
              
**Pipeline for training set:**

        'train': transforms.Compose([
            transforms.Resize(250),
            transforms.RandomRotation ([0, 180]),
            transforms.RandomCrop (224, pad_if_needed=True),
            transforms.RandomHorizontalFlip(),
            transforms.RandomVerticalFlip(),
            transforms.ToTensor(),
            transforms.RandomErasing (),
        ])
    
**Pipeline for validation set:**

          'val': transforms.Compose([
              transforms.Resize(250),
              transforms.CenterCrop(224),
              transforms.ToTensor(),
          ])
          
#### Transfer Learning:

A MobileNet V2 model is picked up with pretrained weights.

        model_ft = models.mobilenet_v2 (pretrained = True)
        
Final Layer of Model changed to give out_features as 4 instead of 1000 (ImageNet)

        model_ft.classifier[1] = torch.nn.Linear(in_features=model_ft.classifier[1].in_features, out_features=4)
        
Converting to use GPU, and defining other parameters

        model_ft = model_ft.to(device)
        criterion = nn.CrossEntropyLoss()
        optimizer_ft = optim.SGD(model_ft.parameters(), lr=0.001, momentum=0.9)
        exp_lr_scheduler = lr_scheduler.StepLR(optimizer_ft, step_size=7, gamma=0.1)
        
Finally Training for 25 epochs.

        model_ft = train_model(model_ft, criterion, optimizer_ft, exp_lr_scheduler, num_epochs=25)

#### Graphs:
![image](https://user-images.githubusercontent.com/42317258/89731843-06936b80-da68-11ea-98db-fa395d09fe3a.png) ![image](https://user-images.githubusercontent.com/42317258/89731872-40fd0880-da68-11ea-872d-5ee22b893656.png)

#### Misclassified Images:

- **Small QuadCopters**

![image](https://user-images.githubusercontent.com/42317258/89731965-ec0dc200-da68-11ea-9ec4-ec426ab80b65.png)

- **Large QuadCopters**

![image](https://user-images.githubusercontent.com/42317258/89732010-47d84b00-da69-11ea-9d92-3868690964f2.png)

- **Winged Drones**

![image](https://user-images.githubusercontent.com/42317258/89732021-5fafcf00-da69-11ea-9749-e11a2a70a11a.png)

- **Flying Birds**

![image](https://user-images.githubusercontent.com/42317258/89732015-545ca380-da69-11ea-8e82-6c3cd67d248e.png)
