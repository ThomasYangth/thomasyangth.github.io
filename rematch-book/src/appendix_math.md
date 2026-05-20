## Appendix A: Mathematical Background

This appendix collects the linear-algebra facts that appear repeatedly throughout the book. Everything here is standard material, but having it in one place should make the main chapters easier to read. We assume familiarity with matrix multiplication, eigenvalues, and the Dirac bra-ket notation.

---

### A.1 Matrix Norms

A **norm** on matrices assigns a non-negative size \\(\|A\|\\) to every matrix \\(A\\), with the usual properties: \\(\|A\| = 0\\) iff \\(A = 0\\), \\(\|\alpha A\| = |\alpha|\,\|A\|\\), and the triangle inequality \\(\|A + B\| \leq \|A\| + \|B\|\\). Three norms appear most often in quantum information.

**Operator norm (spectral norm).** The operator norm of \\(A\\) is its largest singular value:
\\[
\|A\|_{\mathrm{op}} = \sigma_{\max}(A) = \max_{|v\rangle \neq 0} \frac{\|A|v\rangle\|}{\||v\rangle\|}.
\\]
For a Hermitian matrix, this equals the largest absolute eigenvalue. The operator norm is *submultiplicative*: \\(\|AB\|\_{\mathrm{op}} \leq \|A\|\_{\mathrm{op}}\|B\|\_{\mathrm{op}}\\).

**Trace norm.** The trace norm is the sum of the singular values:
\\[
\|A\|_{\mathrm{tr}} = \mathrm{tr}\!\left(\sqrt{A^\dagger A}\right) = \sum_i \sigma_i(A).
\\]
This norm is central to distinguishing quantum states: the trace distance between density matrices \\(\rho\\) and \\(\sigma\\) is \\(\frac{1}{2}\|\rho - \sigma\|\_{\mathrm{tr}}\\).

**Frobenius norm (Hilbert-Schmidt norm).** The Frobenius norm treats the matrix as a vector of its entries:
\\[
\|A\|_F = \sqrt{\mathrm{tr}(A^\dagger A)} = \sqrt{\sum_{i,j} |A_{ij}|^2}.
\\]
Equivalently, \\(\|A\|\_F = \sqrt{\sum\_i \sigma\_i^2}\\). The Frobenius norm comes from the **Hilbert-Schmidt inner product** \\(\langle A, B \rangle = \mathrm{tr}(A^\dagger B)\\), which makes the space of operators into a Hilbert space in its own right. This is the norm we will use most often in this book: it is the natural choice for many-body operators and arises whenever we measure the "size" of an error by averaging over all input states.

**Relations between norms.** For a \\(D \times D\\) matrix \\(A\\),
\\[
\|A\|_{\mathrm{op}} \;\leq\; \|A\|_F \;\leq\; \sqrt{D}\,\|A\|_{\mathrm{op}}.
\\]
The left inequality follows because \\(\sigma\_{\max} \leq \sqrt{\sum\_i \sigma\_i^2}\\). The right inequality follows because \\(A\\) has at most \\(D\\) nonzero singular values, each at most \\(\sigma\_{\max}\\), so \\(\sum\_i \sigma\_i^2 \leq D\,\sigma\_{\max}^2\\).

**Example.** Let \\(A = \mathrm{diag}(3, 1, 1)\\). Then \\(\|A\|\_{\mathrm{op}} = 3\\), \\(\|A\|\_F = \sqrt{9 + 1 + 1} = \sqrt{11}\\), and \\(\|A\|\_{\mathrm{tr}} = 5\\). Note \\(3 \leq \sqrt{11} \leq \sqrt{3} \cdot 3\\), consistent with the bounds above.

---

### A.2 Matrix Exponentials

#### Definition

The exponential of a square matrix \\(A\\) is defined by the power series
\\[
e^A = \sum_{n=0}^{\infty} \frac{A^n}{n!} = I + A + \frac{A^2}{2!} + \frac{A^3}{3!} + \cdots
\\]
This series converges for every finite matrix \\(A\\) (convergence can be checked using the Frobenius norm, since \\(\|A^n\|\_F \leq \|A\|\_F^n\\)).

**Example (diagonal matrix).** If \\(A = \mathrm{diag}(\lambda\_1, \ldots, \lambda\_D)\\), the series acts entry-by-entry:
\\[
e^A = \mathrm{diag}(e^{\lambda_1}, \ldots, e^{\lambda_D}).
\\]

**Example (Pauli matrix).** Consider \\(A = -i\theta\, Z\\) where \\(Z = \mathrm{diag}(1, -1)\\). Then
\\[
e^{-i\theta Z} = \mathrm{diag}(e^{-i\theta}, e^{i\theta}) = \begin{pmatrix} e^{-i\theta} & 0 \\ 0 & e^{i\theta} \end{pmatrix}.
\\]
More generally, for any Pauli matrix \\(\sigma\\) satisfying \\(\sigma^2 = I\\), we have
\\[
e^{-i\theta \sigma} = \cos\theta\, I - i \sin\theta\, \sigma,
\\]
which you can verify by splitting the Taylor series into even and odd powers.

#### Connection to differential equations

The matrix exponential arises as the solution to the first-order linear ODE
\\[
\frac{d\mathbf{x}}{dt} = A\,\mathbf{x}, \qquad \mathbf{x}(0) = \mathbf{x}_0.
\\]
Substituting \\(\mathbf{x}(t) = e^{At}\,\mathbf{x}\_0\\) and differentiating term-by-term confirms this is a solution:
\\[
\frac{d}{dt} e^{At} = A\, e^{At}.
\\]
In quantum mechanics, the Schrodinger equation \\(i\frac{d}{dt}|\psi\rangle = H|\psi\rangle\\) is exactly this kind of ODE with \\(A = -iH\\), so its solution is
\\[
|\psi(t)\rangle = e^{-iHt}\,|\psi(0)\rangle.
\\]
(We set \\(\hbar = 1\\) throughout.) This is the reason the matrix exponential is ubiquitous in quantum physics.

#### Key properties

**Commutativity and products.** For general matrices, \\(e^A e^B \neq e^{A+B}\\). The identity
\\[
e^A e^B = e^{A+B}
\\]
holds **if and only if** \\([A, B] = 0\\). This is one of the most common pitfalls in quantum mechanics. For instance, if \\(H = H\_1 + H\_2\\) with \\([H\_1, H\_2] \neq 0\\), then \\(e^{-i(H\_1 + H\_2)t} \neq e^{-iH\_1 t}\, e^{-iH\_2 t}\\).

*Sketch of proof.* Expand both sides to second order:
\\[
e^A e^B = (I + A + \tfrac{1}{2}A^2 + \cdots)(I + B + \tfrac{1}{2}B^2 + \cdots) = I + A + B + \tfrac{1}{2}A^2 + AB + \tfrac{1}{2}B^2 + \cdots
\\]
while
\\[
e^{A+B} = I + (A+B) + \tfrac{1}{2}(A+B)^2 + \cdots = I + A + B + \tfrac{1}{2}A^2 + \tfrac{1}{2}(AB + BA) + \tfrac{1}{2}B^2 + \cdots
\\]
Comparing the second-order terms, these agree only when \\(AB = \tfrac{1}{2}(AB + BA)\\), i.e., \\([A, B] = 0\\).

**Unitarity.** If \\(H\\) is Hermitian (\\(H^\dagger = H\\)), then \\(U = e^{iH}\\) is unitary:
\\[
U^\dagger U = (e^{iH})^\dagger\, e^{iH} = e^{-iH}\, e^{iH} = e^{-iH + iH} = I,
\\]
where the third equality uses \\([-iH, iH] = 0\\). This guarantees that time evolution in quantum mechanics preserves the norm of the state.

**Inverse.** The inverse of \\(e^A\\) is \\(e^{-A}\\):
\\[
e^A\, e^{-A} = e^{A - A} = e^0 = I,
\\]
since \\([A, -A] = 0\\).

**Determinant.** A useful identity: \\(\det(e^A) = e^{\mathrm{tr}(A)}\\). This follows immediately in the eigenbasis.

#### Similarity transforms

If \\(S\\) is invertible, then
\\[
S\, e^A\, S^{-1} = e^{S A S^{-1}}.
\\]
This is straightforward from the series: \\(S A^n S^{-1} = (S A S^{-1})^n\\), so
\\[
S\, e^A\, S^{-1} = \sum_{n=0}^{\infty} \frac{S A^n S^{-1}}{n!} = \sum_{n=0}^{\infty} \frac{(S A S^{-1})^n}{n!} = e^{S A S^{-1}}.
\\]

This identity justifies the standard strategy for computing matrix exponentials: diagonalize \\(A = S D S^{-1}\\) (where \\(D\\) is diagonal), then
\\[
e^A = S\, e^D\, S^{-1},
\\]
and \\(e^D\\) is trivial since it is just the entrywise exponential of the eigenvalues. In the quantum context, this means that to understand \\(e^{-iHt}\\), it suffices to find the eigenbasis of \\(H\\).

#### Adjoint action (Hadamard lemma)

A frequently needed formula is the expansion of a "conjugation by an exponential":
\\[
e^A\, B\, e^{-A} = B + [A, B] + \frac{1}{2!}[A, [A, B]] + \frac{1}{3!}[A, [A, [A, B]]] + \cdots = \sum_{n=0}^{\infty} \frac{1}{n!}\,\mathrm{ad}_A^n(B),
\\]
where \\(\mathrm{ad}\_A(B) = [A, B]\\) and \\(\mathrm{ad}\_A^n\\) means applying the commutator \\(n\\) times.

*Proof sketch.* Define \\(f(t) = e^{tA}\, B\, e^{-tA}\\). Then \\(f(0) = B\\) and
\\[
f'(t) = A\, e^{tA}\, B\, e^{-tA} - e^{tA}\, B\, e^{-tA}\, A = [A, f(t)].
\\]
Iterating, \\(f^{(n)}(0) = \mathrm{ad}\_A^n(B)\\), and the result follows by Taylor-expanding \\(f(t)\\) around \\(t = 0\\) and setting \\(t = 1\\).

**Example.** Take \\(A = -i\theta Z/2\\) and \\(B = X\\) (Pauli matrices). Since \\([Z, X] = 2iY\\) and \\([Z, Y] = -2iX\\), the series gives
\\[
e^{-i\theta Z/2}\, X\, e^{i\theta Z/2} = \cos\theta\, X + \sin\theta\, Y,
\\]
which is a rotation of the Pauli \\(X\\) operator about the \\(Z\\)-axis by angle \\(\theta\\). This is a basic instance of the Heisenberg picture of time evolution.

#### Baker-Campbell-Hausdorff formula

When \\(A\\) and \\(B\\) do not commute, the exponents do not simply add. The BCH formula gives the correction:
\\[
e^A\, e^B = e^{A + B + \frac{1}{2}[A, B] + \frac{1}{12}([A,[A,B]] - [B,[A,B]]) + \cdots}.
\\]
The higher-order terms involve increasingly nested commutators. In practice, the important point is:

- To **first order** in the commutator: \\(e^A e^B \approx e^{A + B + \frac{1}{2}[A,B]}\\).
- If \\([A, B]\\) commutes with both \\(A\\) and \\(B\\), the series truncates and \\(e^A e^B = e^{A + B + \frac{1}{2}[A,B]}\\) exactly. (This special case is sometimes called the **Glauber formula** and is heavily used in quantum optics.)

#### Trotterization

Even though \\(e^{A+B} \neq e^A e^B\\) in general, we can recover the combined exponential as a limit:
\\[
e^{A+B} = \lim_{n \to \infty} \left(e^{A/n}\, e^{B/n}\right)^n.
\\]
This is the **Trotter product formula** (also called the Lie-Trotter formula). The idea is that for small \\(\epsilon = 1/n\\), the BCH correction is of order \\(\epsilon^2\\):
\\[
e^{A\epsilon}\, e^{B\epsilon} = e^{(A+B)\epsilon + \frac{1}{2}[A,B]\epsilon^2 + O(\epsilon^3)},
\\]
so the error per step is \\(O(\epsilon^2)\\) and after \\(n = 1/\epsilon\\) steps the total error is \\(O(\epsilon)\\), which vanishes as \\(n \to \infty\\).

For a *finite* \\(n\\), the first-order Trotter approximation incurs an error
\\[
\left\|\left(e^{A/n}\, e^{B/n}\right)^n - e^{A+B}\right\| = O\!\left(\frac{1}{n}\right).
\\]
A better approximation is the **symmetric (second-order) Trotter splitting**:
\\[
e^{A+B} \approx \left(e^{A/2n}\, e^{B/n}\, e^{A/2n}\right)^n,
\\]
whose error scales as \\(O(1/n^2)\\).

**Why this matters.** In quantum simulation, we often have a Hamiltonian \\(H = H\_1 + H\_2 + \cdots + H\_k\\) where each \\(H\_j\\) is easy to exponentiate individually (e.g., a local term), but \\(H\\) itself is not. Trotterization lets us approximate the full time evolution \\(e^{-iHt}\\) as a product of simple unitaries, at the cost of a controllable error. This is the foundation of digital quantum simulation algorithms.

*Last modified: 2026-05-20*
