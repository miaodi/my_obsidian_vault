# Krylov subspace
### Definition (Krylov subspace):
$$\mathcal{K}_m(A,v) \coloneqq \text{span}\left\{v, Av, A^2v, \dots, A^{m-1}v \right\}$$ where $v \in\mathbb{R}^n$ and $A$ is a $n$ by $n$ matrix. 
### Definiton (Grade):
Let $A\in \mathbb{R}^{n\times n}$ and $v\in \mathbb{R}^n$, $v\neq 0$, the grade of $v$ with respect to $A$, denoted $\mu$, is the **smallest positive integer** such that $\left\{v, Av, A^2v, \dots, A^{\mu}v \right\}$ is not linearly independent. 
### Properties:
- $\mathcal{K}_m$ is the subspace of all vectors in $\mathcal{R}^n$ that can be written as $x=p(A)v$, where $p$ is a polynomial of degree not exceeding $m-1$.
# GMRES
The Generalized Minimum Residual Method (GMRES) is a projection method that finding the residual in the $L_2$ norm:
$$
\underset{v\in\mathcal{K}_m(A, r_0)}{\texttt{argmin}}J(v)=\|r_0-Av\|_2, \text{ where } r_0=b-Ax_0,
$$
where $\mathcal{K}_m(A, r_0)$ is the $m$-dimensional Krylov subspace. Assuming $V_m$ are orthonormal basis of $\mathcal{K}_m(A, r_0)$, we can rewrite:
$$\begin{aligned}
J(y) &=\|r_0-AV_my\|_2,\quad y\in\mathbb{R}^m \\
     &=\|r_0-V_{m+1}\bar{H}y\|_2 \quad  AV_m=V_{m+1}\bar{H} \texttt{ Arnoldi process}\\
     &=\|\beta V_{m+1}e_1-V_{m+1}\bar{H}y\|_2,\texttt{ where }\beta=\|r_0\|_2, \quad V_{m+1}(:,0)=\frac{r_0}{\|r_0\|} \\
     &= \sqrt{(V_{m+1}(\beta e_1-\bar{H}y))^T(V_{m+1}(\beta e_1-\bar{H}y))} \\
     &= \sqrt{(\beta e_1-\bar{H}y)^T(\beta e_1-\bar{H}y)} \\
     &= \|\beta e_1-\bar{H}y\|_2.
\end{aligned}$$
The minimization problem becomes:
$$
\underset{y\in\mathbb{R}^m}{\texttt{argmin}}\|\beta e_1-\bar{H}y\|_2.
$$
## Givens rotation
The minimization problem can be solved by the following variational problem:
$$
\delta \|\beta e_1-\bar{H}y\|_2^2=\delta y^T\bar{H}^T(\beta e_1-\bar{H}y)=0 \rightarrow \bar{H}^T\bar{H}y=\beta \bar{H}^Te_1.
$$
However, the variational problem is cumbersome as the construction of $\bar{H}^T\bar{H}$ taking $O(m^3)$  not saying the factorization cost.
The Givens rotation provide a way to triangularize the Hessenberg matrix $\bar{H}\in\mathbb{R}^{(m+1)\times m}$ who has non-zero entries on the first subdiagonal:
$$
\bar{H} = 
\begin{pmatrix}
h_{11} & h_{12} & h_{13} & \cdots & h_{1,m-1} & h_{1m} \\
h_{21} & h_{22} & h_{23} & \cdots & h_{2,m-1} & h_{2m} \\
0 & h_{32} & h_{33} & \cdots & h_{3,m-1} & h_{3m} \\
\vdots & \ddots & \ddots & \ddots & \vdots & \vdots \\
0 & \cdots & 0 & 0 & h_{m,m-1} & h_{m,m} \\
0 & \cdots & 0 & 0 &0 & h_{m+1,m}
\end{pmatrix}
$$
Consider the following 2D rotation problem:
$$
\begin{bmatrix}
c & -s \\
s & c
\end{bmatrix}
\begin{bmatrix}
a\\
b
\end{bmatrix}
=
\begin{bmatrix}
r\\
0
\end{bmatrix},
$$
$c$ and $s$ can be computed as:
$$
c=\frac{a}{r}, \texttt{ and } s= -\frac{b}{r}, \texttt{ where } r=\sqrt{a^2+b^2}.
$$
If we multiply $\bar{H}$ by:
$$
\Omega_1 = 
\begin{bmatrix}
c_1 & -s_1 & 0 & \cdots &0 \\
s_1 & c_1 & 0 & \cdots & 0 \\
0 & 0 & 1 & \cdots &0 \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
0 & 0 & 0 & \cdots &1 \\
\end{bmatrix},
$$
we have:
$$
\Omega_1\bar{H} = 
\begin{bmatrix}
h_{11}^1 & h_{12}^1 & h_{13}^1 & \cdots & h_{1m}^1 \\
0 & h_{22}^1 & h_{23}^1 & \cdots & h_{2m}^1 \\
0 & h_{32} & h_{33} & \cdots & h_{3m} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
0 & 0 & 0 & \cdots & h_{m+1,m} \\
\end{bmatrix}, \texttt{ and } \Omega_1 \beta e_1=\begin{bmatrix}c_1\beta \\ s_1\beta \\ 0 \\ \vdots \\ 0\end{bmatrix}.
$$
If we define $Q_m=\Omega_m\Omega_{m-1}\dots\Omega_{1}$, where $\Omega_i$ is the Givens rotation matrix for zero-ing the sub-diagonal of $i^{th}$ column, we have 
$$
Q_m\bar{H}_m=\bar{R}_m\in\mathbb{R}^{(m+1) \times m},\texttt{ where }
\bar{R}_m= 
\begin{bmatrix}
R_m \\
\hline
0
\end{bmatrix}
=
\begin{bmatrix}
h_{11}^m & h_{12}^m  & \cdots & h_{1m}^m \\
0 & h_{22}^m  & \cdots & h_{2m}^m \\
\vdots &  \vdots & \ddots & \vdots \\
0 & 0 &  \cdots & h_{m,m} \\
\hline
0 & 0 &  \cdots & 0 \\
\end{bmatrix},
$$
and
$$
Q_m \beta e_1
=
\begin{bmatrix}
g \\
\hline
0
\end{bmatrix}
=
\begin{bmatrix}
\gamma_1\\
\gamma_2\\
\vdots \\
\hline
\gamma_{m+1}
\end{bmatrix}.
$$
Now the residual norm:
$$\begin{aligned}
J(y)^2 &= \gamma_{m+1}^2+\|g-R_my\|_2^2
\end{aligned}$$
and the minimizer $y$ can be find by solving $R_my=g$, and the residual is $|\gamma_{m+1}|$.