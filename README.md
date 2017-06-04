# Semi-supervised learning GAN in Tensorflow

This is my [Tensorflow](https://www.tensorflow.org/) implementation of **Semi-supervised Learning Generative Adversarial Networks** proposed in the paper [Improved Techniques for Training GANs](http://arxiv.org/abs/1606.03498). The goal of this work is exploiting the samples generated by GAN generators to boost the performance of image classification tasks by improving generalization.

In sum, **the main idea** is training a network playing the roles of both a classifier performing image classification task as well as a discriminator trained to distinguish samples from the generator distribution from real data. To be more specific, the classifier/disciminator takes an image as input and classified it into $n+1$ class, where $n$ is the number of classes of a classification task. True samples are classified into the first $n$ classes and generated samples are classified into the $n+1$-th class Therefore, the loss of this multi-task learning framework can be decomposed into the **supervised loss** 

<img src="figure/s_loss.png" height="25"/>, 

and the **GAN loss** of a discriminator

<img src="figure/gan_loss.png" height="25"/>, 

During the training phase, we jointly minimze the total loss obtained by simply combining the two losses together.

Note that this implementation only follow the main idea of the original paper while differing a lot in implementation details such as model architectures, hyperparameters, applied optimizer, etc. Also, some useful training tricks applied to this implementation are stated at the end of this README.

<img src="figure/example.png" height="200"/>.

## Prerequisites

- Python 2.7 or Python 3.3+
- [Tensorflow 1.0.0](https://github.com/tensorflow/tensorflow/tree/r1.0)
- [SciPy](http://www.scipy.org/install.html)
- [NumPy](http://www.numpy.org/)

## Usage

Download datasets with:

    $ python download.py --dataset mnist cifar

To train a model with downloaded dataset:

    $ python trainer.py --dataset mnist
    $ python trainer.py --dataset cifar

To test with an existing model:

    $ python eval.py --dataset mnist --checkpoint ckpt_dir
    $ python eval.py --dataset cifar --checkpoint ckpt_dir

Or, you can use your own dataset by:

    $ mkdir data/YOUR_DATASET
    ... add images to data/YOUR_DATASET ...
    $ python trainer.py --dataset YOUR_DATASET --input_height h --input_width w --num_class c
    $ python evaler.py --dataset YOUR_DATASET --input_height h --input_width w --num_class c

## Results

### MNIST

### CIFAR10

More results can be found [here](#) and [here](#).

## Training details

Details of the loss of Discriminator and Generator.

Details of the histogram of true and fake result of Discriminator.

## Training tricks

* To avoid the fast convergence of D (discriminator) network, G (generator) network is updated twice for each D network update.
* One-side label smoothing is applied

## Related work
* [Unsupervised and Semi-supervised Learning with Categorical Generative Adversarial Networks](https://arxiv.org/abs/1511.06390)
* [Semi-Supervised Learning with Generative Adversarial Networks](https://arxiv.org/abs/1606.01583)
* [Good Semi-supervised Learning that Requires a Bad GAN](https://arxiv.org/abs/1705.09783)

## Author

Shao-Hua Sun / [@shaohua0116](http://shaohua0116.github.io/)

