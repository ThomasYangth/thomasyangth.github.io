# Rematch Book Outline

## Chapter 1: The Classical Ising Model

### 1.1 Spins on a Chain
- The simplest model of a magnet: discrete spins $s_i = \pm 1$ arranged on a lattice
- Each spin represents a tiny magnetic moment pointing up or down

### 1.2 The Energy Function
- The Ising Hamiltonian: $H = -J \sum_i s_i s_{i+1}$
- What the coupling $J$ means: $J > 0$ favors alignment (ferromagnet), $J < 0$ favors anti-alignment (antiferromagnet)
- Adding an external field: $H = -J \sum_i s_i s_{i+1} - h \sum_i s_i$
- Work through small examples (2-3 spins) to build intuition for which configurations have low/high energy

### 1.3 Statistical Mechanics and the Boltzmann Distribution
- At thermal equilibrium, configurations are sampled with probability $p \propto e^{-\beta H}$
- $\beta = 1/T$ (inverse temperature): low temperature favors low-energy (ordered) states, high temperature makes all states equally likely
- This gives physical meaning to the energy function: it determines which configurations are likely to be observed
- Brief mention: phase transitions in 2D (order/disorder), no phase transition in 1D at finite temperature

---

## Chapter 2: The Quantum Ising Model

### 2.1 From Classical Spins to Qubits
- Replace classical $s_i = \pm 1$ with quantum spin-1/2 degrees of freedom (qubits)
- Each site is a 2-dimensional Hilbert space; the full system of $L$ spins lives in a $2^L$-dimensional Hilbert space
- States are vectors, not just configurations: superpositions are possible
- Review of Pauli matrices $X, Y, Z$ and their physical meaning (from N&C)

### 2.2 The Ising Interaction as an Operator
- The classical $s_i s_{i+1}$ becomes the operator $Z_i Z_{i+1}$
- $Z_i Z_{i+1}$ is diagonal in the computational ($Z$) basis: eigenvalue $+1$ if spins agree, $-1$ if they disagree
- The "classical" Hamiltonian $H = J \sum_i Z_i Z_{i+1} + h_z \sum_i Z_i$ is diagonal -- its eigenstates are exactly the classical configurations
- In this case, the quantum model contains the classical model but doesn't add anything new yet

### 2.3 The Transverse Field: Making It Quantum
- Add a transverse field: $H_{\text{TFIM}} = \sum_i J Z_i Z_{i+1} + h_x X_i$
- What does $X_i$ do? It flips spin $i$: $X|0\rangle = |1\rangle$, $X|1\rangle = |0\rangle$
- The $ZZ$ term and the $X$ term do not commute -- they "compete"
  - $ZZ$ wants spins to align (in the $Z$ basis)
  - $X$ wants each spin to point in the $+x$ direction (eigenstate of $X$)
- Because these terms don't commute, the eigenstates are nontrivial superpositions -- this is what makes the model genuinely quantum
- Work through the 2-site example explicitly to see how the eigenstates mix classical configurations

### 2.4 The Mixed-Field Ising Model (MFIM)
- The most general nearest-neighbor Ising model: $H_{\text{MFIM}} = \sum_i J Z_i Z_{i+1} + h_z Z_i + h_x X_i$
- The longitudinal field $h_z Z_i$: biases spins toward $|0\rangle$ or $|1\rangle$, but is diagonal (classical-like)
- The transverse field $h_x X_i$: causes quantum fluctuations (spin flips)

### 2.5 Making Sense of the Parameter Space
- Three parameters: $J$, $h_z$, $h_x$ (can normalize so $J = 1$)
- Special limits and what they mean physically:
  - $h_x = 0, h_z = 0$: pure Ising interaction, classical
  - $h_x \neq 0, h_z = 0$: the TFIM, turns out to be exactly solvable
  - $h_x = 0, h_z \neq 0$: classical Ising in a longitudinal field, still diagonal
  - $h_x \neq 0, h_z \neq 0$: the full MFIM, generically not solvable
- Why the TFIM is special: it has a hidden structure (integrability) that we will explain later
- Why the full MFIM is harder: the longitudinal field breaks this hidden structure

### 2.6 What Does "Solvable" vs "Not Solvable" Mean?
- Preview: "solvable" (integrable) means we can find all eigenstates analytically and the system has many conserved quantities
- "Not solvable" means we generally cannot, and the system has few conserved quantities
- This distinction has deep physical consequences for whether the system thermalizes -- the subject of the next chapters

---

## Chapter 3: Quantum Dynamics and Conservation Laws

### 3.1 Time Evolution
- The Schrodinger equation: how quantum states evolve in time
- The Hamiltonian as the generator of dynamics
- Unitary evolution: $|\psi(t)\rangle = e^{-iHt}|\psi(0)\rangle$

### 3.2 The Heisenberg Picture
- Operators evolve instead of states: $O(t) = e^{iHt} O e^{-iHt}$
- Deriving the equation of motion: $\frac{dO}{dt} = i[H, O]$
- Connection to classical mechanics (Poisson brackets)

### 3.3 Integrals of Motion
- Definition: an operator $A$ satisfying $[H, A] = 0$
- Physical meaning: $\langle \psi(t)|A|\psi(t)\rangle$ is constant for all $|\psi\rangle$ and all $t$
- Examples: energy ($H$ commutes with itself), total magnetization in symmetric models

### 3.4 Approximate Integrals of Motion
- Operators with $\|[H, A]\|$ small but nonzero
- Nearly conserved for long times, eventually decay
- Motivating question: what physical consequences do approximate IOMs have?

---

## Chapter 4: Solving the TFIM

### 4.1 Integrability and the Jordan-Wigner Transformation
- The TFIM is exactly solvable
- Key idea: map spin operators to fermion operators (Jordan-Wigner transformation)
- The Hamiltonian becomes quadratic in fermions, which can be diagonalized
- Sketch of the procedure: Jordan-Wigner $\to$ Fourier transform $\to$ Bogoliubov transformation

### 4.2 Conserved Quantities of the TFIM
- Integrability implies a full set of IOMs
- The Majorana bilinear IOMs: $A_m$ and $B_m$ operators
- These are constructed from products of Jordan-Wigner fermions
- Physical consequence: the system does not fully thermalize

### 4.3 Why the MFIM Is Not Solvable
- The longitudinal field $h_z Z_i$ maps to a quartic (interacting) term in fermions
- Quartic fermion Hamiltonians cannot be diagonalized analytically in general
- The MFIM is believed to be thermalizing (quantum chaotic) at generic parameters
- Yet it is not "equally chaotic" everywhere -- this is the central question of the project

---

## Chapter 5: Thermalization and Its Absence

### 5.1 The Gibbs State
- In Chapter 1, we wrote down the Boltzmann distribution: configuration $c$ has probability $p_c \propto e^{-\beta E_c}$
- The quantum generalization is the Gibbs state (thermal density matrix): $\rho_{\text{th}} = \frac{e^{-\beta H}}{\text{tr}[e^{-\beta H}]}$
- In the energy eigenbasis, this is diagonal with entries $\propto e^{-\beta E_n}$ -- exactly the Boltzmann distribution
- For a classical model (diagonal $H$), this reduces to what we discussed in Chapter 1
- Thermal expectation values: $\langle O \rangle_{\text{th}} = \text{tr}[\rho_{\text{th}} O]$

### 5.2 Thermalization
- We wrote the Boltzmann distribution "by hand" as a postulate of statistical mechanics -- but why should a system actually obey it?
- Thermalization: expectation values of local observables under unitary evolution approach their Gibbs state values
- Thermalization occurs in many, but not all, quantum many-body systems

### 5.3 How IOMs Prevent Thermalization
- If $[H, A] = 0$, then $\langle A \rangle$ is pinned to its initial value forever
- This initial value generically differs from the thermal value
- Systems with many IOMs (e.g., integrable systems) do not thermalize to Gibbs ensembles
- Instead they thermalize to generalized Gibbs ensembles (GGE) that account for all conserved quantities

### 5.4 Prethermalization
- Some systems thermalize eventually, but remain non-thermal for long timescales
- This is connected to approximate IOMs: $\|[H, A]\| \sim 1/\tau$ means $A$ is approximately conserved up to time $\tau$
- The system "looks non-thermal" on timescale $\tau$, then eventually thermalizes
- Examples: weakly perturbed integrable systems

---

## Chapter 6: Slow Modes in the Quantum Ising Model

### 6.1 Defining Slow Modes
- Relaxing the definition of IOMs: instead of exactly conserved, look for approximately conserved operators
- Two key properties: slowness (small commutator with $H$) and simplicity (overlap with local/small operators)
- The tradeoff: the more slowly an operator evolves, the less simple it can be

### 6.2 The Lindbladian Approach (Paper 1: 2506.02970)
- Add weak local noise to the system (depolarizing channel)
- IOMs with small support decay slowly under noise; generic operators decay fast
- Diagonalize the Lindbladian superoperator $\mathcal{L}^\dagger$
- Low-lying eigenoperators (slow decay rates) correspond to IOMs
- Demonstrated for TFIM, MFIM, and Heisenberg models

### 6.3 The Simple Slow Operator Approach (Paper 2: 2604.13172)
- Define the ensemble variance norm $\|A\|_{\mathcal{E}}$ to measure simplicity
- An operator is "simple" if it has large overlap with local operators (large $\|A\|_{\mathcal{E}}$)
- The $\nu$-$\tau$ plane: each operator maps to a point $(\tau_A, \nu_A)$ where $\tau_A = 1/\|[H,A]\|$ and $\nu_A = \|A\|_{\mathcal{E}}^2$
- The upper envelope $\nu(\tau)$ characterizes the system's thermalization properties
- Main theorem: absence of simple slow operators implies thermalization

### 6.4 The Numerical Problem
- Finding slow modes reduces to a superoperator eigenvalue problem
- Tools: Python, NumPy, QuSpin for constructing spin chain Hamiltonians
- Constructing the Hamiltonian and the superoperator
- Solving the eigenvalue problem and interpreting the results

### 6.5 The Phase Diagram
- Scan over $(h_x, h_z)$ parameter space of the MFIM
- At each point, identify whether slow modes exist and what they are
- Expected structure:
  - Near TFIM ($h_z \approx 0$): Majorana bilinear slow modes
  - Near classical Ising ($h_x \approx 0$): domain-wall-related slow modes
  - Large $h_x$ and $h_z$: fully chaotic, no slow modes
  - Intermediate regions: prethermal slow modes, potentially new mechanisms
- Connection to the "chaoticity phase diagram" from the papers

---

## Appendix A: Mathematical Background

### A.1 Matrix Norms
- Review of different matrix norms: operator norm (largest singular value), trace norm, Frobenius norm
- Frobenius norm: $\|A\|_F = \sqrt{\text{tr}(A^\dagger A)}$
- Relations between norms: operator norm $\leq$ Frobenius norm $\leq \sqrt{D} \times$ operator norm (where $D$ is the dimension)
- For our purposes, we will primarily use the Frobenius norm -- it is natural for many-body operators and connects to the Hilbert-Schmidt inner product

### A.2 Matrix Exponentials
- Definition via Taylor series: $e^A = \sum_{n=0}^{\infty} \frac{A^n}{n!}$
- Relationship to ODEs: $e^{At}$ is the solution to $\frac{dx}{dt} = Ax$ with $x(0) = x_0$, giving $x(t) = e^{At} x_0$
- This is why $|\psi(t)\rangle = e^{-iHt}|\psi(0)\rangle$ solves the Schrodinger equation
- Properties:
  - $e^A e^B = e^{A+B}$ if and only if $[A, B] = 0$ (does not hold in general!)
  - Unitarity: $e^{iH}$ is unitary when $H$ is Hermitian
  - Inverse: $(e^A)^{-1} = e^{-A}$
- Similarity transforms: $S e^{A} S^{-1} = e^{S A S^{-1}}$ -- this justifies thinking about matrix exponentials in the eigenbasis (diagonalize $A = S D S^{-1}$, then $e^A = S e^D S^{-1}$, and $e^D$ is just exponentials of the eigenvalues)
- Adjoint action: $e^A B e^{-A} = B + [A, B] + \frac{1}{2!}[A, [A, B]] + \cdots$
- Trotterization: $e^{A+B} = \lim_{n \to \infty} (e^{A/n} e^{B/n})^n$ -- useful for numerical simulation and for understanding the interplay of non-commuting terms in a Hamiltonian
