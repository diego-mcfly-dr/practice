## Part II: Convexity Proof & Global Optimality

### Step 1: Second-Order Characterization of Convexity
A twice-continuously differentiable function $f: \mathbb{R}^n \to \mathbb{R}$ is convex if and only if its Hessian is positive semi-definite everywhere:

$$\nabla^2 f(x) \succeq 0 \quad \forall x \in \mathbb{R}^n$$

Since $\nabla^2 f(x) = Q$ is constant across $\mathbb{R}^n$, $f(x)$ is convex if and only if:

$$v^T Q v \ge 0 \quad \forall v \in \mathbb{R}^n$$

If $Q \succ 0$ (all eigenvalues $\lambda_i(Q) > 0$), $f(x)$ is **strictly convex**.

### Step 2: Global Minimum Condition
By first-order optimality conditions, $x^\star$ is a stationary point if and only if the gradient vanishes:

$$\nabla f(x^\star) = 0 \implies Q x^\star + b = 0 \implies Q x^\star = -b$$

If $Q \succ 0$, $Q$ is invertible, guaranteeing a unique global minimum:

$$x^\star = -Q^{-1} b$$

---

## Part III: Gradient Descent Formulation & Convergence Analysis

### Step 1: First-Order Update Rule
The standard Gradient Descent (GD) iteration scheme with constant learning rate $\alpha > 0$ is defined as:

$$x_{k+1} = x_k - \alpha \nabla f(x_k)$$

Substituting the analytical gradient $\nabla f(x_k) = Q x_k + b$:

$$x_{k+1} = x_k - \alpha (Q x_k + b)$$

### Step 2: Error Dynamics
Define the parameter error vector at iteration $k$ as $e_k = x_k - x^\star$. Since $Q x^\star = -b$, we rewrite $b = -Q x^\star$:

$$x_{k+1} = x_k - \alpha Q x_k - \alpha b$$
$$x_{k+1} = x_k - \alpha Q x_k + \alpha Q x^\star$$

Subtracting $x^\star$ from both sides:

$$x_{k+1} - x^\star = (x_k - x^\star) - \alpha Q (x_k - x^\star)$$

$$e_{k+1} = (I - \alpha Q) e_k$$

By induction, the error after $k$ steps is given by matrix power iteration:

$$e_k = (I - \alpha Q)^k e_0$$

### Step 3: Spectral Step-Size Bound for Convergence
For the error to vanish as $k \to \infty$ ($e_k \to 0$), the iteration matrix $T = I - \alpha Q$ must be a contraction mapping. This requires its spectral radius $\rho(T)$ to be strictly less than $1$:

$$\rho(I - \alpha Q) = \max_i |1 - \alpha \lambda_i(Q)| < 1$$

For all eigenvalues $\lambda_i(Q) \in [\lambda_{\min}(Q), \lambda_{\max}(Q)]$:

$$-1 < 1 - \alpha \lambda_i(Q) < 1$$

1. **Lower Bound:** $1 - \alpha \lambda_i(Q) < 1 \implies \alpha \lambda_i(Q) > 0 \implies \alpha > 0$ (assuming $Q \succ 0$).
2. **Upper Bound:** $1 - \alpha \lambda_i(Q) > -1 \implies \alpha \lambda_i(Q) < 2 \implies \alpha < \frac{2}{\lambda_i(Q)}$.

To guarantee convergence across all eigen-directions simultaneously, the step size must satisfy the bound dictated by the maximum eigenvalue $\lambda_{\max}(Q)$:

$$0 < \alpha < \frac{2}{\lambda_{\max}(Q)}$$

*   **Optimal Step Size:** $\alpha_{\text{opt}} = \frac{2}{\lambda_{\min}(Q) + \lambda_{\max}(Q)}$ yields the fastest linear rate of convergence.
