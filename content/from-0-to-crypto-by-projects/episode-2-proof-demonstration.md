---
title: "Episode 2: proof and logic, demonstration of disprooving vigenere cisco maths"
date: 2024-10-13T1:25:30+02:00
weight: 2
draft: false
---

## III - Reversing checksum, Méthod by mathematical proof: disproof

## 1 - Analyse sous forme de logique mathématique

Si nous n'avions pas eu le code de comparaison dans packet tracer, nous aurions néanmoins pu procéder à la cryptanalyse de l'algorithme de hachage à sens unique. Ici nous avons la chance de posséder l'algorithme d'inversion. Nous allons donc en profiter afin de nous aider pour concevoir les fondamentaux théoriques derrière l'inversion de la somme de hachage.

Afin de voir ce que nous avons voulu démontrer en latex, vous pouvez compiler la démonstration avec les commandes:

```
sudo apt install -y texlive-latex-recommended texlive-latex-extra
pdflatex maths-PT-decompilation.tex
```

Le reverse engineering de l'algorithme de hachage vigenere cisco a permit de déduire l'algorithme utilisé par cet algorithme. Etant donné qu'il s'agit d'un algorithme de hachage, nous pouvons deviner que les concepteurs pensaient que:

donc:

```math
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

$ \forall h \forall lp \forall hp [hp = "dsfd;kfoA,.iyewrkldJKDHSUBsgvca69834ncxv", \\
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