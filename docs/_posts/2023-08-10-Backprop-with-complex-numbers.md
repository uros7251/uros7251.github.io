---
title:  "Backprop with complex numbers"
date:   2023-08-10
permalink: posts/backprop-complex-numbers
---

One of the building blocks of my [linear circuit solver](https://github.com/uros7251/PyCircuitSolver) is automatic differentiation which calculates the gradient of the loss function with respect to node voltages. However, since node voltages are complex in general case, I needed to find a way to compute gradients with respect to complex values and propagate them through the computational graph. This seemed like a simple, yet interesting task, so I decided to tackle it without previously searching for already developed theory.
## Chain rule
If one briefly sits and thinks about this problem, one soon realizes that the biggest challenge is to figure out how chain rule works in this setting. After all, chain rule lies at the heart of automatic differentiation.

So suppose that we have a real valued function $L$ which depends on multiple complex variables and whose minimum we ought to find. We would like to calculate some analogue of gradient that will guide us in the direction of the steepest descent. More formally, if $L$ is a function of complex variable $z$, we would like to calculate:

$$\frac{\partial L}{\partial x_{z}}, \frac{\partial L}{\partial y_{z}},$$

where $x_{z}, y_{z}$ are real and imaginary component of $z$, respectively. This is of course trivial if $L$ directly depends on $z$, but the problem is how to calculate it effectively when $L$ depends on some other complex variable $w$ which in turn depends on $z$ ie. when $L(w(z))$. One possible solution is to treat real and imaginary part as two independent values, but it turns out that we can do better.

Let us imagine that we already calculated partial derivatives with respect to $w_{x}, w_{y}$, that is we know:

$$\frac{\partial L}{\partial x_{w}}, \frac{\partial L}{\partial y_{w}}.$$

From there we can use standard chain rule to obtain:

$$
\begin{align*}
\frac{\partial L}{\partial x_{z}} &= \frac{\partial L}{\partial x_{w}}\frac{\partial x_{w}}{\partial x_{z}} + \frac{\partial L}{\partial y_{w}}\frac{\partial y_{w}}{\partial x_{z}} \\
\frac{\partial L}{\partial y_{z}} &= \frac{\partial L}{\partial x_{w}}\frac{\partial x_{w}}{\partial y_{z}} + \frac{\partial L}{\partial y_{w}}\frac{\partial y_{w}}{\partial y_{z}}
\end{align*}
$$

We can further simplify by using the following identities:

$$
\begin{align*}
\frac{\partial w}{\partial x_{z}} &= \frac{\partial x_{w}}{\partial x_{z}}+i\frac{\partial y_{w}}{\partial x_{z}} \\ &= \frac{\partial z}{\partial x_{z}}\frac{\partial w}{\partial z} \\ &= \frac{\partial w}{\partial z},\\
\frac{\partial w}{\partial y_{z}} &= \frac{\partial x_{w}}{\partial y_{z}}+i\frac{\partial y_{w}}{\partial y_{z}} \\ &= \frac{\partial z}{\partial y_{z}}\frac{\partial w}{\partial z} \\ &= i\frac{\partial w}{\partial z},
\end{align*}
$$

This allows us to rewrite partial derivatives encountered earlier:

$$
\begin{align*}
\frac{\partial x_{w}}{\partial x_{z}} &= \mathrm{Re}\left(\frac{\partial w}{\partial z}\right) \\ \frac{\partial y_{w}}{\partial x_{z}} &= \mathrm{Im}\left(\frac{\partial w}{\partial z}\right) \\ \frac{\partial x_{w}}{\partial y_{z}} &= \mathrm{Re}\left(i\frac{\partial w}{\partial z}\right) = -\mathrm{Im}\left(\frac{\partial w}{\partial z}\right) \\ \frac{\partial y_{w}}{\partial y_{z}} &= \mathrm{Im}\left(i\frac{\partial w}{\partial z}\right) = \mathrm{Re}\left(\frac{\partial w}{\partial z}\right)
\end{align*}
$$

Thus, we see that partial derivatives are not independent which should not surprise us since analytic complex functions must satisfy Cauchy-Riemann conditions. Consequently, it would have been redundant to treat real and imaginary part as completely separate values. Plugging in above formulas in our chain rule equation, one gets:

$$
\begin{align*}
\frac{\partial L}{\partial x_{z}} &= \mathrm{Re}\left(\frac{\partial w}{\partial z}\right)\frac{\partial L}{\partial x_{w}} + \mathrm{Im}\left(\frac{\partial w}{\partial z}\right)\frac{\partial L}{\partial y_{w}} \\
\frac{\partial L}{\partial y_{z}} &= -\mathrm{Im}\left(\frac{\partial w}{\partial z}\right)\frac{\partial L}{\partial x_{w}} + \mathrm{Re}\left(\frac{\partial w}{\partial z}\right)\frac{\partial L}{\partial y_{w}}
\end{align*}
$$

The key insight at this point is that if we write:

$$
\nabla_{z} = \frac{\partial }{\partial x_{z}}-i\frac{\partial}{\partial y_{z}}
$$

two equations above become:

$$
\begin{align*}
\frac{\partial L}{\partial x_{z}} &= \mathrm{Re}\left(\frac{\partial w}{\partial z}\right)\mathrm{Re}\left(\nabla_{w}L\right) - \mathrm{Im}\left(\frac{\partial w}{\partial z}\right)\mathrm{Im}\left(\nabla_{w}L\right) \\
-\frac{\partial L}{\partial y_{z}} &= \mathrm{Im}\left(\frac{\partial w}{\partial z}\right)\mathrm{Re}\left(\nabla_{w}L\right) + \mathrm{Re}\left(\frac{\partial w}{\partial z}\right)\mathrm{Im}\left(\nabla_{w}L\right)
\end{align*}
$$

which we can compress into one, very simple and elegant:

$$
\nabla_{z}L = \frac{\partial w}{\partial z}\cdot \nabla_{w}L
$$

It is pleasing to express the previous result more generally, in terms of operators, without reference to any particular function:

$$
\nabla_{z}= \frac{\partial w}{\partial z}\cdot \nabla_{w}
$$

## Performing gradient descent
During minimization, we would move along conjugate of gradient (as defined above), performing the step:

$$
z := z - \alpha \overline{\nabla_{z}L}
$$

## Wirtinger derivatives and support for complex autograd in deep learning frameworks
Only after I derived these equations for myself to build autograd supporting complex numbers, I found out that PyTorch also supports it by calculating something called Wirtinger derivatives. These are defined as:

$$
\begin{align*}
\frac{\partial } {\partial z} &= \frac{1}{2}\left(\frac{\partial } {\partial x} - i\frac{\partial } {\partial y}\right), \\
\frac{\partial } {\partial \bar{z}} &= \frac{1}{2}\left(\frac{\partial } {\partial x} + i\frac{\partial } {\partial y}\right) 
\end{align*}
$$

Interestingly, PyTorch and TensorFlow compute $\partial/\partial \bar{z}$, the negative of which is precisely the direction of steepest descent, whereas on the other hand JAX computes $\partial/\partial z$, like I do.