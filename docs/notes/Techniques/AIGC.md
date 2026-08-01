---
icon: fontawesome/brands/openai
tags: [Updating]
comments: true
---

# AIGC

## Autoencoder

<iframe width="560" height="315" src="https://www.youtube.com/embed/hZ4a4NgM3u0?si=HBp7dxa9p9SrFV--" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Ref: <https://lilianweng.github.io/posts/2018-08-12-vae/>

Autoencoder

- Learn an identity function
- An unsupervised way
- Reconstruct the original input
- Efficient and compressed representation

![Autoencoder](https://lilianweng.github.io/posts/2018-08-12-vae/autoencoder-architecture.png)

- Encoder translates the original high-dimensional input into a low-dimensional code, like Principal Component Analysis (PCA) or Matrix Factorization (MF)
- Decoder recovers the data from the code
- Metrics: Cross Entropy, Mean Squared Error (MSE)

### Denoising Autoencoder

- Risk of overfitting when #parameters > #data
- Partially corrupted by adding noises to or masking the input vector

![Denoising Autoencoder](https://lilianweng.github.io/posts/2018-08-12-vae/denoising-autoencoder-architecture.png)

- Motivated by the fact that humans can easily recognize an object or a scene even the view is partially occluded or corrupted
- Discover and capture relationship between dimensions
- Learning robust latent representation

### Variational Autoencoder (VAE)

Recap Bayes' theorem

<iframe width="560" height="315" src="https://www.youtube.com/embed/akClB1J6b28?si=3xaV78cvQUbTxpqe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### Vector Quantized Variational Autoencoder (VQ-VAE)

## Generative Adversarial Network (GAN)

Ref: <https://lilianweng.github.io/posts/2017-08-20-gan/>

## Diffusion Model

### Denoising Diffusion Probabilistic Model (DDPM)

### Latent Diffusion Model (LDM)

Ref: <https://lilianweng.github.io/posts/2021-07-11-diffusion-models/>

## Neural Radiance Field (NeRF)
