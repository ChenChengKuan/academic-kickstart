+++
title = "Some thoughts about NeurIPS 2018"
date = 2018-12-16T20:49:21+08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = true

+++

This post is a quick note about some interesting papers/workshop/talk I found when I go through the program NeurIPS 2018. I also jot down some of my thougts. The content mainly focuses on text generatiton, and molecule design (IMO, these two topics share some similarity) and the list is still ongoing…
<!--more-->

## Text generation
### Papers

#### A Retrieve-and-Edit Framework for Predicting Structured Outputs (oral)
Authors: Tatsunori Hashimoto, Kelvin Guu, Yonatan Oren, Percy Liang<br>
**Summary and thoughts:**The authors generalize the Retrieve-and-Edit framework from unconditional text generation [1] to the conditional program synthesis. The key insight is that it is easier to edit than generate from scratch for complex structured data. To my best knowledge, retrieve something then edit/generate is a trending text generation method this year, it seems to me that people found that generating text from scratch is not that promising especially when our output is complex. In this year, I noticed that such framework (or similar idea) had been successfully applied to medical report generation[2], (controllable) story generation[3], text generation[1] and program generation (this work).<br>

**Question:** Can we also borrow this insight to generate more complex structure such as molecule? For example, retrieve some similar molecules, then edit it to the one with our desired attribute, or first create or retrieve some "template" of molecules then refine the final output based on this template? IMO, this is a promising direction as the model don't need to learn everything from scratch.

[1] Kelvin Guu, Tatsunori B Hashimoto, Yonatan Oren, Percy Liang. "Generating sentences by editing prototypes". ACL2018<br>
[2] Christy Y. Li, Xiaodan Liang, Zhiting Hu, Eric P. Xing. "Hybrid Retrieval-Generation Reinforced Agent for Medical Image Report Generation". NeurIPS2018<br>
[3] Lili Yao, Nanyun Peng, Weischedel Ralph, Kevin Knight, Dongyan Zhao, Rui Yan. "Plan-And-Write: Towards Better Automatic Storytelling". AAAI2019<br>

#### Unsupervised Text Style Transfer using Language Models as Discriminators
Authors: Zichao Yang, Zhiting Hu, Chris Dyer, Eric P. Xing, Taylor Berg-Kirkpatrick1<br>
**Summary and thoughts:** Admittedly, I admire the first two authors who have done many works about the generative model in text, so I biasedly choose this work. The key to this work is that they introduce to use language model as the discriminator, which I think is more natural than the previous binary and ranking score.

#### Content preserving text generation with attribute controls 
Authors: Lajanugen Logeswaran, Honglak Lee, Samy Bengio<br>
**Summary and thoughts:** The technique: Back-Translation has got hotter and hotter since it got success in unsupervised machine translation and won them best paper award in EMNLP2018. This paper applied this technique to create a model that can control multiple attributes of generated text (and the combination of them) at the same time. This work is the first model that can do this. Quick follow-up work in ICLR2019: Multiple-Attribute Text Rewriting from MILA is also based on this techniques and get stronger performance, which confirms me to put back-translation to my toolbox of attribute control of discrete data.<br>

One interesting fact: The conclusion of this paper and the one from MILA is somehow contradicted lol.

## Workshop: Machine Learning for Molecules and Materials
I found so many interesting stuff in this workshop! Below are some of them

### Talk:Learning protein structure with a differentiable simulator
**Summary and thoughts:** This talk introduces how to combine traditional simulation approach and new machine learning tool to get the benefit of both worlds to address the protein folding problem. In short, the author incorporates the simulator as a block into the end to end training procedure. A neural network is used to learn the weight of a potential function jointly with a simulator that draws the sample from this function to calculate the loss. 

I was motivated to understand such topic after reading [Machine Learning for Drug Discovery in a Nutshell](https://medium.com/@stefan.schroedl/machine-learning-for-drug-discovery-in-a-nutshell-part-i-24ae3f65c135) several weeks ago as well as the achievement of [AlphaFold](https://deepmind.com/blog/alphafold/). I found myself still lack enough domain-knowhow and the traditional methods in this field. Gotta find some time to learn more. By the way, this work is also submitted to ICLR2019 ([here](https://openreview.net/pdf?id=Byg3y3C9Km))

### Paper: Powerful, transferable representations for molecules through intelligent task selection in deep multitask networks	
Authors Clyde Fare, Lukas Turcani, Edward O. Pyzer-Knapp<br>
**Summary and thoughts:** This paper uses multi-task learning to learn a more generalizable representation. At first glance, I found the idea is similar to the Taxanomy[1], which make me rethink my original plan to learn a common representation. I am still thinking about learning a shared representation like "See, Hear, and Read: Deep Aligned Representations"

**Question:** A question occurs to my mind is that does the task in chemical/material domain exist a hierarchy of difficulty? For example, some tasks can be solved easier while some are difficult. A good solution for the easier task can help solve the more difficult task. The reason why I ask myself this question is that, in NLP, such hierarchy exists and we can train a model altogether to solve all tasks from easy  (e.g., POS-tag, chunking) to difficult (e.g., reasoning, entailment) end to end like this paper [2]. The advantage of such a training pipeline is that the representation/model learned in the lower level task can be jointly tailored to the more difficult task, which makes the representation more robust. 

[1] Amir Zamir, Alexander Sax, William Shen, Leonidas Guibas, Jitendra Malik, Silvio Savarese. "
Taskonomy: Disentangling Task Transfer Learning". CVPR2018.
[2] Kazuma Hashimoto, Caiming Xiong, Yoshimasa Tsuruoka, Richard Socher. "A Joint Many-Task Model: Growing a Neural Network for Multiple NLP Tasks". EMNLP2017.

## Paper
### Graph Convolutional Policy Network for Goal-Directed Molecular Graph Generation (Spotlight)
Authors:Jiaxuan You, Bowen Liu, Rex Ying, Vijay Pande, Jure Leskovec<br>
**Summary and thoughts** This paper introduces graph convolutional network plus reinforcement learning to generate high validness molecule. They design an OpenAI environment for molecular and using PPO to train their agents. I must say I was mind-blowed by the improvement....and further amazed by the follow-up work in ICLR 2019 ([here](https://arxiv.org/abs/1812.01070)) from MIT ChemML group. It seems to me this is a fast-developing field. An open benchmark with a large dataset like [MOSES](https://github.com/molecularsets/moses) is needed to evaluate these new methods. Also, as pointed out in a [paper](https://chemrxiv.org/articles/Dataset_Bias_in_the_Natural_Sciences_A_Case_Study_in_Chemical_Reaction_Prediction_and_Synthesis_Design/7366973), mislabelled is not uncommon cases. Perhaps we also have to understand our data more to know whether our method can be applied in the wild.



