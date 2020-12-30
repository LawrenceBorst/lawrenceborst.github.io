---
author: Lawrence Borst
excerpt_separator: <!--more-->
permalink: quantum-computing-an-introduction
description: an introduction to quantum computation
tags: [quantum, computation, computing, qubits, introduction]
layout: post
---
During the past few months, I've been reading on quantum computation. For simplicity, I've listed all the resources in the bibliography for the ease of the reader. I strongly recommend to others who wish to learn about quantum computing to start with <a style="color:blue;" href="https://www.amazon.com/Quantum-Computing-Computer-Scientists-Yanofsky/dp/0521879965" target="_blank" rel="noopener noreferer">Quantum Computing for Computer Scientists</a> and just skim through it. This is a slightly dumbed-down approach to quantum computing, but very practical nonetheless. Going through it will equip you with all the knowledge you'd need to make your own quantum computinng emulator, assuming you know a little programming. The next best thing is the quantum bible <a style="color:blue;" href="https://www.amazon.com/Quantum-Computation-Information-10th-Anniversary/dp/1107002176" target="_blank" rel="noopener noreferer">Quantum Computation and Quantum Information</a>, which is more challenging but gives you a more grounded understanding of quantum computation, as well as some of the physics behind it. Besides those resources, I recommend anyone interest in quantum computation to play with <a style="color: blue;" href="https://qiskit.org/" target="_blank" rel="noopener noreferer">Qiskit</a>-a quantum emulator-and to read through its documentation. The stack exchange for quantum computation is also a useful resource.

In this introductory article, I hope to lay out the groundworks for any beginner in the manner that these sources describe. I hope this will pique the interest of someone who may have heard of quantum computing, but has no clue what it really entails.

<!--more-->

<h2>The Quantum Circuit Model</h2>

We begin with some intuition as to what a quantum computer is. Like a classical computer, we expect that quantum computers have registers which store the quantum-equivalent of bits. These quantum registers store qubits. And like a classical computer, which are simulated by the tried-and-tested circuit model of computation, we expect quantum computers to be implemented in the same way.

To get slightly more abstract, this fancy circuit model is really a model of computation equivalent to the Turing model. It is equivalent in the sense that any circuit can simulate an arbitrary Turing machine (a computer running on the rules the turing model prescribes to), and vice versa. The usefulness of the circuit model then follows from the usefulness of the turing model by the Church Turing Thesis.

**Church Turing Thesis:** Every effectively calculable function is a computable function.

According to Turing, "effectively calculable" refers to the "intuitive idea" of a function that can be calculated by any means. A computable function is one that can be computed on a turing machine-that is, if $f(x)$ is defined, then a turing machine given an input $x$ (encoded to fit the model, that is) will halt with $f(x)$ stored in memory; furthermore, if undefined, the turing machine will not run forever.

All these details are not too crucial for a starter, except it is true that an important aim in quantum computation is to show that quantum computers can theoretically perform the same feats as classical computers. This can be effectively showed by showing that the quantum circuit model (the one used by a quantum computer) is equivalent to the classical circuit model. This is indeed the case. This means that classical computers can effectively simulate quantum computers, proving that our emulators can indeed work. It is interesting to note that quantum turing machines are a thing, but likely lost to the quantum circuit model in the same way that classical turing machines lost the classical model; namely for being less practical. The circuit models more realistically encapsulate computers we can build.

As we know from a classical computer, once we have our bits in a register we can perform operations on them. In particular, we apply binary functions to our (generally 64-bit) registers. So a single register can be ascribed completely to a point in ${0, 1}^{64}$, and can represent $2^{64}$ "states" as it were. Mathematically, we would call ${0, 1}^{64}$ the state space. That's a lot of states. A register, as it were, holds some finite amount of information. A quantum register also holds information. In theory, it holds an infinite amount of information, although in practice the information we can observe is the strictly finite $2^{64}$ states. The hidden information that we can play with, however, is much larger, and can be represented by a set of real numbers between $-1$ and $1$ in a space of a whopping $2^{(2^{63})}$ dimensions! Not only that, but unlike classical registers, the individual qubits can be entangled, thus storing information in the form of relationships between the qubits. In quantum computing, it is primarily this information which we manipulate. Not all applications can necessarily be implemented in a way that exploits this entanglement, because it still abides by certain rules. We therefore don't expect a quantum computer to be some magic machine that speeds up all problems. But it has been shown to be asymptotically faster-sometimes exponentially so-on a subset of problems.

According to Quantum Computation and Quantum Information listed below, a quantum computer has the following components:

**Classical resources:** a classical part. Because quantum computers cannot practically speed up all problems, and can even be ill-suited for some, it is useful to have a classical part. We allocate a process to the part which is best suited for it. For storing and reading information into and from the quantum computer, we would use a classical machine. Moreover, we might use a quantum computer only for certain subroutines in the case of more complex processes.

**A suitable state space:** as said, quantum computers will act on some number $n$ of qubits. The state space is a $2^{n}$-dimensional complex Hilbert space in which the state of the system lives. This state encodes all the qubits.

**The ability to prepare states in the computational basis:** the computational basis is a basis in which each individual qubit starts out in the same basis, and the total system is represented by the tensor product of these states; we'll so more closely what this entails. 

**Ability to perform quantum gates:** because we fundamentally choose a quantum circuit model we expect to be able to use quantum gates on individual qubits, as well as sets of qubits. This is analoguous to being able to apply gates to bits, which are binary functions on their states. We'll see that for qubits we'll be using unitary operators instead. It is also mentioned that a universal set of gates should be implemented. These are gates whose representation as operators can be combined (multiplied) in a way that can arbitrarily approximate any unitary operator. In simple terms, these are gates that can pretty much implement any function we want on qubits.

**Ability to perform measurements in the computational basis:** we most certainly want to run algorithms on quantum computers and measure their output. This output would be meaningless if we do not agree on a specific encoding of the information, which we naturally choose to be the defined through the computational basis.

<h2>Quantum Circuits as Graphs</h2>
As a pedagogical tool, we'll use graphs analoguous to quantum circuits to explore the concept of quantum gates, and how they differ from classical gates. The reader may recognise the use of markov processes to explain quantum circuits.

Let us imagine that instead of qubits, our circuits simply acts on the vertices of a graph. That is, the vertices encode the state of the system. At each vertex we'll have a number, let's say a number of marbles. The edges of the graph, which are directed so have a well-defined "start" and an "end", represent some edge-specific probability $p$ of any marbles in the "start" vertex $V_{s}$ to jump to the "end" vertex $V_{e}$. We expect that if $V_{s}$ holds $n$ marbles, $pn$ marbles will jump to $V_{e}$. But of course, this system is complicated, and marbles from $V_{e}$ maybe travel back to $V_{s}$ if there is some way to reach it. Furthermore, the expected number of marbles that cross the edge will change with time, because the expected number of marbles held at any given vertex changes. That is, this system has "dynamics". That is, the state of the system evolves from time $t$ to $t+dt$ in some well-defined manner. We need a way to describe the dynamics. If we encode the state described by $V_{1},...,V_{n}$ as $\psi(0)=\\left [ n_{1},...,n_{n} \\right ]$, where $n_{i}$ is the number of marbles at $V_{i}$, then the state evolves as:

$$\psi(t+dt)=U\psi(t)$$

Where $U$ is some linear function on $\mathbb{R}^{n}$. Now, since we are talking about probabilities, we cannot expect $U$ to tell us precisely what state $\psi$ will be in after some time $dt$, because everytime we run the same simulation we would expect a slightly different outcome. Instead, $U$ will be used to encode the state we expect $\psi$ to enter; that is, the most likely state after some time.

(To be continued)
