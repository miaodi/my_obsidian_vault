# Gram-Schmidt process
## Classic Gram-Schmidt
```pseudo
	\begin{algorithm}
	\caption{Classic Gram-Schmidt}
	\begin{algorithmic}
		\For{\texttt{i=1:n}}
	        \State \texttt{$v_i=x_i$}
	        \For{\texttt{j=1:i-1}}
		        \State \texttt{$v_i = v_i - \langle v_i, v_j \rangle v_j$ }
	        \EndFor
	        \State \texttt{$v_i=\frac{v_i}{\| v_i \|}$}
		\EndFor
	\end{algorithmic}
	\end{algorithm}
```

## Modified Gram-Schmidt
```pseudo
	\begin{algorithm}
	\caption{Modified Gram-Schmidt}
	\begin{algorithmic}
		\For{\texttt{i=1:n}}
	        \State \texttt{$v_i=\frac{x_i}{\| x_i \|}$}
	        \For{\texttt{j=i+1:n}}
		        \State \texttt{$x_j = x_j - \langle v_i, x_j \rangle v_i$ }
	        \EndFor
		\EndFor
	\end{algorithmic}
	\end{algorithm}
```

# Arnoldi process
## Basic Arnoldi process
Arnoldi process is an orthogonal projection method onto $\mathcal{K}_m(A, b)$. 
```pseudo
	\begin{algorithm}
	\caption{Basic Arnoldi}
	\begin{algorithmic}
		\State \texttt{$v_1 = \frac{b}{\|b\|}$}
		\For{\texttt{i = 2:m-1}}
			\State \texttt{$v_i = A v_{i-1}$}
			\For{\texttt{j = 1:i-1}}
				\State \texttt{$h_{j, i-1} = \langle v_i, v_j \rangle$}
				\State \texttt{$v_i = v_i - h_{j,i-1}v_j$}
			\EndFor
			\State \texttt{$h_{i, i-1} = \|v_i\|$}
			\If{\texttt{$h_{i, i-1}==0$}} 
			\STATE \texttt{Stop}
			\EndIf
			\State \texttt{$v_i = \frac{v_i}{h_{i, i-1}}$}
        \EndFor
	\end{algorithmic}
	\end{algorithm}
```
$$
\begin{aligned}
Av_1 &= h_{1, 1}v_1 + h_{2, 1}v_2 \\
Av_2 & = h_{1, 2}v_1 + h_{2, 2}v_2 + h_{3, 2}v_3\\
&\dots \\
Av_{m-1} &= h_{1, m-1}v1 + h_{2, m-1}v_2 + \dots + h_{m, m-1}v_{m}
\end{aligned}
$$
or
$$AV_{m-1} = V_{m}\bar{H}$$
where $\bar{H}\in\mathbb{R}^{m\times {m-1}}$. If we use $w_i = v_ih_{i,i-1}$,
$$AV_{m-1}=V_{m-1}H+w_me_m^T$$
where $e_m|_i=\delta_{im}$. Hence,
$$\begin{aligned}
V^T_{m-1}AV_{m-1} &=V^T_{m-1}V_{m-1}H+V^T_{m-1}w_me_m^T\\
&= H
\end{aligned}
$$
## Householder Arnoldi

