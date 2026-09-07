# Definitions
- A ***bipartite graph*** is a graph whose vertices can be divided into two disjoint sets, i.e. every edge connects a vertex in $U$ to one in $V$. One often write $G=\left(U,V,E\right)$  to denote a bipartite graph whose partition has the parts $U$ and $V$, with $E$ denoting the edges of the graph.
-  A ***matching*** $M$ is a subset $M\subseteq E$ that has no edge incidents to the same vertex.
- A vertex $v\in \left( U \cup V \right)$ is a ***free vertex*** if no edge from $M$ is incident to $v$ (i.e, if $v$ is not matched).
- $P$ is an ***alternating path***, if $P$ is a path in $G$, and for every pair of subsequent edges on $P$, only one of them is in $M$.
- $P$ is an ***augmenting path***, if $P$ is an alternating path with free vertices at the start and end.

```tikz  
\usepackage{xcolor}
\usetikzlibrary{arrows.meta, positioning}
\begin{document}
\begin{tikzpicture}[
	x=1.0cm,y=1.0cm,
	vertex/.style={draw,circle,minimum size=10mm,thick},
	normal/.style={line width=0.9pt},
	match/.style={line width=2.4pt},
	alt/.style={red!70,line width=0.9pt},
	scale=1.25, transform shape
]
% Parameters
\def\xL{0}
\def\xR{6}
\def\dy{1.6}

% Nodes + labels
\foreach \i in {1,...,5} {
	\node[vertex] (a\i) at (\xL,-\i*\dy) {};
	\node[vertex] (b\i) at (\xR,-\i*\dy) {};
	\node[left=6pt]  at (a\i.west) {$a_{\i}$};
	\node[right=6pt] at (b\i.east) {$b_{\i}$};
}

% Thin black edges
\foreach \i in {1,4,5} {\draw[normal] (a\i) -- (b\i);}
\draw[normal] (a4) -- (b5);

% Bold matching edges
\foreach \i in {2,3} {\draw[match] (a\i) -- (b\i);}

% Red diagonals
\foreach \i/\j in {1/2,2/3,3/4} {\draw[alt] (a\i) -- (b\j);}

% Frame (adjust margins as desired)
\draw[rounded corners=2pt,thick] (-1.2,-5.6*\dy) rectangle (\xR+1.2,-0.4*\dy);
\end{tikzpicture}
\end{document}
````
This figure shows a bipartite graph, where $\left\{ a_2-b_2, a_3-b_3\right\}$ is a matching. An augmenting path is given by $\left\{ a_1-b_2-a_2-b_3-a_3-b_4 \right\}$. Vertices $a_1, b_1, a_4, b_4, a_5$ and $b_5$ are free.
# Maximum matching
Given some matching $M$ and an augmenting path $P$, we define: 
$$M'=M\bigoplus P = (M\backslash P)\cup (P \backslash M)$$ Then, $M'$ is also a matching with $|M'|=|M|+1$.
## Theorem
For a given bipartite graph $G$, a matching $M$ is maximum if and only if $G$ has no augmenting paths with respect to $M$.
Proof, see  [ChatGPT](https://chatgpt.com/s/t_691a66b24bf48191ba65c0c36e65f4aa). 

# Reference 
