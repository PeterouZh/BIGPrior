# BIGPrior: Towards Decoupling Learned Prior Hallucination and Data Fidelity in Image Restoration

**Authors**: [Majed El Helou](https://majedelhelou.github.io/), and Sabine Süsstrunk

![Python 3.7](https://img.shields.io/badge/python-3.7-green.svg?style=plastic)
![pytorch 1.1.0](https://img.shields.io/badge/pytorch-1.1.0-green.svg?style=plastic)
![CUDA 10.1](https://camo.githubusercontent.com/5e1f2e59c9910aa4426791d95a714f1c90679f5a/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f637564612d31302e312d677265656e2e7376673f7374796c653d706c6173746963)

{Note: repo under construction, paper under submission}

#### [[Paper to appear]](404)

> **Abstract:** *Image restoration, such as denoising, inpainting, colorization, etc. encompasses fundamental image processing tasks that have been addressed with different algorithms and deep learning methods. Classical image restoration algorithms leverage a variety of priors, either implicitly or explicitly. Their priors are hand-designed and their corresponding weights are heuristically assigned. Thus, deep learning methods often produce superior image restoration quality. Deep networks are, however, capable of strong and hardly-predictable hallucinations of the data to be restored. Networks jointly and implicitly learn to be faithful to the observed data while learning an image prior, and the separation of original data and hallucinated data downstream is then not possible. This limits their wide-spread adoption in image restoration applications. Furthermore, it is often the hallucinated part that is victim to degradation-model overfitting.*
>
> *We present an approach with decoupled network-prior based hallucination and data fidelity terms. We refer to our framework as the Bayesian Integration of a Generative Prior (BIGPrior). Our BIGPrior method is rooted in a Bayesian restoration framework, and tightly connected to classical restoration methods. In fact, our approach can be viewed as a generalization of a large family of classical restoration algorithms. We leverage a recent network inversion method to extract image prior information from a generative network. We show on image colorization, inpainting, and denoising that our framework consistently improves the prior results through good integration of data fidelity. Our method, though partly reliant on the quality of the generative network inversion, is competitive with state-of-the-art supervised and task-specific restoration methods. It also provides an additional metric that sets forth the degree of prior reliance per pixel. Indeed, the per pixel contributions of the decoupled data fidelity and prior terms are readily available in our proposed framework.*

**Key take-aways:** our paper presents a learning-based restoration framework that forms a _generalization of various families of classical methods_. It is both tightly connected with Bayesian estimation upon which it builds, and also to classical dictionary methods. Our BIGPrior makes the _explicit integration of learned-network priors possible_, notably a generative-network prior. Its biggest advantage is that, by decoupling data fidelity and prior hallucination, it structurally provides a _per pixel fusion metric_ that determines the contribution of each. This can be important both for end users and for various downstream applications. We hope this work will foster future learning methods with clearly decoupled network hallucinations, both for interpretability, reliability, and to safeguard against the hazards of black-box restoration. 


## BIGPrior pipeline
The figure below illustrates the BIGPrior pipeline, with a generative-network inversion for the learned prior. 
<p align="center">
  <img src="readme_figures/pipeline.png" width="600px"/>
</p>


### Repo structure overview
All code is in the `code` directory, and _input_ data is in the `data` folder. The `net_data` directory stores the network weights per epoch (along with many other trackers and all experiment parameters), it uses an automated index incrementation strategy on top of the experiment name for avoiding over-writing. We generate a lot of intermediate data for the different experiments, and along with the final outputs, these are written in `inter_data`.


### Setting up the data


### Running the generative inversion
The generative inversion we use is based on [mGAN](https://github.com/genforce/mganprior) but we do some modifications to their code, which is why we have our own version in this repository.

**(1)** You need to download the pre-trained generative networks (we use PGGAN), and put the `pretrain` folder inside `code/mganprior/models/`. You can download them from the original repo, or mGAN's, or from our link [right here](https://drive.google.com/drive/folders/1nWk76mPtPxWrd9-tPJA3H7zyQmHLYznQ?usp=sharing).

**(2)** *(recommended)* You might face some bugs with the perceptual vgg-based loss due to caching, if you run parallel experiments or if you run on remote servers. We recommend you cache the pretrained model. To do this, first download [vgg model vgg16-397923af.pth](https://drive.google.com/file/d/1wp2MKTNT7wqgcZhCDTJYEZ46oYbdopsG/view?usp=sharing) and paste it inside `cache/torch/checkpoints/`, then before starting an experiment run:
```
export XDG_CACHE_HOME=cache/
```

**(3)** We compiled the commands for all experiments in the bash file `runall_mGAN.sh`, you can find the templates inside to rerun each experiment.


### Training for $\phi$



### Testing with our pretrained models

