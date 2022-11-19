---
title: Welcome meeting
date: 2022-11-12
authors:
    - "navid_tawsif"
    - "syed_masrur_ahmed"
---

{{<katex>}}

{{< lead >}}
This is a highlight of the welcome meeting held on 12th November, 2022 (which was also the first actual meeting of the club :partying_face:).
{{</lead>}}

## Introductions

The first segment of the meeting was for introducing Node and the people who conceived it. This can be found in brief in the [about page](../../about) of this website. Through introducing ourselves and face reveals, we also talked about the motivation behind Node and what we want to do with it. This is written in lots of detail in the [club info post](../club-info). 

After that, other members introduced themselves. They also told about their motivation behind joining the club, what they wanted to do with the club, their past experience with maths/programming. This was done so as to make club activities benefecial to as many members as we can.

## Problems

The next segment of the meeting discussed 2 introductory problems for getting the feel of some olympiad maths and informatics.

### Problem 1

Credits to this problem goes to Syed Masrur Ahmed. 

In this problem, we have a game with 2 players. The game has **5 green dots and 5 white dots initially**. Both players alternate in making moves (odd numbered turns are made by player 1, even turns are made by player 2). **On their turn, the player must remove 2 dots**. If the 2 dots they pick are of the **same colour, 1 green dot will be added to the game**. If the 2 dots are of **different colour, 1 white dot will be added instead**. After 9 moves, only 1 dot will remain. If this **dot is green, player 2 wins**, otherwise player 1 wins. The question is, **prove that player 2 can't win**, no matter how they play.

Here is a sample game played with 3 green and white dots instead of 5:

| Turn | Move Type    | n(green) | n(white) |
| ---- | ------------ | -------- | -------- |
| 1    | Same (green) | 2        | 3        |
| 2    | Different    | 1        | 3        |
| 3    | Different    | 0        | 3        |
| 4    | Same (white) | 1        | 1        |
| 5    | Different    | 0        | 1        |

The reasoning for game of 5 dots also works with game of 3 dots.

### Solution 1

We will now apply the basic problem solving technique of understanding what's happening. We do that by investigating individual moves. There are 3 possibilities for a move:

+ Both dots are green - In this case 2 green dots will be removed and 1 green dot will be added. So the number of green dots decreases by 1. Number of white dots remains unchanged.
+ Both dots are white - Similar to above but this time number of green dots remains unchanged and number of white dots decreases by 2.
+ Colours are different - 1 green and 1 white removed, but 1 white added. So number of green dots decreases by 1 and number of white dots remains unchanged.

Now, looking at this we must notice the fundamental difference between how the number green dots change and how number of white dots change.

{{<details summary="The difference">}}
Number of green dots always change by an odd number, i.e. +1 (turn 4) or -1 (turns 1, 2, 3 and 5). On the other hand, number of white dots always change by an even number, i.e. -2 (turn 4), 0 (turns 2, 3 and 5).
{{</details>}}

Why does this difference matter? Well we want to show that player 2 can't win. Let's try to show the contrary, that player 2 can win (you may have seen this technique in your maths class, going by the name proof by contradiction). If player 2 can win, that must mean number of white dots must become 0 and stay that way after turn 4. But can that even happen?

{{<details summary="Can it? And why?">}}
No. It can't happen. This is because initially the number of white dots is odd, but it's always changing by an even number. Odd + even = odd. Hence number of white dots can never go from odd to even and therefore it can't go to 0 either since 0 is even.
{{</details>}}

### Problem 2

Credits to this problem goes to ~~Navid Tawsif~~ https://codeforces.com/problemset/problem/460/B.

The problem statement is simple. Find all integer solutions to $x$ in the range $0 < x < 10^{18}$ to the following equation:
$$x = b \cdot s(x)^a + c$$
Here $s(x)$ gives the sum of the digits in the decimal representation of $x$ and $a,b,c$ are given constants.

For example, for $a = 3, b = 2, c = 8$, there are 3 solutions for $x$: 10, 2008 and 13726.

### Solution 2

Obviously it's not possible to solve for $x$ outright since there are lots of solutions for $x$. So we consut the handy method of guess and check. That is, we try different values of $x$ and see if the equation holds, and if it does we have a solution. So how long will it take to find all solutions if we try all possible values of $x$ (all the way through 1 to 10^18)? Well, it will take the average PC over 60 years! But there's a method we can find all the solutions in under 3 hours, by hand.

{{<details summary="Identity of a solution">}}
Let's consider what a solution consists of. Obviously, every solution has its own unique $x$ value. But notice that $x$ is also a function in $s(x)$ ($b \cdot s(x)^a + c$ is that function). So for every $x$ that is a solution to the equation, it has its unique corresponding $s(x)$. That means every solution is actually characterized by 2 values: $x$ and its corresponding $s(x)$!
{{</details>}}

{{<details summary="Still too many values of x">}}
it might seem like we haven't made any progress but we have. It's obvious we can't check every value of $x$, but remember from the previous hint that we can check every value of something else: $s(x)$. Let's see how many possible values of $s(x)$ there are. Obviously, the minimum value of $s(x)$ is 1. Since $x < 10^{18}$, $x$ has at most 18 digits. If all the digits are 9s, we will get the maximum $s(x)$ which would be $9 \times 18 = 162$. There are only 162 possible values of $s(x)$!
{{</details>}}

We've just reduced the search space by a factor of 10^16! From taking over 60 years, computers will now be able to do this in just 100 milliseconds. All thanks to humans.

{{<details summary="Solution implemented in Python">}}
```python
# a, b and c taken as input somewhere above

def x(s):
    return b * (s**a) + c

def digitSum(x):
    s = 0
    while x > 0:
        s += x % 10
        x //= 10
    return s

solutions = [x(s) for s in range(1, 163) if digitSum(x(s)) == s] # [10, 2008, 13726] for a = 3, b = 2, c = 8
```
{{</details>}}

## End of meeting

At the end we had a small QnA and that's about it. Thanks to everyone who attended the welcome meet and I hope we can start club meets soon!
