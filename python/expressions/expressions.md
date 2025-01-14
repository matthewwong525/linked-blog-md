![[python/glossary/glossary#expression]]
## Evaluation order
Python evaluates expressions from left to right.
However, when evaluating an assignment, the RHS is evaluated before the LHS:

```
expr3, expr4 = expr1, expr2
```

