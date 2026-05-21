## Chapter 5: Thermalization and Its Absence

In the previous chapters, we built up the tools needed to ask one of the deepest questions in quantum statistical mechanics: *does a closed quantum system reach thermal equilibrium?* We have the Hamiltonian and its dynamics (Chapter 3), the notion of integrals of motion that constrain those dynamics (Chapters 3 and 4), and concrete models -- the TFIM and MFIM -- that illustrate both solvable and non-solvable cases (Chapters 2 and 4). In this chapter, we bring these ideas together.

### 5.1 The Gibbs State

In Chapter 1, we introduced the Boltzmann distribution: a classical system in thermal equilibrium at inverse temperature \\( \beta \\) occupies configuration \\( \mathbf{s} \\) with probability

\\[
p(\mathbf{s}) = \frac{e^{-\beta H(\mathbf{s})}}{Z}, \qquad Z = \sum\_{\mathbf{s}} e^{-\beta H(\mathbf{s})}.
\\]

How do we generalize this to quantum mechanics? In a quantum system, the Hamiltonian \\( H \\) is a matrix (an operator on Hilbert space), not just a function on configurations. The natural generalization is a **density matrix** rather than a probability distribution. The quantum thermal state, called the **Gibbs state**, is

\\[
\boxed{\rho\_{\text{th}} = \frac{e^{-\beta H}}{\text{tr}[e^{-\beta H}]}.}
\\]

Here \\( e^{-\beta H} \\) is the matrix exponential of \\( -\beta H \\) (see Appendix A), and the denominator \\( \mathcal{Z} = \text{tr}[e^{-\beta H}] \\) is the **partition function**, ensuring that \\( \text{tr}[\rho\_{\text{th}}] = 1 \\).

**Why is this the right generalization?** Let \\( H \\) have energy eigenstates \\( |n\rangle \\) with eigenvalues \\( E\_n \\), so that \\( H|n\rangle = E\_n |n\rangle \\). Then

\\[
e^{-\beta H} = \sum\_n e^{-\beta E\_n} |n\rangle\langle n|,
\\]

and therefore

\\[
\rho\_{\text{th}} = \sum\_n \frac{e^{-\beta E\_n}}{\mathcal{Z}} |n\rangle\langle n|, \qquad \mathcal{Z} = \sum\_n e^{-\beta E\_n}.
\\]

In the energy eigenbasis, the Gibbs state is **diagonal**, with the \\( n \\)-th diagonal entry equal to \\( e^{-\beta E\_n}/\mathcal{Z} \\). This is exactly the Boltzmann distribution -- each energy level \\( E\_n \\) is occupied with probability proportional to \\( e^{-\beta E\_n} \\). For a classical Hamiltonian (one that is diagonal in the computational basis), the Gibbs state reduces precisely to the classical Boltzmann distribution from Chapter 1.

The thermal expectation value of any observable \\( O \\) is computed as

\\[
\langle O \rangle\_{\text{th}} = \text{tr}[\rho\_{\text{th}} O].
\\]

This is the quantum generalization of the classical formula \\( \langle O \rangle = \sum\_{\mathbf{s}} p(\mathbf{s}) O(\mathbf{s}) \\).

### 5.2 Thermalization

In Chapter 1, we simply *postulated* the Boltzmann distribution as the equilibrium state of a system at temperature \\( T \\). But a real physical system is not handed a probability distribution by decree -- it evolves in time according to its equations of motion. So a fundamental question arises:

> **Why should a system ever reach the Gibbs state?**

In quantum mechanics, the dynamics are unitary: starting from some initial state \\( |\psi(0)\rangle \\), the system evolves as \\( |\psi(t)\rangle = e^{-iHt}|\psi(0)\rangle \\). A **pure** state remains pure under unitary evolution -- it can never become a mixed state like \\( \rho\_{\text{th}} \\). So in what sense can a system "thermalize"?

The answer is subtle and important. We do not expect the full quantum state to become \\( \rho\_{\text{th}} \\). Instead, **thermalization** is a statement about **local observables**: if \\( O \\) is an observable that acts on a small subsystem (for example, a few neighboring spins), then we say the system thermalizes if

\\[
\langle \psi(t) | O | \psi(t) \rangle  \longrightarrow  \text{tr}[\rho\_{\text{th}} O] \qquad \text{as } t \to \infty,
\\]

where the arrow means the expectation value approaches, and then fluctuates close to, the thermal value. The idea is that a small subsystem cannot tell whether it is part of a pure state or a thermal mixture -- the rest of the system acts as an effective heat bath.

This is a remarkable claim: the deterministic, reversible Schrodinger equation can give rise to the irreversible approach to thermal equilibrium, at least from the perspective of local measurements. And indeed, thermalization is observed in many quantum many-body systems. But not all of them.

### 5.3 How Integrals of Motion Prevent Thermalization

In Chapter 3, we established a clean logical chain: if \\( [H, A] = 0 \\), then \\( \langle A \rangle \\) is constant for all time. Let us now see what this implies for thermalization.

Suppose \\( A \\) is an integral of motion, and we prepare an initial state \\( |\psi(0)\rangle \\) such that

\\[
\langle \psi(0) | A | \psi(0) \rangle \neq \text{tr}[\rho\_{\text{th}} A].
\\]

That is, the initial expectation value of \\( A \\) differs from its thermal value. Since \\( A \\) is conserved, we have \\( \langle A \rangle\_t = \langle A \rangle\_0 \\) for all \\( t \\). Therefore

\\[
\langle A \rangle\_t = \langle \psi(0) | A | \psi(0) \rangle \neq \text{tr}[\rho\_{\text{th}} A] \qquad \text{for all } t.
\\]

The system **can never thermalize** with respect to the observable \\( A \\). The conserved quantity "remembers" its initial value forever and prevents the system from reaching the Gibbs state.

For a generic system, the only integral of motion is the Hamiltonian itself (and functions of it), and the Gibbs ensemble already accounts for energy conservation through the temperature parameter \\( \beta \\). But systems with **many** integrals of motion -- such as integrable systems -- have far more constraints on their dynamics. The TFIM, as we discussed in Chapter 4, is integrable: it possesses extensively many independent conserved quantities. As a result, the TFIM does not thermalize to a Gibbs ensemble.

What happens instead? The system reaches a **generalized Gibbs ensemble** (GGE). If \\( A\_1, A\_2, \ldots, A\_k \\) are all the independent integrals of motion, the GGE is the density matrix

\\[
\rho\_{\text{GGE}} = \frac{1}{\mathcal{Z}\_{\text{GGE}}} \exp\!\left( -\sum\_{j=1}^{k} \lambda\_j A\_j \right),
\\]

where the Lagrange multipliers \\( \lambda\_j \\) are fixed by requiring \\( \text{tr}[\rho\_{\text{GGE}} A\_j] = \langle \psi(0) | A\_j | \psi(0) \rangle \\) for each \\( j \\). This is the most general "thermal-like" state that respects all the conservation laws. The ordinary Gibbs state is the special case where the only conserved quantity is the energy \\( H \\), and the single Lagrange multiplier is the inverse temperature \\( \beta \\).

### 5.4 Prethermalization

The story so far has two clean endpoints: systems with no extra conserved quantities thermalize to the Gibbs state, and integrable systems with many exact conserved quantities thermalize to a GGE. But what about systems that are *close* to integrable -- that have *approximate* integrals of motion?

Recall from Chapter 3 that an approximate IOM is an operator \\( A \\) with \\( \|[H, A]\| \\) small but nonzero. The expectation value \\( \langle A \rangle \\) is nearly constant for times \\( t \lesssim \tau \\), where \\( \tau \\) is set by the size of the commutator, but eventually drifts.

This leads to a striking two-stage relaxation process called **prethermalization**:

1. **Short times** (\\( t \lesssim \tau \\)): The approximate IOMs are effectively conserved, and the system relaxes to a **prethermal state** -- a GGE-like state determined by these approximately conserved quantities. Local observables reach quasi-stationary values that differ from their true thermal values.

2. **Long times** (\\( t \gg \tau \\)): The approximate conservation laws break down, the approximate IOMs drift, and the system eventually thermalizes to the true Gibbs state.

The prethermal regime can be extremely long-lived when the system is close to integrability, producing a clear separation of timescales.

**The MFIM as an example.** This is precisely what happens in the mixed-field Ising model

\\[
H\_{\text{MFIM}} = -\sum\_i Z\_i Z\_{i+1} - h\_x \sum\_i X\_i - h\_z \sum\_i Z\_i.
\\]

When the longitudinal field \\( h\_z \\) is small, the MFIM is a weak perturbation of the TFIM. The TFIM is integrable and possesses extensively many exact IOMs (Chapter 4). When \\( h\_z \\) is turned on, these IOMs are no longer exactly conserved, but they become **approximate** IOMs of the MFIM with \\( \|[H\_{\text{MFIM}}, A]\| \sim h\_z \\). The prethermal timescale is therefore \\( \tau \sim 1/h\_z \\).

Concretely: if you prepare the MFIM in some initial state and track local observables, you will first see them relax (on a timescale set by \\( 1/h\_x \\)) to values that are *not* the thermal values, but rather the values predicted by a GGE built from the TFIM's conserved quantities. The system stays near this prethermal plateau for a time of order \\( 1/h\_z \\), and only after this long time does it finally relax to the true Gibbs state.

This is a beautiful example of how the ideas from Chapters 3 and 4 -- integrals of motion, approximate conservation, and integrability -- have direct, observable consequences for the dynamics of quantum systems.

---

**Summary.** The Gibbs state \\( \rho\_{\text{th}} = e^{-\beta H}/\mathcal{Z} \\) is the quantum generalization of the Boltzmann distribution. Thermalization is the statement that local observables relax to their Gibbs state values under unitary evolution. Exact integrals of motion prevent full thermalization, because they pin certain expectation values to their initial (generically non-thermal) values; integrable systems instead relax to generalized Gibbs ensembles. Approximate integrals of motion lead to prethermalization: the system appears non-thermal on intermediate timescales before eventually reaching true thermal equilibrium. The MFIM, as a weakly broken integrable system, is a concrete example of prethermalization.

*Last modified: 2026-05-20*
