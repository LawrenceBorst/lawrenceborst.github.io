---
author: Lawrence Borst
excerpt_separator: <!--more-->
permalink: sums-of-powers
description: a formula for sums of powers
tags: [mathematics, sum, sigma, summation, powers, choose, combinations, combinatorics, number theory]
layout: post
---
In this post we will generalize a "geometric" approach to solving the problem of finding a closed form to

$$\sigma_{k}(n)=\sum_{i=0}^{n}i^k$$

The formula I'll derive is, as far as I'm aware after some . With keywords like "sums of powers, binomial coefficients, combinations", I haven't found anything similar except in the following paper by A.F. Beardon called "Sums of Powers of Integers". I by no means suspect my formula is in any way new. In any case, I hope that the intuition offered here will be vitalizing to the reader.

The problem, which to the best of my knowledge has no singular name, is a well-explored one. Many will have seen the following formula:

$$\sigma_{k}(n)=\frac{1}{k+1}\sum_{j=0}^{k}\begin{pmatrix}
k+1\\ 
j
\end{pmatrix}
B_{j}(n+1)^{k+1-j}$$

There are similar formulae involving the Bernoulli numbers $B_{j}$, which were defined specifically for this problem. They can be defined recursively as:

$$B_{0}=1$$

$$\sum_{j=0}^{m}\begin{pmatrix}
m+1 \\
j
\end{pmatrix}
B_{j}=0$$

We will take a different approach.
<!--more-->

<h2>The Geometric Approach for $\sigma_{1}(n)$ through $\sigma_{3}(n)$</h2>

We will return to middle school and think of numbers as blocks. In this case $\sigma_{1}(n)$ counts the number of blocks in a triangular stack of blocks. There's a famous anecdote about young Carl Friedrich Gauss in arithmetic class being challenged by the teacher to solve this very problem ($\sigma_{1}(100)$). No sooner after he was given this problem, he returned the answer: $5050$. This he derived by summing $50$ pairs of $101$ by appropriate grouping of the terms in the sum. 

Many use this as a testament to Gauss' early genius, which it certainly is. I, however, take the central message to be: "work smart, not hard".

Back to the problem at hand, we see that a similar grouping can be performed for general $n$—albeit there are two cases (even and odd $n$). In this way we see that $\sigma_{1}(n)=\frac{1}{2}n(n+1)=\begin{pmatrix}
n+1\\ 
2
\end{pmatrix}$.

So how do we get $\sigma_{2}(n)$? Well, what does $\sigma_{2}(n)$ signify in terms of blocks? It is a sum of squares... So a sum of geometrical squares. Could we move $k$ up the ladder to $k=2$ by using information about $\sigma_{1}(n)$, where $k=1$?

Well, if $\sigma_{1}(n)$ represents a right triangle of blocks, it's not hard to see how $2\sigma_{1}(n)$ approximates the number of blocks in a rectangle of length $n$ and height $n+1$.

Indeed, the reader will perhaps visualize $2\sigma_{1}(n)$ as two right triangles of blocks, with one rotated, to fill a rectangle of length $n$ and height $n+1$. This discussion lends itself better to visualizing $2\sigma_{1}(n)$ as a single square of length and height $n$ from two right triangles that overlap at the diagonal (so we overcount by $n$ blocks). Here's why:

$\sigma_{2}(n)$ is clearly the sum of squares of blocks. Each square is represented by $2\sigma_{1}(n)$, or $2$ right triangles of blocks, minus the overlap $n$ (a line of blocks). Therefore

$$\sigma_{2}(n)=\sum_{i=0}^{n}\sigma_{1}(i)-\sum_{i=0}^{n}i$$

That looks terribly complicated! Certainly the last sum is just $\sigma_{1}{n}$, but how about the first? Well, actually

$$\sum_{i=0}^{n}\begin{pmatrix}
i+1\\ 
2
\end{pmatrix}
=
\begin{pmatrix}
n+2\\ 
3
\end{pmatrix}$$

The reader should note that, in the above, the binomial coefficients on the left are very similar to those on the right, except on the right we've augmented top and bottom by $1$. One proof is simply this: the LHS represents a sum, and therefore the RHS is the cumulative value of that sum. Therefore to prove the equality above we require that $\begin{pmatrix}
n+2\\ 
3
\end{pmatrix}
-
\begin{pmatrix}
n+2-1\\ 
3
\end{pmatrix}
=
\begin{pmatrix}
n+1\\ 
2
\end{pmatrix}$. This is easily checked to be true. We also require that $\begin{pmatrix}
0+2\\ 
3
\end{pmatrix}
=
\begin{pmatrix}
0+1\\ 
2
\end{pmatrix}$. The first condition is simply saying that the difference of RHS terms for consecutive $n$ should equal the last term in the LHS sum for choice of $n$. The second condition is saying that the LHS and RHS "start" at the same spot for $n=0$.

This little trick can be used to prove the general case: for any positive $n$, $k$ (equation $1$):

$$\sum_{j=0}^{n}\begin{pmatrix}
j+k\\ 
1+k
\end{pmatrix}
=
\begin{pmatrix}
n+k+1\\ 
1+k+1
\end{pmatrix}$$

Equation $1$ will be integral to our discussion.

Returning to $\sigma_{2}(n)$. It is clear now that
$$\sigma_{2}(n)
=
2\begin{pmatrix}
n+2\\ 
3
\end{pmatrix}
-
\begin{pmatrix}
n+1\\ 
2
\end{pmatrix}$$

To recapitulate, the first term represents the sum of right triangles made of blocks. The minus part takes away the overlap.

Now, on to $\sigma_{3}(n)$. Can we do something similar? Let's see, $\sigma_{3}(n)$ represents a sum of cubes. How can we make cubes from whatever $\sigma_{2}(n)$ represents? Well, let's see what $\sigma_{2}(n)$ represents. It is a sum of squares; summing gives a pyramid, analoguous to the right triangle we've associated with $\sigma_{1}(n)$.

So can we make cubes from pyramids? Certainly we can, and this picture shows how:

PICTURE WILL BE ADDED

But we should note that our pyramids are blocky. This causes overlap, and I'll describe exactly the overlap:

- We have three pyramids.
- $3$ sides are overlapping (two pyramids overlap).
- There is exactly $1$ block where all three pyramids overlap.

Great. Now, let's translate this to $\sigma_{3}(n)$. Here are we taking sums of cubes. Each cube will consist of these pyramid, but we will have to do something analoguous to inclusion-exclusion. We will remove the overlap across the pyramids. But we will add back the block we accidentally remove. This gives equation (2):

$$\sigma_{3}(n)=3\sum_{i=0}^{n}\sigma_{2}(i)-3\sum_{i=0}^{n}\sigma_{1}(i)+\sum_{i=0}^{n}\sigma_{0}(i)$$

It might become clear to some reasons what might be happening: $\sum_{i=0}^{n}\sigma_{k}(i)$ represents a kind of $k+1$-dimensional simplex with a right angle in it.

We shall use equation $(1)$ to sum each of these components. Something remarkable happens (because of equation $(1)$); we get to use our expressions for $\sigma_{k}(n)$, except we need only augment the terms in the expression by $1$! Therefore:

$$\sigma_{3}(n)=3\left ( 2\binom{n+3}{4}-\binom{n+2}{3} \right )-3\binom{n+2}{3}+\binom{n+1}{2}$$

How do we quickly check this to be true? Armed with the common knowledge that the LHS is a polynomial of degree $3+1=4$, and so is the RHS (clearly), it is clear we only need to check $3$ values of $n$ (3 points). This would make both the LHS and RHS the unique interpolating polynomial for those $3$ points.

Will this generalize to higher dimensions? Maybe. But how?

I can't speak exactly for what happens in higher dimensions, but squinting our eyes at equation (2), or other similar expressions we obtained for $\sigma_{1}(n)$, $\sigma_{2}(n)$, $\sigma_{3}(n)$ we see the familiar entries in Pascal's triangle as coefficients. It seems, in general, that:

$$\sigma_{k+1}(n)=\sum_{i=0}^{n-1} (-1)^{i + n + 1} \binom{k}{i} \sum_{j=0}^{n} \sigma_{i}(j)$$

Remember that to evaluate $\sum_{j=1}^{n} \sigma_{k}(j)$ we simply augment the upper and lower part of the binomial coefficients appearing in the expression by $1$, making $\sigma_{k+1}(n)$ not all that difficult to produce inductively.

For instance:

$$\sigma_{4}(n)=4 \left ( 3 \left ( 2 \binom{n+4}{5} - \binom{n+3}{4} \right ) - 3 \binom{n+3}{4} + 2 \binom{n+2}{3} \right ) - 6 \left ( 2 \binom{n+3}{4} - \binom{n+2}{3} \right ) + 4 \binom{n+2}{3} - \binom{n+1}{2}$$

With my limited experience I can only make a guess as to what's happening. The binomial coefficients $(-1)^{i+n+1} \binom{k}{i}$ appear as part of a inclusion-exclusion-like expression, and indeed we have seen that in our block-based geometric approach we are kind of overshooting and undershooting the count of blocks. Exactly what is the nature of this overshooting and undershooting? It seems that our $n$-dimensional cube can be made up of $n$ $n$-simplices with a right corner. It's also clear that overshooting or undershooting can only occur at the boundary of the simplex. So let's say we want to compute the number of blocks in an $n$-dimensional cube based on these simplices. As a first approximation, it is simply $n$ times the number of simplices, which we recognize as $\sigma_{n}{N}$, where $N$ represents the "length" or so of the simplex. But we overcount where the boundaries intersect. The boundary of any $n$-dimensional simplex is made up of an $n-1$-dimensional simplex. Let's say, for simplicity, this boundary consists of $n-1$-dimensional "edges". Then our overcount will be the number of blocks over the $n-1$-dimensional "edges" of our $n$-simplices. As a first approximation, this equals the number of blocks on a given such "edge" times the number of such "edges". Guessing that all the $n$-simplices touch each other, it follows that all these "edges" occur exactly where $2$ intersect $n$-simplices intersect. Since there are $n$ $n$-simplices, the number of $n-1$-dimensional "edges" is $\binom{n}{n-2}$. Now we undercount for the boundary of each "edge", and so we go down another dimension, looking at $n-2$-dimensional "edges". In this case $3$ $n$-simplices intersect to form such an "edge", and the number of them is $\binom{n-3}{3}$. You get the gist. This is the intuition I have.

To be continued...