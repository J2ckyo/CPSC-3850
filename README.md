# CPSC-3850 FINAL PROJECT 
## The Levenberg-Marquardt Method
### The Levenberg–Marquardt Method (also known as LM) is a highly robust and widely used iterative algorithm designed for solving nonlinear least-squares problems. It is a hybrid between the Gauss-Newton method and the gradient descent approach, effectively bridging the gap between local convergence speed and global stability.
### 1. Problem Description:
#### The algorithm addresses problems where the objective function $f(x)$ is a sum of squares of $m$ nonlinear functions (residuals):

<p align="center"> $$f(x) = \frac{1}{2} \sum_{j=1}^{m} r_j^2(x) = \frac{1}{2} \|r(x)\|^2$$</p>

#### The goal is to find the parameter vector $x \in \mathbb{R}^n$ that minimizes this sum. This is common in "curve fitting," where one seeks parameters that best match a model to observed data.
### 2. How the Algorithm Works
#### The LM algorithm is a hybrid that adaptively switches between the Gauss-Newton method and Gradient Descent. 
#### The Subproblem
#### At each iteration, the algorithm solves for a step $p$ by minimizing a local quadratic model within a "trust region":
<p align="center"> $$\min_p \frac{1}{2} \|J_k p + r_k\|^2, \quad \text{subject to } \|p\| \le \Delta_k$$ </p>

#### - $J_k$ is the Jacobian matrix of the residuals.
#### - $r_k$ is the current residual vector.
#### - $\delta_k$ is the trust-region radius.
### 3. The Damped Equation
#### The solution to this subproblem is found by solving the "damped" normal equations:
<p align="center"> $$(J^T J + \lambda I) p = -J^T r$$ </p>

#### - Large $\lambda$: When the model is unreliable (far from the minimum), $\lambda$ increases. The $(J^T J)$ term becomes negligible compared to $\lambda I$, and the step $p$ aligns with the negative gradient.
#### - Small $\lambda$: When the model is accurate (near the minimum), $\lambda$ decreases. The algorithm behaves like the Gauss-Newton method, providing rapid convergence.

### 4. Theoretical Properties
#### Global Convergence: Unlike the standard Gauss-Newton method, which can fail if the Jacobian is rank-deficient, the term $\lambda I$ ensures the matrix is always positive definite and invertible. This guarantees that the algorithm can always find a descent direction.
#### Local Convergence: As the algorithm approaches the solution $x^*$, $\lambda$ is reduced toward zero. If the residuals at the solution are small, the method achieves a quadratic or near-quadratic convergence rate, similar to Newton's method.
#### Per-Iteration Cost: The primary cost is solving the linear system $(J^T J + \lambda I) p = -J^T r$. For a dense Jacobian, this typically requires $O(m n^2)$ operations to form $J^T J$ and $O(n^3)$ for the Cholesky factorization.
#### Memory Efficiency: It can be implemented as an augmented least-squares problem to avoid squaring the condition number of $J$, improving numerical stability.