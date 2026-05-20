## Chapter 2: The Quantum Ising Model

In Chapter 1, we studied the classical Ising model: a collection of spins \\( s\_i = \pm 1 \\) sitting on a lattice, interacting with their neighbors. The energy was a simple function of the spin configuration, and "solving" the model meant finding the configuration(s) that minimize the energy. In this chapter, we upgrade the Ising model to a quantum system. This is where things get genuinely interesting -- and where the physics of thermalization ultimately lives.

---

### 2.1 From Classical Spins to Qubits

In the classical Ising model, each site \\( i \\) holds a spin that is either "up" (\\( s\_i = +1 \\)) or "down" (\\( s\_i = -1 \\)). A configuration of \\( L \\) spins is just a list of \\( \pm 1 \\) values, and the state of the system is always one of these \\( 2^L \\) configurations.

In the quantum version, we replace each classical spin with a **qubit** -- a quantum two-level system. You already know from Nielsen and Chuang that a single qubit lives in a 2-dimensional Hilbert space \\( \mathcal{H} \cong \mathbb{C}^2 \\), spanned by the computational basis states \\( |0\rangle \\) and \\( |1\rangle \\). We identify these with the classical spin values:

\\[
|0\rangle \leftrightarrow s = +1 \quad (\text{spin up}), \qquad |1\rangle \leftrightarrow s = -1 \quad (\text{spin down}).
\\]

The crucial difference from the classical case is that a qubit can be in a **superposition**:

\\[
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle, \qquad \alpha, \beta \in \mathbb{C}, \quad |\alpha|^2 + |\beta|^2 = 1.
\\]

This is not the spin being "partly up and partly down" in any classical sense. It is a fundamentally new kind of state with no classical analogue.

For a chain of \\( L \\) qubits, the full Hilbert space is the tensor product:

\\[
\mathcal{H}_{\text{total}} = \underbrace{\mathbb{C}^2 \otimes \mathbb{C}^2 \otimes \cdots \otimes \mathbb{C}^2}_{L \text{ times}} \cong \mathbb{C}^{2^L}.
\\]

The computational basis for this space consists of all \\( 2^L \\) tensor product states like \\( |0010\cdots1\rangle \\), which are exactly the classical spin configurations. But now the state of the system can be an arbitrary superposition of all \\( 2^L \\) configurations:

\\[
|\Psi\rangle = \sum_{\{s\}} c_{\{s\}} |s_1 s_2 \cdots s_L\rangle,
\\]

where the sum runs over all \\( 2^L \\) bitstrings. The dimension of the Hilbert space grows exponentially with system size -- this is both the power and the difficulty of quantum many-body physics.

**The Pauli matrices.** You know these from N&C Chapter 2, but let us recall them here because they are the building blocks of everything that follows:

\\[
X = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \qquad
Y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \qquad
Z = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}.
\\]

Their physical meaning as operators on a single qubit:

- \\( Z \\) is diagonal in the computational basis. Its eigenstates are \\( |0\rangle \\) (eigenvalue \\( +1 \\)) and \\( |1\rangle \\) (eigenvalue \\( -1 \\)). It measures "which classical spin value does this qubit have?"
- \\( X \\) is the **bit-flip** operator: \\( X|0\rangle = |1\rangle \\) and \\( X|1\rangle = |0\rangle \\). Its eigenstates are \\( |+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \\) and \\( |-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle) \\), with eigenvalues \\( +1 \\) and \\( -1 \\) respectively.
- \\( Y = iXZ \\) combines both a bit-flip and a phase-flip.

A key fact: \\( X \\) and \\( Z \\) **do not commute**. In fact, \\( XZ = -ZX \\). This anti-commutation relation is the seed of everything quantum in the Ising model.

When we write an operator like \\( Z\_i \\), we mean \\( Z \\) acting on site \\( i \\) and the identity on every other site:

\\[
Z_i = I \otimes I \otimes \cdots \otimes \underbrace{Z}_{i\text{-th position}} \otimes \cdots \otimes I.
\\]

Similarly for \\( X\_i \\). This is the standard tensor product construction you have seen in N&C.

---

### 2.2 The Ising Interaction as an Operator

In the classical Ising model, the interaction energy between neighboring spins is proportional to \\( s\_i s\_{i+1} \\), which equals \\( +1 \\) if the spins agree and \\( -1 \\) if they disagree. What is the quantum operator that captures this?

The answer is \\( Z\_i Z\_{i+1} \\). Let us verify this explicitly. Acting on computational basis states (which are eigenstates of every \\( Z\_i \\)):

\\[
Z_i Z_{i+1} |s_i s_{i+1}\rangle = (s_i)(s_{i+1}) |s_i s_{i+1}\rangle,
\\]

where \\( s\_i = +1 \\) if site \\( i \\) is in state \\( |0\rangle \\) and \\( s\_i = -1 \\) if site \\( i \\) is in state \\( |1\rangle \\). So \\( Z\_i Z\_{i+1} \\) has eigenvalue \\( +1 \\) when the two spins are the same (both \\( |00\rangle \\) or both \\( |11\rangle \\)) and eigenvalue \\( -1 \\) when they differ (\\( |01\rangle \\) or \\( |10\rangle \\)). This is precisely the classical \\( s\_i s\_{i+1} \\).

We can now write the quantum version of the classical Ising Hamiltonian:

\\[
H_{\text{classical}} = J \sum_{i=1}^{L-1} Z_i Z_{i+1} + h_z \sum_{i=1}^{L} Z_i.
\\]

(Here we use open boundary conditions for simplicity; periodic boundary conditions would add a \\( Z\_L Z\_1 \\) term.)

This Hamiltonian is **diagonal in the computational basis**. Every computational basis state \\( |s\_1 s\_2 \cdots s\_L\rangle \\) is an eigenstate, and its eigenvalue is exactly the classical energy of that configuration:

\\[
E(s_1, \ldots, s_L) = J \sum_{i=1}^{L-1} s_i s_{i+1} + h_z \sum_{i=1}^{L} s_i.
\\]

So at this stage, the quantum model is just the classical model dressed up in operator language. We have gained nothing new. The eigenstates are classical configurations, and the eigenvalues are classical energies. There are no superpositions in sight.

To make something genuinely quantum happen, we need to add a term that does not commute with \\( Z \\).

---

### 2.3 The Transverse Field: Making It Quantum

The **transverse-field Ising model (TFIM)** is obtained by adding a transverse magnetic field in the \\( x \\)-direction:

\\[
H_{\text{TFIM}} = J \sum_{i=1}^{L-1} Z_i Z_{i+1} + h_x \sum_{i=1}^{L} X_i.
\\]

This seemingly simple addition changes the physics completely. Let us understand why.

**What does the \\( X\_i \\) term do?** The operator \\( X\_i \\) flips spin \\( i \\):

\\[
X_i |\cdots 0_i \cdots\rangle = |\cdots 1_i \cdots\rangle, \qquad X_i |\cdots 1_i \cdots\rangle = |\cdots 0_i \cdots\rangle.
\\]

So while the \\( ZZ \\) interaction term is diagonal (it assigns energies to configurations), the \\( X \\) term is off-diagonal (it connects different configurations). In the computational basis, the Hamiltonian matrix has off-diagonal entries: \\( H\_{\text{TFIM}} \\) connects each configuration to every configuration that differs by a single spin flip.

**The competition.** The two terms in the TFIM want incompatible things:

- The \\( ZZ \\) term favors configurations where neighboring spins are aligned (say, all \\( |0\rangle \\) or all \\( |1\rangle \\) when \\( J < 0 \\), which is the ferromagnetic case). These are computational basis states.
- The \\( X \\) term favors each spin being in the \\( |+\rangle \\) state (the \\( +1 \\) eigenstate of \\( X \\)). The product state \\( |+\rangle^{\otimes L} \\) is a uniform superposition of all \\( 2^L \\) computational basis states.

Because \\( Z\_i Z\_{i+1} \\) and \\( X\_i \\) do not commute (since \\( Z\_i \\) and \\( X\_i \\) anti-commute), there is no basis in which both terms are simultaneously diagonal. The eigenstates of \\( H\_{\text{TFIM}} \\) are therefore nontrivial superpositions of computational basis states -- they are genuinely quantum.

This is the essential point: **non-commuting terms in the Hamiltonian force the eigenstates to be superpositions.** A purely diagonal Hamiltonian (like \\( H\_{\text{classical}} \\)) has classical eigenstates. Adding off-diagonal terms that do not commute with the diagonal ones creates quantum entanglement and makes the model qualitatively different.

#### A concrete example: the 2-site TFIM

To make this completely explicit, let us work out the \\( L = 2 \\) case in full detail. The Hamiltonian is:

\\[
H = J \, Z_1 Z_2 + h_x (X_1 + X_2).
\\]

We work in the computational basis \\( \{|00\rangle, |01\rangle, |10\rangle, |11\rangle\} \\). Let us compute each term.

**The \\( Z\_1 Z\_2 \\) term** is diagonal:

\\[
Z_1 Z_2 = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}.
\\]

This assigns eigenvalue \\( +1 \\) to \\( |00\rangle \\) and \\( |11\rangle \\) (spins aligned) and \\( -1 \\) to \\( |01\rangle \\) and \\( |10\rangle \\) (spins anti-aligned).

**The \\( X\_1 \\) term** flips the first spin:

\\[
X_1 = X \otimes I = \begin{pmatrix} 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \end{pmatrix}.
\\]

**The \\( X\_2 \\) term** flips the second spin:

\\[
X_2 = I \otimes X = \begin{pmatrix} 0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{pmatrix}.
\\]

Adding everything together:

\\[
H = \begin{pmatrix} J & h_x & h_x & 0 \\ h_x & -J & 0 & h_x \\ h_x & 0 & -J & h_x \\ 0 & h_x & h_x & J \end{pmatrix}.
\\]

Take a moment to stare at this matrix. The diagonal entries are the classical Ising energies: \\( +J \\) for aligned spins, \\( -J \\) for anti-aligned spins. The off-diagonal entries, all equal to \\( h\_x \\), connect configurations that differ by a single spin flip. This is the transverse field at work -- it mixes classical configurations.

**Finding the eigenstates.** Notice that the Hamiltonian preserves a symmetry: it commutes with the "global spin flip" operator \\( X\_1 X\_2 \\), which maps \\( |00\rangle \leftrightarrow |11\rangle \\) and \\( |01\rangle \leftrightarrow |10\rangle \\). This means we can block-diagonalize \\( H \\) into the \\( +1 \\) and \\( -1 \\) eigenspaces of \\( X\_1 X\_2 \\).

The symmetric (\\( +1 \\)) sector is spanned by \\( \{|00\rangle + |11\rangle, \; |01\rangle + |10\rangle\} \\) (up to normalization), and the antisymmetric (\\( -1 \\)) sector by \\( \{|00\rangle - |11\rangle, \; |01\rangle - |10\rangle\} \\).

In the symmetric sector, the Hamiltonian block is:

\\[
H_{+} = \begin{pmatrix} J & 2h_x \\ 2h_x & -J \end{pmatrix}.
\\]

This is just a \\( 2 \times 2 \\) matrix. Its eigenvalues are:

\\[
E_{\pm}^{(+)} = \pm\sqrt{J^2 + 4h_x^2}.
\\]

In the antisymmetric sector:

\\[
H_{-} = \begin{pmatrix} J & 0 \\ 0 & -J \end{pmatrix}.
\\]

The eigenvalues are simply \\( \pm J \\). (The transverse field does not mix states within this sector because the relevant off-diagonal matrix elements cancel.)

Let us examine the ground state (lowest energy eigenstate) in the symmetric sector when \\( J < 0 \\) (ferromagnetic coupling). The ground state energy is \\( E = -\sqrt{J^2 + 4h\_x^2} \\), and the corresponding eigenstate is a superposition:

\\[
|E_0\rangle \propto \; 2h_x \big(|00\rangle + |11\rangle\big) + \big(\sqrt{J^2 + 4h_x^2} - J\big)\big(|01\rangle + |10\rangle\big).
\\]

When \\( h\_x = 0 \\), this reduces to \\( |00\rangle + |11\rangle \\) -- the "GHZ-like" superposition of the two classical ground states (or just one of \\( |00\rangle, |11\rangle \\) if we break the symmetry). When \\( h\_x \\) is large compared to \\( |J| \\), the state approaches \\( |+\rangle|+\rangle = \frac{1}{2}(|00\rangle + |01\rangle + |10\rangle + |11\rangle) \\), with all four configurations equally weighted.

The key lesson: **the ground state is a nontrivial superposition of classical configurations**, with the mixing controlled by the ratio \\( h\_x / J \\). This is qualitatively different from the classical Ising model, where the ground state is always a definite configuration.

---

### 2.4 The Mixed-Field Ising Model (MFIM)

The most general nearest-neighbor Ising model with single-site fields is the **mixed-field Ising model**:

\\[
H_{\text{MFIM}} = \sum_{i=1}^{L-1} J \, Z_i Z_{i+1} + \sum_{i=1}^{L} \big( h_z \, Z_i + h_x \, X_i \big).
\\]

This contains two types of magnetic field, and it is worth understanding each one carefully.

**The longitudinal field \\( h\_z Z\_i \\).** This term is diagonal in the computational basis. It shifts the energy of each spin depending on whether it is \\( |0\rangle \\) or \\( |1\rangle \\):

\\[
h_z Z_i |0_i\rangle = +h_z |0_i\rangle, \qquad h_z Z_i |1_i\rangle = -h_z |1_i\rangle.
\\]

For \\( h\_z > 0 \\), the state \\( |0\rangle \\) has higher energy, so spins prefer \\( |1\rangle \\); for \\( h\_z < 0 \\), spins prefer \\( |0\rangle \\). This is a "classical" term in the sense that it does not create superpositions. It simply biases the spin toward one computational basis state. Together with the \\( ZZ \\) interaction, the longitudinal field is exactly the classical Ising model in an external field that we discussed in Chapter 1.

**The transverse field \\( h\_x X\_i \\).** As we discussed in Section 2.3, this is the term that makes things quantum. It flips spins, creating off-diagonal matrix elements in the computational basis. It does not commute with either \\( Z\_i \\) or \\( Z\_i Z\_{i+1} \\), and so it forces the eigenstates to be superpositions.

**The interplay of both fields.** The MFIM has all three ingredients at once: the \\( ZZ \\) interaction (which wants spin alignment), the longitudinal field \\( h\_z \\) (which biases spins toward a particular direction), and the transverse field \\( h\_x \\) (which causes quantum fluctuations by flipping spins). The competition among all three makes the MFIM a rich and challenging model.

---

### 2.5 Making Sense of the Parameter Space

The MFIM has three parameters: the coupling \\( J \\), the longitudinal field \\( h\_z \\), and the transverse field \\( h\_x \\). Since the overall energy scale does not affect the physics qualitatively (it only sets the units), we can normalize by setting \\( |J| = 1 \\) and studying the model as a function of \\( h\_z \\) and \\( h\_x \\).

It is very helpful to understand the special limits of this parameter space:

**1. \\( h\_x = 0, \; h\_z = 0 \\): Pure Ising interaction.**
The Hamiltonian is just \\( H = J \sum\_i Z\_i Z\_{i+1} \\). This is completely classical -- the eigenstates are computational basis states, and the physics reduces to the classical Ising model with no external field. There is nothing quantum here.

**2. \\( h\_x \neq 0, \; h\_z = 0 \\): The transverse-field Ising model (TFIM).**
This is \\( H = J \sum\_i Z\_i Z\_{i+1} + h\_x \sum\_i X\_i \\). Despite being a genuinely quantum model, it turns out to be **exactly solvable** (integrable). This is a remarkable and non-obvious fact. The TFIM can be mapped to a system of free fermions via a transformation known as the Jordan-Wigner transformation, which we will discuss in a later chapter. This exact solvability makes the TFIM one of the most important models in all of condensed matter physics.

**3. \\( h\_x = 0, \; h\_z \neq 0 \\): Ising model with longitudinal field only.**
The Hamiltonian \\( H = J \sum\_i Z\_i Z\_{i+1} + h\_z \sum\_i Z\_i \\) is still diagonal in the computational basis. Every computational basis state is an eigenstate, and the problem is entirely classical. Quantum mechanics adds nothing.

**4. \\( h\_x \neq 0, \; h\_z \neq 0 \\): The full mixed-field Ising model.**
This is the most general case, and it is **not exactly solvable**. The longitudinal field breaks the special structure (integrability) that makes the TFIM solvable. We must resort to numerical methods or approximations.

The parameter space can be visualized as the \\( (h\_z, h\_x) \\) plane (with \\( J = 1 \\) fixed). The horizontal axis (\\( h\_x = 0 \\)) is classical. The vertical axis (\\( h\_z = 0 \\)) is the exactly solvable TFIM. The generic interior of the plane is the non-integrable MFIM. This structure will be crucial when we discuss thermalization: integrable and non-integrable models behave very differently.

**Why is the TFIM special?** The TFIM possesses a large number of hidden conservation laws -- quantities that commute with the Hamiltonian and with each other. These conservation laws constrain the dynamics so severely that the system can be solved exactly. We call such a system **integrable**. The existence of these conservation laws is ultimately related to the fact that the TFIM can be mapped to non-interacting fermions, but we will develop this story carefully in later chapters.

**Why does the longitudinal field break integrability?** Adding \\( h\_z Z\_i \\) to the TFIM destroys most of these hidden conservation laws. In the fermion language, the longitudinal field introduces interactions between the fermions, making the problem qualitatively harder. The system is no longer integrable, and its physics changes dramatically -- most importantly, it can now thermalize in a way that the TFIM cannot.

---

### 2.6 What Does "Solvable" vs "Not Solvable" Mean?

We have used the words "solvable" and "integrable" several times, so let us be more precise about what we mean, even if the full story will come later.

**Integrable (solvable).** A quantum system is integrable if it possesses an extensive number of independent conserved quantities -- operators \\( Q\_1, Q\_2, \ldots, Q\_L \\) that all commute with the Hamiltonian and with each other:

\\[
[H, Q_k] = 0, \qquad [Q_j, Q_k] = 0 \quad \text{for all } j, k.
\\]

Having \\( L \\) such conserved quantities (where \\( L \\) is the system size) is enough to fully determine all eigenstates. This is what happens in the TFIM. The system is so constrained by its conservation laws that we can find every eigenstate and eigenvalue analytically.

**Non-integrable (not solvable).** A generic quantum system, like the MFIM with both \\( h\_x \neq 0 \\) and \\( h\_z \neq 0 \\), has very few conserved quantities -- typically just the Hamiltonian itself (energy conservation) and perhaps a small number of symmetries. Without enough conservation laws to pin down the eigenstates, we cannot solve the model analytically. The eigenstates are complicated superpositions that can only be found numerically.

**Why does this matter for physics?** The number of conserved quantities controls whether a system thermalizes -- whether it reaches thermal equilibrium when started in a non-equilibrium state. The basic intuition is:

- In a non-integrable system, the only conserved quantity is energy. As the system evolves, it explores all states consistent with its energy, and local observables relax to thermal (Boltzmann) values. This is **thermalization**.
- In an integrable system, the many conserved quantities \\( Q\_k \\) constrain the dynamics. The system cannot freely explore all states at a given energy; it is confined by the conservation laws. Local observables relax, but to values determined by all the conserved quantities, not just energy. This is a fundamentally different kind of equilibrium.

This distinction -- integrable vs. non-integrable, thermal vs. non-thermal -- is the central theme of this book, and the quantum Ising model in its various forms is the ideal laboratory for studying it. The TFIM (integrable) and the MFIM (non-integrable) give us two models that differ by a single term in the Hamiltonian, yet behave in qualitatively different ways.

In the next chapters, we will develop the tools to make these ideas precise: the eigenstate thermalization hypothesis (ETH), the concept of level statistics, and the machinery of integrability.

*Last modified: 2026-05-20*
