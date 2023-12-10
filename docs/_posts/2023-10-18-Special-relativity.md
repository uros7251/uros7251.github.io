---
title:  "On the Theory of Relativity"
date:   2023-10-18
categories: physics
permalink: posts/relativity
---

> *There is no absolute space, and we    only conceive of relative motion; and yet in most cases mechanical facts are enunciated as if there is an absolute space to which they can be referred. There is no absolute time. When we say that two periods are equal, the statement has no meaning, and can only acquire a meaning by a convention. Not only have we no direct intuition of the equality of two periods, but we have not even direct intuition of the simultaneity of two events occurring in two different places. I have explained this in an article entitled "Mesure du Temps". Finally, is not our Euclidean geometry in itself only a kind of convention of language?"* - Henri Poincare

*This article is not completed, but is a work in progress. I cannot guarantee that everyting written is true.*

## Discussion of Newton's laws and motivations for relativity theory

Newton was the one who propelled the idea of absolute space and time. However, his laws could only allow one to determine if one is accelerating by experiencing a force in the opposite direction, not if one is moving in uniform rectilinear fashion or is stationary with respect to absolute space.

With the emergence of Maxwell’s theory of electromagnetism, which assumed the existence of the aether (a strong candidate for absolute space), the means to measure one’s state of motion with respect to aether emerged as well. However, after performing several experiments that demonstrated no movement whatsoever, some physicists, notably Poincare, started to consider an idea: that it is a fundamental law of nature that one cannot determine one’s state of motion in any way whatsoever. This is the principle of relativity, later stated by Einstein and used as a starting point for his rewriting of the equations of mechanics.

From this principle, and the postulate about the constancy of the speed of light in all reference frames (which can also be regarded as a convention), one can proceed to derive the transformations between inertial reference frames, time dilation, length contraction, the law for the composition of velocities, etc. This is the way Einstein originally followed in his famous paper in 1905. There is, however, an alternative way to introduce the subject. Although it is somewhat more mathematically involved, it does provide a useful perspective.

## Concept of time

Before we start the exposition, it is crucial to first consider the concept of time. We are so accustomed to the idea of time that critically analyzing it becomes challenging. What do we mean by time? It would be fair to say that time is nothing but a useful abstraction. First, we must acknowledge that the concept of time requires change - if nothing were changing, we could not perceive the passing of time. Second, when we quantify time, we essentially associate two events - one being the event we want to measure in terms of time and the other being some conveniently chosen reference event. For instance, when you say, "My plane landed at 2 o'clock," you mean the landing of the plane coincided with your watch showing 2 o'clock. Or when you say something like, "It took me 6 months to finish my Master's thesis," you are relating the start and finish of your writing to specific positions of Earth along its orbit around the Sun. Thus, measuring time involves comparisons with the state of some reference physical processes. These processes are typically periodic, such as Earth's movement around the Sun, oscillations of a pendulum clock, or oscillations of electric and magnetic fields. Time, in this sense, plays a role in physics akin to that of money in economics.

## Principle of stationary action
We would like to start from a variational principle. The motion of a material point can be described by a trajectory in a 4D spacetime coordinate system. One can define a formula for calculating lengths in this coordinate system. It turns out that the metric which is physically meaningful (thus useful) is:

$$ds^{2} = c^{2}dt^{2} - dx^{2}-dy^{2}-dz^{2}$$

Now, consider that during its motion, a material point passes through points A and B in spacetime. Among all possible trajectories, the one that occurs in the physical world has the characteristic that, for it, the following integral attains the maximum value:

$$S = \int_{A}^{B}\sqrt{c^{2}dt^{2} - dx^{2}-dy^{2}-dz^{2}}$$

If we parametrize the trajectory with respect to time ie. define $x(t)$ such that $x(t_{0}) = x_{0},\,x(t_{1}) = x_{1}$, and similarly for $y, z$ we can express it as follows:

$$\begin{align*}
S &= \int_{t_{0}}^{t_{1}}\sqrt{c^{2}-\dot{x}^{2} - \dot{y}^{2} - \dot{z}^{2}}dt \\ &=\int_{t_{0}}^{t_{1}}\sqrt{c^{2}-v^{2}}dt 
\end{align*}$$

[Euler-Lagrange equations](https://en.wikipedia.org/wiki/Calculus_of_variations) corresponding to $x,y,z$ combined yield:

$$\frac{\vec{v}}{\sqrt{c^{2}-v^{2}}} = \frac{\vec{p}}{c} = \text{const.}$$

which corresponds to the conservation of momentum (we know to extract $\vec{p}$ because of units). The above equation clearly shows that the extremal trajectory is a straight line in $x,t$ coordinate system, but it also illustrates that inertia of a body is not a constant, but depends on its speed. Another invariant which can be derived from Euler-Lagrange equations is:

$$\begin{align*}
\sqrt{c^{2}-v^{2}}-\frac{v^{2}}{\sqrt{c^{2}-v^{2}}} &= \text{const.} \\ \frac{c^{2}}{\sqrt{c^{2}-v^{2}}} = \frac{E}{c} &= \text{const.}
\end{align*}$$

which corresponds to the conservation of kinetic energy (again up to a scale factor $c$). Indeed, for speeds negligible compared to the speed of light, we can expand the expression for energy in terms of $v^{2}/c^{2}$:

$$\begin{align*}
E &= \frac{c^{2}}{\sqrt{1-v^{2}/c^{2}}} \\ &\approx c^{2}\left ( \frac{1}{\sqrt{1-v^{2}/c^{2}}}\bigg|_{v/c = 0} + \frac{d}{d(v^{2}/c^{2})}\frac{1}{\sqrt{1-v^{2}/c^{2}}}\bigg |_{v/c = 0}\frac{v^{2}}{c^{2}}\right ) \\ &= c^{2} + \frac{v^{2}}{2}
\end{align*}$$

From here one can infer $v^{2}/2$ is a constant, which is a well-known expression for kinetic energy per unit mass in classical mechanics.

## Derivation of Lorentz transformations from invariance
In the next part of the exposition, we will confine ourselves to one spatial dimension to simplify and clarify the concepts, although the procedure remains the same for all three dimensions.

We find transformation equations by equivalence of reference frames ie. requiring that the metric is invariant:

$$c^{2}dt^{2} - dx^{2} = c^{2}dt'^{2} - dx'^{2}$$

where $x', t'$ are space and time coordinates in another inertial reference frame. Since the equation of hyperbola is $y^{2}-x^{2} = \text{const.}$, we can interpret pairs $(dx, cdt)$ and $(dx', cdt')$ as points on a single hyperbola. The transformation between reference frames then amounts to moving along the curve.

From analytical geometry it is known that hyperbola  can be parametrized by:

$$\begin{align*}
x &= A\sinh{\theta}, \\
y &= A\cosh{\theta}
\end{align*}$$

for $\theta \in \mathbb{R}$ which follows from the hyperbolic identity:

$$\cosh^{2}{\theta}-\sin^{2}{\theta} = 1.$$

Actually, by using the fact that:

$$\begin{align*}
\cosh{\theta} &= \cos{i\theta} \\
\sinh{\theta} &= -i\sin{i\theta}
\end{align*}$$

and trigonometric identities (just as if the argument was a real number), one can derive analogous identities for hyperbolic functions. Two of them will be important to us:

$$\begin{align*}
\sinh{(\theta+\phi)} &= \sinh{\theta}\cosh{\phi}+\cosh{\theta}\sinh{\phi} \\ 
\cosh{(\theta+\phi)} &= \cosh{\theta}\cosh{\phi}+\sinh{\theta}\sinh{\phi}
\end{align*}$$

Thus, if we introduce a transformation:

$$\begin{bmatrix}
dx' \\ cdt'
\end{bmatrix} = \begin{bmatrix}
\cosh{\phi} & \sinh{\phi} \\
\sinh{\phi} & \cosh{\phi} 
\end{bmatrix}\begin{bmatrix}
dx \\ cdt
\end{bmatrix}$$

then $(dx', cdt')$ is shifted along a hyperbola from $(dx, cdt)$ by $\phi$. Consider that one reference frame is moving with respect to other with speed $v$, that is, we have:

$$\begin{bmatrix}
0 \\ cdt'
\end{bmatrix} = \begin{bmatrix}
\cosh{\phi} & \sinh{\phi} \\
\sinh{\phi} & \cosh{\phi} 
\end{bmatrix}\begin{bmatrix}
vdt \\ cdt
\end{bmatrix}$$

Taking just the first equation ($v\cosh{\phi} + c\sinh{\phi} = 0$) coupled with the identity $\cosh^{2}{\theta}-\sinh^{2}{\theta} = 1$, we get:

$$\begin{align*}
\cosh{\phi} &= \frac{1}{\sqrt{1-v^{2}/c^{2}}} \\
\sinh{\phi} &= -\frac{v/c}{\sqrt{1-v^{2}/c^{2}}}
\end{align*}$$

We arrive at Lorentz transformations:

$$\begin{align}
dx' &= \frac{dx-vdt}{\sqrt{1-v^{2}/c^{2}}} \\
dt' &= \frac{dt-v/c^{2}\,dx}{\sqrt{1-v^{2}/c^{2}}}
\end{align}$$

The factor $\left(1-v^{2}/c^{2}\right)^{-1/2}$ is often abbreviated as $\gamma$. Finally, let us express the parameter $\phi$, commonly referred to as rapidity, in terms of velocity $v$:

$$\begin{align*}
e^{\phi} &= \cosh{\phi}+\sinh{\phi} \\
e^{\phi} &= \frac{1-v/c}{\sqrt{1-v^{2}/c^{2}}} \\ e^{\phi} &= \sqrt{\frac{1-v/c}{1+v/c}} \\ \phi &= \frac{1}{2}\log{\frac{1-v/c}{1+v/c}}
\end{align*}$$

## Simultaneity
Lorentz transformations have some interesting consequences. The first we will discuss is abolishing the concept of absolute simultaneity between two events, independent of the observer's frame of reference. Consider two events, seen as simultaneous from the reference frame $S$, yet occuring at different locations ie. $\Delta t = 0, \Delta x \neq 0$. From the Lorentz transformations, we observe that, from the perspective of an observer fixed to reference frame $S'$, these events are not simultaneous, but $\Delta t' = -\gamma v\Delta x/c^{2}$.
## Length contraction
Another consequence is the apparent length contraction in the direction of motion. Let us imagine a rigid body moving along $x$ axis with a uniform velocity $v$ with respect to some reference system $S$. In its own frame of reference, denoted as $S'$, fixed with it, the body is stationary. To measure its extension along the $x$ axis from the reference frame $S$, one can record the $x$ coordinate of its endpoints at the **same** time and find the difference. On the other hand, to measure the same length from the reference frame $S'$, the observer can make these recordings at any two time instants and subtract - the measurement will still be valid because the body doesn't move in this frame. If we denote the length in $S$ as $L$, and the length in $S'$ as $L_{0}$, from Lorentz transformations we get:

$$ L = L_{0}\sqrt{1-v^{2}/c^{2}}$$

This result could also be obtained from the invariance of the spacetime interval between the measuring events. Qualitatively, spacetime interval in $S$ is simply a negative length squared, while in $S'$ it has extra component involving the time difference because, for the observer from $S'$, the two measurements are not simultaneous. We have thus $L_{0}^{2} = c^{2}\Delta t'^{2} + L^{2}$ which clearly shows that $L$ must be smaller than $L_{0}$. Hence, moving objects appear shorter in the direction of their motion compared to their length in their own reference frame.
## Time dilation
Yet another consequence of special relativity is time dilation. Imagine two observers each with a clock, moving uniformly relative to each other. Here, it's crucial to remember that a 'clock' refers to a device housing a physical phenomenon whose state can be measured. Let's establish reference frames $S$ and $S'$ for these observers respectively. Now, consider two events – two ticks of a clock that's stationary in $S'$. In $S'$, the spatial distance between these events is zero, and let's denote time difference by $\Delta t'$. However, in $S$, where the same two events occur with a time difference $\Delta t$, their spatial separation is $v\Delta t$. Lorentz transformations reveal:

$$\begin{align*}
\Delta t' &= \frac{\Delta t-v^{2}/c^{2}\,\Delta t}{\sqrt{1-v^{2}/c^{2}}} \\ \Delta t' &= \Delta t \sqrt{1-v^{2}/c^{2}}
\end{align*}$$

Again, the conclusion that $\Delta t' \leq \Delta t$ can be qualitatively deduced by demanding the invariance of spacetime intervals.

Crucially, it's important to note that this result doesn't imply that time passes slower in $S'$ than in $S$. There exists a perfect symmetry between $S$ and $S'$. It simply means that, from the perspective of an observer fixed in $S$, the clock stationary in $S'$ appears to tick slower, and vice versa. In simpler terms, the progression of the same physical process seems to slow down (takes more time) when it's in motion relative to the observer compared to when it's stationary. However, as emphasized, the terms 'slower' or 'faster' are always relative and require a specified reference frame to be meaningful.
## Velocity-addition formula
Lorentz transformations also influence the way velocities combine. Let's consider two reference frames, $S$ and $S'$, where the latter moves with velocity $v$ relative to the former. Now, envision a material point moving with velocity $u'$ relative to $S'$. What is its velocity $u$ relative to $S$? 

$$\begin{align*}
u &= \frac{dx}{dt} \\ &= \frac{dx'+vdt'}{dt' + v/c^{2}\,dx'} \\ &= \frac{u'dt'+vdt'}{dt' + v/c^{2}\,u'dt'} \\ u &= \frac{u'+v}{1+u'v/c^{2}}
\end{align*}$$

Thus, simply adding velocities is a valid approximation only for speeds significantly smaller than the speed of light.
## Causality
We have established that absolute simultaneity is non-existent and, generally, observers moving relative to each other measure different time intervals between two events. Lorentz transformations also allow for different event orders in different reference frames. However, if event A causally triggers event B, A must occur before B in all reference frames; otherwise, the concept of causality conflicts with relativity. Let the spacetime interval between $A$ and $B$ be $(\Delta x, \Delta t)$ and $(\Delta x', \Delta t')$ from $S$ and $S'$, respectively, and let $u$ be the velocity of propagation of the causal affection. We have then:

$$\begin{align*}
\Delta t' &= \frac{\Delta t - v/c^{2}\,\Delta x}{\sqrt{1-v^{2}/c^{2}}} \\ &= \Delta t \frac{1-uv/c^{2}}{\sqrt{1-v^{2}/c^{2}}}
\end{align*}$$

Since both $\Delta t$ and $\Delta t'$ must be positive (in both frames $A$ happened before $B$), it follows that:

$$uv < c^{2}$$

Since the theory of relativity doesn't allow for speeds greater than $c$, ie. $v < c$, it follows that the velocity of signal's propagation has to be at most $c$ as well. If it weren't, ie. if $u > c$, then we could imagine a frame of reference moving with a velocity $v = c^{2}/u < c$, where the cause and effect would change order. Thus, the theory of relativity requires that the propagation of causal effect doesn't surpass $c$.

## Four-vectors
We saw how we can specify each event by 1 temporal and 3 spatial coordinates. We can write it compactly as a 4-tuple $(t, x, y, z)$ or more compactly $(t, \vec{x})$. We also defined a measure of distance between two tuples representing events to be the spacetime interval. Such 4-tuples are called 4-vectors.

Looking back at the formulas for energy and momentum we derived, it is interesting to note the relationship between them:

$$\begin{align*}
E^{2}-p^{2}c^{2} &= \frac{c^{6}-v^{2}c^{4}}{c^{2}-v^{2}} \\ E^{2}/c^{2}-p^{2} &=c^{2}
\end{align*}$$

It turns out that $E^{2}/c^{2}-p^{2}$ is independent of $v$ and thus invariant under the change of reference frame. Also, this formula bears a striking resemblance to the spacetime interval. Furthermore, it can be demonstrated that energy and momentum transform in the same way as temporal and spatial coordinates. In fact, it turns out that $(E/c, \vec{p})$ is also a 4-vector - we call it energy-momentum vector. Since we have:

$$\begin{align*}E/c &= \frac{c}{\sqrt{1-v^{2}/c^{2}}} \\ \vec{p} &= \frac{\vec{v}}{\sqrt{1-v^{2}/c^{2}}} \end{align*}$$

it is easily shown that energy-momentum vector is tangential to the trajectory in spacetime:

$$\begin{align*} (E/c, \vec{p}) &\propto (c, \vec{v}) \\ &\propto (cdt, d\vec{x}) \end{align*}$$

Another set of physical quantities that transform like 4-vectors are electric potential and magnetic vector potential combined into a single tuple. In this form, it's called electromagnetic four-potential.

## Path towards General Relativity
There's one caveat concerning all the derivations so far: certain reference frames exist where the principle of stationary action, as we defined it, doesn't hold true and consequently all the equations which mathematically follow are also invalid. These we call non-inertial reference frames. The distinction between them and inertial frames are just that laws of physics are much simpler in latter. To accomodate the former, we must modify the formula for the length of the spacetime interval. This is indeed done in General Relativity. The resulting preferred trajectory is then no longer a straight line in spacetime ie. uniform rectilinear motion, but some curve. 