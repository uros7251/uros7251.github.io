---
title:  "Linear Circuit Solver - part 2"
date:   2023-09-22
categories: electrical engineering
permalink: posts/linear-circuit-solver-2
---
# Part 2 - Arbitrary topologies
## Pitfalls of the current solution
The methodology discussed in the [previous part](posts/linear-circuit-solver-1) works well for circuits represented as trees of series and parallel connections. However, its applicability is constrained when dealing with more intricate topologies, such as bridge circuits, where components are interconnected in more complex ways. Consequently, its scope is somewhat limited.

To extend our method to arbitrary circuits with diverse topologies, we must undergo a fundamental shift in our approach. Our solution entails reverting to nodal analysis, a well-established technique in electrical engineering. In our new method, we view the circuit as a graph composed of branches connecting nodes, where nodes serve as points of junction for three or more branches. Each branch, in turn, comprises one or more components connected in series.

## ML-inspired approach
In nodal analysis, we construct a linear system by mandating that the net current flowing out of each node equals zero. However, instead of solving this linear system for exact solutions, our approach leans toward numerical methods. We define our solution as a set of node voltages and quantify the quality of a solution by calculating the sum of squares of net currents over each node, serving as our loss function. The objective is to find a solution that minimizes this loss, ideally reducing it to zero.

$$\begin{align*}
L &= \sum_{v \in V}I_{v}^{2} \\
I_{v} &= \sum_{e \in E}B_{ve}I_{e}
\end{align*}$$

In the previous equations $V$ is a set of nodes, $E$ is a set of branches, $B$ is an incidence matrix, and $I_{e}$ is a current going through branch $e$. The latter is calculated using the method developed in the previous section.

Since currents depend linearly on node voltages, the loss function takes the form of a quadratic function of node voltages. Moreover, since the loss function is the sum of squares, it is bounded from below by zero, rendering it a convex function. This advantageous property simplifies our optimization problem, allowing us to leverage a broad range of well-established methods for convex optimization.

## Calculation of complex gradient
To iteratively progress toward superior solutions, we need to compute the gradient of the loss function with respect to node voltages. Notably, we encounter the challenge of differentiating a real-valued function with respect to complex variables. The key lies in devising a mechanism to store these derivatives in a way that enables their backpropagation through the computational graph.

If we denote real and imaginary parts by $x$ and $y$, respectively, an effective strategy is to store the gradient as follows:

$$\nabla = \frac{\partial}{\partial x} - j\frac{\partial}{\partial y}$$

Here, $j$ denotes the imaginary unit. This formulation allows us to apply the standard chain rule for differentiation, facilitating the propagation of gradients backward through the computational graph. Indeed, if we have two complex variables $z$ and $w$ such that $w$ is a function of $z$, it can be shown that the following equation hold:

$$\nabla_{z} = \frac{\partial w}{\partial z}\cdot \nabla_{w} + \cdots$$

As a result, we can efficiently compute the gradients of real-valued functions with respect to complex variables. For updates, we naturally use the complement of this gradient. For more detailed explanation, see [this post](posts/backprop-complex-numbers).

## Sketch of the implementation

To compute gradients, we implement a compact reverse mode automatic differentiation module, conceptually similar to those commonly found in deep learning frameworks like PyTorch.

The algorithm for determining the node voltages is as follows:

1. **Initialization**: Begin by initializing all node voltages to zero. This serves as the initial solution, assuming the circuit contains no active components.
2. **Forward Computation**: Conduct a forward computation to calculate the loss associated with the current set of node voltages.
3. **Check Loss Value**: If the computed loss value meets the predetermined satisfactory criteria (very close to zero for an ideal solution), return the current set of node voltages as the solution.
4. **Backward Computation**: Perform a backward computation to calculate the gradients of the loss function with respect to the node voltages.
5. **Update Node Voltages**: Utilize the calculated gradients to update the node voltages and proceed to step 2 for another iteration.

Steps 2 to 5 are repeated until the algorithm terminates. Ideally, the loss should decrease with each iteration. At the end of this process, the correct node voltages are determined, enabling the subsequent calculation of current and voltage values for all components within the circuit. Concerning Step 5, many techniques could be used to perform an update including various variants of gradient descent.

While our approach offers a robust framework for circuit analysis, there are a few caveats to discuss:

- **Reference Node**: One node voltage within the circuit can always be set as a reference, typically fixed to zero volts. This reference node provides a point of comparison for other voltage values in the circuit.
- **Ideal Voltage Sources**: In instances where a branch comprises solely an ideal voltage source, a unique constraint is introduced. Such a source imposes a specific relationship between the voltages at its terminal nodes. Consequently, it becomes less preferable to consider these voltages independently. Additionally, since the branch contains only an ideal voltage source, the current flowing through it remains undefined. As a result, we treat this current as a new parameter to be determined within the analysis. Thus, overall, the count of parameters we optimize over remains unchanged.

Again, complete implementation in Python can be found [here](https://github.com/uros7251/PyCircuitSolver).