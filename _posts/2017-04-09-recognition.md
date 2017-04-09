---
layout: post
title: "Deep Learning 4 - Recognize the handwritten digit"
date:  2017-04-09

tags:
- AI
- Deep Learning
- Python
---

If you've read my [deep learning posts]({{site.github.url}}/tags#Deep%20Learning), you could learn [a perceptron]({{site.github.url}}/2017/01/21/perceptron.html), [an activation function]({{site.github.url}}/2017/02/12/activation.html), and [the MNIST dataset]({{site.github.url}}/2017/03/05/mnist.html). Now, you can understand a multiple neural network.

![neural-network]({{site.github.url}}/images/posts/neural-network.png)

This is a 3-layer neural network. Input layer and output layer are same as a perceptron, and there are 2 hidden layers. Each neuron is connected across adjacent layers, but not within a layer.

Let's calculate accuracy for recognition of the MNIST dataset by using this network. The steps are as follows:

1. Get the MNIST dataset
1. Set the weight with [*sample_weight.pkl*](https://github.com/schwalbe10/ThinkageDeepLearning)
1. Transfer the information from input layer to output layer
1. Calculate the accuracy


<div class="filename"><span class="t">04_recognition.py</span></div>
``` python
import os
import numpy as np
import pickle
from mnist import load_mnist
from functions import sigmoid, softmax


def get_data():
    (x_train, t_train), (x_test, t_test) = load_mnist(normalize=True, flatten=True, one_hot_label=False)
    return x_test, t_test

def init_network():
    with open("sample_weight.pkl", 'rb') as f:
        network = pickle.load(f)
    return network

def predict(network, x):
    W1, W2, W3 = network['W1'], network['W2'], network['W3']
    b1, b2, b3 = network['b1'], network['b2'], network['b3']

    l = sigmoid(np.dot(x, W1) + b1)
    m = sigmoid(np.dot(l, W2) + b2)
    y = softmax(np.dot(m, W3) + b3)

    return y


x, t = get_data()
network = init_network()
accuracy_cnt = 0
for i in range(len(x)):
    y = predict(network, x[i])
    p = np.argmax(y)
    if p == t[i]:
        accuracy_cnt += 1

print("Accuracy:" + str(float(accuracy_cnt) / len(x)))
```

There is a new activation function, softmax, in *functions.py*:

<div class="filename"><span class="t">functions.py</span></div>
``` python
import numpy as np

def softmax(x):
    x = x - np.max(x)
    return np.exp(x) / np.sum(np.exp(x))
```

As you can see, this function is expressed by the following equation:

$$
\begin{eqnarray*}
    y_k &=& \frac{\exp(m_k)}{\displaystyle\sum^{n}_{i=1}\exp(m_i)} \\
        &=& \frac{\exp(m_k-m_{max})}{\displaystyle\sum^{n}_{i=1}\exp(m_i-m_{max})}
\end{eqnarray*}
$$

The first one is the definition, and the second one is for calculation to prevent an overflow by exponential functions. The softmax function is often used in the final layer of neural networks.

If you execute it, you can get the accuracy. This is forward propagation of neural networks.

```
python 04_recognition.py
Accuracy:0.9352
```

 You need to learn backward propagation to understand the learning process. Let's move to the next step!

*The sample code is [here](https://github.com/schwalbe10/ThinkageDeepLearning).*

### Reference

<div class="list">
  <ul>
    <li><a href="http://cs231n.github.io/neural-networks-1/">Convolutional Neural Networks for Visual Recognition</a></li>
    <li><a href="https://www.amazon.co.jp/gp/product/4873117585/ref=as_li_tf_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117585&linkCode=as2&tag=schwalbe0d-22">Deep Learning From Scratch (Japanese)</a></li>
  </ul>
</div>
