## Chapter 4: Solving the TFIM

In Chapter 2, we claimed that the transverse-field Ising model (TFIM) is exactly solvable, and in Chapter 3, we saw that integrability means possessing a full set of integrals of motion. In this chapter, we make both of these statements concrete. We will sketch how the TFIM is solved, write down its conserved quantities explicitly, and explain why adding a longitudinal field destroys this beautiful structure.

Recall the TFIM Hamiltonian (with open boundary conditions on \\( L \\) sites):

\\[
H_{\text{TFIM}} = \sum_{i=1}^{L-1} J \, Z_i Z_{i+1} + h \sum_{i=1}^{L} X_i.
\\]

### 4.1 Integrability and the Jordan-Wigner Transformation

The TFIM is solved by a sequence of three transformations, each of which simplifies the Hamiltonian. The final result is a Hamiltonian of non-interacting particles whose energy levels can be read off immediately. Let us walk through the logic.

**Step 1: Jordan-Wigner transformation (spins to fermions).**
The key insight, due to Jordan and Wigner (1928), is that spin-\\( 1/2 \\) operators on a one-dimensional chain can be exactly rewritten in terms of **fermionic** creation and annihilation operators. A fermion is a particle (like an electron) that obeys the Pauli exclusion principle: no two fermions can occupy the same state.

Concretely, we define fermionic operators \\( c_j \\) and \\( c_j^\dagger \\) at each site \\( j \\) through the mapping:

\\[
c_j = \left( \prod_{k=1}^{j-1} X_k \right) \frac{Z_j + i Y_j}{2}, \qquad c_j^\dagger = \left( \prod_{k=1}^{j-1} X_k \right) \frac{Z_j - i Y_j}{2}.
\\]

The string of \\( X \\) operators \\( \prod_{k=1}^{j-1} X_k \\) is called the **Jordan-Wigner string**. It is the crucial ingredient that ensures the operators \\( c_j \\) satisfy the correct fermionic anti-commutation relations:

\\[
\\{c_i, c_j^\dagger\\} = \delta_{ij}, \qquad \\{c_i, c_j\\} = 0,
\\]

where \\( \\{A, B\\} = AB + BA \\) is the anti-commutator. Without the string, the operators at different sites would commute (like bosons) rather than anti-commute (like fermions). You can verify this if you like using the Pauli algebra, though we will not go through the calculation here.

It is also useful to introduce **Majorana fermion** operators, which are the real and imaginary parts of \\( c_j \\):

\\[
\gamma_{2j-1} = c_j + c_j^\dagger, \qquad \gamma_{2j} = i(c_j - c_j^\dagger).
\\]

Majorana operators are Hermitian (\\( \gamma_k^\dagger = \gamma_k \\)) and satisfy \\( \\{\gamma_k, \gamma_l\\} = 2\delta_{kl} \\). They will be the natural language for writing down the conserved quantities of the TFIM.

**Why does this help?** The miracle is that when you express the TFIM Hamiltonian in terms of these fermionic operators, the \\( ZZ \\) interaction and the \\( X \\) field both become **quadratic** (bilinear) in the fermions -- they involve only terms like \\( c_i^\dagger c_j \\) or \\( c_i c_j \\), with at most two fermionic operators per term. Schematically:

\\[
H_{\text{TFIM}} = \sum_{i,j} \left( A_{ij} \, c_i^\dagger c_j + B_{ij} \, c_i^\dagger c_j^\dagger + \text{h.c.} \right) + \text{const}.
\\]

A Hamiltonian that is quadratic in fermions describes **non-interacting** (free) fermions. This is the key to exact solvability.

**Step 2: Fourier transform (real space to momentum space).**
For a translationally invariant system (e.g., with periodic boundary conditions), one performs a Fourier transform to momentum space:

\\[
\tilde{c}_k = \frac{1}{\sqrt{L}} \sum_{j=1}^{L} e^{-ikj} c_j.
\\]

In momentum space, the Hamiltonian decomposes into independent \\( 2 \times 2 \\) blocks, one for each momentum \\( k \\). Each block couples only \\( \tilde{c}_k \\) and \\( \tilde{c}_{-k}^\dagger \\).

**Step 3: Bogoliubov transformation (diagonalization).**
Each \\( 2 \times 2 \\) block is diagonalized by a Bogoliubov transformation -- a canonical change of variables that mixes \\( \tilde{c}_k \\) and \\( \tilde{c}_{-k}^\dagger \\) while preserving the fermionic anti-commutation relations. The result is a set of new fermionic operators \\( \eta_k \\) in terms of which the Hamiltonian takes the diagonal form:

\\[
H_{\text{TFIM}} = \sum_k \varepsilon_k \left( \eta_k^\dagger \eta_k - \frac{1}{2} \right),
\\]

where the single-particle energies are

\\[
\varepsilon_k = \sqrt{(J \cos k + h)^2 + (J \sin k)^2}.
\\]

This is the final answer. The Hamiltonian describes \\( L \\) independent fermionic modes, each with its own energy \\( \varepsilon_k \\). The many-body eigenstates are obtained by choosing which modes to occupy (\\( \eta_k^\dagger \eta_k = 0 \\) or \\( 1 \\)), giving \\( 2^L \\) eigenstates in total -- exactly the dimension of the Hilbert space. The ground state is the "vacuum" with all negative-energy modes filled.

**Summary of the procedure:**

\\[
\text{Spins} \;\xrightarrow{\text{Jordan-Wigner}}\; \text{Fermions (quadratic)} \;\xrightarrow{\text{Fourier}}\; \text{Momentum space} \;\xrightarrow{\text{Bogoliubov}}\; \text{Free modes } \eta_k.
\\]

The essential point is not the algebra of each step, but the logical flow: the Jordan-Wigner transformation reveals that the TFIM is secretly a free-fermion problem, and free-fermion problems reduce to single-particle quantum mechanics.

### 4.2 Conserved Quantities of the TFIM

Since the TFIM is integrable, it must possess a full set of \\( L \\) independent, mutually commuting integrals of motion. In the diagonal form \\( H = \sum_k \varepsilon_k \, \eta_k^\dagger \eta_k + \text{const} \\), these are easy to identify: they are the **occupation numbers** \\( n_k = \eta_k^\dagger \eta_k \\) for each mode \\( k \\). Each \\( n_k \\) commutes with \\( H \\) (since \\( H \\) is diagonal in the \\( \eta_k \\) basis) and with every other \\( n_{k'} \\), and each takes values 0 or 1.

But these occupation-number operators are defined in momentum space. What do the conserved quantities look like when expressed back in terms of the original spin operators? This is important because in the MFIM (where exact diagonalization is not possible), we want to search for *approximate* conserved quantities written as sums of Pauli strings, and we need to know what the exact ones look like for comparison.

It turns out that the conserved quantities of the TFIM can be written as **Majorana bilinears** -- operators built from products of two Majorana fermions, which translate back to specific Pauli string patterns. Following the notation from the research literature, we define two families of conserved quantities, \\( A_m \\) and \\( B_m \\), labeled by a positive integer \\( m \\).

**The \\( A_m \\) family.** These are the simpler ones:

\\[
A_m = \sum_i \left( Y_i X_{i+1} X_{i+2} \cdots X_{i+m-1} Z_{i+m} - Z_i X_{i+1} X_{i+2} \cdots X_{i+m-1} Y_{i+m} \right).
\\]

In compact notation, we write this as

\\[
A_m = Y X^{m-1} Z - Z X^{m-1} Y,
\\]

where the shorthand \\( Y X^{m-1} Z \\) means a Pauli string that starts with \\( Y \\), has \\( m-1 \\) copies of \\( X \\) in the middle, and ends with \\( Z \\), summed over all starting positions \\( i \\).

Let us write out the first few explicitly:

- \\( A_1 = \sum_i (Y_i Z_{i+1} - Z_i Y_{i+1}) \\): a nearest-neighbor operator involving \\( YZ \\) and \\( ZY \\) pairs.
- \\( A_2 = \sum_i (Y_i X_{i+1} Z_{i+2} - Z_i X_{i+1} Y_{i+2}) \\): a next-nearest-neighbor operator with an \\( X \\) in the middle.
- \\( A_3 = \sum_i (Y_i X_{i+1} X_{i+2} Z_{i+3} - Z_i X_{i+1} X_{i+2} Y_{i+3}) \\): spans four sites.

Each \\( A_m \\) has range \\( m+1 \\) (it acts nontrivially on \\( m+1 \\) consecutive sites). The longer the string, the more "nonlocal" the conserved quantity.

**The \\( B_m \\) family.** These are slightly more involved because they depend on the Hamiltonian parameters \\( J \\) and \\( h \\). For \\( m \geq 2 \\):

\\[
B_m = J \sum_i Z_i X_{i+1} \cdots X_{i+m-1} Z_{i+m} - h \sum_i Z_i X_{i+1} \cdots X_{i+m-2} Z_{i+m-1} - h \sum_i Y_i X_{i+1} \cdots X_{i+m-2} Y_{i+m-1},
\\]

or in compact notation:

\\[
B_m = J \, Z X^{m-1} Z - h \, Z X^{m-2} Z - h \, Y X^{m-2} Y \qquad (m \geq 2).
\\]

The first member of this family is special:

\\[
B_1 = J \sum_i Z_i X_{i+1} Z_{i+2} - h \sum_i Z_i Z_{i+1} - h \sum_i Y_i Y_{i+1} - J \sum_i X_i,
\\]

or compactly:

\\[
B_1 = J \, ZXZ - h \, ZZ - h \, YY - J \, X.
\\]

Note that \\( B_1 \\) contains a single-site term (\\( X_i \\)) as well as two-site and three-site terms.

**Physical interpretation.** Each of these operators commutes exactly with \\( H_{\text{TFIM}} \\):

\\[
[H_{\text{TFIM}}, A_m] = 0, \qquad [H_{\text{TFIM}}, B_m] = 0 \qquad \text{for all } m.
\\]

They also commute with each other: \\( [A_m, A_{m'}] = [B_m, B_{m'}] = [A_m, B_{m'}] = 0 \\). Together, the \\( A_m \\) and \\( B_m \\) operators provide the full set of conserved quantities needed for integrability. (In fact, \\( B_1 \\) is proportional to \\( H_{\text{TFIM}} \\) itself, so energy conservation is included as a special case.)

Since these operators are all conserved, their expectation values are frozen for all time. This means the TFIM "remembers" an enormous amount of information about its initial state -- not just the total energy, but the value of every \\( A_m \\) and \\( B_m \\). This is why the TFIM does not thermalize in the usual sense: a thermalizing system forgets everything about its initial state except the conserved quantities, and for a generic (non-integrable) system, the only conserved quantity is energy. The TFIM has \\( L \\) conserved quantities, so it retains far more memory of its initial conditions.

### 4.3 Why the MFIM Is Not Solvable

Now consider the mixed-field Ising model:

\\[
H_{\text{MFIM}} = \sum_i J \, Z_i Z_{i+1} + h_x \sum_i X_i + h_z \sum_i Z_i.
\\]

This differs from the TFIM only by the longitudinal field \\( h_z \sum_i Z_i \\). What happens when we apply the Jordan-Wigner transformation to this extra term?

**The longitudinal field becomes quartic.** Recall that the Jordan-Wigner transformation expresses each Pauli operator in terms of fermions. The operators \\( Z_i Z_{i+1} \\) and \\( X_i \\) both map to quadratic (bilinear) expressions in the fermions \\( c_j, c_j^\dagger \\). But the single-site operator \\( Z_i \\) maps to:

\\[
Z_i = 1 - 2 c_i^\dagger c_i.
\\]

At first glance, this also looks quadratic, and indeed it is. But the subtlety is in how it combines with the other terms. When you write out the full MFIM Hamiltonian in fermion language, the \\( h_z Z_i \\) term can be absorbed into the quadratic part, but the presence of *both* \\( ZZ \\) and \\( Z \\) terms together with the transverse field \\( X \\) produces an effective Hamiltonian that, after the Jordan-Wigner transformation, contains **quartic** (four-fermion) terms of the form \\( c_i^\dagger c_i c_j^\dagger c_j \\).

More precisely, the issue is that the Bogoliubov transformation that diagonalizes the TFIM relies on the Hamiltonian being purely quadratic. The longitudinal field \\( h_z Z_i \\) disrupts this structure. While each individual term in the MFIM can be written in terms of fermions, the resulting Hamiltonian is no longer a free-fermion problem -- it describes **interacting fermions**.

To see this from a slightly different angle: in the TFIM, the Hamiltonian can be written entirely in terms of Majorana bilinears \\( \gamma_k \gamma_l \\) (products of exactly two Majorana operators). The conserved quantities \\( A_m \\) and \\( B_m \\) are also Majorana bilinears, which is why everything fits together so neatly. The longitudinal field \\( Z_i = i \gamma_{2i-1} \gamma_{2i} \\) is itself a Majorana bilinear, but when combined with the other bilinear terms and the boundary conditions, it generates effective four-Majorana (quartic) interactions that cannot be removed by any canonical transformation.

**Quartic means unsolvable (in general).** A quadratic fermion Hamiltonian can always be diagonalized: it reduces to single-particle quantum mechanics, which involves diagonalizing an \\( L \times L \\) matrix. A quartic fermion Hamiltonian describes interacting particles, and the interactions couple all the modes together. There is no known general procedure for diagonalizing such a Hamiltonian -- it is a genuinely many-body problem that requires working in the full \\( 2^L \\)-dimensional Hilbert space.

**Consequences for integrability.** When the quartic interactions are present, the occupation numbers \\( n_k = \eta_k^\dagger \eta_k \\) of the free-fermion modes are no longer conserved:

\\[
[H_{\text{MFIM}}, \eta_k^\dagger \eta_k] \neq 0.
\\]

The Bogoliubov quasiparticles scatter off each other, exchanging occupation between modes. The conservation laws of the TFIM are destroyed.

Similarly, if you compute the commutator of \\( A_m \\) or \\( B_m \\) with \\( H_{\text{MFIM}} \\), you will find it is proportional to \\( h_z \\):

\\[
[H_{\text{MFIM}}, A_m] = h_z \, (\text{some operator}) \neq 0.
\\]

The TFIM's conserved quantities become only *approximately* conserved in the MFIM, with the quality of the approximation controlled by the ratio \\( h_z / J \\) (or \\( h_z / h_x \\)). When \\( h_z \\) is small, the MFIM is "close to integrable," and the \\( A_m, B_m \\) operators drift slowly. When \\( h_z \\) is comparable to the other energy scales, the conservation laws are badly broken, and the system is expected to thermalize.

**Quantum chaos in the MFIM.** Numerical studies confirm that the MFIM at generic parameter values \\( (J, h_x, h_z) \\) exhibits the hallmarks of quantum chaos: its energy levels repel each other (following the statistics of random matrices), and its eigenstates satisfy the eigenstate thermalization hypothesis (ETH). These are signatures that the system has "forgotten" its conservation laws and behaves, in many respects, like a random matrix.

However -- and this is the central question motivating the research project -- the MFIM is not equally chaotic everywhere in parameter space. Near the integrable lines (\\( h_z = 0 \\) or \\( h_x = 0 \\)), remnants of the conservation laws persist as approximate IOMs, and thermalization is slower or incomplete. The degree to which the system thermalizes depends on where you sit in the \\( (h_z, h_x) \\) parameter plane. Understanding this landscape -- how approximate conservation laws emerge, how they constrain dynamics, and how they eventually break down -- is the problem we will tackle in the chapters ahead.

*Last modified: 2026-05-20*
