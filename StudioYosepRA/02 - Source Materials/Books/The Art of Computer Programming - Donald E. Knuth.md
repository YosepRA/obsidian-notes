
*Friday, May 17, 2024 - 07:36*

Tags: [[computer science]]

---

**p2**

**Algorithm E** (*Euclid's algorithm*). Given two positive integers $m$ and $n$, find their *greatest common divisor*, that is, the largest positive integer that evenly divides $m$ and $n$,

**E1**: (Find remainder) Divide $m$ by $n$ and let $r$ becomes the remainder. The result should be $0 \leq r < n$.
**E2**: (Is it zero?) If $r$ is zero, then the algorithm terminates; $n$ is the answer.
**E3**: (Reduce) Set $n$ → $m$, $r$ → $n$. Repeat step E1.


**p**