### Research and training Neural Net pipeline

#### Research

Price estimation of some product depending on many factors is a complicated task if it isn't an everyday buy/sell case like food in a local store. The task is even more sophisticated if you don't have instant physical access to the product and you can only use visual information or the product itself is an image. For such use cases it is good practice to avoid some human-factors, speculative and misleading intentions with delegating the bottleneck point of buy/sell to machine algorithms. We have researched the possibility of using Neural Nets for that algorithm.

The Deep Learning approach of image-to-price task is not commonly used in the market yet, but there are examples of some use cases. For example [Vehicle Price Prediction using Visual Features](https://arxiv.org/abs/1803.11227) and [Vision-based Real Estate Price Estimation](https://www.researchgate.net/publication/318528081_Vision-based_Real_Estate_Price_Estimation). 

Vehicle Price Prediction using Visual Features paper propose the [Linear Regression](https://en.wikipedia.org/wiki/Linear_regression) baseline for image-to-price task. Baseline model pipeline is VGG16 feature extraction + Principle Component Analysis ([PCA](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)) of image low-level features then few fully-connected layers with one neuron as output for linear regression process on the image features information. Our research leads us to believe that Linear Regression on the image features of NFT tokens [isn't working](https://github.com/meat-app-hack/research-and-training-net/blob/main/nft_regression.ipynb). That shows us only the average price of the whole dataset. The result can be compared to linear regression on random noise. There is no connection between image low-rank features and the price BUT (!) it turns out that the price is strongly related to the belonging of the image to a particular collection or similarity with such collections. For the purpose of evaluating images belonging to precize collection or similarity with those we developed a [classification neural network](https://github.com/meat-app-hack/research-and-training-net/blob/main/vgg_classification_net.ipynb). The price of an NFT image is calculated based on the class belonging probability of the given image and the average of the NFT prices of the class predicted.

In order of participation TDeFi Business Hackathon we are proposing to your attention MeatNet🥩 a neural net that do price prediction of NFT image


#### Data parsing

- NFT token address, token id, current market values parsed from SQLite [database](https://www.kaggle.com/simiotic/ethereum-nfts)
- Image data parsed via indexed database of [Infura API](https://infura.io/)

Python scripts for following those steps and further info you can find [there](https://github.com/meat-app-hack/nft-data-parser). Another option for NFT image parse directly from blockchain on TypeScript is [there](https://github.com/meat-app-hack/zora-nft-data-parser)

#### Data preprocessing

- After the data parsing process we had more than 10k NFT images, sadly only 4k of them were used in training. Training on the whole dataset led us to Neural Net biases of class recognition because corresponding classes don't have equal distribution of image units.

- All of the 4k images were labelled by their classes and resized by height, width = (300, 300) with RGB channels (Alpha channel of some of those images replaced)

- On a data loading step images pexels intensity were rescaled by 1./255 for the loss function to converge correctly. Training data generator was configured with a wide range of data augmentation modes

```python
train_datagen = ImageDataGenerator(
 rescale=1./255,
 rotation_range=40,
 width_shift_range=0.2,
 height_shift_range=0.2,
 shear_range=0.2,
 zoom_range=0.2,
 horizontal_flip=True,
 fill_mode='nearest')
 ```
 
 - In the lack of data conditions, we decided to do a train/test split in 30/1 ratio
 
The more data, the more perfect a neural network can be trained.
 
#### Neural Net Architecture

VGG16 feature extractor backbone with Fully-connected and classification layer is our complete design

![image](https://user-images.githubusercontent.com/44669029/142066229-aaf63bac-0a6d-442b-809c-2acb2f74549b.png)

![image](https://user-images.githubusercontent.com/44669029/142066573-6e785095-cd13-42f8-8ced-debacb966b90.png)

#### Training pipeline

- The easier the better. Using [ImageNet](https://www.image-net.org/) pretrained VGG16 backbone for feature extraction as a first step we did 3-epochs predtraining of our last fully-connected layer and classification layer. We used [Categorical Crossentropy](https://keras.io/api/losses/probabilistic_losses/#categorical_crossentropy-function) as loss function of our network output and optimized it with [RMSprop](https://keras.io/api/optimizers/rmsprop/) momentum optimizer and learning rate = 2e-5. [Accuracy](https://keras.io/api/metrics/accuracy_metrics/) has been chosen as a quality metrics.

![12](https://user-images.githubusercontent.com/44669029/142090489-eb92213a-6b2d-4622-892b-e5a309e878b1.png)

- Then the last 3 convolution layers of VGG16 were unfreezed and that part of the convolution base with pretrained classification layers had been training for 100 epochs with the learning rate cutted by half

![34](https://user-images.githubusercontent.com/44669029/142092070-b929f1ea-4eb0-44a5-b004-351b47e77b0d.png)

#### Evaluation results

As you can see [there](https://github.com/meat-app-hack/research-and-training-net/blob/main/classification_eval.ipynb)

```python
test_loss = 1.1514962352521252e-05
test_acc = 1.0
```

#### How to use MeatNet

For more detailes about virtual environment installation and using the model check [there](https://github.com/meat-app-hack/nft-predictor)

#### Useful links

- For the further NFT market analysis [see also this](https://www.kaggle.com/simiotic/ethereum-nft-analysis). Top 16.71% of NFT holders control 80.98% of NFTs [source](https://github.com/bugout-dev/moonstream/blob/main/datasets/nfts/papers/ethereum-nfts.pdf)
- Vision-based Real Estate Price Estimation implementation [tutorial with code](https://www.pyimagesearch.com/2019/01/21/regression-with-keras/)
- About data preprocessing for good loss convergence [link](https://machinelearningmastery.com/how-to-normalize-center-and-standardize-images-with-the-imagedatagenerator-in-keras/)



