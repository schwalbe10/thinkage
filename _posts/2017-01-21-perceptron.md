---
layout: post
title: "Deep Learning 1 - Develop a logic gate by perceptron"
date:  2017-01-21

tags:
- AI
- Deep Learning
- Python
---

The perceptron is an algorithm that signals information from an input layer to an output layer. The figure shows the 2 inputs perceptron.

 ![perceptron]({{site.github.url}}/images/posts/perceptron.png)
w_0
$$ x_1, x_2 $$ are input signals, $$ y $$ is an output signal,  $$ w_0 $$ is a bias, and $$ w_1, w_2 $$ are weights. Signals are also called neurons or nodes. They output 1, only if the sum of inputs is over thresholds. In this case, the function is represented as follows:

$$
\begin{eqnarray*}
    y = \left\{
        \begin{array}{l}
            0 & ( w_0 + w_1x_1 + w_2x_2  \leqq 0) \\
            1 & ( w_0 + w_1x_1 + w_2x_2  > 0)
        \end{array}
    \right.
\end{eqnarray*}
$$

You can create a logic gate with this function. If $$ w_0=-1.5 $$, $$ w_1=1 $$, and $$  w_2=1 $$, it will be the AND gate. This is the truth table for AND, OR, and NAND. Check the values ($$ w_0, w_1, w_2 $$) for the OR and NAND gates by yourself!

|AND|OR|NAND|
|:--:|:--:|:--:|
| $$ x_1 $$  &nbsp; $$ x_2 $$  &nbsp; $$ y $$ | $$ x_1 $$ &nbsp; $$ x_2 $$ &nbsp; $$ y $$ | $$ x_1 $$ &nbsp; $$ x_2 $$ &nbsp; $$ y $$ |
| 0 &nbsp;&nbsp; 0 &nbsp;&nbsp; 0 | 0 &nbsp;&nbsp; 0 &nbsp;&nbsp; 0 | 0 &nbsp;&nbsp; 0 &nbsp;&nbsp; 1 |
| 1 &nbsp;&nbsp; 0 &nbsp;&nbsp; 0 | 1 &nbsp;&nbsp; 0 &nbsp;&nbsp; 0 | 1 &nbsp;&nbsp; 0 &nbsp;&nbsp; 1 |
| 0 &nbsp;&nbsp; 1 &nbsp;&nbsp; 0 | 0 &nbsp;&nbsp; 1 &nbsp;&nbsp; 0 | 0 &nbsp;&nbsp; 1 &nbsp;&nbsp; 1 |
| 1 &nbsp;&nbsp; 1 &nbsp;&nbsp; 1 | 1 &nbsp;&nbsp; 1 &nbsp;&nbsp; 1 | 1 &nbsp;&nbsp; 1 &nbsp;&nbsp; 0 |

It is really simple. You can implement it with the following python code:

~~~ python
import numpy as np


def AND(x1, x2):
    x = np.array([1, x1, x2])
    w = np.array([-1.5, 1, 1])
    y = np.sum(w*x)
    if y <= 0:
        return 0
    else:
        return 1

def OR(x1, x2):
    x = np.array([1, x1, x2])
    w = np.array([-0.5, 1, 1])
    y = np.sum(w*x)
    if y <= 0:
        return 0
    else:
        return 1

def NAND(x1, x2):
    x = np.array([1, x1, x2])
    w = np.array([1.5, -1, -1])
    y = np.sum(w*x)
    if y <= 0:
        return 0
    else:
        return 1


if __name__ == '__main__':
    input = [(0, 0), (1, 0), (0, 1), (1, 1)]

    print("AND")
    for x in input:
        y = AND(x[0], x[1])
        print(str(x) + " -> " + str(y))

    print("OR")
    for x in input:
        y = OR(x[0], x[1])
        print(str(x) + " -> " + str(y))

    print("NAND")
    for x in input:
        y = NAND(x[0], x[1])
        print(str(x) + " -> " + str(y))
~~~

The results are here:

~~~
AND
(0, 0) -> 0
(1, 0) -> 0
(0, 1) -> 0
(1, 1) -> 1
OR
(0, 0) -> 0
(1, 0) -> 1
(0, 1) -> 1
(1, 1) -> 1
NAND
(0, 0) -> 1
(1, 0) -> 1
(0, 1) -> 1
(1, 1) -> 0
~~~~

This is the first step to understand deep learning.

*The sample code is [here](https://github.com/schwalbe10/ThinkageDeepLearning).*

### Reference

<div class="list">
  <ul>
    <li><a href="https://www.amazon.co.jp/gp/product/4873117585/ref=as_li_tf_tl?ie=UTF8&camp=247&creative=1211&creativeASIN=4873117585&linkCode=as2&tag=schwalbe0d-22">Deep Learning From Scratch (Japanese)</a></li>
  </ul>
</div>
