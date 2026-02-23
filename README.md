# Emerging Technologies Assessment

This repository contains coursework for the *Emerging Technologies* module.
The project explores the differences between classical and quantum algorithms
through the Deutsch and Deutsch–Jozsa problems.

The implementation is presented as a Jupyter notebook and is structured to
demonstrate problem-solving, theoretical understanding and clean software
engineering practices suitable for an informed computing audience.

---

## Project Structure

- `problems.ipynb`  
  Main notebook containing implementations, explanations and results for all
  assessment problems.

- `requirements.txt`  
  Lists all Python dependencies required to run the notebook.

- `.gitignore`  
  Excludes unnecessary files from version control.

---

## Running the Project

To run this project locally:

1. Clone the repository:
   ```bash
   git clone <https://github.com/BrianWalsh23/emerging_technologies.git>
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
3. Launch the notebook:
   ```bash
   jupyter notebook problems.ipynb

## Problem 1: Generating Random Boolean Functions

Problem 1 focuses on the construction of Boolean functions that satisfy the
Deutsch–Jozsa promise condition. For a function with four Boolean inputs, there
are 2⁴ = 16 possible input combinations. Under the promise, the function is
guaranteed to be either *constant* or *balanced*.

A constant function returns the same Boolean value for all possible inputs.
A balanced function returns True for exactly half of the input combinations and
False for the remaining half. These properties are fundamental to the operation
of the Deutsch–Jozsa algorithm and are enforced explicitly in this implementation.

The notebook defines helper generators for constant and balanced functions and
then composes them into a single function, `random_constant_balanced`, which
randomly returns one of the two valid function types. Balanced functions are
constructed by selecting exactly half of the possible input combinations to
evaluate to True this ensures the promise condition is satisfied by construction.

Verification code is included to evaluate generated functions across
all possible inputs. This confirms that constant functions produce uniform
outputs, while balanced functions produce an equal number of True and False
results. This explicit verification demonstrates correctness and provides a
classical baseline for comparison with later quantum implementations.

## Problem 2: Classical Testing for Function Type

Problem 2 examines how a classical deterministic algorithm can be used to
determine whether a Boolean function satisfying the Deutsch–Jozsa promise
condition is constant or balanced.

Given a function with four Boolean inputs, a classical approach must rely on
evaluating the function on multiple inputs and observing the resulting outputs.
This requires evaluating all 2⁴ = 16 possible input combinations to guarantee a correct classification.

The notebook implements a classical classifier that evaluates the function on
the full input space and checks whether all outputs are identical or evenly
split between True and False. This strategy guarantees correctness
but highlights the exponential growth in required function evaluations as the
number of inputs increases.

The notebook includes a theoretical efficiency analysis. Under the promise condition, a balanced
function can produce at most eight identical outputs. As a result, if nine
evaluated outputs are identical this means the function must be constant. This establishes
that a classical deterministic algorithm requires at most 2ⁿ⁻¹ + 1 function
calls to be 100% certain, which is nine calls for the four-input case.

This problem provides a classical baseline for comparison with the quantum
Deutsch–Jozsa algorithm, which determines the same global property using a
single oracle query. The contrast illustrates a fundamental limitation of
classical computation when solving promise problems and motivates the use of
quantum query algorithms in later problems.

## Problem 3: Quantum Oracles for Deutsch's Algorithm

Problem 3 transitions from classical to quantum computation by implementing the
quantum oracles required for Deutsch's algorithm. In the single-input case,
there are exactly four possible Boolean functions: two constant (f(x) = 0,
f(x) = 1) and two balanced (f(x) = x, f(x) = ¬x).

Each oracle is implemented as a reversible quantum circuit that encodes its
corresponding Boolean function through the transformation |x⟩|y⟩ -> |x⟩|y ⊕ f(x)⟩.
The constant oracles are straightforward: the f(x) = 0 oracle performs no
operation, while the f(x) = 1 oracle applies an X gate to flip the output qubit.
The balanced oracles require conditional logic: the identity function uses a
CNOT gate, while the NOT function uses an X-CNOT-X sequence to invert the
control condition.

The notebook implements Deutsch's algorithm, which determines whether a function
is constant or balanced through a single oracle evaluation. The algorithm
exploits quantum superposition and phase kickback to extract global properties
of the function without evaluating individual inputs. Measurement outcomes
confirm that constant functions produce result 0, while balanced functions
produce result 1. This demonstrates the quantum advantage over the classical
two-query requirement.

This problem establishes the foundation for quantum query algorithms by
introducing the oracle model and demonstrating how quantum interference enables
more efficient function classification than classical deterministic approaches.






## References
- Deutsch, D., & Jozsa, R. (1992). Rapid solution of problems by quantum 
  computation. *Proceedings of the Royal Society of London A*, 439(1907), 
  553–558. https://doi.org/10.1098/rspa.1992.0167

- Jozsa, R. (1993). Computation and quantum superposition. *Proceedings 
  of the 7th Annual Structure in Complexity Theory Conference*, IEEE, 
  192–194.

- IBM Quantum. *Deutsch–Jozsa Algorithm*.  
  https://quantum.cloud.ibm.com/learning/en/modules/computer-science/deutsch-jozsa  
  Used to define the Deutsch–Jozsa problem, including the promise condition that
  Boolean functions are either constant or balanced.

- IBM Quantum. *Deutsch’s Algorithm*.  
  https://quantum.cloud.ibm.com/learning/en/courses/fundamentals-of-quantum-algorithms/quantum-query-algorithms/deutsch-algorithm  
  Provides background on the single-input case and motivates the extension to
  multi-input functions explored in this project.

- IBM Quantum. *Qiskit*.  
  https://www.ibm.com/quantum/qiskit  
  Official framework used for implementing and simulating quantum circuits in
  the quantum sections of the notebook.
