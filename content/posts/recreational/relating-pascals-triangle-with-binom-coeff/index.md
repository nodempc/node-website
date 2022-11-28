---
title: Relating Pascal's Triangle with Binomial Coefficients
date: 2022-11-19
authors:
    - "navid_tawsif"
summary: Answering how nCr gives the element in the n-th row and r-th column of Pascal's Triangle.
categories: ["Recreational"]
tags: ["mathematics", "combinatorics"]
---
{{<katex>}}

{{<lead>}}
This post can be originally found on my [personal blog](https://colossal-pepe.github.io/false-productivity/posts/2021/may-2/).
{{</lead>}}

## A seemingly unrelated counting problem

We'll start our journey with the following puzzle:

---

Given is a $n \times m$ grid. The cell in the $i$-th row and $j$-th column are denoted as $(i, j)$. Count the number of paths from cell $(1, 1)$ to cell $(n, m)$ if the only possible moves from the current cell are the following:
+ Move to the cell that is immediately to the right of the current cell
+ Move to the cell that is just below the current cell

---

It is recommended to ponder the problem for some time before moving on.

## Solution by counting

The first solution to the problem is quite elementary. There is a more novel (and faster to compute) solution which will be presented later but the more elementary solution is the basis of the relation. The crucial observation here is that for any cell $(i, j)$ where $i > 1$ and $j > 1$, you can go to it from either $(i - 1, j)$ or $(i, j - 1)$ **and** any path that contains the cell $(i - 1, j)$ cannot contain $(i, j - 1)$. Hence, all the paths to $(i - 1, j)$ are different from all the paths to $(i, j - 1)$! This means that the total number of paths to $(i, j)$ is simply all the ways you can come to it from $(i - 1, j)$ plus all the ways you can come to it from $(i, j - 1)$.

![Grid with paths counted](img/relating-pascals-triangle-with-binom-1.png)
*Notice that all the cells at the sides ahve only 1 way to come to them, which is intuitive enough.*

More formally, let $f(i, j)$ be the number of paths to cell $(i, j)$. We can recursively define this like so:

$$
f(i, j) = \begin{cases} f(i - 1, j) + f(i, j - 1) & \text{if $i$ > 1 and $j$ > 1} \\\ 1 & \text{otherwise} \end{cases}
$$

## A more novel solution

Changing our perspective ~~signficantly~~ slightly, we can observe that each path from cell $(1, 1)$ to cell $(i, j)$ can be described as a sequence of $i - 1$ Rs (R for right) and $j - 1$ Ds (D for down) in some order.Framing the problem this way, it becomes apparent that the number of paths to $(i, j)$ is simply the number of ways to choose positions for the Rs (the D positions will be fixed after choosing the R positions) in the sequence. Let $g(i, j)$ be the answer for going from $(1, 1)$ to $(i, j)$. Therefore we have:

$$
g(i, j) = \binom{i + j - 2}{i - 1} = \binom{i + j - 2}{j - 1}
$$

*There are $i - 1$ Rs and the total path length is $i - 1 + j - 1$.*

## Equivalence

Now that the fun puzzle is solved, we are equipped to conncet the dots. Obviously, $f(i, j) = g(i, j)$. But notice the similarity between the counting solution and the way each number pascal's triangle is obtained. It's actually the same! Tortating the above figure 45 degrees clockwise and laying it on the triangle, we get the following:

![Grid with paths counted on top of triangle](img/relating-pascals-triangle-with-binom-2.png)

As can be seen from the picture, for getting to the 9th row and 5th column of the triangle, a $5 \times 5$ grid can be constructed. For the number in row $r$ and column $c$ of the triangle, a $(r + 1 - c) \times c$ grid can be constructed. And so the problem of "find the number in row $r$ and column $c$ in pascal's triangle" can be completely translated into the problem stated at the top of this page.
