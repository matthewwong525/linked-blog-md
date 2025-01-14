Empirical analysis is when we actually see how an algorithm performs. To compare two algorithms, we program them, run them each on a suite of test data and measure the actual running times. 

The biggest drawback is that empirical testing is subject to many possible complications, including unfair selection of test data, and inaccuracies in the time measurements due to variations in the computing environment between various executions of the programs.

Usually, we prefer theoretical 

> [!pros] Advantages of Empirical Analysis
> - Compare between algorithms with the **same asymptotic complexity**.
> 	- e.g. insertion sort and bubble sort both have the same best-, worst- and average case complexities. With empirical testing, we can compare the two based on their actual runtimes.
> - Compare the efficiency of algorithms on **small input**.

> [!cons] Limitations of Empirical Analysis
> - **Required implementation of the algorithm, which may be difficult**
> - **Different choices of input => Different results.** 
> 	- It is impossible to provide timing data for all infinitely many possible inputs. Therefore, choosing good inputs is extremely important.
> - **Time measurements will differ between machines/runtime environment.**
> 	- Algorithms are platform-independent; an algorithm can be implemented in any programming language on any computer running any operating system. 
> 	- However, the running time of a program is too dependent on the choice of a specific computer. For instance, a computer today can execute an algorithm significantly faster than a computer from the 1960s.

> [!NOTE|gray|outlined] Empirical Analysis Method
> <u>Steps</u>
> 1. Write a program that implements the algorithm
> 2. Run the program with inputs of varying sizes
> 3. Measure the runtime
> 4. Plot the results
>
> <u>Measuring Time</u>
> We can measure the running time of a program using the Linux `time` utility:
>
> ```shell
> time ./program
> # real 0m0.440s 
> # user 0m0.380s 
> # sys  0m0.000s
> ```
>
> The `time` command produces three different times:
> - **real**: total time elapsed (user + system)
> - **user**: CPU time spent executing program code
> - **sys**: CPU time spent by the operating system on behalf of the program e.g. opening a file
>
> Since we are interested in the *relative* change in time as the input size increases, we run the program multiple times with different input sizes.
>

## Empirical Comparison of Sorting Algorithms
To compare two sorting algorithms, the simplest approach would be to program both and measure their running times. However, doing fair empirical comparisons is difficult because the running time for many sorting algorithms depends on specifics of the input values. The number of records, the size of the keys and the records, the allowable range of the key values, and the amount by which the input records are “out of order” can all greatly affect the relative running times for sorting algorithms. 

The advantages to empirical comparisons is we can compare the timing results for 
