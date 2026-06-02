## Chapter 4: Symmetry

Among all the properties a Hamiltonian can have, **symmetry** is one of the most powerful and far-reaching. In physics, we say that a Hamiltonian has a symmetry if there is a transformation that leaves it unchanged. In quantum mechanics, such transformations are represented by operators, and the condition for a symmetry is a simple commutation relation. This chapter introduces symmetry, derives its consequences, and illustrates the ideas with examples from the Ising models we have been studying.

### 4.1 What Is a Symmetry?

Let \\( U \\) be a unitary operator (\\( U^\dagger U = I \\)). We say that \\( U \\) is a **symmetry** of the Hamiltonian \\( H \\) if

\\[
[H, U] = 0, \quad \text{equivalently,} \quad UHU^\dagger = H.
\\]

(The equivalence follows by multiplying \\( HU = UH \\) on the right by \\( U^\dagger \\).) Recall that applying a similarity transform to a matrix is equivalent to viewing the same matrix under a different basis, the condition \\( UHU^\dagger = H \\) has an appealing interpretation: applying the transformation \\( U \\) to every state in the system leaves the Hamiltonian unchanged. The physics is *invariant* under \\( U \\).

**Why unitary?** In quantum mechanics, physical transformations must preserve the inner product (lengths and angles in Hilbert space), which forces them to be unitary. Examples include spatial rotations, reflections, and spin flips. (There is also an important class of *anti-unitary* symmetries such as time reversal, but we will not need them here.)

### 4.2 Symmetry Generators and Symmetry Groups

In Chapter 3, we defined an integral of motion as an observable, i.e., a Hermitian operator \\( A \\) satisfying \\( [H, A] = 0 \\). Now we are talking about *unitary* operators that commute with \\( H \\). These are generally not Hermitian. What is the connection between the two?

**When the symmetry operator is itself Hermitian.**
Some symmetry operators happen to be both unitary and Hermitian at the same time. Recall the conditions: unitary means \\( U^\dagger U = I \\), and Hermitian means \\( U^\dagger = U \\). Together, these force \\( U^2 = I \\), so \\( U \\) is its own inverse. The eigenvalues of such an operator must satisfy \\( \lambda^2 = 1 \\), giving \\( \lambda = \pm 1 \\) -- real numbers that also lie on the unit circle. The Ising parity \\( P = \prod_i X_i \\) is exactly this: \\( P^\dagger = P \\) (each \\( X_i \\) is Hermitian) and \\( P^2 = I \\). So \\( P \\) is directly an observable. When \\( [H, P] = 0 \\), it is a Hermitian IOM just like in Chapter 3, and \\( \langle P \rangle \\) is constant under time evolution.

**The generator of a continuous symmetry.**
The deeper connection stems from the theory of *Lie groups and Lie algebras*. Consider we have a Hermitian operator \\( G \\) that is conserved. One can verify that for any number \\( \theta \\), the operator

\\[
U(\theta) = e^{i\theta G}
\\]

would also commute with the Hamiltonian. Furthermore, it is unitary. Therefore, one can always generate *a family of* (parameterized by \\( \theta \\)) symmetries given any conserved observable. In this case, the collection of symmetries \\( U(\theta) \\) is called a *symmetry group*, and \\( G \\) the *generator* of this group.

**Group theory** is central to the characterization of symmetries. A group is a mathematical structure that is a collection of "elements", where one element is called the identity, and the elements can be composed (the composition is not necessarily commutative), and each element has an inverse such that the composition of an element with its inverse gives the identity element. The set of symmetries is always a group: the identity is "do nothing to the system", and any two symmetry operators can be composed in the sense that if two transformations respectively leaves a system invariant, then doing them in sequence also leaves the system invariant. Symmetry operators are also required to be invertible.

People often characterize a system's symmetry by naming its symmetry group. The most common groups appearing in our models are \\( \mathbb{Z}_2 \\) and \\( \text{U}(1) \\), described below.

#### \\(\mathbb{Z}_2\\) Symmetry

The simplest nontrivial symmetry group is \\( \mathbb{Z}_2 \\), the "integers modulo 2": elements are 0 and 1, and composition is addition modulo 2. The element 0 is the identity, and 1+1=0 modulo 2, so every non-identity element is its own inverse. A symmetry operator \\( U \\) with \\( U^2 = I \\) has the same structure -- applying it twice returns you to the start -- and so one says it generates a \\( \mathbb{Z}_2 \\) symmetry. Its eigenvalues are \\( \pm 1 \\), splitting the Hilbert space into an **even** sector (eigenvalue \\( +1 \\)) and an **odd** sector (eigenvalue \\( -1 \\)). In general, "\\( \mathbb{Z}_2 \\) symmetry" and "parity" are used interchangeably.

**Example: Ising parity symmetry.** The most important \\( \mathbb{Z}_2 \\) symmetry in our models is the **parity operator**:

\\[
P = X_1 \otimes X_2 \otimes \cdots \otimes X_L = \prod_{i=1}^{L} X_i.
\\]

This operator flips every spin simultaneously. Using the Pauli algebra, conjugation by \\( X \\) gives:

\\[
X Z X = -Z, \qquad X X X = X.
\\]

(The first follows from the anticommutation \\( XZ = -ZX \\), and the second is trivial since \\( X^2 = I \\).) So \\( P \\) conjugates each site as \\( Z_i \to -Z_i \\) and \\( X_i \to X_i \\).

Now let us check whether \\( P \\) is a symmetry of the TFIM and MFIM:

- **ZZ coupling:** \\( Z_i Z_{i+1} \to (-Z_i)(-Z_{i+1}) = Z_i Z_{i+1} \\). Unchanged. ✓
- **Transverse field:** \\( X_i \to X_i \\). Unchanged. ✓
- **Longitudinal field:** \\( Z_i \to -Z_i \\). Changes sign. ✗

Therefore, \\( P \\) **is** a symmetry of the TFIM (\\( [H_{\text{TFIM}}, P] = 0 \\)), but **is not** a symmetry of the MFIM when \\( g \neq 0 \\). Adding a longitudinal field breaks the \\( \mathbb{Z}_2 \\) parity symmetry. This is partly what we meant in Chapter 2 when we said the longitudinal field makes the model "more quantum and less symmetric" -- the transverse field preserves the symmetry, but the longitudinal field breaks it.

#### U(1) Symmetry

\\( \text{U}(1) \\) is the group of complex numbers of magnitude 1, i.e., phases \\( e^{i\theta} \\) for \\( \theta \in [0, 2\pi) \\), where composition is multiplication. This is a *continuous* group: there is an uncountably infinite family of elements, one for each angle \\( \theta \\), smoothly connected to the identity (\\( \theta = 0 \\)). It is precisely the kind of symmetry that arises from the generator construction above: if \\( G \\) is a conserved Hermitian operator with integer eigenvalues, then \\( U(\theta) = e^{i\theta G} \\) traces out a \\( \text{U}(1) \\) group as \\( \theta \\) varies -- the integer eigenvalue condition ensures that \\( U(0) = U(2\pi) \\), so the symmetry is truly periodic and the group closes. In contrast to \\( \mathbb{Z}_2 \\), which has only two elements, \\( \text{U}(1) \\) has infinitely many, one for each angle.

**Example: total magnetization conservation.** In Chapter 3, we showed that the total magnetization \\( M = \sum_i Z_i \\) commutes with the pure ZZ Hamiltonian \\( H_{ZZ} \\). So \\( G = M/2 \\) is the generator of a \\( \text{U}(1) \\) symmetry:

\\[
U(\theta) = e^{i\theta M/2} = \prod_{i=1}^{L} e^{i\theta Z_i/2}.
\\]

This corresponds to rotating every spin by an angle \\( \theta \\) around the \\( z \\)-axis. The eigenvalues of \\( M \\) are integers from \\( -L \\) to \\( L \\) (in steps of 2).

#### Other Symmetries

Beyond \\( \mathbb{Z}_2 \\) and \\( \text{U}(1) \\), a few other symmetry groups appear frequently in the physics of spin chains:

- \\( \mathbb{Z}_N \\): cyclic group of order \\( N \\), generated by \\( U \\) with \\( U^N = I \\). Eigenvalues are the \\( N \\)-th roots of unity \\( 1, e^{2\pi i/N}, e^{4\pi i/N}, \ldots \\)
- \\( \text{SU}(2) \\): the group of \\( 2\times 2 \\) unitary matrices with determinant 1, generated by spin operators. A spin chain with full \\( \text{SU}(2) \\) symmetry conserves total spin in all three spatial directions simultaneously.
- **Translation symmetry**: if the Hamiltonian is the same on every site (periodic boundary conditions), then the translation operator \\( T \\) (which shifts all spins by one site) commutes with \\( H \\). We will discuss this in more detail below.

### 4.3 Symmetry Sectors

#### 4.3.1 Action on Eigenstates and Simultaneous Diagonalizability

Suppose \\( |E\rangle \\) is an eigenstate of \\( H \\) with energy \\( E \\):

\\[
H |E\rangle = E |E\rangle.
\\]

What happens when we apply the symmetry \\( U \\) to this state? We compute:

\\[
H (U |E\rangle) = U (H |E\rangle) = U (E |E\rangle) = E (U |E\rangle),
\\]

where in the first step we used \\( HU = UH \\). So \\( U |E\rangle \\) is *also* an eigenstate of \\( H \\) with the *same* energy \\( E \\). In other words, **symmetry operators map energy eigenstates to energy eigenstates at the same energy level**.

This has two cases:
- **Non-degenerate eigenvalue**: If \\( E \\) has only one eigenstate, then \\( U |E\rangle \\) must be proportional to \\( |E\rangle \\). That means \\( |E\rangle \\) is itself an eigenstate of \\( U \\): \\( U|E\rangle = \lambda |E\rangle \\) for some \\( \lambda \\). So the energy eigenstates are automatically symmetry eigenstates.
- **Degenerate eigenvalue**: If multiple eigenstates share the same energy \\( E \\), the symmetry must map within this degenerate subspace -- it cannot send a state of energy \\( E \\) to a state of a different energy. Now consider the matrix of \\( U \\) written in the energy eigenbasis. Since \\( U \\) only mixes states within the same energy level, it has no matrix elements between states of different energies; it is therefore block diagonal in the energy eigenbasis, with one block per energy level. A block-diagonal matrix can be diagonalized block by block, so one can always *choose* a basis within each degenerate subspace that simultaneously diagonalizes both \\( H \\) and \\( U \\).

The general statement is: **commuting Hermitian (or unitary) operators can always be simultaneously diagonalized** -- they share a common eigenbasis. The commutation condition \\( [H, U] = 0 \\) is exactly the criterion. This is a standard theorem in linear algebra (see Chapter 2.1.5 of Nielsen & Chuang), and it is one of the most useful facts in quantum mechanics.

#### 4.3.2 Block Diagonalization and Symmetry Sectors

The most practically useful consequence of symmetry is **block diagonalization**. Let us see why.

Since \\( U \\) is unitary, its eigenvalues lie on the unit circle in the complex plane: \\( U |u\rangle = e^{i\phi} |u\rangle \\). (If \\( U = e^{i\theta G} \\) is generated by some Hermitian \\( G \\), then the eigenvalues of \\( U \\) are just \\( e^{i\theta g} \\) where \\( g \\) are the eigenvalues of \\( G \\), so labeling sectors by eigenvalues of \\( U \\) is equivalent to labeling them by eigenvalues of \\( G \\).) The Hilbert space decomposes into **symmetry sectors** (also called **charge sectors**), where each sector consists of all states with a given eigenvalue of \\( U \\):

\\[
\mathcal{H} = \mathcal{H}_{e^{i\phi_1}} \oplus \mathcal{H}_{e^{i\phi_2}} \oplus \cdots
\\]

Now, suppose \\( |\psi\rangle \\) and \\( |\psi'\rangle \\) lie in *different* sectors: \\( U|\psi\rangle = e^{i\phi}|\psi\rangle \\) and \\( U|\psi'\rangle = e^{i\phi'}|\psi'\rangle \\) with \\( e^{i\phi} \neq e^{i\phi'} \\). Consider the matrix element \\( \langle \psi'|H|\psi\rangle \\). Using \\( H = U^\dagger H U \\):

\\[
\langle \psi'|H|\psi\rangle = \langle \psi'|U^\dagger H U|\psi\rangle = e^{i(\phi - \phi')} \langle \psi'|H|\psi\rangle.
\\]

Since \\( e^{i(\phi - \phi')} \neq 1 \\), the only consistent solution is \\( \langle \psi'|H|\psi\rangle = 0 \\). **The Hamiltonian has no matrix elements between different symmetry sectors.** In matrix form (with states grouped by sector), \\( H \\) is block diagonal:

\\[
H = \begin{pmatrix} H_1 & 0 & 0 \\ 0 & H_2 & 0 \\ 0 & 0 & \ddots \end{pmatrix},
\\]

where \\( H_k \\) is the restriction of \\( H \\) to the \\( k \\)-th symmetry sector. This is enormously useful: instead of diagonalizing one large matrix, we can diagonalize each block separately, which is much cheaper numerically. For a system of \\( L \\) spins (total Hilbert space dimension \\( 2^L \\)), if the symmetry splits the space into two equal sectors, each block is only \\( 2^{L-1} \times 2^{L-1} \\) -- half the size, and diagonalization costs scale as the cube of the dimension.

**Symmetry sectors of our models.** Let us now identify the symmetry sectors for the two symmetries introduced in Section 4.2. For the \\( \mathbb{Z}_2 \\) parity symmetry \\( P \\) of the TFIM, the eigenvalues of \\( P \\) are \\( \pm 1 \\), giving exactly two sectors: the **even** sector (\\( P = +1 \\)) and the **odd** sector (\\( P = -1 \\)), and the TFIM Hamiltonian is block diagonal in this decomposition. For the \\( \text{U}(1) \\) magnetization symmetry of the pure ZZ model, the generator \\( M = \sum_i Z_i \\) has eigenvalues \\( -L, -L+2, \ldots, L-2, L \\), giving \\( L+1 \\) sectors labeled by the total number of up-spins (ranging from 0 to \\( L \\)). Each sector is the subspace of states with a fixed number of up-spins, and the ZZ Hamiltonian does not mix states between sectors.

There is also one symmetry whose symmetry sector is enormously useful: translation symmetry. However, due to its complexity, it's not feasible to introduce it here. You can find out details about it in [this lecture note](https://arxiv.org/abs/1101.3281).

### 4.4 Summary

The key ideas of this chapter are:

1. A symmetry is a unitary operator \\( U \\) with \\( [H, U] = 0 \\), equivalently \\( UHU^\dagger = H \\).
2. When \\( U \\) is also Hermitian (\\( U^2 = I \\), eigenvalues \\( \pm 1 \\)), it is directly a Hermitian IOM and observable.
3. For a continuous family \\( U(\theta) = e^{i\theta G} \\), the generator \\( G \\) is a Hermitian IOM: \\( [H, G] = 0 \\) and \\( \langle G \rangle \\) is conserved under time evolution.
4. Energy eigenstates can always be chosen to be simultaneously eigenstates of \\( U \\) (simultaneous diagonalizability).
5. The Hilbert space splits into symmetry sectors labeled by eigenvalues of \\( U \\); the Hamiltonian is block diagonal across these sectors.
6. The \\( \mathbb{Z}_2 \\) parity symmetry \\( P = \prod_i X_i \\) is present in the TFIM but broken by the longitudinal field in the MFIM.
7. The \\( \text{U}(1) \\) magnetization conservation is present in the pure ZZ model but broken by the transverse field.

In the next chapter, we will use the \\( \mathbb{Z}_2 \\) symmetry of the TFIM explicitly when we solve it: the Jordan-Wigner transformation that maps the TFIM to free fermions maps the two parity sectors to different fermion boundary conditions.

*Last modified: 2026-06-01*
