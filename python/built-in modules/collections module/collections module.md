Python’s [`collections`](https://docs.python.org/3/library/collections.html#module-collections) module provides a set of **specialised container data types** and wrapper classes.

- Write **readable** and **explicit** code with `namedtuple`
- Build **efficient queues and stacks** with `deque`
- **Count** objects quickly with `Counter`
- Handle **missing dictionary keys** with `defaultdict`
- Guarantee the **insertion order** of keys with `OrderedDict`
- Manage **multiple dictionaries** as a single unit with `ChainMap`

|                                                                                                                       |                                                                                                      |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| [`namedtuple()`](https://docs.python.org/3/library/collections.html#collections.namedtuple "collections.namedtuple")  | factory function for creating tuple subclasses with named fields                                     |
| [`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque")                   | list-like container with fast appends and pops on either end                                         |
| [`ChainMap`](https://docs.python.org/3/library/collections.html#collections.ChainMap "collections.ChainMap")          | dict-like class for creating a single view of multiple mappings                                      |
| [`Counter`](https://docs.python.org/3/library/collections.html#collections.Counter "collections.Counter")             | dict subclass for counting [hashable](https://docs.python.org/3/glossary.html#term-hashable) objects |
| [`OrderedDict`](https://docs.python.org/3/library/collections.html#collections.OrderedDict "collections.OrderedDict") | dict subclass that remembers the order entries were added                                            |
| [`defaultdict`](https://docs.python.org/3/library/collections.html#collections.defaultdict "collections.defaultdict") | dict subclass that calls a factory function to supply missing values                                 |
| [`UserDict`](https://docs.python.org/3/library/collections.html#collections.UserDict "collections.UserDict")          | wrapper around dictionary objects for easier dict subclassing                                        |
| [`UserList`](https://docs.python.org/3/library/collections.html#collections.UserList "collections.UserList")          | wrapper around list objects for easier list subclassing                                              |
| [`UserString`](https://docs.python.org/3/library/collections.html#collections.UserString "collections.UserString")    | wrapper around string objects for easier string subclassing                                          |
https://realpython.com/python-collections-module/