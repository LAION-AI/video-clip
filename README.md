# video-clip

We want to build a model that can understand video and text the same way CLIP can understand images and text. One big issue with training a model like this is the computational cost of running an entire video through a deep learning model. Our current approach to solving this issue is to build on top of the work that CLIP did and instead of modeling the temporal dimension in pixel space we want to model it in CLIP space by pooling together sequences of the CLIP embeddings of frames. Here are a few of our hypotheses as to why we think this approach will be succesful:

*  Re-using CLIP's understanding of imagery will make temporal modeling easier.
*  Modeling higher-level, coarse semantic sequences will improve long context video understanding.
*  Lower computational cost allows for more experimentation and therefore more refined algorithms.

Ref LAION project menu - https://github.com/LAION-AI/project-menu/issues/22

## Tools

### [video2numpy](https://github.com/iejMac/video2numpy):
video2numpy is a library for downloading and decoding videos into numpy arrays for further processing at large scale. Our goal of training a large contrastive represtenation learning model will require a lot of video data which is costly to download and decode. We built this library because it seems like a lot of projects could benefit from a tool like this so we hope members of those projects will come together to help developing this tool so we can all efficiently train large models on giant video datasets.

### [clip-video-encode](https://github.com/iejMac/clip-video-encode):
clip-video-encode is a library like video2numpy, however it performs an additional processing step of encoding the frames using a CLIP image encoder. The embedding sequences produced by clip-video-encode can be used for semantic search within videos as shown in [this example](https://github.com/iejMac/clip-video-encode/tree/main/examples/thing_detector). 

### Contributions:
If you'd like to contribute to video-clip tooling I suggest visiting the github pages of the tools and looking at the issues to see if there are any you'd like to solve.

## Datasets

Our plan to create the training dataset for video-clip is to combine the available dataset into one large frame_embedding-text dataset. You can find a list of datasets we plan on converting to our standard format [here](https://docs.google.com/document/d/12zYnjZabR2e17vPO2XpctIf1qUQeEX7kYC8GdDqWM-k/edit). The format is specified in [clip-video-encode/dataset](https://github.com/iejMac/clip-video-encode/tree/main/clip_video_encode/dataset) along with a few helpful scripts for converting datasets into it.

### Contributions:
Converting one of the datasets in the aformentioned document into our standard format using our tools is probably the lowest effort and highest impact thing you can help out with. Creating the dataset will likely take a lot of small efforts like these so picking out one dataset and guiding/tweaking the scripts to prepare them for our large training runs is very helpful and doesn't require a lot of expertise. You can find an example of how we did this with Kinetics700 at the bottom of [clip-video-encode/dataset](https://github.com/iejMac/clip-video-encode/tree/main/clip_video_encode/dataset)

## Modeling

There are a lot of potential methods of pooling together semantic frame embeddings to produce one global frame embedding. We investigaate them in [this repository](https://github.com/LAION-AI/temporal-embedding-aggregation). 


## Useful literature

* Video Swin Transformer
* Swin Transformer
* An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale
* TokenLearner: What Can 8 Learned Tokens Do for Images and Videos?
* Masked Feature Prediction for Self-Supervised Visual Pre-training
* BEIT: BERT Pre-Training of Image Transformers
* Multiview Transformers for Video Recognition
* SiT: Self-supervised vIsion Transformer
* Unsupervised Pre-Training of Image Features on Non-Curated Data
* Co-training Transformer with Videos and Images Improves Action Recognition
* Emerging Properties in Self-Supervised Vision Transformers
* Florence: A New Foundation Model for Computer Vision
* Swin Transformer V2: Scaling Up Capacity and Resolution
* Neural Machine Translation by Jointly Learning to Align and Translate
* MERLOT Reserve: Neural Script Knowledge through Vision and Language and Sound

### contrastive

https://arxiv.org/abs/2203.12602
https://github.com/MCG-NJU/VideoMAE
