---
title: "Episode 2: Reversing cryptography algorithm made to be unreversables (checksum). Method by mathematical proof: disproof"
date: 2024-10-13T1:25:30+02:00
weight: 2
draft: false
---

## I - Identify

According to the documentation and as it is mentionned that type 7 is an hashing algorithm.

A secure hash algorithm is an hash algorithm so that for any function hash that transform the original (plaintext) value $ hased = H(plain) $ there does not exist a function $ rev(hashed) $ so that $ rev(hashed) = plain $. 

## 1 - Analysis under mathematical thinking


The reverse engineering of the hash of vigenere cisco has permitted to deduct the method taken by this algorithm.

We could then guess that the researchers thanks then that:

![image](/gogo-s-blog-cpe/from-0-to-crypto-by-projects/episode-2-proof-demonstration/theory-behind-type7-hash.png)

The question is to proove that there exists a function $ rev(hashed) $ so that $ \forall plain [rev(H(plain)) = plain] $ then $ \forall x [x = H(plain)]$


We intuitevely see points to split the issue into easier pieces:

- the algorithm threat data block by blocks with blocks of two opcodes (numbers between 0 and 256) knowns bigram.

The algorith treat bigrams as following:

- the two opcodes are both xored to the hardcoded password.






We now have the mathematical proof (demonstration) that the algorithm is vulnerable [in this paper]( /gogo-s-blog-cpe/from-0-to-crypto-by-projects/episode-2-proof-demonstration/latex-reverse-type7.pdf ).