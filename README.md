# Good First Issues in Qiskit Terra - Qiskit Advocate Mentorship 2021
We present here a detailed report on the work that was done in the Qiskit advocate mentorship project titled "Good First Issues in Qiskit Terra". The project was under the mentoring of Dr.Luciano Bello.

### Goal of the project
The goal of this project was to fix good first GitHub issues of Qiskit Terra.

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

Below, we provide more details on the issues we worked to fix.

### 1. Classical conditioning of gates on single bits
Our primary aim of this sub-project was to introduce the feature that enables users to condition gates on individual classical bits. The main challenge was to introduce this feature while also ensuring that the number of functions that break due to this addition is minimal. We managed to make this addition while breaking a handful of functions. The functions that were broken are mentioned in [#6475](https://github.com/Qiskit/qiskit-terra/issues/6475) and are as follows:
- All the drawers break when trying to draw a circuit that contains gates with classical conditioning on a single cbit.
- ```qc.qasm()``` breaks when circuit qc contains gates with classical conditioning on a single cbit.
- ```qc.depth()``` also breaks.
- ```disassemble(qc_assembled)``` breaks where ```qc_assembled``` is an assembled ```Qobj```.
- ```qc.num_connected_components``` breaks.
- ```circuit_to_instruction(qc)``` breaks.
- ```_check_wires_list()``` and ```substitute_node_with_dag()``` methods in ```qiskit/dagcircuit/dagcircuit.py``` break.
- ```_is_same_c_conf()``` method in ```ForwardMatch``` and ```BackwardMatch``` classes in ```qiskit/transpiler/passes/optimization/template_matching``` breaks.
- ```run()``` method in ```ConsolidateBlocks``` class in ```qiskit/transpiler/passes/optimization``` breaks.
By the end of the project, we fixed all three drawers ([#6261](https://github.com/Qiskit/qiskit-terra/pull/6261), [#6248](https://github.com/Qiskit/qiskit-terra/pull/6248), [#6259](https://github.com/Qiskit/qiskit-terra/pull/6259)) and the ```qc.depth()``` function ([#6476](https://github.com/Qiskit/qiskit-terra/pull/6476)). As for the other issues, we are actively working on fixing them.

On introducing this feature, the users can now condition gates on classical bits. As an example, Qiskit terra now supports conditioning gates like as below:
```python
q = QuantumRegister(3)
c = ClassicalRegister(2)
circuit = QuantumCircuit(q,c)
circuit.h(q[0])
circuit.measure(q[0], c[0])
circuit.h(q[1]).c_if(c[0], True)
circuit.h(q[2]).c_if(c[0], 1)
```

We also worked on enabling this feature on registerless circuits.

### 2. Issues in visualizion, testing and documentation.
In visualization, testing and documentation, we worked on various relatively independent issues, although we focused more on the issues relating to bugs in visualization. For most of the issues, we only neede to do some addition and/or modification of code in their corresponding classes.

#### 2.1 Issues related to text drawer
We worked on and fixed three issues that related to the text drawer. The first issue ([#6290](https://github.com/Qiskit/qiskit-terra/pull/6290)) was that the text drawings of the classical conditions when ```cregbundle``` was set to ```False``` was inconsistent with the other two drawers. While the latex and MPL drawers drew classical control as bullets, they were drawn as boxes in the text drawer. While resolving this issue, we found a related issue in the text drawer that when ```cregbundle``` is set to ```False``` and ```reverse_bits``` is set to ```True```, the ordering of the bullets of classical conditions were incorrect. We fixed these bugs in [#6370](https://github.com/Qiskit/qiskit-terra/issues/6370).
We also fixed an issue of text drawer ([#6178](https://github.com/Qiskit/qiskit-terra/pull/6178)) in which when custom instructions are added to a circuit using arbitrary qubit and classical bit inputs, the drawer drew them incorrectly. This issue was fixed in [#6242](https://github.com/Qiskit/qiskit-terra/pull/6242).

#### 2.2 Issues related to MPL drawer
As for the issues in MPL drawer, we fixed an issue of drawer incorrectly drawing custom instructions that involved classical bits ([#3006](https://github.com/Qiskit/qiskit-terra/issues/3006), [#3201](https://github.com/Qiskit/qiskit-terra/issues/3201)). The drawer drew the gate boxes only over the qubits, ignoring the involvement of classical bits. This issue was fixed in [#6339](https://github.com/Qiskit/qiskit-terra/pull/6339).

#### 2.3 Issues related to latex drawer
Similar to the issue fixed in the MPL drawer, the latex drawer also incorrectly drew custom instructions that involved classical bits ([#3006](https://github.com/Qiskit/qiskit-terra/issues/3006), [#3202](https://github.com/Qiskit/qiskit-terra/issues/3202)). In this case too, the drawer ignored the classical bits of the custom instructions. In [#6240](https://github.com/Qiskit/qiskit-terra/pull/6240), we fixed this issue following similar style of the fix of MPL drawer.
One other issue on latex drawer we worked on was the issue of missing active wire numberings ([#2092](https://github.com/Qiskit/qiskit-terra/issues/2092)). While the text and MPL drawers, numbered the active wires of a custom instruction, this was missing in the latex drawer. So we added numbering of active wires in latex drawer in [#6153](https://github.com/Qiskit/qiskit-terra/pull/6153).

#### 2.4 Testing and documentation
As far as the testing is concerned, apart from fixing the above issues, we also added various test to avoid unwanted effects on the fixed elements due to changes in code at a later point of time.
Along with this, we also tried to port the latex text to a binder setup. Currently, the latex tests are performed by first generating the latex source code and then verifying it with the reference code. However, it is hard to detect visual irregularities if any. So, we worked on performing latex tests in binder, similar to how the current MPL drawer tests are performed ([#4544](https://github.com/Qiskit/qiskit-terra/pull/4544)). We were able to do the same in [#6450](https://github.com/Qiskit/qiskit-terra/pull/6450). This now allows for a more visual way of testing.
We also worked on a small documentation issue in which an unclear message was output when an unroller reaches a node with no definition ([#5840](https://github.com/Qiskit/qiskit-terra/issues/5840)). The fix was simple ([6235](https://github.com/Qiskit/qiskit-terra/pull/6235)). We updated the method to output an error message that is more comprehensible to the user.

### Project statistics
We present here some statistics of our project that we found to be interesting.
- Total number of issues addressed and/or closed : 15
- Total number of new issues created : 5
- Total number of completed PRs made during this time : 15
    - Number of PRs that were merged       : 9
    - Number of PRs in the review pipeline : 6
- Month of opening of the oldest issue we worked on : Oct 2018 (Pretty old!)
- Month of opening of the latest issue we worked on : May 2021

The link to a short recording in which we explain the details of this project more visually can be found [here](https://github.com/TharrmashasthaPV/Good-First-Issues-in-Qiskit-Terra/blob/main/Good%20First%20Issues%20in%20Qiskit%20Terra%20-%20Presentation.avi) and the slides used in the recording can be found [here](https://github.com/TharrmashasthaPV/Good-First-Issues-in-Qiskit-Terra/blob/main/Good%20First%20Issues%20in%20Qiskit%20Terra%20-%20Slides.pdf).
Even though the project has come to an end, the project has ensured that my contributions to the Qiskit community woud hardly cease.

#### Acknowledgements
I learnt a varied lot of things in the duration of this project, ranging from the written norms of python to unwritten courtesies of the open source community. Working on this project with Lucianno was a lot of fun and equally educational. His mentoring thoughout the project was amazing. A big thanks to Luciano for all his support. I would also like to thank Kevin Krushlin for his support in the classical conditioning sub-project and would like to thank Edwin Navarro for helping me in fixes relating to the drawers.
