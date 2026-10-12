Answering my own question: the conjecture is true, and it reduces to the **single**-alphabet case ($y=0$), which is a theorem of Lenart. The argument assumes three standard results and yields an explicit combinatorial formula for $p_u^w(y,\beta)$ in which every term is a single monomial with coefficient $+1$.

Conventions are as in the question: $\mathfrak G_{w_0}(x;y)=\prod_{i+j\le n}(x_i\oplus y_j)$ with $a\oplus b=a+b+\beta ab$, $\pi_i=\partial_i(1+\beta x_{i+1})$ acting on $x$, and $\mathfrak S_w(x;y)=\mathfrak G^{(0)}_w(x;-y)$. Write $\mathfrak G_w(x)=\mathfrak G_w(x;0)$ and $\mathfrak S_w(x)=\mathfrak S_w(x;0)$ for the single polynomials, and $a\star b$ for the Demazure (0-Hecke) product on $S_n$.

## Three known ingredients

**(A) Cauchy formula for double Grothendieck polynomials** (Fomin–Kirillov, *Grothendieck polynomials and the Yang–Baxter equation*, FPSAC 1994; this is the $\beta$-homogenized form). For all $u\in S_n$,
$$
\mathfrak G_u(x;y)\;=\;\sum_{\substack{a,v\in S_n\\ a\star v=u}}\beta^{\ell(a)+\ell(v)-\ell(u)}\;\mathfrak G_{a^{-1}}(y)\,\mathfrak G_v(x).
$$
Equivalently, in the 0-Hecke algebra with $T_i^2=\beta T_i$ (so $T_aT_v=\beta^{\ell(a)+\ell(v)-\ell(a\star v)}T_{a\star v}$),
$\sum_u\mathfrak G_u(x;y)T_u=\Big(\sum_a\mathfrak G_{a^{-1}}(y)T_a\Big)\Big(\sum_v\mathfrak G_v(x)T_v\Big)$.
Note the inverse on the $y$-factor. Each $\mathfrak G_{a^{-1}}(y)$ is a sum over (not necessarily reduced) pipe dreams $P$ of $a^{-1}$ of $\beta^{|P|-\ell(a)}y^{\mathrm{wt}(P)}$, so $\mathfrak G_{a^{-1}}(y)\in\mathbb N[\beta,y]$.

**(B) Lenart's theorem** (*Noncommutative Schubert calculus and Grothendieck polynomials*, Adv. Math. 143 (1999)). For all $v\in S_n$,
$$
\mathfrak G_v(x)\;=\;\sum_{v'\ge v}\beta^{\ell(v')-\ell(v)}\,c_{v,v'}\,\mathfrak S_{v'}(x),\qquad c_{v,v'}\in\mathbb Z_{\ge 0},
$$
with an explicit combinatorial model for $c_{v,v'}$ (see also Lascoux's transition formula for Grothendieck polynomials). This is exactly the $y=0$ case of the conjecture.

**(C) Cauchy formula for double Schubert polynomials.** Let $\Phi(x;y)=\sum_w\mathfrak S_w(x;y)\,u_w$ in the nilCoxeter algebra ($u_i^2=0$, $u_au_v=u_{av}$ when lengths add). Fomin–Kirillov (*The Yang–Baxter equation, symmetric functions, and Schubert polynomials*, 1996; equivalently Macdonald, *Notes on Schubert polynomials*, (6.3)) give $\Phi(x;y)=\Phi(y)^{-1}\Phi(x)$ with $\Phi(x)=\Phi(x;0)$. Hence $\Phi(x)=\Phi(y)\,\Phi(x;y)$, i.e. for all $v'\in S_n$
$$
\mathfrak S_{v'}(x)\;=\;\sum_{\substack{v'=bw\\ \ell(b)+\ell(w)=\ell(v')}}\mathfrak S_b(y)\,\mathfrak S_w(x;y),
$$
and $\mathfrak S_b(y)=\sum_{R}y^{\mathrm{wt}(R)}\in\mathbb N[y]$ over reduced pipe dreams $R$ of $b$.

## The proof

Substitute (B) into (A), then (C) into the result, and read off the coefficient of $\mathfrak S_w(x;y)$:

$$
\boxed{\;
p_u^w(y,\beta)\;=\;
\sum_{\substack{a\star v=u}}\;
\sum_{v'\ge v}\;
\sum_{\substack{b:\ bw=v'\\ \ell(b)+\ell(w)=\ell(v')}}
\beta^{\,\ell(a)+\ell(v')-\ell(u)}\;c_{v,v'}\;\mathfrak G_{a^{-1}}(y)\;\mathfrak S_b(y).
\;}
$$

(The $\beta$-exponent is $(\ell(a)+\ell(v)-\ell(u))+(\ell(v')-\ell(v))$, and it is $\ge 0$ since $a\star v=u$ forces $\ell(u)\le\ell(a)+\ell(v)$ and $v'\ge v$.) Every factor on the right lies in $\mathbb N[\beta,y]$: the $\beta$-power trivially, $c_{v,v'}$ by (B), $\mathfrak G_{a^{-1}}(y)$ and $\mathfrak S_b(y)$ by their pipe-dream expansions. Hence $p_u^w(y,\beta)\in\mathbb N[\beta,y]$. $\blacksquare$

Unwinding, $p_u^w$ is the generating function of triples $(P,D,R)$ — a pipe dream $P$ of $a^{-1}$, an object $D$ counted by $c_{v,v'}$, a reduced pipe dream $R$ of $b$ — glued by $a\star v=u$ and $bw=v'$ (lengths adding), each weighted by the monomial $\beta^{|P|+\ell(v')-\ell(u)}y^{\mathrm{wt}(P)}y^{\mathrm{wt}(R)}$ (the boxed $\beta$-power together with the excess $\beta^{|P|-\ell(a)}$ that $P$ carries inside $\mathfrak G_{a^{-1}}(y)$). No variable is substituted anywhere and no cancellation occurs.

## Remarks

* The whole content of the double statement beyond the single one is the two Cauchy formulas; the only "positivity" input is Lenart's theorem (B), which is necessary anyway since it is the specialization $y=0$.
* Degree check: with $\deg\beta=-1$, $\deg y_i=1$, the right side is homogeneous of degree $\ell(u)-\ell(w)$, as it must be.
* Sanity check, $n=2$: the pairs with $a\star v=s_1$ are $(e,s_1),(s_1,e),(s_1,s_1)$, giving
$$\mathfrak G_{21}(x;y)=(1+\beta y_1)\,\mathfrak S_{21}(x;y)+(2y_1+\beta y_1^2)\,\mathfrak S_{12}(x;y),$$
and indeed $(1+\beta y_1)(x_1-y_1)+2y_1+\beta y_1^2=x_1+y_1+\beta x_1y_1$. For $u=132$ one gets $p^{132}_{132}=(1+\beta y_1)^2(1+\beta y_2)$, $p^{231}_{132}=\beta(1+\beta y_1)(1+\beta y_2)$, $p^{123}_{132}=\big((1+\beta y_1)^2(1+\beta y_2)^2-1\big)/\beta$, and $p^{213}_{132}=0$.
* I have checked the boxed formula against a direct divided-difference expansion for all $u\in S_n$, $n\le 4$, and on samples in $S_5$ (it is implemented as `dgroth_to_dschub_positive` in my `schubmult` package), independently of the $n\le 8$ verification of the conjecture itself mentioned in the question.
* The formula is a sum over *triples*; a single-family model (one decorated pipe dream of $u$ per monomial, in the spirit of (B)) would be nicer, and I don't know one. I'd be glad to hear of one.
