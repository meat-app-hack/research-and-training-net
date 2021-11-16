### Research and training Neural Net pipeline

#### Research

Price estimation of some product depending on many factors is a complicated task if it isn't evetyday buy/sell case like food in local store. 

There Deep Learning approach of image to price task is not commonly used practice yet on market, but there are examples of  some use cases. For example [Vehicle Price Prediction using Visual Features](https://arxiv.org/abs/1803.11227) and [Vision-based Real Estate Price Estimation](https://www.researchgate.net/publication/318528081_Vision-based_Real_Estate_Price_Estimation).

For the further nft market analysis [see also](https://www.kaggle.com/simiotic/ethereum-nft-analysis)

#### Data parsing
- NFT token address, token id, current market values parsed from SQLite [database](https://www.kaggle.com/simiotic/ethereum-nfts)
- Image data parsed via indexed database of [Infura API](https://infura.io/)

Python scripts for folowing those steps and further info you can find [there](https://github.com/meat-app-hack/nft-data-parser). Another option for nft image parse directly from blockchain on TypeScript is [there](https://github.com/meat-app-hack/zora-nft-data-parser)

#### Data preprocessing

#### Neural Net Architecture

#### Hyperparameters, methrics and training process 

#### Evaluation results
