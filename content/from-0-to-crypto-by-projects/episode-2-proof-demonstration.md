---
title: "Episode 2: proof and logic, demonstration of disprooving vigenere cisco maths"
date: 2024-10-13T1:25:30+02:00
weight: 2
draft: false
---

## III - Reversing checksum, Method by mathematical proof: disproof

According to the documentation and as it is mentionned that type 7 is an hashing algorithm.

A secure hash algorithm is an hash algorithm so that there does not exist a function `f(enc)` so that `f(enc) = original_plaintext`. 

## 1 - Analysis under mathematical thinking


The reverse engineering of the hash of vigenere cisco has permitted to deduct the method taken by this algorithm.

We could then guess that the researchers thanks then that:

```latex
\documentclass{article}
\usepackage{amsmath}
\usepackage{mathtools, nccmath}
\usepackage{amssymb, amsthm, mathrsfs}
\begin{document}
According to the decompilation of the Ciso Vigenere hash algorithm, when the password length is less than 16 the idea behind Ciso Vigenere hash algorithm is: \\
Let p be the password that the user types. \\
Let hp be the hardcoded password in the code of Packet Tracer. \\
Let lp be the length of the user input password. \\
Let h be the hash value obtained from the custom algorithm. \\
So that:

$ \forall h \forall lp \forall hp [hp = (d, s, f, d, ;, k, f, o, A, ,, ., i, y, e, w, r, k, l, d, J, K, D, H, S, U, B, s, g, v, c, a, 6, 9, 8, 3, 4, n, c, x , v), \\
0 < lp < 16, \\
h_{0} = 0, \\
h_{1} = 8, \\
h = \Sigma_{i=2}^{lp}
\begin{cases}
    ((p_i \oplus hp_{8 + i}) \gg 4) + 0x30,                                   & \text{if } (p_{i} \oplus hp_{i+8} \land 0xfffffff0 < 0xa0)        \text{ and if } i \equiv 0 \pmod 2 \\
    ((p_i \oplus hp_{8 + i}) \gg 4) + 0x37,                                   & \text{if } (p_{i} \oplus hp_{i+8} \land 0xfffffff0 \geq 0xa0)     \text{ and if } i \equiv 0 \pmod 2 \\
    ((p_i \oplus hp_{8 + i}) \land 0xf) + 0x30,                               & \text{if } (p_{i} \oplus hp_{i+8} \land 0xf < 0x0a)               \text{ and if } i \equiv 1 \pmod 2 \\
    ((p_i \oplus hp_{8 + i}) \land 0xf) + 0x37,                               & \text{if } (p_{i} \oplus hp_{i+8} \land 0xf \geq 0x0a)            \text{ and if } i \equiv 1 \pmod 2
\end{cases} \\
] \implies \nexists p[p = \mathbf{rev}(h)] $ \\


\end{document}
```
.

We now have the mathematical proof (demonstration) that the algorithm is vulnerable.