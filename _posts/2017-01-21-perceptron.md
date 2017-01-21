---
layout: post
title: "Deep Learning 1 - Perceptron"
date:  2017-01-21

tags:
- Deep Learning
- Python
---

The perceptron is an algorithm that signals information from an input layer to an output layer. The figure shows the 2 inputs perceptron.

 ![perceptron]({{site.github.url}}/images/posts/perceptron.png)

$$ x_1, x_2 $$ are input signals, $$ y $$ is an output signal, and $$ w_1, w_2 $$ are weights. Signals are also called neurons or nodes. They output 1, only if the sum of inputs is over thresholds. In this case, the function is represented as follows:

$$
\begin{eqnarray*}
    y = \left\{
        \begin{array}{l}
            0 & ( b + w_1x_1 + w_2x_2  \leqq 0) \\
            1 & ( b + w_1x_1 + w_2x_2  > 0)
        \end{array}
    \right.
\end{eqnarray*}
$$

Here, $$ b $$ is a bias. You can create a logic gate with this function. If $$ b=-1.5 $$, $$ w_1=1 $$, and $$  w_2=1 $$, it will be the AND gate. This is the truth table for AND, OR, and NAND. Check the values ($$ b, w_1, w_2 $$) for the OR and NAND gates by yourself!

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


def and(x1, x2):
    x = np.array([x1, x2])
    w = np.array([1, 1]) 
    b = -1.5
    y = np.sum(w*x) + b 
    if y <= 0:
        return 0
    else:
        return 1

def or(x1, x2):
    x = np.array([x1, x2])
    w = np.array([1, 1]) 
    b = -0.5
    y = np.sum(w*x) + b 
    if y <= 0:
        return 0
    else:
        return 1

def nand(x1, x2):
    x = np.array([x1, x2])
    w = np.array([-1, -1])
    b = 1.5 
    y = np.sum(w*x) + b 
    if y <= 0:
        return 0
    else:
        return 1


if __name__ == '__main__':
    input = [(0, 0), (1, 0), (0, 1), (1, 1)] 
    
    print("AND")
    for x in input:
        y = and(x[0], x[1])
        print(str(x) + " -> " + str(y))
    
    print("OR")
    for x in input:
        y = or(x[0], x[1])
        print(str(x) + " -> " + str(y))
    
    print("NAND")
    for x in input:
        y = nand(x[0], x[1])
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
This is the first step to understand deep learning!
