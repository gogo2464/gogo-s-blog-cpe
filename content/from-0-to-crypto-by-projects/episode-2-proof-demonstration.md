---
title: "Episode 2: Reversing cryptography algorithm made to be unreversable (checksum). Method by mathematical proof: disproof"
date: 2024-10-13T1:25:30+02:00
weight: 2
draft: false
---

## I - Identify

According to the documentation and as it is mentionned that type 7 is an hashing algorithm.

A secure hash algorithm is an hash algorithm so that for any function hash that transform the original (plaintext) value $ hased = H(plain) $ there does not exist a function $ rev(hashed) $ so that $ rev(hashed) = plain $. 

## II - Notes:

I really definitely insist on this point: `It is crucial for a cryptologist to PROOVE his statement. Not just calculating.` If you only calculate, you could reach some proprietary algorithms such as this one but you will never ever be able to code CVE exploits on modern algorithms. I insist in the point you have to read [book fo proof](https://www.people.vcu.edu/~rhammack/BookOfProof/Main.pdf) if you did not do it yet. It is to do theorem proving.

## III - Analysis under mathematical thinking

The reverse engineering of the hash of vigenere cisco has permitted to deduct the method taken by this algorithm.

We could then guess that the researchers thanks then that:

![image](/gogo-s-blog-cpe/from-0-to-crypto-by-projects/episode-2-proof-demonstration/theory-behind-type7-hash.png)

The question is to proove that there exists a function $ rev(hashed) $ so that $ \forall plain [rev(H(plain)) = plain] $ then $ \forall x [x = H(plain)] $


## IV/ 1- solving the theorem finding a way to proove the case.

There are a lot of different method to proove a theorem. You could pick the one you prefer or the one you find easier.

The big picture is to split the proof into several cases. 

There a serveral various operations including:
- splitting number between 0 and 256 to two differnt more little number (the shift: $ \ggg $ and the logical and: $ \land 0xf0 $ ). Reversable by mergingtwo numbers in a single one with same algortihm.
- adding. You could simply substract to reverse.
- doing an boolean exclusive logical or to a known password. 
  -  as each number exclusively logically set to logical or (xored) with itself has the final value of 0 and as 0 set to logical or with another number will return this number, ![image](/gogo-s-blog-cpe/from-0-to-crypto-by-projects/episode-2-proof-demonstration/reversing-exclusive-or.png) it follows that logically set to logical or to the hardcoded password one time will change the values but logically set to logical or a second time to the same hardcoded value will change it to the original value. See [boolean algebra](https://en.wikipedia.org/wiki/Exclusive_or#Definition), and see this schems provided with the tool name `cryptool-2`.

All of these are reversables.

Then I decide to choose a proof in the form: as $ A \implies B \implies C $, then $ A \implies C $.

Let's check it out that [in this paper]( /gogo-s-blog-cpe/from-0-to-crypto-by-projects/episode-2-proof-demonstration/latex-reverse-type7.pdf )!