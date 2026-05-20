## Chapter 6: Slow Modes in the Quantum Ising Model

In the previous chapters, we built up a picture of quantum dynamics, integrals of motion, and thermalization. We saw that exact IOMs (as in the TFIM) prevent a system from reaching thermal equilibrium, while systems without IOMs (as in the MFIM at generic parameters) are expected to thermalize. But the boundary between these two regimes is not sharp. In practice, we care about operators that are *approximately* conserved -- operators that change slowly under time evolution. This chapter introduces the concept of **slow modes**, connects it to two concrete mathematical frameworks, and lays out the numerical project that ties everything together.

### 6.1 Defining Slow Modes

Recall from Chapter 3 that an integral of motion satisfies \\( [H, A] = 0 \\), so that \\( A(t) = A \\) for all time. We also introduced approximate IOMs: operators with \\( \|[H, A]\| \\) small but nonzero, whose expectation values drift slowly. Now we want to be more precise about what "slowly changing" means, and we want to add a second requirement.

**Slowness.** Given an operator \\( A \\), we define its **timescale** as

\\[
\tau_A = \frac{\|A\|}{\|[H, A]\|}.
\\]

This has a natural interpretation: since \\( dA(t)/dt = i[H, A(t)] \\), the ratio \\( \|A\| / \|[H,A]\| \\) estimates how long it takes for \\( A(t) \\) to change appreciably relative to its own size. A large \\( \tau\_A \\) means \\( A \\) evolves slowly. An exact IOM has \\( \tau\_A = \infty \\).

**Simplicity.** Slowness alone is not enough. The Hamiltonian \\( H \\) itself is exactly conserved (\\( [H,H] = 0 \\)), but it is typically a sum of many terms spread across the whole system -- it does not tell us anything about *local* physics. More dramatically, any function of \\( H \\) (such as \\( H^2 \\) or \\( e^{iH} \\)) is also exactly conserved, but these are generically very complicated operators with no simple physical interpretation.

What we actually care about are conserved (or approximately conserved) operators that have a significant overlap with **local** or **simple** operators -- operators that you could, in principle, measure by looking at only a few neighboring sites. We call this property **simplicity**.

To make this precise, we need a way to measure how "simple" an operator is. We will introduce such a measure in Section 6.3, but the intuition is clear: an operator that is mostly supported on small clusters of sites is simple, while one that involves complicated correlations among many distant sites is not.

**The tradeoff.** Here is the key physical insight: in a thermalizing system, there is a tension between slowness and simplicity. You can always find slowly evolving operators (functions of \\( H \\)), but they tend to be very complicated. And you can always find simple operators (like a single \\( Z\_i \\)), but they tend to evolve quickly. The interesting question is whether there exist operators that are *both* slow and simple -- what we call **simple slow operators** (SSOs). The existence or absence of SSOs determines whether the system thermalizes.

### 6.2 The Lindbladian Approach

One concrete way to identify slow modes is to couple the system weakly to an environment and ask: which operators survive the longest? This is the idea behind the Lindbladian approach developed in [Paper 1 (arXiv: 2506.02970)](https://arxiv.org/abs/2506.02970).

**The setup.** We add weak **depolarizing noise** to the system. Each qubit independently experiences random Pauli kicks at a small rate \\( \gamma \\). In the Heisenberg picture, the time evolution of an operator \\( O \\) is governed by the **Lindblad master equation**:

\\[
\frac{dO}{dt} = \mathcal{L}^\dagger[O] = i[H, O] + \sum_j \frac{\gamma}{4} \left( L_j^\dagger O L_j - \frac{1}{2}\{L_j^\dagger L_j, O\} \right),
\\]

where the sum runs over all sites \\( j \\) and over jump operators \\( L\_j \in \{X\_j, Y\_j, Z\_j\} \\). The superoperator \\( \mathcal{L}^\dagger \\) is called the **adjoint Lindbladian**. The first term, \\( i[H, O] \\), is the usual unitary (Hamiltonian) evolution. The remaining terms describe the effect of the noise.

**Why depolarizing noise?** This particular choice of noise has a beautiful property. Consider expanding any operator \\( O \\) in the Pauli basis:

\\[
O = \sum_P c_P \, P,
\\]

where \\( P \\) ranges over all \\( n \\)-qubit Pauli strings (products of \\( I, X, Y, Z \\) on each site). Define the **size** of a Pauli string \\( P \\), written \\( S(P) \\), as the number of sites where \\( P \\) acts nontrivially (i.e., is not the identity). For example, \\( S(X\_1 Z\_3) = 2 \\) on a 5-site chain.

Under depolarizing noise *alone* (setting \\( H = 0 \\)), each Pauli string \\( P \\) decays independently at a rate proportional to its size:

\\[
P(t) = e^{-\gamma \, S(P) \, t} \, P.
\\]

This means that operators with small support (low size) decay slowly, while operators with large support decay quickly. The noise acts as a *filter*: it washes away the complicated, nonlocal parts of an operator while preserving the simple parts.

**The key idea.** Now turn the Hamiltonian back on. Under the full Lindbladian \\( \mathcal{L}^\dagger \\), which combines unitary evolution and noise, the dynamics is more complex -- the Hamiltonian mixes Pauli strings of different sizes. But if \\( \gamma \\) is small, the noise is a perturbation on top of the Hamiltonian dynamics. In this regime:

- An operator that is an exact IOM of \\( H \\) and has small size will decay very slowly -- its rate is set by \\( \gamma \\) times its typical size.
- A generic operator will spread to large sizes under Hamiltonian evolution and then get rapidly killed by the noise.

Therefore, the **slowly decaying modes** of the Lindbladian are precisely the operators that manage to remain simple under Hamiltonian dynamics -- that is, the (approximate) IOMs with small support.

**Diagonalizing the Lindbladian.** Since \\( \mathcal{L}^\dagger \\) is a superoperator (a linear map on the space of operators), we can look for its eigenoperators:

\\[
\mathcal{L}^\dagger[O_k] = \lambda_k \, O_k.
\\]

The eigenvalues \\( \lambda\_k \\) are generally complex, with \\( \text{Re}(\lambda\_k) \leq 0 \\) (operators can only decay, not grow). The eigenoperators with the *least negative* real parts -- those closest to zero -- are the **slow modes**. They are the operators that survive the longest under the combined Hamiltonian-plus-noise dynamics.

In the TFIM, the slow modes found this way turn out to be exactly the Majorana bilinear IOMs from Chapter 4, dressed by small corrections from the noise. In the MFIM at generic parameters, no anomalously slow modes appear -- all operators decay at rates set by the noise strength times the system size, indicating chaos.

### 6.3 The Simple Slow Operator Approach

The Lindbladian approach identifies slow modes by coupling to an environment. An alternative, purely Hamiltonian framework was developed in [Paper 2 (arXiv: 2604.13172)](https://arxiv.org/abs/2604.13172). Instead of adding noise, we directly construct a quantity that measures both slowness and simplicity, and then optimize over operators.

**Measuring simplicity: the ensemble variance norm.** We need a concrete way to quantify how "simple" an operator is. The idea is to pick an ensemble \\( \mathcal{E} \\) of simple initial states (such as random product states), and measure how much of \\( A \\) you can "see" from those states.

For the ensemble of **random product states** (RPS), each qubit is independently in a uniformly random pure state. The **ensemble variance norm** is defined as

\\[
\|A\|_{\text{RPS}}^2 = \text{Var}_{\mathcal{E}}\!\left[\langle \psi | A | \psi \rangle\right],
\\]

the variance of the expectation value of \\( A \\) over random product states \\( |\psi\rangle \\). If \\( A \\) is a simple, local operator, different product states will give noticeably different expectation values, so the variance is large. If \\( A \\) is a complicated many-body operator, its expectation value is nearly the same for every product state (it "self-averages"), so the variance is tiny.

There is a beautiful formula for this norm in the Pauli basis. Expand \\( A = \sum\_P c\_P P \\) where \\( P \\) are Pauli strings. Then

\\[
\|A\|_{\text{RPS}}^2 = \sum_P |c_P|^2 \, 3^{-|P|},
\\]

where \\( |P| \\) denotes the weight of the Pauli string \\( P \\) (the number of non-identity factors). Notice the factor \\( 3^{-|P|} \\): Pauli strings with larger weight are exponentially suppressed. This is exactly the quantification of simplicity we want -- the norm is dominated by contributions from low-weight (simple) Pauli strings.

We can write this more abstractly as \\( \|A\|\_{\text{RPS}}^2 = \langle A, \mathcal{M}\_{\text{RPS}}[A] \rangle \\), where \\( \mathcal{M}\_{\text{RPS}} \\) is a superoperator (a diagonal matrix in the Pauli basis) that multiplies each Pauli component by \\( 3^{-|P|} \\), and \\( \langle \cdot, \cdot \rangle \\) is the Hilbert-Schmidt inner product \\( \langle A, B \rangle = \text{tr}(A^\dagger B) / 2^n \\).

**The \\( \nu \\)-\\( \tau \\) plane.** Every traceless operator \\( A \\) (normalized so that \\( \|A\| = 1 \\) in the Hilbert-Schmidt norm) maps to a point in the **\\( \nu \\)-\\( \tau \\) plane**:

\\[
\tau_A = \frac{1}{\|[H, A]\|}, \qquad \nu_A = \|A\|_{\mathcal{E}}^2.
\\]

Here \\( \tau\_A \\) measures slowness (large \\( \tau \\) means slow) and \\( \nu\_A \\) measures simplicity (large \\( \nu \\) means simple). An operator that is both slow and simple sits in the **upper-right** corner of this plane.

The **upper envelope** \\( \nu(\tau) \\) is defined as

\\[
\nu(\tau) = \max_{\substack{A:\, \|A\|=1 \\ \tau_A \geq \tau}} \nu_A.
\\]

It answers the question: among all operators that are at least as slow as \\( \tau \\), what is the maximum simplicity? The shape of \\( \nu(\tau) \\) encodes the system's thermalization properties.

**The main theorem.** Paper 2 proves that if \\( \nu(\tau) \\) decays sufficiently rapidly as \\( \tau \to \infty \\) -- meaning there are no simple slow operators -- then the system thermalizes. More precisely, for any simple initial state from the ensemble \\( \mathcal{E} \\), local observables approach their thermal equilibrium values.

Conversely, if \\( \nu(\tau) \\) remains large out to long timescales (meaning SSOs exist), the system fails to thermalize: there are local observables whose expectation values remember the initial state for a very long time.

**The eigenvalue problem.** To find the operators that maximize \\( \nu\_A \\) subject to a constraint on \\( \tau\_A \\), we use a Lagrange multiplier. This leads to the **generalized eigenvalue problem**

\\[
\mathcal{M}_{\mathcal{E}}[A] + \theta \, (\text{ad}_H)^2 [A] = \mu \, A,
\\]

where \\( (\text{ad}\_H)^2[A] = [H, [H, A]] \\) is the double commutator with \\( H \\), and \\( \theta \geq 0 \\) is a parameter that controls the tradeoff between simplicity and slowness. Varying \\( \theta \\) from 0 to \\( \infty \\) traces out the upper envelope \\( \nu(\tau) \\).

At \\( \theta = 0 \\), we maximize simplicity with no constraint on slowness, so the optimal operators are just single-site Paulis. As \\( \theta \to \infty \\), we demand extreme slowness, and the optimal operators approach the IOMs (if they exist) or become increasingly complex.

### 6.4 The Numerical Problem

Both approaches above reduce to **superoperator eigenvalue problems** that can be solved numerically. Here is the workflow you will follow.

**Step 1: Build the Hamiltonian.** For the mixed-field Ising model on \\( n \\) sites,

\\[
H = -\sum_{i=1}^{n-1} Z_i Z_{i+1} - h_x \sum_{i=1}^n X_i - h_z \sum_{i=1}^n Z_i,
\\]

construct \\( H \\) as a \\( 2^n \times 2^n \\) matrix. You can use [QuSpin](https://quspin.github.io/QuSpin/) to build spin chain Hamiltonians, or construct it directly using Kronecker products in NumPy. For \\( n \\) up to about 10--12, the matrices fit in memory.

**Step 2: Build the superoperator.** We work in the space of \\( 2^n \times 2^n \\) operators, which has dimension \\( 4^n \\). There are two standard ways to handle this:

- **Vectorization.** Reshape each operator \\( A \\) (a \\( 2^n \times 2^n \\) matrix) into a vector of length \\( 4^n \\). Then the commutator \\( [H, A] = HA - AH \\) becomes a matrix-vector multiplication: the superoperator \\( \text{ad}\_H \\) is represented as the \\( 4^n \times 4^n \\) matrix \\( H \otimes I - I \otimes H^T \\).

- **Pauli basis.** Expand everything in the \\( n \\)-qubit Pauli basis. The commutator \\( [H, \cdot] \\) and the simplicity kernel \\( \mathcal{M}\_{\mathcal{E}} \\) become matrices acting on the vector of Pauli coefficients. The Pauli basis has the advantage that \\( \mathcal{M}\_{\text{RPS}} \\) is diagonal (the entry for Pauli string \\( P \\) is \\( 3^{-|P|} \\)).

For the Lindbladian approach (Section 6.2), construct \\( \mathcal{L}^\dagger \\) as a \\( 4^n \times 4^n \\) matrix and find its eigenvalues and eigenoperators.

For the SSO approach (Section 6.3), construct the matrices for \\( \mathcal{M}\_{\mathcal{E}} \\) and \\( (\text{ad}\_H)^2 \\), then solve the eigenvalue problem for a range of \\( \theta \\) values.

**Step 3: Diagonalize.** Use `numpy.linalg.eigh` (or `scipy.sparse.linalg.eigsh` for larger systems) to find the eigenvalues and eigenvectors. For the Lindbladian, you want the eigenvalues with the least negative real part. For the SSO problem, you want the largest eigenvalues \\( \mu \\) at each \\( \theta \\).

**Step 4: Interpret the results.** For each eigenoperator, examine its Pauli decomposition to understand what kind of operator it is. Key questions to ask:

- What is its typical size/weight? (Is it local or nonlocal?)
- Does it resemble a known physical quantity (magnetization, energy density, domain wall operator)?
- How does the decay rate or timescale compare to generic operators?

### 6.5 The Phase Diagram

The ultimate goal of this project is to map out the **slow-mode structure** across the parameter space \\( (h\_x, h\_z) \\) of the MFIM.

**What to scan.** For each point \\( (h\_x, h\_z) \\) on a grid, solve the eigenvalue problem (either Lindbladian or SSO), extract the slowest nontrivial mode, and record its timescale and simplicity. This produces a "phase diagram" of slow modes.

**Expected structure.** Based on the results of Papers 1 and 2, the parameter space has several distinct regions:

1. **Near the TFIM line** (\\( h\_z \approx 0 \\)). The system is integrable, with exact Majorana bilinear IOMs. These are simple and exactly conserved (\\( \tau = \infty \\)). As you turn on a small \\( h\_z \\), the IOMs become approximate -- they acquire a finite but large timescale. This is the **prethermal** regime: the system looks non-thermal on intermediate timescales before eventually thermalizing.

2. **Near the classical Ising line** (\\( h\_x \approx 0 \\)). The dominant slow modes are related to **domain walls** (kinks between regions of up and down spins). In the classical limit \\( h\_x = 0 \\), domain walls are exactly conserved because the \\( ZZ \\) interaction commutes with every \\( Z\_i \\). A small \\( h\_x \\) makes domain walls mobile but does not immediately destroy them as slow modes.

3. **Large fields** (both \\( h\_x \\) and \\( h\_z \\) large compared to the \\( ZZ \\) coupling). Here the system is **fully chaotic**. No simple slow operators exist -- the upper envelope \\( \nu(\tau) \\) drops off rapidly. The system thermalizes quickly, and there is no memory of initial conditions beyond the energy.

4. **Intermediate regions.** Between the integrable/prethermal edges and the fully chaotic interior, there may be a smooth crossover or sharper features. One goal of the project is to determine how abruptly the slow modes disappear as you move into the chaotic regime.

**What to plot.** Useful quantities to visualize across the \\( (h\_x, h\_z) \\) plane include:

- The timescale \\( \tau \\) of the slowest nontrivial mode (excluding the Hamiltonian itself and trivial symmetries).
- The simplicity \\( \nu \\) of the slowest mode.
- The gap between the slowest and second-slowest mode (a large gap indicates a single dominant slow mode; a small gap indicates a cluster).
- The Pauli weight distribution of the slowest mode, to see whether it is a Majorana bilinear, a domain wall operator, or something else.

**Connection to thermalization.** The resulting diagram directly answers the question posed in Chapter 5: *where in parameter space does the MFIM thermalize, and where does it not?* Regions with SSOs are non-thermalizing (or prethermalizing), and regions without SSOs are thermalizing. By studying how the slow modes evolve across the phase diagram, we can build a complete picture of the interplay between integrability, chaos, and thermalization in the quantum Ising model.

This is the central computational project of the book. The tools are linear algebra and exact diagonalization; the physics spans everything we have developed in the previous five chapters.

*Last modified: 2026-05-20*
