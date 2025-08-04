# Krylov subspace
### Definition (Krylov subspace):
$$\mathcal{K}_m(A,v) \coloneqq \text{span}\left\{v, Av, A^2v, \dots, A^{m-1}v \right\}$$ where $v \in\mathbb{R}^n$ and $A$ is a $n$ by $n$ matrix. 
### Definiton (Grade):
Let $A\in \mathbb{R}^{n\times n}$ and $v\in \mathbb{R}^n$, $v\neq 0$, the grade of $v$ with respect to $A$, denoted $\mu$, is the **smallest positive integer** such that $\left\{v, Av, A^2v, \dots, A^{\mu}v \right\}$ is not linearly independent. 
### Properties:
- $\mathcal{K}_m$ is the subspace of all vectors in $\mathcal{R}^n$ that can be written as $x=p(A)v$, where $p$ is a polynomial of degree not exceeding $m-1$.
