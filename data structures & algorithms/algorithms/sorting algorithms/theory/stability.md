## Stability
> **Stable sort algorithms maintain the relative order of records with equal keys.**
### What is stability?
A sort is **stable** if two objects with equal keys appear in the same order in the sorted output as they appear in the input.

![|500](https://images.javatpoint.com/tutorial/daa/images/daa-stable-sorting.png)

Some examples of stable sorting algorithms include: counting sort, merge sort, and insertion sort.
### When is stability important?
- When sorting input with *duplicate key values*.
	- Does not change the relative ordering of records with identical key values.
- % When sorting the *same input* multiple times on *different keys*.
	- Stability preserves the order over multiple sorts on the same data set.
	- Some sorting algorithms rely on this, for example, [[radix sort]].
	- Applications: Sorting a list using a [[data structures & algorithms/appendix/glossary#primary vs secondary key|primary and secondary key]].
### When is stability NOT important?
Stability doesn’t matter if:
- All items have unique keys
- The key is the entire item
### Applications of stable sort
Stability is important when sorting items on multiple keys. For example, cards can be represented as a record (rank, suit) and we can sort them by suit first AND then rank.

Stable sort preserves any ordering on the input that is already done.

Therefore, we should sort by the **secondary key first**, then perform a **stable sort on the primary key** to maintain the ordering of the secondary done.

> [!help|gray|no-title]
> **Primary key** is the main criterion for sorting. The **secondary key** is used to break any ties in the primary key (i.e. two elements have the same value for the primary key).

> [!example]- Example: Sorting first and last names using stable sort
> Sort an array of student records such that:
> 1. First names are in alphabetical order. (<span id="aside">primary key</span>)
> 2. If we have 2 students with the same first name, then their last name should be sorted in alphabetical order. (<span id="aside">secondary key</span>)
>
> Method:
> 1. First **sort** the students by **last name** (<i>secondary key</i>).
> 2. Then *stable sort* the student by **first name** (*primary key*).
>
> ![[stable-sort-example-1.png|An example of stable sort on names. When the cards are sorted by first name with a stable sort, the two Alices and the two Andrews must remain in the same order in the sorted output that they were originally in.|400]]
>

> [!example]- Example: Sorting playing cards using stable sort
> Sort a list of cards such that:
> 1. Suites are in the order: clubs (♣), diamonds (<font color="#d83931">♦</font>), hearts (<font color="#d83931">♥</font>), spades (♠).
> 2. Within each suit, cards are sorted by rank.
>
> This can be done by:
> 1. First **sort** by **rank** (any sort)
> 2. Then *stable sort* by **suit** ⇒ preserves the ordering by rank from the previous step
>
> ![[stable-sort-example-2.png|An example of stable sort on cards. Cards are first sorted by suit, and then using a stable sort to sort by suit.|400]]
