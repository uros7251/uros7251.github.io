---
title:  "Frenet formulas"
date:   2023-07-31
permalink: /posts/frenet-formulas
---
In kinematics, the so-called natural coordinate system is fixed to a moving body point with base vectors (axes) defined as follows:

- $\mathbf{T}$ is the unit vector in the direction of the tangent of motion of the material point
- $\mathbf{N}$ is a unit vector whose direction coincide with the centripetal (normal) acceleration of the material point.
- $\mathbf{B}$ is a unit vector obtained as a vector product $\mathbf{T}\times\mathbf{N}$. Thus, the vector obtained when $\mathbf{N}$ is rotated 90 degrees around $\mathbf{T}$ counterclockwise.

So, if we start from the parametric equation of motion of a material point, we get the tangential vector as the limiting value of the ratio of differential of the displacement vector and the length of the path traveled during that differential displacement, when the path length tends to zero:


$$\begin{equation*}
     \mathbf{T} = \frac{d\mathbf{r}}{ds}
\end{equation*}$$


As the displacement vector coincides with the traveled path in this limiting case, the upper vector is a unit vector.

The normal vector is proportional to the limit value of the difference of tangential vectors in two adjacent points and the length of the path traveled between those two points, when the path length tends to zero:


$$\begin{equation*}
     \frac{d\mathbf{T}}{ds} = \kappa \mathbf{N}
\end{equation*}$$


The proportionality coefficient is called the curvature of the curve and tells how abrupt the change in tangent is. This coefficient has a very interesting meaning because it serves to compare the curve traced by the material point with the movement along a circle. Here is what is obtained when the above derivative is calculated for a circle of radius $r$.


$$\begin{align*}\frac{d}{ds}\left< \cos{\theta}, \sin{\theta}\right> &= \frac{d\theta}{ds}\left< -\sin{\theta}, \cos{\theta}\right> \\ &= \frac{1}{r}\left< -\sin{\theta}, \cos{\theta}\right> \end{align*}$$


So, in the case of a circle, the curvature of the curve is equal to the reciprocal of the radius of the circle. Therefore, we can introduce the more general notion of radius of curvature as the reciprocal of the curvature of a curve, which can be calculated for an arbitrary curve. This measure tells us about the local similarity of the curve to the circle with the corresponding radius. Indeed, if we were to develop the displacement into the Taylor series and stick only to the second order terms, we would get:


$$\begin{align*}d\mathbf{r} &= \frac{d\mathbf{r}}{ds} ds + \frac{1}{2}\frac{d^{2}\mathbf{r} }{ds^{2}}ds^{2} + \mathcal{O}(ds^{3}) \\ &= \mathbf{T}\,ds + \frac{\kappa}{2}\mathbf {N}\,ds^{2} + \mathcal{O}(ds^{3})\end{align*}$$


Therefore, the curve itself could be approximated around some point $P$ by a circle of radius $1/\kappa$ with the center in the direction determined by the unit vector $\mathbf{N}$.

The vector $\mathbf{N}$ is indeed normal to the vector $\mathbf{T}$ which is easily proved:


$$\begin{equation*}
     \frac{d}{ds}\left (\mathbf{T}\cdot \mathbf{T} \right ) = 2\frac{d\mathbf{T}}{ds}\cdot \mathbf{T} = 0
\end{equation*}$$


The length of the vector $\mathbf{T}$ is equal to one at all points of the curve, so the derivative on the left side is also equal to zero at all points. This argument obviously works for all vectors of constant magnitude.


The vectors $\mathbf{T}$ and $\mathbf{N}$ determine the plane that is parallel to the curve at a certain point. That plane is called the osculating plane, and its normal vector, which we mark with $\mathbf{B}$, so called binormal vector, is obtained as the vector product of the previous two unit vectors and completes the vector base.


$$\begin{equation*}
     \mathbf{B} = \mathbf{T} \times \mathbf{N}
\end{equation*}$$


If we look for the derivative of this vector with respect to the distance traveled, $s$, we will get:


$$\begin{align*}\frac{d\mathbf{B}}{ds} &= \frac{d\mathbf{T}}{ds}\times \mathbf{N} + \mathbf{T}\times \frac{d\mathbf{N}}{ds} \\ &= \kappa \mathbf{N} \times \mathbf{N} + \mathbf{T}\times \frac{d\mathbf{N}}{ds } \\ &= \mathbf{T}\times \frac{d\mathbf{N}}{ds}\end{align*}$$


Since $d\mathbf{N}/ds$ is normal to $\mathbf{N}$, it follows that it lies in the plane determined by $\mathbf{T}$ and $\mathbf{B}$, i.e. it represents a linear the combination of these two vectors. It follows that $d\mathbf{B}/ds$ must be parallel to $\mathbf{N}$ (making use of $\mathbf{T}\times \mathbf{T} = 0$):


$$\begin{equation*}
     \frac{d\mathbf{B}}{ds} = -\tau \mathbf{N},
\end{equation*}$$


The coefficient $\tau$ determines how fast the binormal changes and is called torsion of the curve. The minus sign is a matter of convention and is taken so that for a helix following the right-hand rule, the torsion is a positive value.
On the other hand, for the vector $\mathbf{N}$:


$$\begin{equation*}
     \mathbf{N} = \mathbf{B}\times\mathbf{T},
\end{equation*}$$


and if we look for its derivative with respect to $s$, we get:


$$\begin{align*}\frac{d\mathbf{N}}{ds} &= \frac{d\mathbf{B}}{ds}\times \mathbf{T} + \mathbf{B}\times \frac{d\mathbf{T}}{ds} \\ &= -\tau \mathbf{N}\times \mathbf{T} + \mathbf{B}\times \kappa\mathbf{N} \\ &= \tau\mathbf{B} - \kappa \mathbf{T}\end{align*}$$


Finally, the so-called Frenet formulas read:


$$\begin{align*} \frac{d\mathbf{T}}{ds} &= \kappa \mathbf{N} \\ \frac{d\mathbf{N}}{ds} &= \tau\mathbf{ B} - \kappa \mathbf{T} \\ \frac{d\mathbf{B}}{ds}&= -\tau\mathbf{N}\end{align*}$$