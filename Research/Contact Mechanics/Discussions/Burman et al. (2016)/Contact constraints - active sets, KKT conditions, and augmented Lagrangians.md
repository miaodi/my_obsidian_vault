# Contact constraints: active sets, KKT conditions, and augmented Lagrangians

Parent review: [[Research/Contact Mechanics/Burman et al. (2016) - Augmented Lagrangian finite elements]]

Discussion date: 2026-09-07. Source: Burman, Hansbo and Larson, arXiv:1609.03326v1 (Zotero ZAV78EWP), pp. 1–2, equations (1.1), (1.2), (2.1). The equation and sign conventions were verified against the original PDF's web text; Zotero extraction dropped symbols.

## Question and source statement

How does equation (2.1) encode contact?

$$\lambda=-\gamma^{-1}[u-\gamma\lambda]_+,\qquad [x]_+=\max(0,x),\quad \gamma>0.$$

The paper uses $u\le0$, $\lambda\le0$, $u\lambda=0$. Positive displacement penetrates the obstacle; negative multiplier is compression. Equation (2.1) replaces these three conditions by one nonlinear equality.

> [!important] Main value of equation (2.1)
> **It exactly converts the contact inequality and complementarity part of the KKT conditions into a single nonlinear, nonsmooth equality, for every positive $\gamma$.** Equilibrium supplies the remaining stationarity condition. This is the key interpretation identified and understood by the user in discussion.

## Discussion-derived explanation and algebra

At each point set $q=u-\gamma\lambda$.

- If $q\le0$, the positive part vanishes, hence $\lambda=0$. Then $q=u\le0$: separation or unloaded touching.
- If $q>0$, $\lambda=-q/\gamma<0$. Multiplication by $\gamma$ gives $\gamma\lambda=-u+\gamma\lambda$, hence $u=0$: touching under compression.

Conversely, if the three contact conditions hold, either $\lambda=0$ and $u\le0$, or $\lambda<0$ and $u=0$. Substitution in either case proves (2.1). The corner $u=\lambda=0$ is included.

The identity is exact for every positive $\gamma$ at the continuous algebraic level; no limit $\gamma\to0$ is needed. Discrete stability and parameter selection are separate issues. It is an implicit relation between two unknowns, not an explicit force formula from displacement alone. Equilibrium determines the reaction magnitude on the contact branch.

Illustrative checks (ours), with $\gamma=1$: $(u,\lambda)=(-2,0)$ and $(0,-3)$ satisfy the identity; $(-2,-3)$ does not because its right side is $-1$, not $-3$.

## Why equation (2.2) subtracts the multiplier square

Source locator: p. 2, equations (2.2)–(2.3). The following differentiation and branch expansion are discussion-derived explanations of those formulas.

The user asked whether $-\gamma\|\lambda\|_C^2/2$ makes the multiplier unique because contact permits any negative multiplier. Its direct purpose is instead to produce exactly the contact equation under multiplier stationarity.

$$D_\lambda\left(\frac1{2\gamma}\|[u-\gamma\lambda]_+\|_C^2\right)[\mu]=-\langle[u-\gamma\lambda]_+,\mu\rangle_C,$$
$$D_\lambda\left(-\frac\gamma2\|\lambda\|_C^2\right)[\mu]=-\gamma\langle\lambda,\mu\rangle_C.$$

Their sum vanishes precisely when $[u-\gamma\lambda]_++\gamma\lambda=0$, i.e. (2.1). Without the third term, multiplier stationarity would give only $[u-\gamma\lambda]_+=0$, which is not complementarity and excludes compressed contact.

On the branch $u-\gamma\lambda>0$, the scalar contact density expands to

$$\frac{(u-\gamma\lambda)^2}{2\gamma}-\frac\gamma2\lambda^2=\frac{u^2}{2\gamma}-u\lambda.$$

Thus the subtraction cancels the multiplier square, recovering the mixed coupling and a displacement penalty. At $u=0$, the density is zero for every $\lambda\le0$; it does not by itself select a unique contact pressure. Equilibrium determines the multiplier together with displacement. The functional is treated through stationarity/saddle structure, not joint minimization in $u$ and $\lambda$.

## Active sets: the physical meaning of a contact multiplier

Discussion update: 2026-09-07. The explanation below is our pedagogical reconstruction, not a solver algorithm claimed or analyzed by the paper. It connects the contact conditions on p. 1 to equations (2.1)–(2.3) on p. 2.

> [!important] Contact constraints are temporary supports
> **Impose $u=0$ on a guessed active contact region and compute the reaction needed to enforce it. Add a constraint if an unconstrained location penetrates; release a constraint if its reaction would require the obstacle to pull.** The condition $\lambda\le0$ means “the obstacle only pushes.” This interpretation made the multiplier formulation clear to the user.

For a guessed active region $A$:

- On $A$, impose $u=0$ and solve for the unknown reaction $\lambda$.
- Outside $A$, set $\lambda=0$ and retain the displacement unknowns.
- After solving, add inactive locations with $u>0$ to $A$ and release active locations with $\lambda>0$.
- Repeat until the inequalities are satisfied. Borderline points and cycling require suitable update rules in an actual solver.

Only inactive multiplier unknowns can be omitted; displacement unknowns outside contact remain in equilibrium. A current separation does not imply permanent separation. These pointwise/nodal descriptions assume a compatible discrete constraint representation; general multiplier bases and weak contact constraints need corresponding discrete inequalities.

With a fixed active set, a typical discrete system is

$$
\begin{bmatrix}K&-B_A^T\\B_A&0\end{bmatrix}
\begin{bmatrix}U\\\Lambda_A\end{bmatrix}
=
\begin{bmatrix}F\\0\end{bmatrix}.
$$

Here $B_AU=0$ represents the active contact constraints. Displacement and reaction are solved simultaneously. Staggering is a solver choice, not a requirement of Lagrange multipliers.

## From active sets to the ordinary Lagrangian and KKT conditions

Define $E(u)=\frac12a(u,u)-(f,u)_\Omega$. In the paper's negative-reaction convention the ordinary Lagrangian is

$$L(u,\lambda)=E(u)-\langle\lambda,u\rangle_C,\qquad
\min_{u\in V}\max_{\lambda\le0}L(u,\lambda).$$

This formal expression assumes suitable displacement and multiplier spaces and pairing. The equilibrium condition is

$$a(u,v)-\langle\lambda,v\rangle_C=(f,v)_\Omega.$$

Constrained maximization in $\lambda$ supplies $u\le0$, $\lambda\le0$, and $u\lambda=0$. Unrestricted stationarity in the ordinary multiplier would instead impose $u=0$ on the entire potential contact region, preventing separation.

The contact conditions express two admissible states: separation with zero reaction, or touching with a compressive reaction. They are the contact part of the KKT system; equilibrium supplies stationarity.

For general finite-dimensional constraints $g_i(x)\le0$, use nonnegative multipliers $p_i\ge0$:

$$L(x,p)=E(x)+\sum_i p_i g_i(x),$$
$$\nabla E(x)+\sum_i p_i\nabla g_i(x)=0,\qquad
g_i(x)\le0,\quad p_i\ge0,\quad p_i g_i(x)=0.$$

Here $p=-\lambda$ for the paper's contact convention. Under appropriate constraint qualifications KKT conditions are necessary at a local optimum; convexity provides the usual sufficiency conditions. An active-set method guesses which $g_i=0$ constraints to enforce and sets the remaining multipliers to zero. The compact KKT form hides the switching decision and requires a suitable constrained or complementarity solver.

## Projected multiplier updates and the positive-part equality

One illustrative projected Uzawa iteration first solves equilibrium with the current multiplier:

$$a(u^{k+1},v)=(f,v)_\Omega+\langle\lambda^k,v\rangle_C.$$

Then, since the multiplier gradient is $-u^{k+1}$, take an ascent step and project:

$$\lambda^{k+1}=\min(0,\lambda^k-\rho u^{k+1}),\qquad\rho>0.$$

This is pointwise in an appropriate function setting, or componentwise for compatible discrete variables with the chosen metric. General FEM coefficient gradients/projections can involve mass matrices. The formula does not establish convergence of the iteration.

At a fixed point, with $\rho=1/\gamma$,

$$\lambda=\min(0,\lambda-u/\gamma)
=-\gamma^{-1}[u-\gamma\lambda]_+.$$

Thus equation (2.1) encodes the same contact logic as a projection fixed point. Coupling it with equilibrium also permits simultaneous nonlinear solution, for example using a suitable semismooth Newton method.

## Penalty terms and positive-part multiplier coupling are different

The ordinary coupling is $-\langle\lambda,u\rangle_C$, with $\lambda\le0$. Replacing it by $-\langle\lambda,[u]_+\rangle_C$ can encode feasibility through maximization, but loses the ordinary reaction interpretation: at $u<0$ the coupling vanishes for every multiplier, so it does not select zero reaction during separation. Its displacement dependence is nonsmooth at touching.

A quadratic penalty is valid:

$$E_\varepsilon(u)=E(u)+\frac1{2\varepsilon}\|[u]_+\|_C^2,\qquad
\lambda_\varepsilon=-\varepsilon^{-1}[u]_+.$$

A nonzero penalty reaction requires positive penetration at finite $\varepsilon$. The augmented relation instead permits a compressive reaction at exact contact $u=0$.

## Discussion progress

The user has confirmed the exact KKT-reformulation interpretation and the active-set interpretation of multipliers as reactions enforcing temporary zero-displacement constraints. The multiplier-square subtraction in (2.2) generates the correct contact stationarity equation; it does not independently select a unique reaction at fixed $u=0$.

Next starting point: connect displacement variation of the augmented functional to equilibrium in (2.3). Include the load potential $-(f,u)_\Omega$ when deriving its right-hand side; the displayed (2.2) omits that term.
