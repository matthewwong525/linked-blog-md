- **Module**: a file to be **imported** into another script or module
- **Script**: a file to be **executed directly** from the command line: `python script.py`
- A Python file can act as both a **module** and a **script** by putting executable code in the `if __name__ == "__main__"` idiom.

#TODO : https://cvw.cac.cornell.edu/python-intro/modules/index
# python source code
Python source files use the `.py` extension and are called "modules".
Modules can contain both executable code, as well as function and variable definitions.

```python hl:4 info:7-8 success:14-15  file="📁 hello.py"
#!/usr/bin/python3

# import modules used here -- sys is a very standard one
import sys

# Gather our script code in a main() function
def main():
    print('Hello there', sys.argv[1])
    # Command line args are in sys.argv[1], sys.argv[2] ...
    # sys.argv[0] is the script name itself and can be ignored

# Standard boilerplate to call the main() function to begin
# program execution
if __name__ == '__main__':
    main()
```

We can **run this module as a script** from the command-line like so:

```shell
python3 hello.py 
```

# executing modules as scripts
When we run a module directly — as above `python3 hello.py` — the module is executed as a **script**. The interpreter executes a script starting from the top of the file, going down line by line.

1. & All <b>top-level statements (<font color="#d83931">at level 0 indentation</font>)</b> in the file (outside function definitions) are executed. <font color="#a5a5a5">Highlighted yellow above.</font>
2. & When **a module name is encountered in an `import` statement**, all the top-level code[^1]  in that module is executed.
4. % Functions are not executed unless called directly in the script.


> [!problem]
>  If the module was imported and used from a different module, the executable code would unintentionally execute as well.
>
> ```python error:2 success:4-5
> # File1.py
> print('Hello from File1!') # this will execute when File1 is imported
> 
> def greet():  # this won't execute
>     print("Greetings")
> ```
>
> ```python error:2
> # File2.py
> import File1
> 
> File1.greet()
> ```
>
> When we execute File2 using `python3 File2.py`, we get the output:
>
> ```
> Hello from File1!   
> Hello from File1!
> Greetings
> ```

> [!solution]
> To make a file usable as both a script as well as an importable module, put code intended for script use only within the  **`__name__ == '__main__'`** block.

## `__name__ == '__main__'`

Unlike C, Python **does not** have a "main" function that defines the entry point of a program and is automatically called to start program execution.

Instead, we put all the script code to run when the module is executed as the "main" module/program/script inside the `if __name__ == '__main__'` block:

```python
# code on this level is always executed (top-level code)

if __name__ == "__main__":
	# execute if module is executed directly
	# if module is imported, the code is not run
    ...
else:
	# execute if module is being imported
    ...
```

> [!info|white]- When the module is <font color="#d83931">run directly</font> from the command-line, `__name__` is set equal to `"__main__"`
>
> ```python file="📁 File1.py"
> if __name__ == "__main__": 
> 	print ("File1 is being run directly") 
> else:
>     print ("File1 is being imported") 
> ```
>
> ```shell
> python3 file1.py
> # File1 is being run directly
> ```

> [!info|white]-  When the module is <font color="#d83931">run from another module</font> i.e. being imported, `__name__` is set to the module name (its own filename).
>
> ```python file="📁 File2.py" hl:1
> import File1
> 
> if __name__ == "__main__":  
> 	print ("File2 is being run directly") 
> else:  
>     print ("File2 is being imported") 
> ```
>
> ```shell
> python3 file2.py
> # File1 is being imported
> # File2 is being run directly
> ```
# executable python scripts
On Unix systems, python scripts can be made directly executable, like shell scripts, by putting the hashbang line:

```
#!/usr/bin/env python3
```

(assuming that the interpreter is on the user’s `PATH`) at the beginning of the script and giving the file an executable mode.

The script can be given an executable mode, or permission, using the **chmod** command:

```shell
chmod +x myscript.py
```

You can then run the python file from the command-line like so:

```shell
./myscript.py
```

[^1]: The outermost top-level statements are only executed the *first* time the module is imported somewhere. These statements are often used as a "one-time setup" to initialise the module and set up its variables and functions.
