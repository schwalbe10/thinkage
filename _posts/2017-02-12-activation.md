---
layout: post
title: "Deep Learning 2 - Introduce the activation functions for neural network"
date:  2017-02-12

tags:
- AI
- Deep Learning
- Python
---

Before we learn neural network, it is better to understand an activation function which converts input into output. Below is the other form of the perceptron equation in [Deep Learning 1](https://schwalbe10.github.io/thinkage/2017/01/21/perceptron.html).

$$
\begin{equation}
    y = h ( w_0 + w_1x_1 + w_2x_2 )
\end{equation}
$$

$$
\begin{eqnarray*}
    h(x) &=& \left\{
        \begin{array}{l}
            0 & ( x \leqq 0) \\
            1 & ( x > 0)
        \end{array}
    \right.
\end{eqnarray*}
$$

$$ h(x) $$ is the step function that is the simplest one. There are other common functions used for deep learning.

## Sigmoid Function

\begin{equation}
    h(x) = \frac{1}{1+exp(-x)}
\end{equation}

## Reflected Liner Unit (ReLU)

$$
\begin{eqnarray*}
    h(x) &=& \left\{
        \begin{array}{l}
            0 & ( x \leqq 0) \\
            x & ( x > 0)
        \end{array}
    \right.
\end{eqnarray*}
$$

They are non-linear functions, and it is important for neural network. This figure shows the functions.

 ![activation-function]({{site.github.url}}/images/posts/activation-function.png)

You can plot it by the following code.

~~~ python
import numpy as np
import matplotlib.pylab as plt


def step(x):
    return np.array(x > 0, dtype=np.int)

def sigmoid(x):
    return 1 / (1 + np.exp(-x))

def relu(x):
    return np.maximum(0, x)

x = np.arange(-5.0, 5.0, 0.1)
y_step = step(x)
y_sigmoid = sigmoid(x)
y_relu = relu(x)

plt.plot(x, y_step, label='Step', color='k', lw=1, linestyle=None)
plt.plot(x, y_sigmoid, label='Sigmoid', color='k', lw=1, ls='--')
plt.plot(x, y_relu, label='ReLU', color='k', lw=1, linestyle='-.')
plt.ylim(-0.1, 1.1)
plt.legend()
plt.show()
~~~

*The sample code is [here](https://github.com/schwalbe10/ThinkageDeepLearning).*

### Reference

<div class="list">
  <ul>
    <li><a href="http://cs231n.github.io/neural-networks-1/">Convolutional Neural Networks for Visual Recognition</a></li>
    <li><a href="https://www.amazon.co.jp/gp/product/4873117585/ref=as_li_tf_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117585&linkCode=as2&tag=schwalbe0d-22">Deep Learning From Scratch (Japanese)</a></li>
  </ul>
</div>
