---
title: "What the Computation Validates"
subtitle: "A finite mathematical construction inspired by CTMU"
date: "19 September 2026 | Research manuscript"
lang: en-US
---

# Abstract

A successful computation can verify a mathematical construction without validating the philosophical theory that motivated it. This paper examines that distinction through CTMU-F 0.2, a finite stochastic model inspired by Christopher Langan's Cognitive-Theoretic Model of the Universe. The model combines an evolving binary rule selector, a four-state data space, and an exponential weighting of complete histories by a chosen recurrence functional. Every one of its 512 supported six-transition histories is enumerated. A retrospective audit reproduces the original probabilities, passes 26 implementation and mathematical-property tests, corrects an inadequately controlled memory diagnostic, and constructs a forward-time Markov representation of the entire weighted ensemble. The representation requires bounded state augmentation and time-dependent transition coefficients, not access to a realized future. Additional analysis distinguishes altered initial preparation from altered conditional evolution, establishes the non-identifiability of an unrestricted utility, and characterizes the dependence on the terminal horizon. These results verify a particular probability model and several consequences of its definitions. They do not establish that the model satisfies CTMU's central claims, that its utility is intrinsic to reality, or that it predicts physical observations. The contribution is a reproducible example of how a metaphysically motivated construction can be made precise, tested against conventional mathematical alternatives, and assigned an evidential status proportional to what was actually demonstrated.

**Keywords:** CTMU; computational verification; finite stochastic systems; exponential tilting; Doob transform; state augmentation; model validation; utility identification.

# 1. Introduction: the object of validation

The statement that a computation validates a theory is incomplete until its object is specified. A program may correctly implement equations whose physical interpretation is unsupported. A mathematical model may be internally coherent while representing only a weakened version of its motivating theory. A distribution may differ dramatically from a baseline because the investigator explicitly defined it to do so.

This paper examines a case in which all three distinctions matter. CTMU-F 0.2 was developed as a computational interpretation of selected CTMU themes. Its initial presentation emphasized changing syntax, globally weighted histories, and apparent memory. A subsequent audit showed that the arithmetic largely survived scrutiny while several interpretations required correction [5].

The claim defended here is therefore narrow:

> The computation verifies a small mathematical construction inspired by CTMU, together with specific consequences of that construction. It does not validate CTMU as a theory of reality.

Here, **verification** concerns the relation between a specification and an implementation. **Constructive mathematical validation** concerns the existence and properties of the specified object. **Interpretive validation** would require an adequate correspondence between that object and the intended theoretical claims. **Empirical validation** would require comparison with observations under a specified physical interpretation. These are working distinctions for this paper, not a claim that every discipline uses the terminology identically.

The investigation is a retrospective computational case study. It contains no physical measurements, fitted physical constants, preregistered hypothesis test, or independently conducted external replication. The supplied audit was rerun for this manuscript, and its result data reproduced exactly after JSON parsing. Additional identities were checked in a separate supplementary script [5,6]. The ordinary proofs below, rather than floating-point agreement alone, establish the general mathematical statements.

# 2. Relationship to the motivating theory

Langan's 2002 paper describes reality as a self-configuring, self-processing language, or SCSPL. It proposes internally unified processing, state and production structure, together with the joint refinement of syntax and state under generalized utility. It also introduces unbound telesis, mind-reality identification, and a stronger-than-ordinary account of recursive determination. Its explicit grammar specification is $\Gamma=(O,R,P,\mu)$, involving processors, products, productions and an initial form [1, pp. 1, 6-7, 36-37, 45].

Those claims motivated the experiment; they were not derived or established by it. In particular, the binary selector $\gamma$ below is not Langan's grammar $\Gamma$. The notation must not disguise the difference.

The implemented model contains an already selected state space, a fixed transition kernel, and an externally specified reward. Its dynamics can change the value of a rule-selecting variable, but it does not internally derive the total interpretation or update mechanism. Consequently, the construction should be evaluated as a proposed finite analogue, not as a faithful implementation established by a correspondence theorem.

The use of an external computer is not itself the objection. A simulation can represent an internally closed mathematical system. The relevant issue is what the represented system contains and which claimed properties have actually been demonstrated. Here, preservation of a finite domain is established; explanatory self-containment is not.

# 3. The finite construction

## 3.1 Configuration space and execution

Let the data space and selector space be

$$
S=\{0,1\}^{2},\qquad G=\{0,1\}.
$$

A complete configuration is

$$
z=(\gamma,s)=(\gamma,(x,y))\in\mathcal Z=G\times S,
\qquad |\mathcal Z|=8.
$$

The term *physical state* used in the original program refers only to the designated component $s$. No experimental meaning is assigned to its bits.

Define deterministic meta-execution by

$$
x_d=x\oplus y\oplus\gamma,\qquad y_d=x,
$$

$$
\gamma_d=\gamma\oplus(x_d\land y_d),
\qquad M(z)=(\gamma_d,(x_d,y_d)).
$$

Here $\oplus$ is exclusive OR and $\land$ is Boolean AND. Let

$$
B(\gamma,(x,y))=(\gamma,(1-x,y)).
$$

The stochastic transition kernel is

$$
K(z,z')=\frac45\mathbf 1_{\{z'=M(z)\}}
       +\frac15\mathbf 1_{\{z'=B(M(z))\}}.
$$

The perturbation is applied after $\gamma_d$ has been calculated. It changes the first data bit but retains that already calculated selector value. This ordering is part of the model and cannot be silently replaced by recomputing the selector after perturbation.

The initial law is uniform, $\mu_0(z)=1/8$. For a supported history $h=(z_0,\ldots,z_T)$,

$$
P_0^{(T)}(h)=\mu_0(z_0)\prod_{t=0}^{T-1}K(z_t,z_{t+1}).
$$

Write $\mathcal H_T$ for the support of this law. All subsequent probability statements concern this support. The principal enumeration uses $T=6$ [5].

## 3.2 Elementary structure of the baseline

**Proposition 1.** The model defines a normalized finite Markov chain. Its uniform distribution is stationary, and $|\mathcal H_T|=8\cdot2^T$.

**Proof.** Each configuration has two distinct successors, with probabilities summing to one. To see that $M$ is a permutation, let its output be $(u,(v,w))$. Its input is recovered uniquely by

$$
x=w,\qquad\gamma=u\oplus(v\land w),
\qquad y=v\oplus w\oplus\gamma.
$$

Since $B$ is also a permutation, $K$ is a convex combination of two permutation matrices. Its columns, as well as its rows, sum to one. Hence the uniform distribution is stationary. Finally, the initial configuration and the sequence of binary branch choices determine distinct complete histories, yielding $8\cdot2^T$ histories. $\square$

The baseline history entropy has the independent expression

$$
H(P_0^{(T)})=\log8+T\left[-\frac45\log\frac45-\frac15\log\frac15\right].
$$

At $T=6$, this is approximately $5.081856$ nats, agreeing with enumeration [6]. This is Shannon entropy of a finite ensemble, not a derived thermodynamic entropy.

## 3.3 History utility and exponential weighting

The chosen recurrence functional is

$$
V_T(h)=\sum_{t=1}^{T}\mathbf 1_{\{s_t=s_0\}}
 +\frac12\sum_{t=2}^{T}\mathbf 1_{\{z_t=z_{t-2}\}}.
$$

The first term rewards returns to the initial data state. The second rewards two-step recurrence of the complete configuration. The coefficient $1/2$ is a modeling choice, not a derived constant.

For finite real $\lambda$, define

$$
P_\lambda^{(T)}(h)=
\frac{P_0^{(T)}(h)e^{\lambda V_T(h)}}{Z_T(\lambda)},
\qquad
Z_T(\lambda)=\sum_{h\in\mathcal H_T}P_0^{(T)}(h)e^{\lambda V_T(h)}.
$$

Positive $\lambda$ favors higher-scoring histories; negative $\lambda$ favors lower-scoring ones. This is an exponential tilt of a path measure. Its relation to established conditioned-process mathematics is substantive, rather than a resemblance in vocabulary [2,3]. The label *telic* is an interpretation proposed for this weighting, not a property established by normalization.

# 4. Mathematical guarantees and their evidential limits

## 4.1 Normalization, recovery and non-idleness

**Proposition 2.** For finite $\lambda$, $P_\lambda^{(T)}$ is a probability law with the same support as $P_0^{(T)}$. At $\lambda=0$ it equals the baseline. For nonzero $\lambda$, equality with the baseline holds if and only if $V_T$ is constant on that support.

**Proof.** The partition sum is finite and strictly positive. At zero tilt it equals one. For nonzero tilt, equality of the two laws requires $e^{\lambda V_T(h)}=Z_T(\lambda)$ for every supported history, which is equivalent to constancy of $V_T$. The converse follows by cancellation. $\square$

Thus the observation that a nonconstant reward changes the distribution is guaranteed by the definition. It is an implementation check, not a discovery favoring a particular metaphysics.

A support qualification is important. With a restriction to an admissible subset $A$ of positive baseline probability, zero tilt gives

$$
P_{0,A}(h)=\frac{P_0(h)\mathbf 1_A(h)}{P_0(A)}.
$$

It recovers the original baseline only when $P_0(A)=1$. The original binary canonicalization operator excludes no admitted configuration and contributes no substantive selection result [5].

## 4.2 Partition identities

Suppress $T$ where unambiguous. Differentiating the finite sum gives

$$
\frac{d\log Z}{d\lambda}=\mathbb E_\lambda[V],
\qquad
\frac{d^2\log Z}{d\lambda^2}=\operatorname{Var}_\lambda(V).
$$

Consequently,

$$
\frac{d\mathbb E_\lambda[V]}{d\lambda}
=\operatorname{Var}_\lambda(V)\geq0.
$$

This monotonicity is not evidence that a system discovers its own purpose. It follows because increasing $\lambda$ increases the relative weights assigned to larger values of the specified score.

The relative entropy is

$$
D_{\mathrm{KL}}(P_\lambda\Vert P_0)
=\lambda\mathbb E_\lambda[V]-\log Z(\lambda).
$$

All logarithms in this paper are natural. Relative entropies and Shannon entropies are therefore reported in nats.

## 4.3 Variational representation

**Proposition 3.** Among probability laws $Q$ on $\mathcal H_T$, the unique maximizer of

$$
\lambda\mathbb E_Q[V]-D_{\mathrm{KL}}(Q\Vert P_0)
$$

is $P_\lambda$, and the maximum is $\log Z(\lambda)$.

**Proof.** Substitute the definition of $P_\lambda$ into relative entropy:

$$
D_{\mathrm{KL}}(Q\Vert P_\lambda)
=D_{\mathrm{KL}}(Q\Vert P_0)-\lambda\mathbb E_Q[V]+\log Z.
$$

Non-negativity, with equality exactly when $Q=P_\lambda$, proves the claim. $\square$

This finite identity belongs to the familiar path-measure variational framework [3]. It establishes that the weighted law balances expected reward against divergence from the chosen baseline. It does not derive either the baseline or the reward, and it does not uniquely identify a physical selection mechanism.

# 5. Computational protocol and numerical results

## 5.1 What was actually computed

The audit enumerates all supported histories rather than sampling them. Baseline probabilities are stored as exact rational numbers; twice the utility is stored as an integer. Exponential tilts use floating-point arithmetic with log-sum-exp normalization. Exhaustive enumeration removes Monte Carlo sampling error, but does not remove numerical rounding or the possibility of a programming mistake [5].

The 26 tests check configuration counts, stochastic normalization, stationary uniformity, agreement with the original program, utility decomposition, partition identities, memory controls, initial-law changes, and the forward Markov reconstruction. They also test constant-reward cancellation, utility rescaling, a target-distribution construction, and horizon dependence. All pass in the manuscript rerun [5,6]. A passing suite is evidence about its tested assertions, not a formal proof of complete program correctness.

The exact baseline moments are

$$
\mathbb E_0[V]=\frac{51679}{25000}=2.06716,
\qquad
\operatorname{Var}_0(V)=\frac{1674043459}{625000000}=2.6784695344.
$$

The partition sum can also be represented as a finite polynomial in $e^{\lambda/2}$ with rational coefficients; the full coefficient table is retained in the result file [5].

## 5.2 Response to the weighting parameter

**Table 1. Globally normalized six-transition ensembles.**

| $\lambda$ | $\mathbb E_\lambda[V]$ | $\operatorname{Var}_\lambda(V)$ | $D_{\mathrm{KL}}(P_\lambda\Vert P_0)$ |
|---:|---:|---:|---:|
| 0.00 | 2.067160 | 2.678470 | 0.000000 |
| 0.25 | 3.169873 | 6.600775 | 0.158445 |
| 0.50 | 5.314536 | 9.500563 | 0.978826 |
| 1.00 | 8.085082 | 1.773354 | 2.876230 |
| 2.00 | 8.476634 | 0.044193 | 3.356899 |

These reproduced values [5,6] show substantial sensitivity to the weighting parameter. They do not compare CTMU with established physics: $P_0$ is the invented finite baseline, not quantum theory, general relativity, or an observationally calibrated physical model.

The increasing mean and eventual reduction in variance indicate concentration on high-scoring histories. That description follows from the score and distribution; further claims about cognition or self-actualization would require separate operational definitions.

## 5.3 Corrected memory diagnostics

The original memory diagnostic omitted the selector $\gamma_t$ and pooled different times. Both choices can confound history dependence. In particular, the designated data component is already non-Markovian under the baseline:

$$
P_0(s_2=(0,1)\mid s_1=(1,1))=\frac12,
$$

$$
P_0(s_2=(0,1)\mid s_1=(1,1),s_0=(1,0))=\frac15.
$$

The difference is $0.300$ before weighting. Prior data states reveal information about an omitted selector, so an observed memory effect is not automatically evidence of a new dynamical principle [5].

**Table 2. Maximum conditional-probability discrepancies.**

| Diagnostic | $\lambda=0$ | $\lambda=1$ |
|:---|---:|---:|
| Original pooled data-state pair test | 0.300000 | 0.679506 |
| Fixed-time data-state pair test | 0.300000 | 0.783755 |
| Fixed-time complete-configuration pair test | Below $10^{-14}$ | 0.343444 |
| Fixed-time augmented state versus full prefix | Below $10^{-14}$ | Below $10^{-14}$ |

Pair tests compare conditioning on the current state with conditioning on current and previous states. The augmented test compares its present state with the complete preceding configuration history. Every corrected comparison holds time fixed [5].

The complete-configuration result shows that weighting does introduce memory relative to $z_t$. However, the maximum discrepancy does not summarize every aspect of dependence. The time-averaged conditional mutual information $I(s_{t+1};s_{t-1}\mid s_t)$ decreases from approximately $0.129511$ to $0.016795$ nats. A larger extreme discrepancy therefore coexists with a smaller probability-weighted measure. Claims that memory simply becomes stronger require a specified metric.

# 6. An exact forward-time Markov representation

## 6.1 Bounded state augmentation

The reward remembers the initial data state and a two-step configuration recurrence. It can therefore be accumulated using

$$
a_t=(s_0,z_{t-1},z_t),
$$

with $z_{-1}=\bot$ at initialization. For a next configuration $z'$ with data component $s'$, set

$$
r(a_t,z')=\mathbf 1_{\{s'=s_0\}}
+\frac12\mathbf 1_{\{z_{t-1}\ne\bot,\ z'=z_{t-1}\}},
$$

$$
f(a_t,z')=(s_0,z_t,z').
$$

Then $V_T(h)=\sum_{t=0}^{T-1}r(a_t,z_{t+1})$. After initialization, the memory space has at most $4\cdot8\cdot8=256$ triples, before reachability restrictions. The time index and terminal horizon additionally enter the transition rule.

## 6.2 Forward-representation theorem

**Theorem 4.** For every finite $T$ and real $\lambda$, the weighted path law has an exact forward, time-inhomogeneous Markov representation on the augmented state space.

**Proof.** Define backward weights by

$$
b_T(a)=1,
\qquad
b_t(a)=\sum_{z'}K(z,z')e^{\lambda r(a,z')}b_{t+1}(f(a,z')),
$$

where $z$ is the current complete configuration contained in $a$. Each weight is positive. Define

$$
Q_t(z'\mid a)=
\frac{K(z,z')e^{\lambda r(a,z')}b_{t+1}(f(a,z'))}{b_t(a)}.
$$

The defining recurrence makes each row sum to one. For $a_0=(s_0,\bot,z_0)$, use the initial law

$$
\mu_\lambda(z_0)=\frac{\mu_0(z_0)b_0(a_0)}{Z_T(\lambda)}.
$$

It is normalized because $Z_T(\lambda)=\sum_{z_0}\mu_0(z_0)b_0(a_0)$. Along a supported history,

$$
\mu_\lambda(z_0)\prod_{t=0}^{T-1}Q_t(z_{t+1}\mid a_t)
=\frac{\mu_0(z_0)\prod_tK(z_t,z_{t+1})e^{\lambda V_T(h)}}{Z_T(\lambda)}.
$$

All intermediate backward weights cancel, and $b_T=1$. The right-hand side is exactly $P_\lambda^{(T)}(h)$. $\square$

This is a finite-horizon Doob-transform construction, consistent with established representations of exponentially weighted path measures [2]. Here it is proved directly for the implemented model. The backward calculation determines coefficients; forward generation does not consult a realized future event.

## 6.3 Computational and interpretive consequences

The audit reconstructs all 512 path probabilities at $\lambda\in\{-1,0,0.5,1,2\}$ under both global and fixed-initial normalization. The largest individual discrepancy is approximately $2.11\times10^{-15}$. This is numerical agreement with an algebraic identity, not an approximate large-time equivalence [5].

**Corollary 4.1.** Any observation obtained from these histories through the same observation rule has the same distribution under the weighted and forward representations.

**Proof.** If $L(y\mid h)$ is an observation kernel, its induced law is $\sum_hL(y\mid h)P(h)$. Equal path laws give equal observation laws. $\square$

Accordingly, no statistic of the specified histories alone distinguishes the two representations. A proposed intervention would require additional rules explaining how each model changes under that intervention; equality of the present path laws does not settle that separate question.

This is not a theorem about spatial locality, relativistic causation, or every possible interpretation of teleology. It shows that this particular global description requires no mathematically distinct alternative to forward stochastic dynamics once sufficient state information and time dependence are included.

# 7. Initial preparation, reward meaning and identifiability

## 7.1 Global selection changes the starting distribution

The initial law is uniform under $P_0$, not generally under $P_\lambda$. At $\lambda=1$, the initial probability of $z_{\mathrm{ref}}=(0,(0,0))$ becomes approximately $0.951001$, rather than $0.125$ [5].

To keep preparation fixed, define

$$
P_\lambda^{\mathrm{fix}}(h)=
\mu_0(z_0)\frac{P_0(h\mid z_0)e^{\lambda V_T(h)}}{Z_T(\lambda;z_0)},
$$

$$
Z_T(\lambda;z_0)=\mathbb E_0[e^{\lambda V_T}\mid z_0].
$$

The conditional continuation laws agree with those of the global ensemble, but the mixture over initial configurations is different. The same $Q_t$ kernels generate this ensemble when initialized with $\mu_0$ instead of $\mu_\lambda$.

**Table 3. Two normalization conventions at $\lambda=1$.**

| Quantity | Global tilt | Fixed initial law |
|:---|---:|---:|
| $P(z_0=z_{\mathrm{ref}})$ | 0.951001 | 0.125000 |
| $\mathbb E[V]$ | 8.085082 | 3.489354 |
| $P(z_T=z_{\mathrm{ref}})$ | 0.883720 | 0.167672 |

Neither convention is mathematically invalid. They answer different questions, and their predictions cannot be interchanged while claiming that the preparation remained fixed [5].

The relative-entropy chain rule makes the distinction explicit:

$$
D_{\mathrm{KL}}(P_\lambda\Vert P_0)
=D_{\mathrm{KL}}(\mu_\lambda\Vert\mu_0)
+\mathbb E_{\mu_\lambda}\!
\left[D_{\mathrm{KL}}(P_\lambda(\cdot\mid z_0)\Vert P_0(\cdot\mid z_0))\right].
$$

It follows by splitting the path likelihood ratio into initial and conditional factors. At $\lambda=1$, the supplementary calculation gives $2.876230=1.794537+1.081693$ nats, to displayed precision [6]. A substantial part of the total divergence concerns altered starting weights.

## 7.2 The selected reward favors stasis

The maximum score at $T=6$ is $8.5$. Exactly three supported histories achieve it, and each remains in a constant complete configuration. Their total probability rises from $0.032784$ to $0.881027$ between $\lambda=0$ and $\lambda=1$. Expected selector changes fall from $1.5$ to approximately $0.094162$ [5].

In the limit $\lambda\to+\infty$, divide all weights by $e^{\lambda V_{\max}}$. Lower-scoring histories vanish, leaving the baseline conditioned on the maximizing histories. The limiting probabilities of the constant histories at $(0,(0,0))$, $(0,(1,1))$, and $(1,(0,0))$ are respectively $2048/2049$, $1/4098$, and $1/4098$ [6].

The result is a particularly simple form of concentration, dominated by remaining unchanged. Calling the reward coherence does not establish a measure of cognition. Calling it self-actualization does not establish a theory of purpose. Those interpretations would need observable criteria that do not merely restate the definition of the reward.

## 7.3 An unrestricted utility specifies any positive target law

**Theorem 5.** Let $Q$ be any strictly positive probability distribution on $\mathcal H_T$. For any fixed nonzero $\lambda$, the choice

$$
V_Q(h)=\frac1\lambda\log\frac{Q(h)}{P_0(h)}
$$

makes the corresponding weighted law equal to $Q$.

**Proof.** Substitution gives $P_0(h)e^{\lambda V_Q(h)}=Q(h)$. The partition sum is therefore one. $\square$

The theorem concerns unrestricted finite utilities. It does not claim that every target law remains obtainable under independently imposed bounds, locality restrictions, or a particular internally generated reward architecture. Its significance is that such restrictions must be supplied before the weighting formula has discriminating explanatory content.

There is also a scale ambiguity. For any nonzero $a$ and real $b$, replacing $V$ by $aV+b$ and $\lambda$ by $\lambda/a$ leaves the normalized law unchanged. Consequently, the numerical meaning of $\lambda$ depends on a fixed utility scale. In the present work it is selected, not measured.

For a specified, nonconstant $V$, the finite family has strictly positive $\operatorname{Var}_\lambda(V)$ and hence a strictly increasing mean score. The parameter is then identifiable at the level of complete path distributions. Observation loss can still impair practical identification. This conditional statistical fact does not supply the missing physical interpretation.

# 8. Horizon dependence and formal amendments

## 8.1 Terminal-horizon dependence

The weighted six-transition law need not equal the six-transition marginal of the seven-transition law. In the audited model their total-variation distance at $\lambda=1$ is approximately $0.076023$; at zero tilt it vanishes to numerical precision [5].

The source of the difference can be stated exactly. For a prefix $h\in\mathcal H_T$, let

$$
c_\lambda(h)=\sum_{z'}K(z_T,z')e^{\lambda r(a_T,z')}.
$$

Then

$$
\sum_{z'}P_\lambda^{(T+1)}(h,z')
=P_\lambda^{(T)}(h)\frac{Z_T(\lambda)}{Z_{T+1}(\lambda)}c_\lambda(h).
$$

The two prefix laws agree if and only if $c_\lambda(h)$ is constant on supported prefixes, with value $Z_{T+1}/Z_T$. The supplementary script checks this identity directly [6].

Thus separate finite-horizon normalizations do not automatically define a single consistent infinite-time process. A boundary prescription, a proven limit, or a different consistent construction is needed. This is a modeling requirement, not a contradiction within any one normalized finite ensemble.

## 8.2 What the executable model did not implement

The original canonicalization map is the identity on admitted configurations and is unused by the transition and weighting calculations. Its idempotence cannot be promoted into a result about emergence from unconstrained possibility [5].

Likewise, a rule selector does not construct a reflexive object in categorical semantics. In the usual notation, such an object requires an exponential $D^D$ and maps

$$
\operatorname{encode}:D^D\to D,
\qquad \operatorname{decode}:D\to D^D,
$$

$$
\operatorname{decode}\circ\operatorname{encode}
=\operatorname{id}_{D^D}.
$$

This is the relevant retraction direction [4, Definition 16]. An earlier proposal reversed it. The correction is to this reconstruction, not an error demonstrated in Langan's paper. No such reflexive object was implemented. In the ordinary category of sets, a finite set with $n>1$ elements cannot encode all $n^n$ self-maps injectively into itself. Restricting the admissible maps or changing the ambient category requires an explicit separate construction.

No observer model, mind-reality correspondence, sheaf-gluing system, quantum amplitude structure, spacetime metric, or operational measurement map was included in the code [5]. Their appearance in earlier conceptual proposals cannot count as computational verification.

# 9. The precise scope of validation

The following distinctions summarize the relation between the mathematical results and the motivating theory.

**Table 4. Evidential status of the construction.**

| Level | Finding |
|:---|:---|
| Implementation checks | The tested computations reproduce their stated specification. |
| Constructive existence | The finite chain and weighted path measures are well defined. |
| Derived properties | Normalization, partition identities and the forward representation follow mathematically. |
| Limited conceptual illustration | Rule-state coupling and whole-history preference have precise finite examples. |
| CTMU correspondence | No proof that the model satisfies the central CTMU claims was supplied. |
| Physical validation | No observational comparison or physically calibrated prediction was performed. |

The formal difference is between exhibiting a model of the toy assumptions and establishing a model of the intended theory. Writing $A_{\mathrm{toy}}$ for the assumptions actually specified, the construction supports

$$
\exists\mathcal M\;(\mathcal M\models A_{\mathrm{toy}}).
$$

It does not establish $\mathcal M\models A_{\mathrm{CTMU}}$, because the required formalization and interpretation have not been provided. Accordingly, it is not a consistency proof for CTMU as a whole. Nor does the inadequacy of this analogue refute a stronger theory that it has not been shown to represent.

The distinction also prevents a misleading inference from successful mathematics to novelty. The use of established probability theory is not a defect. A valuable theory may use familiar methods while adding independently justified constraints, explanatory economy, or successful predictions. What cannot be claimed here is that exponential weighting itself establishes a specifically CTMU mechanism.

Similarly, observational equivalence does not exhaust philosophical evaluation. Two interpretations can agree on outcomes while differing in explanatory commitments. Such commitments should be assessed through their arguments and assumptions, rather than credited with empirical support from a computation that predicts no difference between them.

The main achievement is therefore a clarified boundary. Global preference and forward stochastic evolution coexist in one exact finite model. Apparent memory depends on the state description. Initial preparation must be distinguished from continuation dynamics. A freely adjustable utility supplies flexibility rather than a unique explanation. These are substantive conclusions about the construction and its evidential use.

# 10. Requirements for a stronger successor

A stronger successor should first define the particular theoretical claim it intends to represent and the mathematical conditions that would count as representing it. Terms such as self-configuration, internal interpretation, and observer must correspond to specified operations and invariants, not only names assigned to variables.

The next requirement is an independently restricted utility. A derivation is one route; a clearly stated additional postulate with independently testable consequences is another. The unsuccessful derivation of a utility from selected assumptions would reveal underdetermination in those assumptions, not establish a universal impossibility theorem. Within the present model, retaining the same configuration space and kernel while replacing $V$ by $-V$ already demonstrates that finite transition closure alone does not determine the preference.

A physical application would also require a defined observation map, a justified baseline, and a specification of allowed interventions. The ordinary comparison class must be restricted on independently motivated grounds, such as state dimension, accessible information, symmetry, causal structure, or resource limits. An unrestricted alternative that reproduces the same path law cannot be distinguished using those paths alone. Conversely, ruling out one overly narrow Markov model would not rule out all conventional representations.

Finally, boundary conditions and horizon behavior must be specified before interpreting global selection as a law applying beyond a single finite ensemble. Any asserted large-system or continuum limit would require its own existence and convergence analysis. Recovering the invented baseline at $\lambda=0$ is not a derivation of a known physical limit.

These requirements make the next investigation more demanding but also more informative. Its success would be measured by what the new restrictions explain or predict, not by how dramatically an adjustable reward changes a chosen simulation.

# 11. Conclusion

CTMU-F 0.2 verifies an explicit finite stochastic construction inspired by selected CTMU themes. Its histories can be enumerated completely, its baseline probabilities represented exactly, and its weighted ensemble analyzed both algebraically and computationally. The audit reproduces the numerical results while correcting the interpretation of memory, initialization and reward.

The strongest mathematical result is an exact forward-time Markov representation after bounded state augmentation. The model's global history preference is therefore compatible with an ordinary sequential probability law. Its reward is not derived from CTMU, its parameters are not measured from nature, and its observed concentration largely favors stasis.

What survives is not a computational proof of a theory of everything. It is a reproducible example of disciplined model construction: assumptions are explicit, consequences can be checked, alternative representations can be constructed, and unsupported inferences can be removed without discarding the mathematics that remains valid.

**The computation validates the stated finite construction in a limited mathematical sense. Establishing a correspondence with CTMU, and establishing a correspondence with physical reality, remain separate tasks.**

# Data, code and research disclosure

The accompanying archive contains the preserved original model, the retrospective audit, the manuscript rerun, the supplementary calculation script, and integrity hashes. The audit uses only the Python standard library and was rerun under Python 3.13.5. The original archive is preserved without modification. Full numerical outputs retain greater precision than the tables.

The construction and retrospective analysis originated in an AI-assisted conversation. The present rerun is a reproducibility check of supplied artifacts, not an independent external replication or peer review. No experimental data, human participants, or fitted physical parameters are involved. Tests and ordinary mathematical proofs are reported separately; no proof-assistant verification of this manuscript is claimed.

To reproduce the principal checks from the archive's `reproduction` directory:

```text
cd ctmu_f_02_audit
python audit.py --output ../current_run/audit_results.json
python -m unittest -v test_audit.py
cd ..
python supplement.py
```

# References

[1] Langan, C. M. (2002). *The Cognitive-Theoretic Model of the Universe: A New Kind of Reality Theory*. 56-page paper. Particularly pp. 1, 6-7, 36-37 and 45. Primary source for the motivating claims, not for the finite stochastic model developed here.

[2] Chetrite, R., and Touchette, H. (2014). *Nonequilibrium Markov processes conditioned on large deviations*. arXiv:1405.5157, version 2 consulted; published in *Annales Henri Poincare*, 16 (2015), beginning at p. 2005. DOI: 10.1007/s00023-014-0375-8. Especially Section V.2 and Appendices D-E.

[3] Chetrite, R., and Touchette, H. (2015). *Variational and optimal control representations of conditioned and driven processes*. *Journal of Statistical Mechanics: Theory and Experiment*, P12001. arXiv:1506.05291v3. DOI: 10.1088/1742-5468/2015/12/P12001. Especially Section III.4.

[4] van der Leer, A., Wullaert, K., and Ahrens, B. (2025). *Scott's Representation Theorem and the Univalent Karoubi Envelope*. arXiv:2506.22196v2. Especially Definition 16. Cited for the reflexive-object retraction, not as a validation of CTMU.

[5] *CTMU-F 0.2: Retrospective Computational Audit* (2026). Unpublished generated project artifacts: `audit.py`, `test_audit.py`, `audit_results.json`, `README.md`, preserved original model, and test output. Supplied in the accompanying research archive.

[6] *Manuscript Reproduction and Supplementary Checks* (19 September 2026). Fresh execution logs, reproduced audit results, and `supplement.py` with `supplementary_checks.json`. Includes the initial/conditional relative-entropy decomposition, analytic baseline entropy, maximizing-history limits, and horizon-extension identity. Supplied in the accompanying research archive.
