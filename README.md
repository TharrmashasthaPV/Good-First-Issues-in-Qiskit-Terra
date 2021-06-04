# Good First Issues in Qiskit Terra - Qiskit Mentorship 2021
This repo contain detailed information on the Qiskit mentorship project titled "Good First Issues in Qiskit Terra".

### Goal of the project
The goal of this project is simple; fix good first GitHub issues of Qiskit Terra. The project was under the mentoring of Dr.Luciano Bello.

### Our Work
Our work primarily comprises of two parts. In the first part, we worked on introducing a new feature that allows a user to condition gates on individual classical bits. In the second part, we worked on multiple independent issues in visualization, testing and documentation. A list of issues we worked on during the project is as follows:

- Classical conditioning of gates on single bits.
    - Classical conditioning on single classical bits. ([#1160](https://github.com/Qiskit/qiskit-terra/issues/1160))
    - Single classical bit conditioning breaks various functions. ([#6475](https://github.com/Qiskit/qiskit-terra/issues/6475))
        - Text, latex and MPL drawers break when drawing circuits that contain gates conditioned on single classical bits.
        - qc.depth() breaks on circuits that contain gates conditioned on single classical bits.
- Issues in visualization, testing and documentation.
    - Inconsistency in drawing classical control in text drawer when cregbundle=False. ([#6290](https://github.com/Qiskit/qiskit-terra/issues/6290))
    - The ordering of condition bullets are incorrect when cregbundle=True and reverse_bits=True. ([#6290](https://github.com/Qiskit/qiskit-terra/issues/6290))
    - Incorrect drawing of custom instructions involving classical bits when using text drawer. ([#6178](https://github.com/Qiskit/qiskit-terra/issues/6178))
    - Latex drawer support for complex custom instructions. ([#3006](https://github.com/Qiskit/qiskit-terra/issues/3006), [#3202](https://github.com/Qiskit/qiskit-terra/issues/3202))
    - Need to show active wires in multi-qubit gates drawn in latex. ([#2092](https://github.com/Qiskit/qiskit-terra/issues/2092))
    - MPL drawer support for complex custom instructions. ([#3006](https://github.com/Qiskit/qiskit-terra/issues/3006), [#3201](https://github.com/Qiskit/qiskit-terra/issues/3201))
    - Testing Latex drawer using binder. ([#6371](https://github.com/Qiskit/qiskit-terra/issues/6371))
    - Unroller raises unclear error when reaching a node without a definition. ([#5840](https://github.com/Qiskit/qiskit-terra/issues/5840))
