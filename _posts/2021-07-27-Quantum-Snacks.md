---
layout: post
title:  "Hacky Holidays - Space Race: Quantum Snacks"
tag: [quantum]
usemathjax: True
---

# Challenge Information

Computers speak the language of binary (zeros and ones), and every computer program is basically just applying logic gates (e.g NOT, OR, AND, XOR etc) to these bit to get a desired outcome. The important point here is to remember that a bit is a single variable that can have one of 2 values, either zero or one).

Quantum computers speak a very different language. Instead of a bit we have a qubit (quantum bit), which can be represented as a two-dimensional vector. Classical bit 0 is equivalent to the qubit 
$$
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$,
and the classical bit 1 is equivalent to the qubit 
$$
    \begin{pmatrix}
    0\\
    1\\
    \end{pmatrix}
$$,
but there are many other qubit states that do not have a classical equivalence, which means that qubits can store much more information than classical bits. The goal of this challenge is to understand this concept better.

To change the state of a (q)bit we apply logic gates to it. In quantum computing logic gates are represented as matrices, and the outcome of this operation can be calculated by multiplying the logic gate (a matrix) with the initial qubit state (a vector). Mathematically it looks like this:
$$
    \begin{pmatrix}
    a & b \\
    c & d \\
    \end{pmatrix}
$$
$$
    \begin{pmatrix}
    a & b \\
    c & d \\
    \end{pmatrix}
$$
$$=$$
$$
    \begin{pmatrix}
    ax_1 + bx_2 \\
    cx_1 + dx_1 \\
    \end{pmatrix}
$$

In this challenge we limit ourselves to three 1-qubit logic gates:

$$
X = \begin{pmatrix}
    0 & 1 \\
    1 & 0 \\
    \end{pmatrix}
$$


$$
Z = \begin{pmatrix}
    1 & 0\\
    0 & -1\\
    \end{pmatrix}
$$


$$
H = \frac{1}{\sqrt2}
    \begin{pmatrix}
    1 & 1\\
    1 & -1\\
    \end{pmatrix}
$$

Note: in practice there are more logic gates that result in an infinite possible quantum states. Because we are only considering 3 specific logic gates then the number of states is finite.



### [50 points] Question 1: How many states?
Considering only these 3 logic gates, and starting in the
$$
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$
state, how many states can the qubit have?  
Hint: Start applying the logic gates in random order. Drawing the result in x-y coordinates will greatly help you understand the result.

---

# Introduction: Part 1

A tl;dr summary of the challenge information:

1. There are 3 logic gates: `X`, `Z` and `H`.
2. Each logic gate has a 2x2 vector tied to it
3. All states are represented by a 1x2 vector
4. Passing a state through a logic gate, states may or may not change
5. To determine if states change when passed through the logic gate, we multiply the logic gate vector with the state vector

As a disclaimer: I hate math. So, in the spirit of taking the easy way out, I found [a website](https://matrixcalc.org/en/) that can do the math for me!

---

# Solving the challenge: Part 1

Playing around with the logic gates, here's what I found. In plain English:

- `X` flips the top vector to the bottom vector
- `Z` flips the sign of the bottom vector

Now for the challenging part, `H`

Since `H` is tricky mathematics, here's how I simplified it: I assume that $$\frac{1}{\sqrt2}$$ equal to a variable `a`. From there, I calculate the result of passing something through `H` logic gate. From this, I see an interesting pattern.

If I pass
$$
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$
through `H` repeatedly:

1. I get
$$
    \begin{pmatrix}
    a\\
    a\\
    \end{pmatrix}
$$
2. Next, I get
$$
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$
3. Next, I get
$$
    \begin{pmatrix}
    a\\
    a\\
    \end{pmatrix}
$$
ad infinitum

If I pass:
$$
    \begin{pmatrix}
    0\\
    1\\
    \end{pmatrix}
$$ through `H` repeatedly

1. I get
$$
    \begin{pmatrix}
    a\\
    -a\\
    \end{pmatrix}
$$
2. Next, I get
$$
    \begin{pmatrix}
    0\\
    1\\
    \end{pmatrix}
$$
3. Next, I get
$$
    \begin{pmatrix}
    a\\
    -a\\
    \end{pmatrix}
$$ ad infinitum

If I pass
$$
    \begin{pmatrix}
    0\\
    -1\\
    \end{pmatrix}
$$ through `H` repeatedly:

1. I get
$$
    \begin{pmatrix}
    -a\\
    a\\
    \end{pmatrix}
$$
2. Next, I get
$$
    \begin{pmatrix}
    0\\
    -1\\
    \end{pmatrix}
$$
3. Next, I get
$$
    \begin{pmatrix}
    -a\\
    a\\
    \end{pmatrix}
$$
ad infinitum

What all this is telling me is, there is an upper limit to the number of states each vector can take. So far, I have only seen the following values:  
$$\begin{pmatrix}-a, & a, & -1, & 1, & 0\end{pmatrix}$$  

Mathematically, if there are 2 coordinates, and 5 possible values that these vectors can take, that means that the upper limit is 25 permutations.\
Drawing out the possibilities on a 5x5 grid and crossing out impossible permutations, I got 8 possible states.

Flag: `8`

---

# Question 2: Make a circuit [50 points]

Provide a circuit (a series of operations) that transforms the
$$
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$
state to the
$$
    \begin{pmatrix}
    -1\\
    0\\
    \end{pmatrix}
$$
state, only using the `H` and `X` operations. A possible (wrong) answer is `HHXHXHXH`.

---

# Solving the challenge: Part 2

Hey! looks like explaining the logic gates in simple English was a good thing. Now, this should be easy to figure out.

A refresher:
1. `X` flips the top vector to the bottom vector.
2. `H`, well, it's a little difficult to describe what H does. Best refer to my diagram above.

Now, to solve this challenge:

- `Start vector`
$$
    =
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$
- `X`
$$
    =
    \begin{pmatrix}
    0\\
    1\\
    \end{pmatrix}
$$
- `XH`
$$
    =
    \begin{pmatrix}
    a\\
    -a\\
    \end{pmatrix}
$$
- `XHX`
$$
    =
    \begin{pmatrix}
    -a\\
    a\\
    \end{pmatrix}
$$
- `XHXH`
$$
    =
    \begin{pmatrix}
    0\\
    -1\\
    \end{pmatrix}
$$
- `XHXHX`
$$
    =
    \begin{pmatrix}
    -1\\
    0\\
    \end{pmatrix}
$$

Got the flag!

Flag: `CTF{quantum_circuit_master}`

---

# Question 3: Short circuit [50 points]

Same as question 2 but now provide the shortest circuit possible (minimal number of gates). You are allowed to use `H`, `X` and `Z`.

---

# Solving the challenge: Part 3

Great! This looks simple enough:

- `Start vector`
$$
    =
    \begin{pmatrix}
    1\\
    0\\
    \end{pmatrix}
$$
- `X`
$$
    =
    \begin{pmatrix}
    0\\
    1\\
    \end{pmatrix}
$$
- `XZ`
$$
    =
    \begin{pmatrix}
    0\\
    -1\\
    \end{pmatrix}
$$
- `XZX`
$$
    =
    \begin{pmatrix}
    -1\\
    0\\
    \end{pmatrix}
$$

Flag: `XZX`
