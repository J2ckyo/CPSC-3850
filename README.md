# CPSC-3850 FINAL PROJECT 
## ABSTRACTION: The Levenberg-Marquardt Method
### The Levenberg–Marquardt Method (also known as LM) is a highly robust and widely used iterative algorithm designed for solving nonlinear least-squares problems. It is a hybrid between the Gauss-Newton method and the gradient descent approach, effectively bridging the gap between local convergence speed and global stability.
### - Problem Description:
#### The algorithm addresses problems where the objective function $f(x)$ is a sum of squares of $m$ nonlinear functions (residuals):

<p align="center"> $$f(x) = \frac{1}{2} \sum_{j=1}^{m} r_j^2(x) = \frac{1}{2} \|r(x)\|^2$$</p>

#### The goal is to find the parameter vector $x \in \mathbb{R}^n$ that minimizes this sum. This is common in "curve fitting," where one seeks parameters that best match a model to observed data.
### - How the Algorithm Works
#### The LM algorithm is a hybrid that adaptively switches between the Gauss-Newton method and Gradient Descent. 
#### The Subproblem
#### At each iteration, the algorithm solves for a step $p$ by minimizing a local quadratic model within a "trust region":
<p align="center"> $$\min_p \frac{1}{2} \|J_k p + r_k\|^2, \quad \text{subject to } \|p\| \le \Delta_k$$ </p>