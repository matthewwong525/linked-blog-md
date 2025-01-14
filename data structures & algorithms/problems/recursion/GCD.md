---
difficulty: 
status: Todo
topics:
---
## Task
The greatest common divisor, or GCD, of two integers $a$ and $b$ is the largest integer that divides both $a$ and $b$ with no remainder.

For example, the GCD of $1616$ and $2828$ is $44$ because $16=4×416=4×4$ and $28=4×728=4×7$, and there is no larger integer than divides both.

One way to calculate the GCD would be to totally factor both numbers and find common factors, but there is a much faster and easier way to do it.

If $r$ is the remainder when we divide $a$ by $b$, then the common divisors of $a$ and $b$ are precisely the same as the common divisors of $b$ and $r$, so the following identity holds:

$$ \text{gcd}(a,b)=\text{gcd}(b,r) $$

If we start with any two positive integers, and apply this identity repeatedly, $r$ will eventually become zero, and the other number in the pair is the greatest common divisor.

This is an amazing method known as Euclid's algorithm, and is probably the oldest known non-trivial algorithm; it was first described in Euclid's *Elements* in around 300 BC.

Your task is to implement the following function in `gcd.c`:

```c
int gcd(int a, int b);
```

This function should find the GCD of two integers using Euclid's algorithm as described above.

You can assume that `a` and `b` are non-negative, and that at most one of them is 0.

> [!danger|no-title]
> You must use recursion. A non-recursive solution will not receive any marks.

> [!hint]-
> **The base case is implied by the following passage:**
> 
> If we start with any two positive integers, and apply this identity repeatedly, $r$ will eventually become zero, and the other number in the pair is the greatest common divisor.
> 
> **The recursive case is implied by the following passage:**
> 
> If $r$ is the remainder when we divide $a$ by $b$, then the common divisors of $a$ and $b$ are precisely the same as the common divisors of $b$ and $r$, so the following identity holds:
> 
> $$ \text{gcd}(a,b)=\text{gcd}(b,r) $$
> 
> **Remember that the mod operator (`%`) gets the remainder when dividing two numbers.**
## Testing
Here are some examples of its usage:
```
$ ./gcd 16 28
The GCD of 16 and 28 is 4

$ ./gcd 25 15
The GCD of 25 and 15 is 5

$ ./gcd 12 72
The GCD of 12 and 72 is 12

$./gcd 64 25
The GCD of 64 and 25 is 1

$./gcd 0 42
The GCD of 0 and 42 is 0
```
## My Solutions