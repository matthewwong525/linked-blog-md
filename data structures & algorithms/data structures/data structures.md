A data structure is any data representation and its associated operations.

Selecting a Data Structure
When selecting a data structure to solve a problem, you should follow these steps.


1. Analyze your problem to determine basic operations[^1] that must be supported.
2. Quantify the [[data structures & algorithms/appendix/glossary#resource constraints|resource constraints]] for each operation
3. Select the data structure that best meets these requirements.


Knowing the basic operations required to solve your problem is the first step to selecting a suitable data structure.

Knowing the resource constraints for your problem's basic operations is the second step to selecting a suitable data structure.

Once you know the basic operations and their resource constraints, then you can select a data structure that matches.

This three-step approach to selecting a data structure operationalizes a data-centered view of the design process. The first concern is for the data and the operations to be performed on them, the next concern is the representation for those data, and the final concern is the implementation of that representation.



Resource constraints on certain key operations, such as search, inserting data records, and deleting data records, normally drive the data structure selection process.

1. Are all data items inserted into the data structure at the beginning, or are insertions interspersed with other operations?
2. Can data items be deleted? If so, this will probably make the implementation more complicated.
3. Are all data items processed in some well-defined order, or is search for specific data items allowed? “Random access” search generally requires more complex data structures.


ADT (abstract data type)
The specification of a data type, independent of an implementation. 

[^1]: Examples of basic operations include **inserting** a data item into the data structure, **deleting** a data item from the data structure, and **finding** a specified data item.
