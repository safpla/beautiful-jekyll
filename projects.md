---
layout: page
title: Projects
subtitle: AutoLoss, Focus.
---

# AutoLoss {#autoLoss}
SAILING LAB, Carnegie Mellon University, 2018.3-. Advisor: Prof. Eric Xing. [Paper]

***Abstract***

Many machine learning problems involve iteratively and alternately optimizing different task objectives with respect to different sets of parameters. Appropriately scheduling the optimization of a task objective or a set of parameters is usually crucial to the quality of convergence. In this paper, we present AutoLoss, a meta-learning framework that **automatically learns and determines the optimization schedule**. AutoLoss provides a generic way to represent and learn the discrete optimization schedule from metadata, allows for a dynamic and data-driven schedule in ML problems that involve alternating updates of different parameters or from different loss objectives.

***Architecture***

<img src="/img/AutoLoss/architecture.png" width="60%" height="24%">

>*Figure 1: AutoLoss Architecture*

***Results***

**1. Design the optimization schedule of L1 regularization**

At each training step, meta-controller tells the task model whether to minimize the objective function (mse loss in d-ary regression and cross-entropy in MLP classification) or minimize L1-loss. Baseline is a linear combination of objective function and L1-loss.

<img src="/img/AutoLoss/l1_regularization.PNG" width="100%" height="35%">
>*Figure 2: AutoLoss reaches good convergence regardless of λ for both d-ary regression (left) and MLP classification (right) with L1 regularization.*

**2. Design the optimization schedule of GAN on MNIST dataset**

At each training step, meta-controller tells the task model whether to update the discriminator or to update the generator. Baseline models are vanilla GAN with pre-define ratio between updating steps of discriminator and generator. 

<img src="/img/AutoLoss/GAN_MNIST.PNG" width="100%" height="20%">
>*Figure 3: The training progress (<a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{IS}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{IS}" title="\mathcal{IS}" /></a> vs. epochs) of four best performed baselines compared with AutoLoss. If an instance does not improve for 20 Epochs, we terminate its training and regard it as converged.*

**3. Transferability**

We did three set of experiments to evaluate the transferability of our meta-controller.

**Transfer to different models.** First we fix the architecture of the task model (GAN) and train a meta-controller.  Then we use the meta-controller to guide the training of a new GAN from scratch, on the same dataset (MNIST). We compare the averaged converged <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{IS}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{IS}" title="\mathcal{IS}" /></a> of the trained model between with and without the meta-controller, as in Figure 4(b).

**Transfer to different data distributions.** We first train a meta-controller for a task model on one dataset. We then fix the parameters of the controller, and use it to guide the training of the same task model from scratch, but on other dataset with different distributions. We compare the training of AutoLoss guided model with vanilla one. We report the comparison results in Figure 4(a) and Figure4(c) on two tasks: (a) MLP classifier, that we train the controller using a dataset generated following a process. We then generate another three sets of synthetic samples using different specifications of the process. (c) GANs, where we first train a controller for digit generation on MNIST, and then use the controller to guide the training of the same GAN architecture on CIFAR-10.

<img src="/img/AutoLoss/transfer.PNG" width="60%" height="40%">

>*Figure 4: (a) Comparing the MLP classification results for the data transfer experiments. DGS represents Dense Grid Search. (b) Comparing the final convergence (in term of <a href="https://www.codecogs.com/eqnedit.php?latex=\mathcal{IS}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathcal{IS}" title="\mathcal{IS}" /></a>) of randomly sampled DCGAN architectures trained with and without a trained meta-controller. Clearly, we see AutoLoss outperforms DCGAN in 16 out of 20 architectures. (c) The training progress comparison of a vanilla GAN and a AutoLoss-guided GAN on CIFAR-10.*

***Future Work***

We are currently applying AutoLoss to several practical applications.

**1. AutoDrive:** We have several experts to provide supervision signal to train a driving agent. However, all experts are imperfect. Our goal is to train a meta-controller to tell the task model which expert to use at each training step.

**2. Curriculum Learning:** We use AutoLoss to automaticly design the syllabus.

**3. Multi-task Learning:** We use AutoLoss to automaticly design the schedule of training and knowledge transfering in multi-task learning process.

# Chinese Named Entity Recognition with Self-Attention {#t2t}
Deeplycurious.ai, Beijing, 2017.9-2018.2

***Abstract***

We proposed an self-attention based sequence labeling model and applied it to a Chinese Named Entity Recognition task. Our model can directly capture the relationships between two tokens regardless of their distance. Our model outperforms state of the art on MSRA bakeoff3 dataset and achieves a better performance on the company's internal dataset.

***Architecture***

<img src="/img/t2t/architecture.png" width="70%" height="60%">

>*Figure 5: The model has N idential layers (each contains a self-attention sub-layer and a feed forward sub-layer), a softmax classification layer with feed back mechanism (green arrows), and an object memory to store recognized entities (red arrows) and maintain global consistence (blue arrows).*

***Results***

<img src="/img/t2t/results.png" width="80%" height="30%">

>*Figure 6: Compared with two baselines. (Dong et al, 2016. "Character-Based LSTM-CRT with Radical-Level Features for Chinese Named Entity Recognition." Lecture Notes in Computer Science)*

# Document Classification with Paragraph Reasoning {#focus}
Deeplycurious.ai, Beijing, 2017.9-2018.2

***Abstract***

In document classification tasks, sometimes we need to deal with documnets that contain contradicting opinions. For example, a court verdict may contains plaintiff's claims and defendant's defenses which are usually contradictory to each other. Traditional deep learning methods, no matter CNN or RNN, usually take the document as a whole, neglect the contradiction between paragraphs. We proposed a document classification model with a paragraph reasoning module to solve feature conflicts between paragraphs. We use a hierarchical structure to construct our network. At sentence level, we use a CNN to extract the representation of each sentence. At paragraph level, we use the representation of sentences to make prediction about each paragraph. The network could be a CNN, RNN or simply pooling layer. At document level, predictions of all paragraphs are combined together by a resaoning module to give the final classification label.

***Architecture***

<img src="/img/focus/architecture.png" width="80%" height="40%">

>*Figure 7: The architecture of our model. The paragragh level network is simply a max pooling layer. The reasoning module here is a 2-layer fully-connected network. We also have label information about each sentence. To exploit this, we provide supervision not only at document level, but also at sentence level, i.e. the objective function is a linear combination of document level loss and sentence level loss.



[Paper]: /paper/autoLoss.pdf

