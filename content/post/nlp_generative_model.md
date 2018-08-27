+++
title = "Generative Model for text: An overview of recent advancements"
date = 2018-08-26T14:54:06+08:00
draft = true

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []
math = true
# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = false

+++
{{% toc %}}

# Introduction
The recent progress of generative adversarial network (GAN) has shown siginificant imporvment of learning latent representation of high-dimensional continuous data such as images and videos in vision domain. Many amazing applications such as video synthesis andvisual style transfer are based on the capability of GAN.


With these successful applications in vision domain, it is natural to ask: 
Can we apply similar techniques to language to achieve similar results?

Unfortunately, compared with hundreds of development of GAN[link here]() and its applications, only a few progress has been made for the text. In general, it is the discrete structure of text that makes apply GAN to language inappropriate, which is designed for continuous data.  According to [Goodfellow](https://www.reddit.com/r/MachineLearning/comments/40ldq6/generative_adversarial_networks_for_text/), the generator learn how to slightly change the synethetic data through the gradient information from the discriminator. Such slight change is only meaningful for continuous data. For example, it is resaonable to change a pixel value from 1 to 1 + 0.001 while it is not for changing "penguin" to  "penguin" + 0.001.

Despite of the difficulty, many methods have been proposed in the last two years to address this issue and some of them have many interesting results. In this article, I will give an overview of these methods, issue about evaluation and their applications.

# Model for text generation
## Improved training of GAN
Perhaps the most basic task to study the capability of generating meaningful text is to generate simple character with certain pattern. Kusner et al. [1] propose to approximate the discrete output distribution by Gumbel-softmax distribution, which is a conttious approximation of softmax function parameterized by $\tau$. For each time step $t$, the output $y_{t}$ is approximated by

\begin{align}
\boldsymbol{y}_{i} = \textrm{softmax}(\frac{h_i + g_i}{\tau}), i = 1,...,k~,
\end{align}
where $g_i$
## Policy gradient
## Variational Autoencoder
## Autoencoder
## Alternative decoding objective

# Evaluation
# Application
## Image to text generation
## (Visual) Dialog generation
## Style tranfer for text
# Final Words


