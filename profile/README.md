# Qevedo

**Open-source software for compiling and simulating quantum programs, fast, on your own machine.**

```bash
pip install qevedo
```

| Project | Package | What it does |
|---|---|---|
| [**qevedo-simulator**](https://github.com/qevedo/qevedo-simulator) | [![PyPI](https://img.shields.io/pypi/v/qevedo-simulator?label=qevedo-simulator)](https://pypi.org/project/qevedo-simulator/) | **qvd**, a quantum circuit simulator in Rust with five methods, chosen automatically: an AVX2 state vector, a Stim-style stabilizer simulator, matrix product states, and a Clifford-frame near-Clifford simulator. |
| [**qevedo-compiler**](https://github.com/qevedo/qevedo-compiler) | [![PyPI](https://img.shields.io/pypi/v/qevedo-compiler?label=qevedo-compiler)](https://pypi.org/project/qevedo-compiler/) | **QCC**, a technology-agnostic quantum circuit compiler: OpenQASM 2/3 in and out, lowered and optimized for a device profile. |
| [**openqasm**](https://github.com/qevedo/openqasm) | [![PyPI](https://img.shields.io/pypi/v/openqasm?label=openqasm)](https://pypi.org/project/openqasm/) | An OpenQASM 2 and 3 parser and semantic checker for Python. |
| [**qevedo**](https://github.com/qevedo/qevedo) | [![PyPI](https://img.shields.io/pypi/v/qevedo?label=qevedo)](https://pypi.org/project/qevedo/) | All of the above in one install. |

```python
from qevedo.compiler import compile_source, emit_qasm
from qevedo.simulator import run

compiled = compile_source(open("circuit.qasm").read())  # native gates of your device
result = run(emit_qasm(compiled), shots=1000)           # the best simulation method, automatically
print(result.counts, result.backend)
```

## Fast where it counts

Measured on one workstation (Intel i9-14900K, 62 GB), against the reference tools on the same circuits:

- **State vector:** 3–4× faster than Google's qsim and 7–12× faster than Qiskit Aer at 26–30 qubits.
- **Clifford circuits:** a distance-101 surface code (20,401 qubits, 1M measurements) samples 10,000 shots in 1.5 s, 8× faster than Stim.
- **Low entanglement (MPS):** 1.6–14× faster than the faster of Qiskit Aer and quimb, with matching fidelity estimates.
- **Clifford + T:** 200 qubits with 20 T gates sample in 0.11 s; every Qiskit Aer method takes over 10 minutes or does not support the circuit.

<img src="https://raw.githubusercontent.com/qevedo/qevedo-simulator/master/benchmarks/charts/stabilizer.svg" alt="Surface code sampling: qvd vs Stim vs Qiskit Aer" width="49%"> <img src="https://raw.githubusercontent.com/qevedo/qevedo-simulator/master/benchmarks/charts/nearclifford.svg" alt="Clifford+T circuits: qvd vs Qiskit Aer" width="49%">

Methods, raw data and how to reproduce every number: [qevedo-simulator/benchmarks](https://github.com/qevedo/qevedo-simulator/tree/master/benchmarks).

## Get involved

Issues and pull requests are welcome in each repository. Everything is open source under the MIT license.

[qevedo.com](https://qevedo.com)
