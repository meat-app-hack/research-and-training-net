### Research and training Neural Net pipeline

#### Research

Price estimation of some product depending on many factors is a complicated task if it isn't an everyday buy/sell case like food in a local store. The task is even more sophisticated if you don't have instant physical access to the product and you can only use visual information or the product itself is an image. For such use cases it is good practice to avoid some human-factors, speculative and misleading intentions with delegating the bottleneck point of buy/sell to machine algorithms. We have researched the possibility of using Neural Nets for that algorithm.

The Deep Learning approach of image to price task is not commonly used in the market yet, but there are examples of some use cases. For example [Vehicle Price Prediction using Visual Features](https://arxiv.org/abs/1803.11227) and [Vision-based Real Estate Price Estimation](https://www.researchgate.net/publication/318528081_Vision-based_Real_Estate_Price_Estimation). 

In order of participation TDeFi Business Hackathon we are proposing to your attention MeatNet🥩 a neural net that do price prediction of nft image


#### Data parsing
- NFT token address, token id, current market values parsed from SQLite [database](https://www.kaggle.com/simiotic/ethereum-nfts)
- Image data parsed via indexed database of [Infura API](https://infura.io/)

Python scripts for folowing those steps and further info you can find [there](https://github.com/meat-app-hack/nft-data-parser). Another option for nft image parse directly from blockchain on TypeScript is [there](https://github.com/meat-app-hack/zora-nft-data-parser)

#### Data preprocessing

#### Neural Net Architecture

![image](https://user-images.githubusercontent.com/44669029/142066229-aaf63bac-0a6d-442b-809c-2acb2f74549b.png)

![image](https://user-images.githubusercontent.com/44669029/142065880-f561c248-faf1-446d-b754-5e8d11896a37.png)

#### Hyperparameters, methrics and training process 

#### Evaluation results



For the further nft market analysis [see also](https://www.kaggle.com/simiotic/ethereum-nft-analysis)
