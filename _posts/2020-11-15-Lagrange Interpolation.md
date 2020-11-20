---
layout: post
author: Lawrence Borst
---
To launch this website, let's begin with the simple but elegant idea of Lagrange interpolation.

The aim is to find a polynomial of degree $n$ that passes through $n-1$ points. People educated in linear algebra often can see that this is possible just by setting up the associated system of linear equations. For completeness:

If $P(x)=a_{0}+a_{1}x+\cdots+a_{n}x^{n}$ and $P(x_{0})=y_{0}$, $P(x_{1})=y_{1}$,$\cdots$,$P(x_{n-1})=y_{n-1}$ then we have the following system:

$$y_{0}=a_{0}+a_{1}x_{0}+\cdots+a_{n}x_{0}^{n}$$

$$y_{1}=a_{0}+a_{1}x_{1}+\cdots+a_{n}x_{1}^{n}$$

$$\vdots$$

$$y_{n-1}=a_{0}+a_{1}x_{n-1}+\cdots+a_{n}x_{n-1}^{n}$$

$n$ unknowns and $n$ equations. This we know is solveable. You can solve this by hand for a few points—and a computer will have no trouble with thousands of points—but our aim is to find a closed-form formula for the interpolating polynomial. Looking at this set of equations might not get us anywhere close to solving this problem.

Instead of revealing the trick, I encourage the reader to think about the problem. A good line of reasoning is something like this: "The main difficulty is that when you assume a function $P(x)$ and tweak the coefficients to fit through some point, the polynomial will inevitably slip away from other points." It is a bit like trying to get rid of a crease on your bedsheets; flattening one part will cause a pinch to pop up elsewhere. So then we might ask ourselves: "Is there a way to treat an individual point without disturbing the rest?"

Well, consider one of the points we're trying to pass through. If we can associate a polynomial (which is what the question is about) with an individual point that's "nice" in a way that "does not disturb the others", we would need a total of $n$ polynomials to address all points. Every polynomial should act in a similar way to its associated point, because no point is "special". So something should be quite "natural" about this polynomial. It should pass through a point, and as for the others... Well, be equal to $0$ at the others (can you think of anything else?). This is quite a natural thing to do with the other points, and as it turns out, it is easy to find the associated polynomial. Promising.

Let's say $P_{i}(x)=0$ at $x=x_{j}$ for all $j \neq i$ and $P_{i}(x_{i})=y_{i}$. By the fundamental theorem of calculus, we have:

$$P_{i}(x)=C_{i}\prod_{j \neq i} (x - x_{j})$$

For some constant $C_{i}$. Plugging in $P_{i}(x)=y_{i}$ gives $C_{i}=y_{i} / \prod_{j \neq i} (x_{i} - x_{j})$.

We have tamed the problem in the sense that we can find a polynomial of degree $n-1$ through a given point, that equals $0$ at all the other points. The attempt so far may not lead anywhere—as happens often when you're tackling a problem for the first time—but some thought reveals that the sum of all these polynomials goes through the points $(y_{0}, x_{0}), (y_{1}, x_{1}),\cdots,(y_{n-1}, x_{n-1})$. Therefore

$$P(x)=\sum_{i=0}^{n-1}y_{i} \frac{\prod_{j \neq i} (x - x_{j})}{\prod_{j \neq i} (x_{i} - x_{j})}$$

Solves the problem.