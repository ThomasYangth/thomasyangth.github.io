## The Classical Ising Model

In this chapter, we introduce the Ising model -- one of the simplest and most important models in all of physics. It captures the essential idea behind magnetism using nothing more than binary variables and nearest-neighbor interactions. Despite its simplicity, the Ising model exhibits rich behavior, including phase transitions, and serves as the starting point for understanding more sophisticated quantum models that we will encounter later.

### 1.1 Spins on a Chain

Imagine a row of atoms, each carrying a tiny magnetic moment that can point either **up** or **down**. We label the atoms by an index \\( i = 1, 2, \ldots, N \\), and we describe the state of each atom by a variable

\\[ s_i = +1 \quad (\text{up}) \qquad \text{or} \qquad s_i = -1 \quad (\text{down}). \\]

This is called a **spin** variable. A complete specification of all \\( N \\) spins,

\\[ (s_1, s_2, \ldots, s_N), \\]

is called a **configuration** of the system. For \\( N \\) spins, there are \\( 2^N \\) possible configurations in total (each spin has two choices, and the choices are independent).

For example, a chain of \\( N = 3 \\) spins has \\( 2^3 = 8 \\) configurations:

\\[ (+1,+1,+1),\quad (+1,+1,-1),\quad (+1,-1,+1),\quad (+1,-1,-1), \\]
\\[ (-1,+1,+1),\quad (-1,+1,-1),\quad (-1,-1,+1),\quad (-1,-1,-1). \\]

You can think of each configuration as a "microstate" of the magnet. The central question of statistical mechanics is: **which of these configurations are likely to occur, and why?** To answer this, we need a way to assign an energy to each configuration.

### 1.2 The Energy Function

#### The Ising Hamiltonian

The **Hamiltonian** (energy function) of the Ising model on a chain is

\\[ H = -J \sum_{i=1}^{N-1} s_i s_{i+1}. \\]

Here \\( J \\) is a constant called the **coupling strength**, and the sum runs over all nearest-neighbor pairs along the chain. (We are using open boundary conditions here, so spin 1 is only coupled to spin 2, and spin \\( N \\) is only coupled to spin \\( N-1 \\).)

The key observation is that the product \\( s\_i s\_{i+1} \\) equals \\( +1 \\) when the two spins are **aligned** (both up or both down) and \\( -1 \\) when they are **anti-aligned** (one up, one down). Because of the overall minus sign in \\( H = -J \sum s\_i s\_{i+1} \\):

- When \\( J > 0 \\): aligned pairs contribute \\( -J < 0 \\) to the energy (lowering it), while anti-aligned pairs contribute \\( +J > 0 \\) (raising it). The system **prefers alignment**. This is called a **ferromagnet**.
- When \\( J < 0 \\): the situation is reversed. Anti-aligned pairs lower the energy. The system **prefers alternation** (up-down-up-down...). This is called an **antiferromagnet**.

For the rest of this chapter, we focus on the ferromagnetic case \\( J > 0 \\).

#### Why "ferromagnet"?

Define the **total magnetization** as the sum of all spins:

\\[
M = \sum\_{i=1}^{N} s\_i.
\\]

This quantity measures the net magnetic moment of the system: if most spins point up, \\( M \\) is large and positive; if most point down, it is large and negative; if spins are randomly oriented, \\( M \approx 0 \\).

For a ferromagnet (\\( J > 0 \\)), the lowest-energy states are the fully aligned ones: all spins up (\\( M = +N \\)) or all spins down (\\( M = -N \\)). Both have the maximum possible \\( |M| \\). This means that at low temperatures, the system spontaneously develops a nonzero total magnetization -- it becomes a magnet, even without an external magnetic field pushing the spins in one direction. This is the origin of the name "ferromagnet."

For an antiferromagnet (\\( J < 0 \\)), the ground state alternates up-down-up-down, so \\( M \approx 0 \\). The system has no net magnetic moment.

#### A concrete example: 3-spin chain

Let us work out the energy of every configuration for \\( N = 3 \\) with \\( J > 0 \\). The Hamiltonian is

\\[ H = -J(s_1 s_2 + s_2 s_3). \\]

| Configuration \\( (s\_1, s\_2, s\_3) \\) | \\( s\_1 s\_2 \\) | \\( s\_2 s\_3 \\) | Energy \\( H \\) |
|---|---|---|---|
| \\( (+1,+1,+1) \\) | \\( +1 \\) | \\( +1 \\) | \\( -2J \\) |
| \\( (-1,-1,-1) \\) | \\( +1 \\) | \\( +1 \\) | \\( -2J \\) |
| \\( (+1,+1,-1) \\) | \\( +1 \\) | \\( -1 \\) | \\( 0 \\) |
| \\( (+1,-1,-1) \\) | \\( -1 \\) | \\( +1 \\) | \\( 0 \\) |
| \\( (-1,-1,+1) \\) | \\( +1 \\) | \\( -1 \\) | \\( 0 \\) |
| \\( (-1,+1,+1) \\) | \\( -1 \\) | \\( +1 \\) | \\( 0 \\) |
| \\( (+1,-1,+1) \\) | \\( -1 \\) | \\( -1 \\) | \\( +2J \\) |
| \\( (-1,+1,-1) \\) | \\( -1 \\) | \\( -1 \\) | \\( +2J \\) |

Notice a few things:

1. The **lowest-energy** (ground state) configurations are the two fully aligned states: all up and all down, each with energy \\( -2J \\).
2. The **highest-energy** configurations are the two fully alternating states, with energy \\( +2J \\).
3. The four configurations with one "domain wall" (one pair aligned, one pair anti-aligned) sit at intermediate energy \\( 0 \\).

This makes physical sense: a ferromagnet wants all its spins to point the same way. Every place where neighboring spins disagree costs energy.

#### Adding an external magnetic field

In practice, we might also apply an external magnetic field \\( h \\) that biases the spins to point in one direction. This adds a term to the Hamiltonian:

\\[ H = -J \sum_{i=1}^{N-1} s_i s_{i+1}  -  h \sum_{i=1}^{N} s_i. \\]

The field term \\( -h \sum\_i s\_i \\) favors spins pointing up (\\( s\_i = +1 \\)) when \\( h > 0 \\) and spins pointing down (\\( s\_i = -1 \\)) when \\( h < 0 \\). For our 3-spin example with \\( h > 0 \\), the all-up state \\( (+1,+1,+1) \\) now has energy \\( -2J - 3h \\), while the all-down state \\( (-1,-1,-1) \\) has energy \\( -2J + 3h \\). The field breaks the symmetry between "all up" and "all down," selecting a unique ground state.

### 1.3 Statistical Mechanics and the Boltzmann Distribution

So far we have assigned an energy to each configuration. But which configuration does the system actually sit in?

#### The ground state

A first answer is simple: the system sits in the **ground state**, the configuration with the lowest energy. This is a natural guess -- physical systems tend to "settle down" to their lowest-energy state, just as a ball rolls to the bottom of a hill. The justification is that any system coupled to an environment will gradually lose energy to its surroundings, and the only state from which no further energy can be extracted is the ground state.

For the ferromagnetic Ising model, the ground states are the fully aligned configurations (all up or all down), as we computed above. So the ground-state picture already explains why a ferromagnet is magnetized.

#### The Boltzmann distribution

The ground-state picture is correct at zero temperature, but real systems are at finite temperature. At nonzero temperature, the system is constantly exchanging energy with its environment, and it does not sit in the ground state alone -- it fluctuates among many configurations. The question becomes: how likely is each configuration?

The answer comes from **statistical mechanics**. At thermal equilibrium at temperature \\( T \\), the probability of finding the system in a configuration \\( \mathbf{s} = (s\_1, \ldots, s\_N) \\) is given by the **Boltzmann distribution**:

\\[ p(\mathbf{s}) = \frac{1}{Z} e^{-\beta H(\mathbf{s})}, \\]

where \\( \beta = 1/T \\) is the **inverse temperature** (we set the Boltzmann constant \\( k\_B = 1 \\) for simplicity), and

\\[ Z = \sum_{\text{all configurations } \mathbf{s}} e^{-\beta H(\mathbf{s})} \\]

is the **partition function**, which serves as a normalization constant ensuring that probabilities sum to one.

The factor \\( e^{-\beta H} \\) is called the **Boltzmann weight**. It has a beautifully intuitive meaning:

- **Low-energy configurations** have large Boltzmann weight (since \\( H \\) is very negative, \\( -\beta H \\) is very positive, and the exponential is large).
- **High-energy configurations** have small Boltzmann weight.

So the Boltzmann distribution tells us that **low-energy states are more probable**. The energy function is not just an abstract quantity -- it directly determines which configurations you are likely to observe in nature.

#### The role of temperature

The inverse temperature \\( \beta = 1/T \\) controls how sharply the distribution is peaked on low-energy states:

- **Low temperature** (\\( \beta \to \infty \\), i.e., \\( T \to 0 \\)): The Boltzmann weight \\( e^{-\beta H} \\) becomes extremely sensitive to energy differences. Only the ground state (or states very close to it in energy) have appreciable probability. The system is **ordered** -- for the ferromagnetic Ising model, this means nearly all spins point the same way. In the \\( T \to 0 \\) limit, the Boltzmann distribution reduces to the ground-state picture we discussed above.

- **High temperature** (\\( \beta \to 0 \\), i.e., \\( T \to \infty \\)): The Boltzmann weight \\( e^{-\beta H} \approx 1 \\) for all configurations, regardless of their energy. Every configuration is equally likely. The system is **disordered** -- spins point up or down at random, and the magnet has no net magnetization.

- **Intermediate temperature**: There is a competition between energy (which favors order) and **entropy** (the fact that there are many more disordered configurations than ordered ones). This competition is at the heart of statistical mechanics.

#### Example: 3-spin chain at finite temperature

Returning to our 3-spin chain with \\( h = 0 \\), let us compute the Boltzmann weights at inverse temperature \\( \beta \\):

| Energy | Number of configurations | Boltzmann weight each |
|---|---|---|
| \\( -2J \\) | 2 | \\( e^{2\beta J} \\) |
| \\( 0 \\) | 4 | \\( 1 \\) |
| \\( +2J \\) | 2 | \\( e^{-2\beta J} \\) |

The partition function is

\\[ Z = 2e^{2\beta J} + 4 + 2e^{-2\beta J}. \\]

At low temperature (\\( \beta J \gg 1 \\)), the term \\( 2 e^{2\beta J} \\) dominates, so the system is almost certainly in one of the two ground states. At high temperature (\\( \beta J \ll 1 \\)), all three exponentials are approximately 1, so \\( Z \approx 8 \\) and every configuration has probability \\( \approx 1/8 \\) -- complete randomness.

#### Energy and temperature

There is a precise relationship between temperature and the average energy of a system. The **average energy** (or **internal energy**) at temperature \\( T \\) is the expectation value of the Hamiltonian under the Boltzmann distribution:

\\[
\langle H \rangle = \sum\_{\mathbf{s}} p(\mathbf{s}) H(\mathbf{s}) = \frac{1}{Z} \sum\_{\mathbf{s}} H(\mathbf{s}) e^{-\beta H(\mathbf{s})}.
\\]

There is a useful trick: the average energy can be computed from the partition function by taking a derivative,

\\[
\langle H \rangle = -\frac{\partial}{\partial \beta} \ln Z.
\\]

Let us carry this out explicitly for our 3-spin chain. We computed \\( Z = 2e^{2\beta J} + 4 + 2e^{-2\beta J} \\). Then

\\[
\ln Z = \ln\!\left(2e^{2\beta J} + 4 + 2e^{-2\beta J}\right),
\\]

and differentiating:

\\[
\langle H \rangle = -\frac{\partial \ln Z}{\partial \beta} = -\frac{4J e^{2\beta J} - 4J e^{-2\beta J}}{2e^{2\beta J} + 4 + 2e^{-2\beta J}} = -\frac{4J \sinh(2\beta J)}{2\cosh(2\beta J) + 2}.
\\]

Let us check the limits:

- **Low temperature** (\\( \beta J \gg 1 \\)): \\( \sinh(2\beta J) \approx \cosh(2\beta J) \approx \frac{1}{2}e^{2\beta J} \\), so \\( \langle H \rangle \approx -2J \\). This is exactly the ground-state energy -- at low temperature, the system sits in its ground state.

- **High temperature** (\\( \beta J \ll 1 \\)): \\( \sinh(2\beta J) \approx 2\beta J \\) and \\( \cosh(2\beta J) \approx 1 \\), so \\( \langle H \rangle \approx -\frac{4J \cdot 2\beta J}{4} = -2\beta J^2 \approx 0 \\). At high temperature, the system samples all configurations roughly equally, and the positive and negative energy contributions cancel out.

This illustrates a general principle: **temperature controls the average energy of the system**. Low temperature means low energy (close to the ground state), and high temperature means the energy is spread broadly across all configurations.

Conversely, the relationship works the other way: **if we know the average energy of a system, we can determine its temperature**. Since \\( \langle H \rangle \\) is a monotonically increasing function of \\( T \\) (higher temperature means higher energy), there is a one-to-one correspondence between the two. Given a system with a known average energy, we can invert this relationship to find the unique temperature \\( T \\) of the Boltzmann distribution that reproduces that energy. This idea -- that energy determines temperature -- will reappear in the quantum setting when we discuss thermalization in Chapter 5.

#### A glimpse ahead: phase transitions

A natural question is: as we smoothly tune the temperature, does the system transition **sharply** from ordered to disordered, or does the change happen gradually?

The answer depends on the dimensionality of the lattice:

- **1D Ising model** (a chain): There is **no phase transition** at any finite temperature. Any nonzero temperature introduces enough thermal fluctuations to destroy long-range order. The transition from order to disorder is smooth and gradual. (This can be proven exactly using the transfer matrix method, which we will encounter later.)

- **2D Ising model** (a square grid): There **is** a sharp phase transition at a critical temperature \\( T\_c \\). Below \\( T\_c \\), the system is ordered (net magnetization); above \\( T\_c \\), it is disordered. This was famously solved by Lars Onsager in 1944 and remains one of the landmark results in theoretical physics.

The existence or absence of phase transitions is one of the deepest questions in statistical mechanics, and understanding it will be a recurring theme as we move toward quantum models.

---

**Summary.** The classical Ising model assigns a binary spin \\( s\_i = \pm 1 \\) to each site of a lattice, with an energy function that rewards alignment (for \\( J > 0 \\)) between neighbors. At thermal equilibrium, the probability of each configuration is given by the Boltzmann distribution \\( p \propto e^{-\beta H} \\), where the inverse temperature \\( \beta \\) controls the tradeoff between energetic order and entropic disorder. In the next chapter, we will see how this classical picture is modified when we allow the spins to be quantum mechanical.

*Last modified: 2026-05-21*
