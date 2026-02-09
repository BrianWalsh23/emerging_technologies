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
