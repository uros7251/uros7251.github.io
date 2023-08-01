## Analysis of the dynamics of a material point in a gravitational field
Assuming that a gravitational force acts on a material point (oriented towards the coordinate origin, inversely proportional to the square of the distance), the acceleration of the material point is given by:
$$\begin{equation*}
\frac{d^{2}\vec{r}}{dt^{2}} = -G\frac{M}{r^{2}}\hat{r}
\end{equation*}$$
where $M$ is the mass of the body fixed at the coordinate origin.
The acceleration on the right-hand side can be written as a gradient:
$$\begin{align*}\hat{r} &= \nabla r\\
-G\frac{M}{r^{2}}\hat{r} &= \nabla \left(\frac{GM}{r}\right)\end{align*}$$
If we project the above equation onto the direction of the tangent and multiply it by the velocity (effectively taking a dot product of both sides with the velocity vector), we get:
$$\begin{align*}\frac{d^{2}\vec{r}}{dt^{2}}\cdot \frac{d\vec{r}}{dt} &= \nabla \left(\frac{GM}{r}\right)\cdot \frac{d\vec{r}}{dt}\\
\frac{d}{dt}\left(\frac{1}{2}\left(\frac{d\vec{r}}{dt}\cdot \frac{d\vec{r}}{dt}\right) \right) &= \frac{d}{dt}\left(\frac{GM}{r}\right)\\
\frac{v^{2}}{2}-\frac{GM}{r} &= \text{const.}\end{align*}$$
This represents the conservation of energy.
On the other hand, if we multiply the above equation vectorially with the position vector, the right-hand side of the equation is zero, and we get:
$$\begin{align*}\vec{r}\times\frac{d^{2}\vec{r}}{dt^{2}} &= -\vec{r}\times G\frac{M}{r^{2}}\hat{r}\\
\frac{d}{dt}\left(\vec{r}\times \frac{d\vec{r}}{dt}\right)-\frac{d\vec{r}}{dt}\times \frac{d\vec{r}}{dt} &= 0\\
\vec{r}\times \frac{d\vec{r}}{dt} &= \text{const.}\end{align*}$$
This is the conservation of angular momentum. Since we only used the fact that the force field is central to cancel out the right-hand side, this result holds for all central fields, including those that do not follow Newtonian form. From this, we can conclude that during the motion, the material point remains in a plane whose normal is represented by the angular momentum vector. If we now introduce a cylindrical coordinate system whose $z$-axis coincides with the normal to the plane of motion, the above equation becomes:
$$\begin{align*}r\hat{r}\times \left(\dot{r}\hat{r}+r\dot{\theta}\hat{\theta}\right) &= h\hat{z} \\r^{2}\dot{\theta} &= h\end{align*}$$

The product of the square of the distance and the angular velocity, which represents both the double sectoral velocity and the moment of momentum, is constant during motion. The law of conservation of energy in cylindrical coordinates is:

$$\begin{equation*}
\frac{1}{2}\left(\dot{r}^{2}+r^{2}\dot{\theta}^{2}\right)-\frac{GM}{r} = E
\end{equation*}$$

Using the law of conservation of momentum, we can eliminate the angular velocity from the equation, so we get:

$$\begin{equation*}
\frac{\dot{r}^{2}}{2} + \underbrace{\frac{h^{2}}{2r^{2}}-\frac{GM}{r}}_{U_{eff}} = E
\end{equation*}$$

This reduces the problem to a one-dimensional problem with a different potential energy function (see Figure \ref{fig:pot_well}). The energy of the material point determines the limits of its motion.

![Potential well](../assets/images/2023-07-30-central-field-dynamics/potential-well.png)

To study the geometry of motion, it is necessary to eliminate time from the equations (i.e. differentiate with respect to time). The radial velocity can be written as:

$$\dot{r}=\frac{dr}{d\theta}\dot{\theta}$$

This is only possible when the angular velocity is zero, but then the trajectory is trivial - a straight line connecting the material point and the center.

Substituting in the conservation of energy equation, we get:

$$\begin{align*}\frac{1}{2}\left(\left(\frac{dr}{d\theta}\right)^{2}+r^{2}\right)\frac{h^{2}}{r^{4}}-\frac{GM}{r} &= E \\
\frac{h^{2}}{2}\left(\left(\frac{1}{r^{2}}\frac{dr}{d\theta}\right)^{2}+\frac{1}{r^{2}}\right)-\frac{GM}{r} &= E \\
\frac{h^{2}}{2}\left ( \left ( \frac{d}{d\theta}\frac{1}{r} \right )^{2}+\frac{1}{r^{2}} \right )-\frac{GM}{r} &= E\end{align*}$$
The last equation provides us with a reason to consider the reciprocal value of the distance and introduce:
$$\begin{equation*}
\rho = \frac{1}{r}
\end{equation*}$$
and the equation becomes:
$$\begin{align*}\frac{h^{2}}{2}\left(\left(\frac{d\rho}{d\theta}\right)^{2}+\rho^{2}\right)-GM\rho &= E \\
\left(\frac{d\rho}{d\theta}\right)^{2}+\rho^{2}-2\frac{GM}{h^{2}}\rho &= \frac{2E}{h^{2}} \\
\left(\frac{d\rho}{d\theta}\right)^{2}+\left(\rho-\frac{GM}{h^{2}}\right)^{2} &= \frac{1}{h^{2}}\left(2E+\frac{G^{2}M^{2}}{h^{2}}\right)\end{align*}$$
The last equation represents a circle in the coordinate system $\left(\rho, d\rho/d\theta\right)$ with a center at point $\left(GM/h^{2}, 0\right)$. If we put:
$$\begin{equation*}
\rho-\frac{GM}{h^{2}} = \frac{1}{h}\sqrt{2E+\frac{G^{2}M^{2}}{h^{2}}}\cos{\theta}
\end{equation*}$$
then it follows:
$$\begin{equation*}
\frac{d\rho}{d\theta} = -\frac{1}{h}\sqrt{2E+\frac{G^{2}M^{2}}{h^{2}}}\sin{\theta}
\end{equation*}$$
and the above equation is indeed satisfied. Therefore, one of the possible solutions is:
$$\begin{align*} \rho&=\frac{GM}{h^{2}} + \frac{1}{h}\sqrt{2E+\frac{G^{2}M^{2}}{h^{2}}}\cos{\theta} \\\frac{1}{r} &= \frac{1+\sqrt{\frac{2Eh^{2}}{G^{2}M^{2}}+1}\cos{\theta}}{\frac{h^{2}}{GM}}\end{align*}$$
This is the equation of a conic section. We can read off its eccentricity from it:
$$\begin{equation*}
e = \sqrt{\frac{2Eh^{2}}{G^{2}M^{2}}+1}
\end{equation*}$$
And indeed, the fraction inside the square root is a dimensionless quantity (all units cancel out). When the energy of the particle is less than zero, the eccentricity is less than one, so the path is an ellipse. When the energy is equal to zero, the path is a parabola, while in the opposite case, it is a hyperbola. In each of these cases, one of the foci lies at the origin of the coordinate system. The length of the longer semiaxis can also be calculated using the well-known expression for an ellipse:
$$\begin{align*}a(1-e^{2}) &= \frac{h^{2}}{GM} \\-a\frac{2Eh^{2}}{G^{2}M^{2}} &= \frac{h^{2}}{GM} \\a &= -\frac{GM}{2E}\end{align*}$$
By inserting this result into the formula for the period, we obtain:
$$\begin{align*}
T &= \frac{2\pi ab}{h} \\
T &= \frac{2\pi a}{h} \sqrt{\frac{ah^{2}}{GM}} \\
T &= 2\pi \sqrt{\frac{a^{3}}{GM}}
\end{align*}$$