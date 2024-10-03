
# Introduction to Qiskit patterns

A Qiskit pattern is a general framework for breaking down domain-specific problems and contextualizing required capabilities in stages. This allows for the seamless composability of new capabilities developed by IBM Quantum™ researchers (and others) and enables a future in which quantum computing tasks are performed by powerful heterogenous (CPU/GPU/QPU) computing infrastructure. Blocks or groups of blocks perform the steps of a pattern, with the Qiskit SDK providing an important foundational layer, supported by other tools or services developed by IBM Quantum or the quantum open-source community. Qiskit patterns allow domain experts to specify a problem and compose the tooling (blocks) that achieves a Qiskit pattern. That pattern can then be executed locally, through cloud services, or deployed with Qiskit Serverless.



## The four steps of a Qiskit pattern are as follows:

- [Map problem to quantum circuits and operators](https://docs.quantum.ibm.com/guides/map-problem-to-circuits)
- [Optimize for target hardware](https://docs.quantum.ibm.com/guides/optimize-for-hardware)
- [Execute on target hardware](https://docs.quantum.ibm.com/guides/execute-on-hardware)
- [Post-process results](https://docs.quantum.ibm.com/guides/post-process-results)


![](https://docs.quantum.ibm.com/images/qiskit-patterns/patterns.svg)

Each step is detailed in the sections below.
## Map problem to quantum circuits and operators

This step describes how a user starts with a classical problem and figures out how to map it to a quantum computer. For example, in applications such as chemistry and quantum simulation, this step generally involves constructing a quantum circuit representing the Hamiltonian you are attempting to solve. During this step, for certain problems, it might also be desirable to specify the mapping of the problem onto qubits in the heavy-hex (or gross) lattice of IBM;reg; hardware from the outset if the structure of the problem lends itself to optimization earlier. It is also worth considering at this point what the outcome of the particular algorithm will be in preparation for the later execute step - for example, if the desired outcome involves inferring correlation functions using Hadamard tests, you might prepare to use Sampler, whereas specifying observables would use the Estimator and could provide many error mitigation options.

The output of this step is normally a collection of circuits or quantum operators that can be optimized for hardware in the next step.

## Optimize for target hardware
In this step you take the abstract circuits (or operators) produced from the map step and perform a series of optimizations on them. This can include mapping the route and layout of the circuit to physical qubit hardware, converting to basis gates of the hardware, and reducing the number of operations, all designed to optimize the likelihood of success in the later execute step. At this point you might also wish to test out your circuits with a simulator before executing on real hardware in the next step.

During this step, abstract circuits must be transpiled to Instruction Set Architecture (ISA) circuits. An ISA circuit is one that only consists of gates understood by the target hardware (basis gates), and any multi-qubit gates needed to obey any connectivity constraints (coupling map). Only ISA circuits can be run on IBM hardware using IBM Qiskit Runtime.
## Execute on target hardware
This step involves running your circuits on hardware and produces the outputs of the quantum computation. The ISA circuits produced in the previous step can be executed using either a Sampler or Estimator primitive from Qiskit Runtime, initialized locally on your computer or from a cluster or other heterogeneous compute environment. These can be executed in a Batch, which allows parallel transpilation for classical computational efficiency - or a Session, which allows iterative tasks to be implemented efficiently without queuing delays. During this step, there is also the option to configure certain error suppression and mitigation techniques provided by Qiskit Runtime.

Depending on whether you are using the Sampler or Estimator primitive, the outcome of this step will be different. If using the Sampler, the output will be per-shot measurements in the form of bitstrings. If using the Estimator, the output will be expectation values of observables corresponding to physical quantities or cost functions.

## Post-process results
This final step involves stitching the outputs from the prior step back together to obtain the desired result. This can involve a range of classical data-processing steps such as visualizing results, readout error mitigation techniques, marginalizing quasi-probability distributions to ascertain results on smaller sets of qubits, or post-selection on inherent properties of the problem, such as total spin, parity, or particle conservation by removing unphysical observables.

As the field moves from bespoke circuit construction to utility-scale workflows, the flexibility and ease with which Qiskit patterns allow users to compose the different steps of the pattern opens quantum computing to a wide variety of applications and techniques for easy use by quantum computational scientists.

# Guides demonstrating Qiskit patterns in action
## Guides focused on one or more pattern steps

- [Map problem to quantum circuits and operators](https://docs.quantum.ibm.com/guides/map-problem-to-circuits)
- [Optimize for target hardware](https://docs.quantum.ibm.com/guides/optimize-for-hardware)
- [Execute on target hardware](https://docs.quantum.ibm.com/guides/execute-on-hardware)
- [Post-process results](https://docs.quantum.ibm.com/guides/post-process-results)

## Guides focused on the full patterns workflow
- [Qiskit Serverless](https://docs.quantum.ibm.com/guides/serverless)

    - [Overview of Qiskit Serverless](https://docs.quantum.ibm.com/guides/serverless)
    - [Write your first Qiskit Serverless program](https://docs.quantum.ibm.com/guides/serverless-first-program)
    - [Run your first Qiskit Serverless workload remotely](https://docs.quantum.ibm.com/guides/serverless-run-first-workload)
    - [Manage Qiskit Serverless compute and data resources](https://docs.quantum.ibm.com/guides/serverless-manage-resources)
    - [Port code to Qiskit Serverless]()
- [Qiskit Functions](https://docs.quantum.ibm.com/guides/serverless-port-code)

    - [Q-CTRL Optimization Solver](https://docs.quantum.ibm.com/guides/q-ctrl-optimization-solver)
    - [QunaSys QURI Chemistry](https://docs.quantum.ibm.com/guides/qunasys-quri-chemistry)