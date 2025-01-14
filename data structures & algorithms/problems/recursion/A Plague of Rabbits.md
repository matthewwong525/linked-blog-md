---
difficulty: 
status: Todo
topics:
  - Recursion
---
## Task
I have a terrible rabbit problem.

I used to have a pair of baby rabbits; they were extremely cute and fluffy, so of course I got them. But the shopkeeper I got them from - a guy named Leonardo, of Pisa Pets - didn't tell me they would mature very fast, and breed even faster.

After a month, I had a mature pair of rabbits... and, of course, they bred. Damn.

So, a month later, I had a pair of adults and a pair of baby rabbits.

And a month later, I had two pairs of adults, and another pair of baby rabbits.

And a month later, I had three pairs of adults, and two pairs of baby rabbits.

And a month later, I had five pairs of adults, and three pairs of baby rabbits.

HELP! I HAVE SO MANY RABBITS, I'M GOING HOPPING MAD!

Can you help me figure out how many rabbits I'll have?

Given that I started with one pair of baby rabbits, implement the following function in `rabbits.c` that tells me how many rabbits I'll have after a given number of months.

```c
long long rabbits(int months);
```

You can assume I won't ask about any time longer than 60 months - surely the rabbits will have taken over the world by then…

> [!NOTE]
>  A `long long` is like an `int`, but is 8 bytes in size, so it can store larger values than can be stored in an `int`.

> [!NOTE]
> You must not use while loops, for loops, do loops or goto statements. Solutions that use any of these will not receive any marks.

> [!hint]-
> Write down the number of rabbits after 0 months, 1 month, 2 months, and so on. Can you observe any pattern?


```
$ ./rabbits 0
Number of rabbits after 0 month(s): 2

$ ./rabbits 1
Number of rabbits after 1 month(s): 2

$ ./rabbits 2
Number of rabbits after 2 month(s): 4

$ ./rabbits 12
Number of rabbits after 12 month(s): 466

$ ./rabbits 42
... after a long pause ...
Number of rabbits after 42 month(s): 866988874
```
