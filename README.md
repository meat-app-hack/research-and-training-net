### Research and training Neural Net pipeline

#### Research

Price estimation of some product depending on many factors is a complicated task if it isn't an everyday buy/sell case like food in a local store. The task is even more sophisticated if you don't have instant physical access to the product and you can only use visual information or the product itself is an image. For such use cases it is good practice to avoid some human-factors, speculative and misleading intentions with delegating the bottleneck point of buy/sell to machine algorithms. We have researched the possibility of using Neural Nets for that algorithm.

The Deep Learning approach of image-to-price task is not commonly used in the market yet, but there are examples of some use cases. For example [Vehicle Price Prediction using Visual Features](https://arxiv.org/abs/1803.11227) and [Vision-based Real Estate Price Estimation](https://www.researchgate.net/publication/318528081_Vision-based_Real_Estate_Price_Estimation). 

Vehicle Price Prediction using Visual Features paper propose the [Linear Regression](https://en.wikipedia.org/wiki/Linear_regression) baseline for image-to-price task. Baseline model pipeline is VGG16 feature extraction + Principle Component Analysis ([PCA](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)) of image low-level features then few fully-connected layers with one neuron as output for linear regression process on the image features information. Our research leads us to believe that Linear Regression on the image features of NFT tokens isn't working well. That shows us only the average price of the whole dataset. The result can be compared to linear regression on random noise there is no connection between image low-rank features and the price BUT (!) it turns out that the price is strongly related to the belonging of the image to a particular collection or similarity with such collections. For the purpose of evaluating images belonging to precize collection or similarity with those we developed a classification neural network.

In order of participation TDeFi Business Hackathon we are proposing to your attention MeatNet🥩 a neural net that do price prediction of NFT image


#### Data parsing
- NFT token address, token id, current market values parsed from SQLite [database](https://www.kaggle.com/simiotic/ethereum-nfts)
- Image data parsed via indexed database of [Infura API](https://infura.io/)

Python scripts for folowing those steps and further info you can find [there](https://github.com/meat-app-hack/nft-data-parser). Another option for NFT image parse directly from blockchain on TypeScript is [there](https://github.com/meat-app-hack/zora-nft-data-parser)

#### Data preprocessing

#### Neural Net Architecture

VGG16 feature extractor backbone with Fully-connected and classification layer is our complete design


![image](https://user-images.githubusercontent.com/44669029/142066229-aaf63bac-0a6d-442b-809c-2acb2f74549b.png)

![image](https://user-images.githubusercontent.com/44669029/142066573-6e785095-cd13-42f8-8ced-debacb966b90.png)




#### Hyperparameters, methrics 

#### Training process

- The easier the better. Using [ImageNet](https://www.image-net.org/) predtrained VGG16 backbone for feature extraction as a first step we did 3-epochs predtraining of our last fully-connected layer and classification layer. We used [Categorical Crossentropy](https://keras.io/api/losses/probabilistic_losses/#categorical_crossentropy-function) as loss function of our network output and optimized it with [RMSprop](https://keras.io/api/optimizers/rmsprop/) momentum optimizer and learning rate = 2e-5. [Accuracy](https://keras.io/api/metrics/accuracy_metrics/) has been chosen as a quality metrics. 

![12](https://user-images.githubusercontent.com/44669029/142090489-eb92213a-6b2d-4622-892b-e5a309e878b1.png)

- Then



#### Evaluation results



For the further NFT market analysis [see also](https://www.kaggle.com/simiotic/ethereum-nft-analysis)
