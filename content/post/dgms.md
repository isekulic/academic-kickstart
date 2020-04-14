+++
title = "I learned something about Variational Inference in NLP"
date = 2018-12-08T19:30:04+01:00
draft = false
math = true

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["NLP"]
categories = []

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

Last week I had a chance to attend a truly great 2-day tutorial by [Philip Schultz](https://github.com/philschultz) and [Wilker Aziz](https://wilkeraziz.github.io/). It was held in Mathematikon, Heidelberg and the guys really did an amazing job. You can find the slides and a practice notebook on the tutorial’s official [github page](https://github.com/philschulz/VITutorial). 

This was my first experience with **Variational Inference** and **Deep Generative Networks**, so my head was spinning from the start. I tried to keep up as long as I could, finally losing grip on the second day. Nevertheless, I managed to gather my thoughts over the weekend, by going through [my notes](/files/vitutorial_notes.pdf) and finishing the coding part of the tutorial. You can find the solved jupyter notebook at my [github](https://github.com/isekulic/VITutorial). This post is an attempt to describe what I learned at a very high level, and in the process, wrap my head around it. The post will mostly be focused on **Variational Autoencoders** (VAE).

### Why VAE?
One of the most obvious reasons to turn to variational inference is their ability to find the underlying (latent) distribution of data, without the need for the data to be labeled.
This is not only important because the majority of available data in the world is not labeled, but also, in many scientists' opinions, is a way towards a (more) general artificial intelligence.
Knowing the underlying distribution of our data can help us distinguish different samples, and at the same time learn specific aspects of the data.
We know about the autoencoder's ability to learn the latent variables that can represent data, so why the need for VI?
Well, Variational Autoencoders are much more than standard autoencoders, since they learn the real distribution which the data cames from, giving us the ability to create new samples by sampling that distribution -- meaning they are a part of generative models family.

### What is VAE?
To start off, it's important to know what Generative Models are.
 A GM is any model of the joint probability distribution on $P(X, Z)$, with $X$ and $Z$ being random variables, observable and target variable, respectively.
 Another two important terms are **the likelihood** of observed data given the underlying (target) distribution $z$: $p(x|z)$, and **the prior** over $Z$: $p(z)$.
 By applying the good old Bayes rule, we find our goal to be computing **the posterior** p(z|x) = p(x|z)p(z), which is often impossible due to the unknown functional form of the posterior, or intractable computation.

 This is where **Variational Inference** comes in! We approximate uncomputable $p(z|x)$ by an auxiliary distribution $q(z)$ that is as close as possible to $p(z|x)$ and computable.
 Closeness of two distributions p and q is given with **Kullback-Leibler divergence** $KL(q || p)$, which is one of the backbones of VI.
 We won't go into explaining KL-divergence here, just note that it is asymetric and always $>= 0$. You can find a detailed explanation [here](https://towardsdatascience.com/demystifying-kl-divergence-7ebe4317ee68).
 
### How does it work?
As in standard autoencoders, we can think of our model's architecture as encoder-decoder networks.
We have a **generator (decoder)** part of our model, which is used to generate samples $x$ from the latent representation $z$. It is defined as $p(x|z,\theta)$, where \theta are parameters of a neural network.
Since everything in VAE is probabilistic, we are actually modeling mean $\mu\_{x|z}$ and covariance $\Sigma\_{x|z}$ of $p(x|z)$, assuming we chose Gaussian as our target distribution (we can chose whichever distribution makes sense).
So, essentialy, we are always **modeling the parameters of distributions**.

Ok, but how do we get the $z$? We use an **inference (encoder)** network to model mean and covariance of $p(z|x,\lambda)$, where $\lambda$ are the parameters of an inference neural network.
Then we can sample from the distribution defined by $\mu\_{z|x}$ and $\Sigma\_{z|x}$ and get the latent representation $z$, that we then use as input to generator network.

### All together
Given the data $x$, we use infrence network to model the latent distribution $p(z|x,\lambda)$. From that distribution, we sample $z$ and using generator network model the likelihood $p(x|z,\theta)$.
But, how to we train both parts together?
We have two parts of the loss function, one maximizing the likelihood of original input being reconstructed, and other forcing approximate posterior distribution in inference network close to prior (close means that we use KL-divergence).
Training is actually maximizing the **ELBO** (Evidence Lower BOund), which we'll not go into here, but you can find its derivation in links below.
Another important component is the **reparametrization trick**, which we use to make our complete network tractable, so we can backpropagate easily. In a nutshell, it just rewrites the problem so the distribution with respect to which we take the gradient is independent of network parameters, by using $\mathcal{N}(0, I)$.


### Cool references
If you are interested in learning more, and I'm sure you are, I'd recomend some of the following references:

* [Arxiv Insights'](https://www.youtube.com/watch?v=9zKuYvjFFS8) short, but great overview of VAEs.

* [VAE tutorial](https://arxiv.org/abs/1606.05908) by Carl Doersch.

* [Ali Ghodsi's lecture](https://youtu.be/uaaqyVS9-rM) that provides clear and intuitive explanation of all the math in VAEs.

* [Stanford's lecture](https://www.youtube.com/watch?v=5WoItGTWV54&t=2703s) about generative models (great pictures).

* [Yoshua Bengio's talk](https://youtu.be/Yr1mOzC93xs) on disentangled representations and the future of AI.

* [Blei et al. (2016) paper](https://arxiv.org/abs/1601.00670) on Variational Inference.

* [Kucukelbir et al. (2017) paper](http://jmlr.org/papers/v18/16-107.html) on Automatic Differentiation Variational Inference.
 
