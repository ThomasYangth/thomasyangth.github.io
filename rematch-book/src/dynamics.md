## Chapter 3: Quantum Dynamics and Conservation Laws

In the previous chapters, we wrote down the Hamiltonians for several Ising models and studied their energy spectra. But a Hamiltonian does more than determine energy levels -- it governs how quantum states change in time. In this chapter, we develop the machinery of quantum dynamics and arrive at one of the most important ideas in physics: **conservation laws** and the operators that encode them.

### 3.1 Time Evolution

The fundamental law governing quantum dynamics is the **Schrodinger equation**:

\\[
i \frac{d}{dt} |\psi(t)\rangle = H |\psi(t)\rangle.
\\]

Here \\( H \\) is the Hamiltonian of the system, and we work in units where \\( \hbar = 1 \\). This equation tells us that the Hamiltonian is the *generator of time evolution*: it dictates how any quantum state changes from one instant to the next.

When \\( H \\) does not depend on time (which is the case for every model in this book), we can solve the Schrodinger equation directly. The solution is

\\[
|\psi(t)\rangle = e^{-iHt} |\psi(0)\rangle,
\\]

where \\( e^{-iHt} \\) is the **time-evolution operator** (see Appendix A for a review of matrix exponentials). We often write \\( U(t) = e^{-iHt} \\).

A crucial property: \\( U(t) \\) is **unitary**, meaning \\( U(t)^\dagger U(t) = I \\). You can verify this by noting that \\( U(t)^\dagger = e^{iHt} \\) when \\( H \\) is Hermitian, so

\\[
U(t)^\dagger U(t) = e^{iHt} e^{-iHt} = I.
\\]

Unitarity guarantees that the norm of the state is preserved: \\( \langle \psi(t) | \psi(t) \rangle = \langle \psi(0) | \psi(0) \rangle = 1 \\). Probabilities are conserved, as they must be.

### 3.2 The Heisenberg Picture

So far, the states evolve and the operators stay fixed. This is the **Schrodinger picture**. There is an equivalent formulation called the **Heisenberg picture**, in which states are frozen at their initial values and operators carry all the time dependence. The two pictures make identical physical predictions.

In the Heisenberg picture, we define the time-evolved operator

\\[
O(t) = e^{iHt} \, O \, e^{-iHt}.
\\]

The expectation value is the same in both pictures:

\\[
\langle \psi(t) | O | \psi(t) \rangle = \langle \psi(0) | \, e^{iHt} O \, e^{-iHt} | \psi(0) \rangle = \langle \psi(0) | O(t) | \psi(0) \rangle.
\\]

**Equation of motion.** We can derive how \\( O(t) \\) changes by differentiating:

\\[
\frac{dO(t)}{dt} = \frac{d}{dt} \left( e^{iHt} O \, e^{-iHt} \right).
\\]

Applying the product rule (and using \\( \frac{d}{dt} e^{iHt} = iH e^{iHt} \\), \\( \frac{d}{dt} e^{-iHt} = -i e^{-iHt} H \\)):

\\[
\frac{dO(t)}{dt} = iH e^{iHt} O \, e^{-iHt} + e^{iHt} O \, (-iH) e^{-iHt} = i \left( H O(t) - O(t) H \right).
\\]

This gives us the **Heisenberg equation of motion**:

\\[
\boxed{\frac{dO(t)}{dt} = i [H, O(t)],}
\\]

where \\( [H, O(t)] = HO(t) - O(t)H \\) is the commutator. This is the quantum analog of Hamilton's equations in classical mechanics, where the commutator plays the role of the Poisson bracket.

The Heisenberg equation is the key formula of this chapter. It says: *the rate of change of any observable is controlled by its commutator with the Hamiltonian.*

### 3.3 Integrals of Motion

Suppose we have an operator \\( A \\) that commutes with the Hamiltonian:

\\[
[H, A] = 0.
\\]

What does the Heisenberg equation of motion tell us?

\\[
\frac{dA(t)}{dt} = i[H, A(t)] = i \, e^{iHt} [H, A] \, e^{-iHt} = 0.
\\]

(In the second step we used the fact that \\( [H, A] = 0 \\) implies \\( [H, A(t)] = e^{iHt}[H,A]e^{-iHt} = 0 \\); you should verify this as an exercise.) So \\( A(t) = A(0) = A \\) -- the operator does not change in time at all!

Consequently, for **any** initial state \\( |\psi(0)\rangle \\):

\\[
\langle \psi(t) | A | \psi(t) \rangle = \langle \psi(0) | A(t) | \psi(0) \rangle = \langle \psi(0) | A | \psi(0) \rangle.
\\]

The expectation value of \\( A \\) is **constant in time**. We call such an operator an **integral of motion** (IOM), or equivalently a **conserved quantity**.

This is the quantum version of a conservation law. Let us summarize the logical chain:

1. \\( [H, A] = 0 \\) (the operator commutes with the Hamiltonian).
2. Therefore \\( dA(t)/dt = 0 \\) (the Heisenberg-picture operator is constant).
3. Therefore \\( \langle A \rangle \\) is constant for every state and for all time.

**Example: energy conservation.** The simplest integral of motion is the Hamiltonian itself, since \\( [H, H] = 0 \\) trivially. This tells us that the expectation value of energy is conserved -- not a surprise, but a good consistency check.

**Example: total magnetization in the Ising model.** Consider the \\( ZZ \\) interaction Hamiltonian on \\( n \\) sites (with no transverse field):

\\[
H_{ZZ} = -\sum_{i=1}^{n-1} Z_i Z_{i+1}.
\\]

Define the **total magnetization** operator

\\[
M = \sum_{i=1}^{n} Z_i.
\\]

Does \\( M \\) commute with \\( H_{ZZ} \\)? We need to check \\( [Z_i Z_{i+1},\, Z_j] \\) for each pair. Since \\( Z \\) matrices commute with each other (\\( [Z_i, Z_j] = 0 \\) for all \\( i, j \\)), we have

\\[
[H_{ZZ}, M] = -\sum_{i,j} [Z_i Z_{i+1}, Z_j] = 0.
\\]

So the total magnetization \\( M \\) is an integral of motion for \\( H_{ZZ} \\). Physically, this means that if you prepare a state with a definite total magnetization (say, 3 spins up and 2 down), the \\( ZZ \\) interaction alone can never change that total.

**What about the transverse field?** Now add the transverse-field term to get the TFIM:

\\[
H_{\text{TFIM}} = -\sum_{i} Z_i Z_{i+1} - h \sum_{i} X_i.
\\]

Is \\( M = \sum_i Z_i \\) still conserved? We need to check \\( [X_i, Z_i] \\). Recall from Chapter 1 that the Pauli matrices satisfy \\( [X, Z] = -2iY \\). Therefore:

\\[
\left[ -h \sum_i X_i, \; \sum_j Z_j \right] = -h \sum_i [X_i, Z_i] = -h \sum_i (-2iY_i) = 2ih \sum_i Y_i \neq 0.
\\]

The transverse field **breaks** the conservation of total magnetization. Intuitively, the \\( X_i \\) operator flips spin \\( i \\), so it changes the number of up-spins and down-spins. Once you turn on the transverse field, \\( \langle M \rangle \\) is no longer constant.

### 3.4 Approximate Integrals of Motion

In many physically interesting systems, we encounter operators that *almost* commute with the Hamiltonian:

\\[
\| [H, A] \| \approx 0 \quad \text{(small but nonzero)}.
\\]

Here \\( \| \cdot \| \\) denotes an appropriate operator norm. Such an operator \\( A \\) is called an **approximate integral of motion** (approximate IOM).

What does this mean physically? Return to the Heisenberg equation:

\\[
\frac{dA(t)}{dt} = i[H, A(t)].
\\]

If the right-hand side is small (in norm), then \\( A(t) \\) changes slowly. The expectation value \\( \langle A \rangle \\) is *nearly* constant -- it is conserved to a good approximation over some timescale, but eventually drifts. The smaller \\( \| [H, A] \| \\) is, the longer \\( A \\) remains approximately conserved.

**Example.** Consider the TFIM with a weak transverse field, \\( h \ll 1 \\). We showed above that \\( [H_{\text{TFIM}}, M] \\) is proportional to \\( h \\). When \\( h \\) is small, the total magnetization is an approximate IOM: it is nearly conserved for times \\( t \ll 1/h \\), but eventually the transverse field causes it to drift.

Approximate integrals of motion turn out to be far more than a curiosity. In certain disordered systems, there exist *extensively many* approximate IOMs that remain nearly conserved for extraordinarily long times. This has profound consequences for the dynamics: the system retains a memory of its initial state far longer than one might naively expect. We will explore these ideas in the chapters ahead.

**Looking forward.** The central question motivating the rest of this book is: *what physical consequences do approximate integrals of motion have?* In particular, when a system possesses many approximate IOMs, how does this constrain its approach to thermal equilibrium? This question will lead us to the phenomena of thermalization, many-body localization, and beyond.

*Last modified: 2026-05-20*
