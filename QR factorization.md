
# Householder QR

Reflection across the plane orthogonal to a unit normal vector $v$ can be expressed in matrix form as:
$$H=I-2vv^T$$
For example,

$$
\begin{aligned}
Hx &= x-2vv^Tx\\
   &= x-2(v\cdot x)v
\end{aligned}
$$
![[reflect.png|300]]
If we take $u=x-s\|x\|e_1$ where $s=\pm 1$ and $v=\frac{u}{\|u\|}$, then
$$
\begin{aligned}
u\cdot x &= \|x\|^2-s\|x\|x_1 \\
		 &= \|x\|(\|x\|-s x_1)\\
u\cdot u &= \|x\|^2-2s\|x\|x_1+\|x\|^2    \\
         &= 2\|x\|(\|x\|-sx_1)\\
Hx &= \left(I-2\frac{uu^T}{u\cdot u}\right)x \\
   &= (x-u) \\
   &=s\|x\|e_1.
\end{aligned}
$$
![[reflect_to_e1.png|500]]
The Householder reflection operator is unitary and symmetry:
$$
\begin{aligned}
H&=I-2vv^T=(I-2vv^T)^T\\
HH&= (I-2vv^T)(I-2vv^T) = I-4vv^T+4vv^Tvv^T=I.
\end{aligned}
$$
For the reason of numerical stability [ChatGPT explanation](https://chatgpt.com/s/t_6890598223808191a167cd7eea235154) , people uses $w=\frac{u}{u_1}$ instead of $u$ directly. From  $u=x-s\|x\|e_1$, we have $u_1=x_1-s\|x\|$. 
$$\begin{aligned}
u\cdot u &= -2s\|x\|u_1 \\
uu^T &= u_1^2(ww^T) \\
H &= I-2\frac{uu^T}{u\cdot u} \\
  &= I-\tau ww^T, \texttt{ with $\tau=\frac{su_1}{\|x\|}$}.
\end{aligned}
$$
Now, the Householder QR decomposition can be written as:
$$
\begin{aligned}
R&=H_nH_{n-1}\dots H_1A\\
Q&=H_1H_2\dots H_n \\
\texttt{and } QR&= (H_1H_2\dots H_n)(H_nH_{n-1}\dots H_1A)=A.
\end{aligned}
$$
