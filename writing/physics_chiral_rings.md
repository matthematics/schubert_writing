# Exact vortex-corrected chiral rings of flag-manifold gauge theories, at any rank

*schubmult computes the twisted-mass-deformed twisted chiral ring of the A-twisted quiver gauge theory whose Higgs branch is a (partial) flag manifold — all vortex corrections, all masses, exactly — at ranks far beyond what Coulomb-branch localization can reach.*

---

## The physics problem

Take the 2d $\mathcal N=(2,2)$ linear quiver gauge theory with gauge group

$$G = U(1)\times U(2)\times\cdots\times U(n-1),$$

bifundamental chiral multiplets between adjacent nodes, and $n$ fundamental chirals on the last node. At generic Fayet–Iliopoulos parameters its Higgs branch is the complete flag manifold $Fl(n)$; this is the standard gauged linear sigma model for $Fl(n)$. Switch on

* a complexified FI parameter $t_i$ at each node, $q_i = e^{-t_i}$, and
* twisted masses $m_1,\dots,m_n$ for the $U(n)$ flavor symmetry acting on the fundamentals,

and perform the topological A-twist. The observable is the **twisted chiral ring**: the algebra of twisted chiral operators $\mathcal O_w$,

$$\mathcal O_u\,\mathcal O_v=\sum_w c^{\,w}_{uv}(q,m)\,\mathcal O_w ,$$

equivalently the three-point functions $\langle\mathcal O_u\mathcal O_v\mathcal O_w\rangle_{S^2}$ as exact functions of the FI parameters and the twisted masses.

By the Bethe/gauge correspondence (Nekrasov–Shatashvili) and the Coulomb-branch localization formulas for the A-twist on $S^2$ (Closset–Cremonesi–Park; Benini–Zaffaroni), this ring is the **torus-equivariant quantum cohomology** $QH^*_T(Fl(n))$ of the target: the FI parameters are the quantum parameters and the twisted masses are the equivariant parameters. Its structure constants are three-point, genus-zero, degree-$d$ **equivariant Gromov–Witten invariants**, one for every vortex number $d=(d_1,\dots,d_{n-1})$.

That is exactly what `schubmult_q_double` computes.

## The dictionary

| gauge theory | geometry / schubmult |
|---|---|
| A-twisted $U(1)\times\cdots\times U(n-1)$ quiver GLSM | $QH^*_T(Fl(n))$ |
| $e^{-t_i}$, FI parameter of node $i$ | quantum parameter $q_i$ |
| twisted mass $m_i$ | equivariant parameter $y_i$ |
| eigenvalues of the vector-multiplet scalars $\sigma$ | Chern roots $x_i$ |
| twisted chiral operator $\mathcal O_w$, $w\in S_n$ | quantum double Schubert polynomial $\mathfrak S^q_w(x;y)$ |
| OPE coefficient $c^{\,w}_{uv}(q,m)$ | structure constant output by `schubmult_q_double u - v` |
| coefficient of $q^d=\prod q_i^{d_i}$ | vortex-number-$d$ (worldsheet-instanton) contribution |
| $m\to 0$ | ordinary Gromov–Witten invariants, $QH^*(Fl(n))$ |
| $q\to 0$ | equivariant cohomology, no vortices |
| both $\to 0$ | classical Schubert calculus |

Signs and normalizations of $q$ and $m$ are convention-dependent (factors of $2\pi i$, the sign of $t$); the ring is the same.

## A worked example: $Fl(3)$, the $U(1)\times U(2)$ theory

This theory has six Coulomb vacua, one per permutation $w\in S_3$. The two degree-one operators are $\mathcal O_{s_1}$ and $\mathcal O_{s_2}$ (permutations `2 1 3` and `1 3 2` in one-line notation). Their OPE:

```
$ schubmult_q_double 2 1 3 - 2 1 3
()          q_1
(2, 1)      -y_1 + y_2
(3, 1, 2)   1
```

Reading the three lines:

$$\mathcal O_{s_1}\,\mathcal O_{s_1} \;=\; \mathcal O_{s_2 s_1} \;+\; (m_2-m_1)\,\mathcal O_{s_1} \;+\; q_1\,\mathbf 1 .$$

The first term is classical Schubert calculus, the second is the twisted-mass (equivariant) correction, and the third is a single vortex at the $U(1)$ node — the quantum correction that makes the ring deformed. Every term has total degree 2 once $\deg q_i = 2$ and $\deg m_i = 1$. Products of higher operators have vortices at both nodes:

```
$ schubmult_q_double 2 3 1 - 3 1 2
()          q_1*q_2
(3, 2, 1)   -y_1 + y_3
(4, 2, 1, 3) 1
```

$$\mathcal O_{s_1 s_2}\,\mathcal O_{s_2 s_1} \;=\; (m_3-m_1)\,\mathcal O_{w_0} \;+\; q_1 q_2\,\mathbf 1 \qquad\text{in } QH^*_T(Fl(3)).$$

The software computes in the stable limit $Fl(\infty)$, so its output also lists `(4, 2, 1, 3)`, a class that only exists for $n\ge 4$; restricting to $Fl(3)$ means discarding every permutation that is not in $S_3$. The two surviving terms are the two-vortex sector (one vortex at each node) and the top equivariant class.

## $Fl(4)$: the $U(1)\times U(2)\times U(3)$ theory

Here rank $G=6$ and there are 24 vacua. The square of the operator $\mathcal O_{s_1 s_3}$ (one-line `2 1 4 3`):

```
$ schubmult_q_double 2 1 4 3 - 2 1 4 3 --display-mode latex
()             q_{1} q_{3}
(1, 2, 4, 3)   q_{1} (y_{4} - y_{3})
(2, 1)         q_{3} (y_{2} - y_{1})
(1, 2, 5, 3, 4) q_{1}
(1, 3, 4, 2)   q_{1}
(2, 1, 4, 3)   (y_{2} - y_{1})(y_{4} - y_{3})
(3, 1, 2)      q_{3}
(2, 1, 5, 3, 4) y_{2} - y_{1}
(2, 3, 4, 1)   y_{2} - y_{1}
(3, 1, 4, 2)   y_{4} - y_{1}
(4, 1, 2, 3)   y_{4} - y_{3}
(3, 1, 5, 2, 4) 1
(3, 2, 4, 1)   1
(4, 1, 3, 2)   1
(5, 1, 2, 3, 4) 1
```

Eleven operators of $Fl(4)$ appear (the four lines containing a 5 are $Fl(5)$ classes from the stable limit and are dropped). The vortex expansion is visible by inspection: the $q^0$ terms are the equivariant classical product, the $q_1$ and $q_3$ terms are single vortices at the first and third nodes (the two commuting $\mathfrak{sl}_2$'s inside $Fl(4)$, each behaving like the $Fl(3)$ computation above), and $q_1q_3$ is the two-vortex sector. No $q_2$ appears in this product. Every coefficient is a polynomial in the $q_i$ and in the mass differences $m_j - m_i$, $i<j$, with **nonnegative** integer coefficients — Mihalcea's equivariant quantum positivity theorem, which is the mathematical statement of the expectation that a vortex expansion with masses has positive weights.

## Partial flags: $U(k)$ SQCD with $n$ flavors

The simplest case physicists actually study is a single node: 2d $\mathcal N=(2,2)$ $U(k)$ gauge theory with $n$ fundamental chirals, Higgs branch the Grassmannian $Gr(k,n)$, one FI parameter $q=e^{-t}$ of degree $n$, twisted masses $m_1,\dots,m_n$. The Coulomb vacua are the $\binom nk$ choices $\sigma=(m_{i_1},\dots,m_{i_k})$; the operators are the Schubert classes $\sigma_\lambda$, $\lambda$ a partition in the $k\times(n-k)$ box. In schubmult a partial flag is specified by its block sizes, so $Gr(2,4)$ — $U(2)$ with four flavors — is `--parabolic 2 2`, and the Schubert classes are the permutations with a single descent at position 2: `1324` $=\sigma_1$, `2413` $=\sigma_{21}$, `3412` $=\sigma_{22}$ (the point class), and so on.

```
$ schubmult_q_double 1 3 2 4 - 2 4 1 3 --parabolic 2 2 --display-positive
()            q_1
(2, 4, 1, 3)  -y_1 + y_4
(3, 4, 1, 2)  1
```

$$\sigma_1\,\sigma_{21} \;=\; \sigma_{22} \;+\; (m_4-m_1)\,\sigma_{21} \;+\; q\,\mathbf 1 .$$

At $m=0$ this is the quantum Pieri relation $\sigma_1\sigma_{21}=\sigma_{22}+q$ that appears in every treatment of $QH^*(Gr(2,4))$, with the mass correction now included. A more interesting one, the square of the point class:

```
$ schubmult_q_double 3 4 1 2 - 3 4 1 2 --parabolic 2 2 --display-positive
()            q_1**2
(1, 3, 2)     (-y_1 + y_3)*(-y_2 + y_4)*(-y_2 + y_3)*q_1
(1, 4, 2, 3)  (-y_2 + y_4)*(-y_2 + y_3)*q_1
(2, 3, 1)     (-y_1 + y_3)*(-y_2 + y_3)*q_1
(2, 4, 1, 3)  (-y_1 + y_2 - y_3 + y_4 + 2*(-y_2 + y_3))*q_1
(3, 4, 1, 2)  (-y_1 + y_3)*(-y_1 + y_4)*(-y_2 + y_4)*(-y_2 + y_3)
```

Read physically, vacuum by vacuum. The $q^0$ term is $(m_3-m_1)(m_4-m_1)(m_3-m_2)(m_4-m_2)\,\sigma_{22}$: the point class is supported on the vacuum $\sigma=(m_1,m_2)$, and the coefficient is exactly the product of the effective masses $m_j-\sigma_a$ of the four fundamentals that are massive there — the one-loop determinant that Coulomb-branch localization produces at that vacuum. The $q^1$ terms are one-vortex corrections weighted by masses (the $\sigma_{21}$ coefficient is $(m_3+m_4-m_1-m_2)\,q$, written by `--display-positive` in the simple roots $m_{i+1}-m_i$), and $q^2\,\mathbf 1$ is the two-vortex sector; at $m=0$ the product collapses to $\sigma_{22}^2=q^2$, which at $q=1$ is the statement that the top field of the $U(2)$ level-$2$ WZW model fuses with itself to the identity.

### Stability, and why the block sizes must be given

For complete flags the coefficients are **stable**: $c^{\,w}_{uv}$ computed in $Fl(N)$ for any $N\ge n$ agrees with $Fl(n)$ once permutations outside $S_n$ are discarded. That is what lets the software work in $Fl(\infty)$ with a single set of $q_i$, and it is why the $Fl(3)$ and $Fl(4)$ outputs above contained a few extra lines. Partial-flag coefficients are **not** stable in this sense: the degree of $q$ is $n$ for $Gr(k,n)$, so the vortex corrections depend on the number of flavors even when the operators do not. The same two operators in $U(2)$ with five flavors:

```
$ schubmult_q_double 1 3 2 4 - 2 4 1 3 --parabolic 2 3 --display-positive
(2, 4, 1, 3)     -y_1 + y_4
(2, 5, 1, 3, 4)  1
(3, 4, 1, 2)     1
```

$$\sigma_1\,\sigma_{21} \;=\; \sigma_{22}+\sigma_{31}+(m_4-m_1)\,\sigma_{21}\qquad\text{in }Gr(2,5):$$

no vortex term at all, because $\deg q=5>3$. So a Grassmannian or partial flag computation must be told the block sizes (`--parabolic k n-k`, or `--parabolic a b c` for a two-step flag), whereas a complete-flag computation needs no $n$. Internally the partial-flag answer is obtained from the complete-flag one by the Peterson–Woodward comparison formula, in the equivariant form due to Huang and Li, which is why the same kernel serves every quiver in the $A$ series.

`--display-positive` rewrites each coefficient as a manifestly positive expression — for mixed variables, as a sum of products of roots $y_i-z_j$ found by integer programming; for a single set of masses, in the simple roots $m_{i+1}-m_i$ — which is the form in which the localization one-loop factors appear. It is optional and costs a little time; the raw output is the same polynomial.

## What you actually get

A single coefficient $c^{\,w}_{uv}(q,m)$ is the natural unit: it is a three-point function (with the third operator in the Poincaré-dual basis; the equivariant two-point pairing, a polynomial in the masses, converts to any other basis), and a three-point function is exactly what one residue computation, one Bethe-ansatz calculation, or one mirror-symmetry prediction produces. Concretely:

- **Ground truth for localization.** A Coulomb-branch correlator is a sum over Bethe vacua of one-loop determinants times an inverse Hessian, and beyond $Fl(3)$ the Bethe equations have no closed-form solution, so at rank the residue sum is evaluated at numerical $(q,m)$ — one point at a time, with the vacua found numerically. The exact coefficients here turn that into a check: contract $c^{\,w}_{uv}$ with the equivariant pairing to get $\langle\mathcal O_u\mathcal O_v\mathcal O_w\rangle$ as a polynomial in $q$ and $m$, evaluate at the same numerical point, and compare; the integrality of the coefficients means a handful of points already verifies the polynomial identity.
* **Duality checks.** Level–rank duality for Grassmannians and the quiver-mutation dualities of flag quivers (Benini–Park–Zhao) require isomorphic twisted chiral rings once masses and FI parameters are mapped. The equivariant quantum cohomology is the invariant object both sides must reproduce, coefficient by coefficient.
* **Surface defects.** Coupled to 4d $\mathcal N=2$ $SU(n)$ gauge theory as a surface operator (Gukov–Witten, Gaiotto–Gukov–Seiberg), the 2d twisted masses become the 4d Coulomb-branch parameters and the ring relations reproduce the Seiberg–Witten curve. The $m$-dependence of every coefficient is dependence on the 4d moduli.
* **Coulomb vacua without solving Bethe equations.** The idempotents of the ring are the vacua; the spectrum of multiplication by $\mathcal O_{s_i}$ gives the $\sigma$-vevs — the Bethe roots of the Toda or five-vertex model — as exact algebraic functions of $(q,m)$, rather than numerically one vacuum at a time.
* **Mirror symmetry.** Rietsch's Landau–Ginzburg mirror of the flag variety predicts each of these coefficients from its Jacobi ring; every coefficient is one check of the mirror, including its equivariant form.
* **Data.** Positive combinatorial formulas for these coefficients are known for Grassmannians (Buch–Mihalcea's equivariant quantum puzzles) and unknown for flag manifolds; exact data at $n=7,8$ is where conjectures get made and killed.

## Integrable systems

The same ring has a second life. Kim's theorem (after Givental–Kim) identifies $QH^*_T(Fl(n))$ with the algebra of conserved charges of the **quantum Toda chain**: the relations of the twisted chiral ring are

$$H_k(\sigma;\,q)=e_k(m_1,\dots,m_n),\qquad k=1,\dots,n,$$

with $H_k$ the quantum Toda Hamiltonians, the twisted masses as the spectrum and $q_i$ the exponentiated Toda coordinates. This is the flag-manifold instance of the Bethe/gauge correspondence. For Grassmannians (`--parabolic`), Gorbounov–Korff realize the equivariant quantum cohomology as a Bethe algebra of a five-vertex model with the $m_i$ as inhomogeneities, and at $q=1$, $m=0$ the structure constants become the fusion rules of the $U(k)$ WZW model (Witten; Korff–Stroppel). Structure constants computed here are therefore also matrix elements in those integrable models.

## Why this is out of reach by the usual methods

The physics route to $c^{\,w}_{uv}(q,m)$ is Coulomb-branch localization: sum Jeffrey–Kirwan residues over the solutions of the vacuum (Bethe) equations $\partial W_{\rm eff}/\partial\sigma_a\in 2\pi i\,\mathbb Z$. For the $Fl(n)$ quiver, $\operatorname{rank}G=n(n-1)/2$ and there are $n!$ vacua. The literature works out $\mathbb P^{N-1}$, $Gr(2,4)$ and $Fl(3)$ (rank 3, six vacua); $Fl(4)$ (rank 6, 24 vacua) is already a substantial symbolic computation, and the result still has to be rotated from the $\sigma$ basis into the operator basis in which the coefficients are enumerative.

`schubmult_q_double` produces the exact OPE of two arbitrary operators in the $Fl(8)$ theory — rank 28, 40 320 vacua — in about 24 seconds on a laptop, and does the same for any partial flag quiver via the Peterson–Woodward comparison formula (Huang–Li for the equivariant case). Since version 5.0 the multiplication kernels are compiled C++; the coefficients themselves are exact symbolic expressions, never numerically evaluated.

## Using it

```
pip install --pre schubmult
```

Binary wheels are provided for Linux, macOS and Windows (CPython 3.10–3.14); no compiler is needed.

Command line — permutations in one-line notation, separated by `-`:

```
schubmult_q_double 3 1 4 2 - 2 4 1 3                # QH*_T(Fl(4))
schubmult_q_double 3 4 1 2 - 3 4 1 2 --parabolic 2 2  # QH*_T(Gr(2,4)): U(2), 4 flavors
schubmult_q_double 2 1 4 3 - 2 1 4 3 --display-positive  # manifestly positive coefficients
schubmult_q_double --code 1 0 1 - 0 2               # permutations given by Lehmer code
schubmult_q        2 1 4 3 - 2 1 4 3                # non-equivariant (m = 0)
schubmult_double   2 1 4 3 - 2 1 4 3                # no vortices (q = 0)
```

Python:

```python
from schubmult import QDSx, Permutation

p = QDSx([2, 1, 4, 3]) * QDSx([2, 1, 4, 3])     # element of QH*_T(Fl(4)) in the Schubert basis
p[Permutation([1, 2, 4, 3])]                      # -> (-y_3 + y_4)*q_1
```

Coefficients are `symengine` expressions in `q_i` and `y_i` and can be substituted, expanded, or exported to LaTeX (`--display-mode latex` on the command line).

---

*The mathematics: the operators $\mathcal O_w$ are the quantum double Schubert polynomials $\mathfrak S^q_w(x;y)$ of Kirillov–Maeno and Ciocan-Fontanine–Fulton, which represent the equivariant Schubert classes in $QH^*_T(Fl(n))$; the structure constants are computed by an exact combinatorial algorithm (no localization, no residues) that reduces the product to iterated Pieri/Monk-type steps. Positivity of the output in the $q_i$ and $y_{j}-y_i$ is a theorem of Mihalcea. References: Witten, "The Verlinde algebra and the cohomology of the Grassmannian"; Givental–Kim, "Quantum cohomology of flag manifolds and Toda lattices"; Kim, "Quantum cohomology of flag manifolds G/B and quantum Toda lattices"; Nekrasov–Shatashvili, "Supersymmetric vacua and Bethe ansatz"; Closset–Cremonesi–Park, "The equivariant A-twist and gauged linear sigma models on the two-sphere"; Gorbounov–Korff, "Quantum integrability and generalised quantum Schubert calculus"; Mihalcea, "Positivity in equivariant quantum Schubert calculus"; Woodward, "On D. Peterson's comparison formula for Gromov–Witten invariants of G/P"; Huang–Li, "On equivariant quantum Schubert calculus for G/P".*
